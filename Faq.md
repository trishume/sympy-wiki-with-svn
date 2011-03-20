## [Why does SymPy say that two equal expressions are unequal?](#hello with a space)

The equality operator (`==`) tests whether expressions have identical form, not whether they are mathematically equivalent.

To make equality testing useful in basic cases, SymPy tries to rewrite mathematically equivalent expressions to a canonical form when evaluating them. For example, SymPy evaluates both `x+x` and `-(-2*x)` to `2*x`, and `x*x` to `x**2`.

The simplest example where the default transformations fail to generate a canonical form is for nonlinear polynomials, which can be represented in both factored and expanded form. Although clearly \( a(1+b) = a+ab \) mathematically, SymPy gives:
```py
>>> bool(a*(1+b) == a + a*b)
False
```

Likewise, SymPy fails to detect that the difference is zero:
```py
>>> bool(a*(1+b) - (a+a*b) == 0)
False
```

If you want to determine the mathematical equivalence of nontrivial expressions, you should apply a more advanced simplification routine to both sides of the equation. In the case of polynomials, expressions can be rewritten in a canonical form by expanding them fully. This is done using the **`.expand()`** method in SymPy:
```py
>>> A, B = a*(1+b), a + a*b
>>> bool(A.expand() == B.expand())
True
>>> (A - B).expand()
0
```

If `.expand()` does not help, try **`simplify()`**, **`trigsimp()`**, etc, which attempt more advanced transformations. For example,
```py
>>> trigsimp(cos(x)**2 + sin(x)**2) == 1
True
```


## [I did the same calculation twice and got different results. What's going on?](#I did the same calculation twice and got different results. What's going on?)
This problem is probably due to erroneous caching of assumptions. Please report the bug to the [[mailing list|http://groups.google.com/group/sympy]] or the [[issue tracker|http://code.google.com/p/sympy/issues/list]].

## [What is the best way to create symbols?](#What is the best way to create symbols?)

The most convenient way to create symbols when using SymPy interactively is via `var`. For example:
```py
>>> var('x y')
>>> x + y
x + y
```

The `var` function uses a hack to add the symbols to the current namespace, so you don't have to type each symbol name twice. In library code, it is better to create symbols explicitly:
```py
x = Symbol('x')
y = Symbol('y')
```
This makes the code much clearer.



## [How good is SymPy's performance?](#How good is SymPy's performance?)
SymPy is efficient enough for interactive use as an advanced calculator. The order-of-magnitude time to evaluate a simple algebraic operation (say, multiplying two small polynomials) is around 1/1000 of a second. Operations like limits and symbolic integration are generally much slower.

SymPy is written entirely in Python. Compared to CASes written in compiled languages (including Mathematica, Maple and Maxima), SymPy is generally at least an order of magnitude (10x) slower: This is partly due to the overhead of Python, and partly because SymPy in many cases only implements the most basic algorithm. Nonetheless, experimentation has shown that that symbolic computations can be done nearly as efficiently in Python as in compiled languages by using the right data structures and designing the code to minimize various Python overheads. The [[sympycore|http://code.google.com/p/sympycore/]] project is currently attempting to redesign SymPy's internals to provide better performance, and the results are promising so far. See [[sympycore wiki: PerformanceHistory|http://code.google.com/p/sympycore/wiki/PerformanceHistory]] and [[sympycore wiki: Performance|http://code.google.com/p/sympycore/wiki/Performance]] for more details.

## Where is SymPy going to? What are the nearest plans?

See our roadmap: http://wiki.sympy.org/wiki/Plan_for_SymPy_1.0

The current state of SymPy as of January 3, 2008 is summed up in the blogpost: http://ondrejcertik.blogspot.com/2008/01/sympysympycore-pure-python-up-to-5x.html

And in the email: http://groups.google.com/group/sympy/msg/da52a78c1ef9f02b

But the secret plan is to be the best CAS in Python. :)

## What about Sage?

Sage will be the best opensource CAS (hopefully). More information here:

http://code.google.com/p/sympy/wiki/Motivation

## How do I clear the cache?

You can see/clear the cache content as follows:
```py
In [1]: from sympy.core.cache import *

In [2]: print_cache()
============================
<function gcd at 0xb7a96f7c>
============================

*** 0 ***

  ((2, 1), ()) :        1
  ((1, 30), ()) :       1
  ((1, 6), ()) :        1

*** 1 ***

  1 :   1

... lots of output follows ...

In [3]: clear_cache()
```


## How do I turn off caching?

Simply set the environment variable "SYMPY_USE_CACHE=no", for example:
```bash
$ SYMPY_USE_CACHE=no py.test sympy/core
```

This was implemented in {{hg|fdca1475fb92}}.

## Is there a method to get a list with all symbols in an expression?

Yes `.atoms(Symbol)`, use it like this:
```py
In [1]: e = x + y*sin(z**2)

In [2]: e.atoms()
Out[2]: set([z, y, x, 2])

In [3]: e.atoms(Symbol)
Out[3]: set([z, y, x])
```


## How can I make my editor highlight trailing whitespace red?

This depends on your editor.

* For [[Vim/Gvim|http://www.vim.org]], add the following to your .vimrc:
```vim
if has('gui_running')
    hi WhiteSpaceEOL guibg=#FF0000
else
    hi WhiteSpaceEOL ctermbg=Red endif
match WhitespaceEOL /\s\+\%#\@<!$/
```

## How to connect to our IRC channel?

We are at #sympy at FreeNode.

To connect there, just start some irc program. Ondrej uses XChat (but you can use any other irc client):

http://www.xchat.org/

if you use Ubuntu or Debian, just do:
```bash
apt-get install xchat
```

Start it, it will ask you to select a nick (select some) and connect
to a network, connect to "FreeNode" (select it from the list) and then
after you connect, type
```irc
/join #sympy
```
and that's it. If you have any troubles, please ask on our [[mailinglist|http://groups.google.com/group/sympy]].


## Why doesn't changing one variable change another that depends it?

The short answer is "because it **doesn't** depend on it." :-)
Even though you are working with equations, you are still working with Python objects.
The equations you are typing use the values present at the time of creation to
"fill in" values, just like regular python definitions. They are not altered by
changes made afterwards. Consider the following:
```py
>>> a = Symbol('a') # create an object with name 'a' for variable a to point to
>>> b = a + 1; b    # create another object that refers to what 'a' refers to
1 + a
>>> a = 4; a        # a now points to the literal integer 4, not Symbol('a')
4
>>> b
1 + a               # but b is still pointing at Symbol('a')
```

Changing quantity `a` does not change `b`; you are not working with a set of simultaneous equations. It might be helpful to remember that the string that gets printed when you print a variable refering to
a sympy object is the string that was give to it when it was created; that string does not have to
be the same as the variable that you assign it to:
```py
>>> r, t, d = var('rate time short_life')
>>> d = r*t; d
>>> rate*time
>>> r=80; t=2; d    # we haven't changed d, only r and t
rate*time
>>> d=r*t; d        # now d is using the current values of r and t
160
```

## When I copy and paste an expression during interactive work, why do I get a different answer?

Even though you are working with sympy objects, not everything you type is a sympy object. If you are working with a python version earlier than 3 and have not issued a `from __future__ import division` command then dividing an integer by a larger integer will give 0
```py
>>> a=4; 1/a
0
>>> from __future__ import division
>>> 1/a
0.25
```

This could be the source of the difference that you see when you copy and paste a result. The work-around for this is to use sympify() on that copied expression which changes integers to a sympy object or just use a index to access the piece of the output that you are interested in:
```py
>>> a,b = symbols('ab')
>>> solve((2*a-b)*a-3, a)
[b/4 - (24 + b**2)**(1/2)/4, b/4 + (24 + b**2)**(1/2)/4]
>>> root1 = b/4 - (24 + b**2)**(1/2)/4; root1
-1/4 + b/4                                                 # the 1/2 went to 0
>>> root1 = sympify('b/4 - (24 + b**2)**(1/2)/4'); root1
b/4 - (24 + b**2)**(1/2)/4                                 # sympy preserves the integers
>>> solve((2*a-b)*a-3,a)
[b/4 - (24 + b**2)**(1/2)/4, b/4 + (24 + b**2)**(1/2)/4]
>>> root1=_[0]; root1
b/4 - (24 + b**2)**(1/2)/4
```

## How can I get sympy to not change what I enter?

Sometimes you might want a fraction in an unsimplified form (e.g. 2/4 instead of 1/2) or you might want terms raised to a power to not have the power distributed to each term (e.g. `(x*y)**2` instead of `x**2*y**2`). Presently, the way to get the raw form is by building the expression with the `evaluate=False` option, e.g.
```py
>>> Mul(2, Rational(1,4), evaluate = False)
2/4
>>> Pow(x*y, 2, evaluate = False)
(x*y)**2
```
