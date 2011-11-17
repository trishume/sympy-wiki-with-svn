# Tutorial

## Introduction

<!-- wikitest release,master -->

This tutorial gives an overview and introduction to SymPy. Read this to have an idea what SymPy can do for you (and how) and if you want to know more, read the [[API|http://sympy.googlecode.com/svn/api/sympy.html]] documentation (that is generated from the sources) or the [[sources|http://sympy.googlecode.com/svn/trunk/]] directly.

## Installation

See the [[Downloads|http://code.google.com/p/sympy/wiki/DownloadInstallation?tm=2]] tab and follow the instructions specific to your platform.

## Importing SymPy

To import SymPy from the standard Python shell, just type

```py
&gt;&gt;&gt; from sympy import *
```

and most common functions will be imported. Other modules of interest include `sympy.limits`, `sympy.solvers`, etc.

There is also a little app called isympy (located in `bin/isympy` if you are running from the source directory) which is just a standard Python shell that has already imported the relevant SymPy modules and defined the symbols `x`, `y` and `z`.

# Using SymPy as a calculator

Sympy has two built-in numeric types: `[[Real|http://sympy.googlecode.com/svn/api/sympy.core.numbers.Real-class.html]]` and `[[Rational|http://sympy.googlecode.com/svn/api/sympy.core.numbers.Rational-class.html ]]`.

The `Rational` class represents a rational number as a pair of two integers: the numerator and the denominator, so `Rational(1,2)` represents 1/2, `Rational(5,2)` 5/2 and so on.

```py
&gt;&gt;&gt; from sympy import *
&gt;&gt;&gt; a = Rational(1,2)

&gt;&gt;&gt; a
1/2

&gt;&gt;&gt; a*2
1

&gt;&gt;&gt; Rational(2)**50/Rational(10)**50
1/88817841970012523233890533447265625
```

Proceed with caution while working with Python&#39;s `int` since they truncate integer division, and that&#39;s why:

```py
&gt;&gt;&gt; 1/2
0

&gt;&gt;&gt; 1.0/2
0.5
```

You can however do:

```py
&gt;&gt;&gt; from __future__ import division # doctest: +SKIP

&gt;&gt;&gt; 1/2 # doctest: +SKIP
0.5
```

It&#39;s going to be standard in Python, hopefully soon...

We also have some special constants, like `e` and `pi`, that are treated as symbols (&lt;code&gt;1+pi&lt;/code&gt; won&#39;t evaluate to something numeric, rather it will remain as `1+pi`), and have arbitrary precision:

```py
&gt;&gt;&gt; pi**2
pi**2

&gt;&gt;&gt; pi.evalf()                  # doctest: +SKIP
3.141592653589793238462643383

&gt;&gt;&gt; (pi+exp(1)).evalf()         # doctest: +SKIP
5.859874482049203234066343309
```

As you see, `evalf` evaluates the expression to a floating-point number.

There is also a class representing mathematical infinity, called `oo`:

```py
&gt;&gt;&gt; oo &gt; 99999
True
&gt;&gt;&gt; oo + 1
oo
```

## Symbols

In contrast to other Computer Algebra Systems, in SymPy you have to declare symbolic variables explicitly:

```py
&gt;&gt;&gt; from sympy import *
&gt;&gt;&gt; x = Symbol(&#39;x&#39;)
&gt;&gt;&gt; y = Symbol(&#39;y&#39;)
```

Then you can play with them:

```py
&gt;&gt;&gt; x+y+x-y
2*x

&gt;&gt;&gt; (x+y)**2
(x + y)**2

&gt;&gt;&gt; ((x+y)**2).expand()
 x**2 + 2*x*y + y**2
```

And substitute them for other symbols or numbers using `subs(var, substitution)`:

```py
&gt;&gt;&gt; ((x+y)**2).subs(x, 1)
(y + 1)**2

&gt;&gt;&gt; ((x+y)**2).subs(x, y)
4*y**2
```

# Calculus

## Limits

Limits are easy to use in SymPy. They follow the syntax `limit(function, variable, point)`, so to compute the limit of f(x) as x -&gt; 0, you would issue `limit(f, x, 0)`.

```py
&gt;&gt;&gt; from sympy import *
&gt;&gt;&gt; x=Symbol(&quot;x&quot;)
&gt;&gt;&gt; limit(sin(x)/x, x, 0)
1
```

You can also calculate the limit at infinity:

```py
&gt;&gt;&gt; limit(x, x, oo)
oo

&gt;&gt;&gt; limit(1/x, x, oo)
0

&gt;&gt;&gt; limit(x**x, x, 0)
1

&gt;&gt;&gt; limit((5**x + 3**x)**(1/x), x, oo)  # doctest: +SKIP
5
```

For some non-trivial examples on limits, you can read the test file `[[test_demidovich.py|http://hg.sympy.org/sympy/file/tip/sympy/series/tests/test_demidovich.py]]`.

## Differentiation

You can differentiate any SymPy expression using `diff(func, var)`. Examples:

```py
&gt;&gt;&gt; from sympy import *
&gt;&gt;&gt; x = Symbol(&#39;x&#39;)
&gt;&gt;&gt; diff(sin(x), x)
cos(x)
&gt;&gt;&gt; diff(sin(2*x), x)
2*cos(2*x)

&gt;&gt;&gt; diff(tan(x), x)
tan(x)**2 + 1
```

You can check, that it is correct by:

```py
&gt;&gt;&gt; limit((tan(x+y)-tan(x))/y, y, 0)
tan(x)**2 + 1
```

Higher derivatives can be calculated using the `diff(func, var, n)` method:

```py
&gt;&gt;&gt; diff(sin(2*x), x, 1)
2*cos(2*x)

&gt;&gt;&gt; diff(sin(2*x), x, 2)
-4*sin(2*x)

&gt;&gt;&gt; diff(sin(2*x), x, 3)
-8*cos(2*x)
```

## Series expansion

Use `.series(var, order)`:

```py
&gt;&gt;&gt; from sympy import *
&gt;&gt;&gt; x = Symbol(&#39;x&#39;)
&gt;&gt;&gt; cos(x).series(x, 0, 10)
1 - x**2/2 + x**4/24 - x**6/720 + x**8/40320 + O(x**10)
&gt;&gt;&gt; (1/cos(x)).series(x, 0, 10)
1 + x**2/2 + 5*x**4/24 + 61*x**6/720 + 277*x**8/8064 + O(x**10)
```

## Integration

SymPy has support for indefinite and definite integration of transcendental elementary and special functions via `integrate()` facility, which uses powerful extended Risch-Norman algorithm and some heuristics and pattern matching.

```py
&gt;&gt;&gt; from sympy import *
&gt;&gt;&gt; x, y = symbols(&#39;x y&#39;)
```

You can integrate elementary functions:

```py
&gt;&gt;&gt; integrate(6*x**5, x)
x**6
&gt;&gt;&gt; integrate(sin(x), x)
-cos(x)
&gt;&gt;&gt; integrate(log(x), x)
x*log(x) - x
&gt;&gt;&gt; integrate(2*x + sinh(x), x)     # doctest: +PRETTY
     2          
    x  + cosh(x)
```

Also special functions are handled easily:

```py
&gt;&gt;&gt; integrate(exp(-x**2)*erf(x), x)     #doctest: +RELEASE_ONLY
pi**(1/2)*erf(x)**2/4
&gt;&gt;&gt; integrate(exp(-x**2)*erf(x), x)     #doctest: +FUTURE_ONLY
sqrt(pi)*erf(x)**2/4
```

It is possible to compute definite integral:

```py
&gt;&gt;&gt; integrate(x**3, (x, -1, 1))
0
&gt;&gt;&gt; integrate(sin(x), (x, 0, pi/2))
1
&gt;&gt;&gt; integrate(cos(x), (x, -pi/2, pi/2))
2
```

Also improper integrals are supported as well:

```py
&gt;&gt;&gt; integrate(exp(-x), (x, 0, oo))
1
&gt;&gt;&gt; integrate(log(x), (x, 0, 1))
-1
```

## Complex numbers

```py
&gt;&gt;&gt; from sympy import Symbol, exp, I
&gt;&gt;&gt; x = Symbol(&quot;x&quot;)
&gt;&gt;&gt; exp(I*x).expand()
exp(I*x)
&gt;&gt;&gt; exp(I*x).expand(complex=True)
I*exp(-im(x))*sin(re(x)) + exp(-im(x))*cos(re(x))
&gt;&gt;&gt; x = Symbol(&quot;x&quot;, real=True)
&gt;&gt;&gt; exp(I*x).expand(complex=True)
I*sin(x) + cos(x)
```

## Differential equations

In *isympy*:
```py
In [9]: Eq(f(x).diff(x, x) + f(x), 0)
Out[9]:
   2
  d
─────(f(x)) + f(x) = 0
dx dx

In [10]: dsolve(Eq(f(x).diff(x, x) + f(x), 0), f(x))
Out[10]: C1*sin(x) + C2*cos(x)
```

## Algebraic equations

In *isympy*:
```py
In [19]: solve(Eq(x**4, 1), x)
Out[19]: [1, -1, -I, I]

In [20]: solve([Eq(x + 5*y, 2), Eq(-3*x + 6*y, 15)], [x, y])
Out[20]: {y: 1, x: -3}
```

# Linear Algebra

## Matrices

Matrices are created as instances from the `[[Matrix|http://sympy.googlecode.com/svn/api/sympy.modules.matrices.Matrix-class.html]]` class. This class is located in `sympy.matrices`, but at usual, *isympy* imports this for you:

```py
&gt;&gt;&gt; from sympy import *
&gt;&gt;&gt; from sympy.matrices import Matrix
&gt;&gt;&gt; Matrix([[1,0], [0,1]])
[1, 0]
[0, 1]
```

You can also put symbols in it:
```py
&gt;&gt;&gt; x = Symbol(&#39;x&#39;)
&gt;&gt;&gt; y = Symbol(&#39;y&#39;)
&gt;&gt;&gt; A = Matrix([[1,x], [y,1]])
&gt;&gt;&gt; A
[1, x]
[y, 1]

&gt;&gt;&gt; A**2
[x*y + 1,     2*x]
[    2*y, x*y + 1]
```

For more information and examples with matrices, see the [[Linear Algebra tutorial|Linear Algebra Module]].

# Pattern matching

Use the `.match()` method, along with the `Wild` class, to perform pattern matching on expressions. The method will return a dictionary with the required substitutions, as follows:

```py
&gt;&gt;&gt; from sympy import *
&gt;&gt;&gt; x = Symbol(&#39;x&#39;)
&gt;&gt;&gt; p = Wild(&#39;p&#39;)
&gt;&gt;&gt; q = Wild(&#39;q&#39;)
&gt;&gt;&gt; (5*x**2 + 3*x).match(p*x**2 + q*x)
{p_: 5, q_: 3}

&gt;&gt;&gt; (x**2).match(p*x**q)
{p_: 1, q_: 2}
```

If the match is unsuccessful, it returns `None`:

```py
&gt;&gt;&gt; print (x+1).match(p**x)
None
```

One can also make use of the `WildFunction` class to perform more specific matches with functions and their arguments:

```py
&gt;&gt;&gt; f = WildFunction(&#39;f&#39;, nofargs=1)
&gt;&gt;&gt; (5*cos(x)).match(p*f)
{p_: 5, f_: cos(x)}
&gt;&gt;&gt; (cos(3*x)).match(f(p*x))
{p_: 3, f_: cos}
&gt;&gt;&gt; g = WildFunction(&#39;g&#39;, nofargs=2)
&gt;&gt;&gt; (5*cos(x)).match(p*g)
{p_: 5, g_: cos(x)}
```

One can also use the `exclude` parameter of the `Wild` class to ensure that certain things do not show up in the result:

```py
&gt;&gt;&gt; x = Symbol(&#39;x&#39;)
&gt;&gt;&gt; p = Wild(&#39;p&#39;, exclude=[1,x])
&gt;&gt;&gt; print (x+1).match(x+p) # 1 is excluded
None
&gt;&gt;&gt; print (x+1).match(p+1) # x is excluded
None
&gt;&gt;&gt; print (x+1).match(x+2+p) # -1 is not excluded
{p_: -1}
```


# Printing

SymPy comes pre-packed with several ways of printing expressions. The most basic way to print an expression is simply though the use of `str(expression)` or `repr(expression)`. 

Also a printing module available, `sympy.printing`. Level 2 printing is made possible through the pretty printing component of the printing module. Other printing methods available trough this module are:

* `pretty(expr)`, `pretty_print(expr)`, `pprint(expr)`
    * Return or print, respectively, a pretty representation of `expr`. This is the same as the second level of representation described above.
* `latex(expr)`, `print_latex(expr)`
    * Return or print, respectively, a [[LaTeX|http://www.latex-project.org/]] representation of `expr`.
* `mathml(expr)`, `print_mathml(expr)`
    * Return or print, respectively, a [[MathML|http://www.w3.org/Math/]] representation of `expr`.
* `print_gtk(expr)`
    * Print `expr` to [[Gtkmathview|http://helm.cs.unibo.it/mml-widget/]], a GTK widget that displays MathML code. The [[Gtkmathview|http://helm.cs.unibo.it/mml-widget/]] program is required.
* `print_pygame(expr)`
    * Print `expr` to a [[PyGame|http://www.pygame.org/news.html]] window. The PyGame library is required, along with the Python [[pexpect|http://pexpect.sourceforge.net/]] library, the [[LaTeX|http://www.latex-project.org/]] program, and the [[dvipng|http://savannah.nongnu.org/projects/dvipng/]] program.

# Modules
The following list provides links to documentation for some of the various modules SymPy offers

* [[Geometry Module]]
* [[Linear Algebra Module]]
* [[Numerics Module]]
* [[Plotting Module]]
* [[Concrete Mathematics Module]]
* [[Polynomials Module]]
* [[Statistics Module]]
* [[Pretty Printing]]