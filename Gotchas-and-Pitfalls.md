SymPy runs under Python, so there are some things that may behave differently than they do in other independent computer algebra systems like Maple or Mathematica.  These are some of the gotchas and pitfalls that you may encounter when using SymPy.  See also the [[FAQ]], the [[Tutorial]], the [SymPy Docs](http://docs.sympy.org/), and the [official Python Tutorial](http://docs.python.org/tutorial/).  If you are already familiar with C or Java, you might also want to look this [4 minute tutorial](http://www.nerdparadise.com/tech/coding/python/4minutes/).

<!-- wikitest release -->

## Equals sign (=)
The equals sign (\(=\)) is the assignment operator, not an equality.  That if you want to do \(x=y\), use `Eq(x,y)` for equality.  Alternatively, all expressions are assumed to equal zero, so you can just subtract one side and use `x - y`.

The proper use of the equals sign is to assign expressions to variables.  For example,
```py
    >>> from sympy.abc import x, y
    >>> a = x - y
    >>> print a
    x - y
```

Double equals signs (\(==\)) are used to test equality.  However, this tests expressions exactly, not symbolically.  For example,
```py
    >>> (x + 1)**2 == x**2 + 2*x + 1
    False
    >>> (x + 1)**2 == (x + 1)**2
    True
```

If you want to test for symbolic equality, one way is to subtract one expression from the other and run it through functions like `expand()`, `simplify()`, and `trigsimp()` and see if the equation reduces to 0.

```py
    >>> from sympy import simplify, expand, sin, cos
    >>> simplify((x + 1)**2 - (x**2 + 2*x + 1))
    0

    >>> simplify(sin(2*x) - 2*sin(x)*cos(x))
    -2*cos(x)*sin(x) + sin(2*x)
    >>> expand(sin(2*x) - 2*sin(x)*cos(x), trig=True)
    0
```

See also the [[FAQ]] (#Why_does_SymPy_say_that_two_equal_expressions_are_unequal?).

## Variables
When you use `=` to do assignment, remember that in Python, as in most programming languages, the variable does not change if you change the value you assigned to it.  The equations you are typing use the values present at the time of creation to "fill in" values, just like regular python definitions. They are not altered by changes made afterwards. Consider the following:

```py
    >>> from sympy import Symbol
    >>> a = Symbol('a') # create an object with name 'a' for variable a to point to
    >>> b = a + 1; b    # create another object that refers to what 'a' refers to
    1 + a
    >>> a = 4; a        # a now points to the literal integer 4, not Symbol('a')
    4
    >>> b               # but b is still pointing at Symbol('a')
    1 + a
```

Changing quantity `a` does not change `b`; you are not working with a set of simultaneous equations. It might be helpful to remember that the string that gets printed when you print a variable refering to
a sympy object is the string that was give to it when it was created; that string does not have to
be the same as the variable that you assign it to:

```py
    >>> from sympy import symbols
    >>> r, t, d = symbols('rate time short_life')
    >>> d = r*t; d
    rate*time
    >>> r=80; t=2; d    # we haven't changed d, only r and t
    rate*time
    >>> d=r*t; d        # now d is using the current values of r and t
    160
```

See also the [[FAQ]] (#Why_doesn't_changing_one_variable_change_another_that_depends_it?)

    >>> del x

Also, Symbols are variables, and like all other variables, they need to be assigned before you can use them.  For example:

```py
    >>> from sympy import *
    >>> x**2 # x is not defined yet
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    NameError: name 'x' is not defined
    >>> var('x') # this is the easiest way to define x as a standard symbol
    x
    >>> x**2
    x**2
```

If you use isympy, it runs the following commands for you, giving you some default symbols:
```py
    >>> from __future__ import division
    >>> from sympy import *
    >>> x, y, z = symbols('xyz')
    >>> k, m, n = symbols('kmn', integer=True)
    >>> f, g, h = map(Function, 'fgh')
```

You can also import common symbol names from `sympy.abc`:
```py
    >>> from sympy.abc import w
    >>> w
    w
    >>> import sympy
    >>> dir(sympy.abc)
     ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'Symbol', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z', '__builtins__', '__doc__', '__file__', '__name__', '__package__', 'a', 'alpha', 'b', 'beta', 'c', 'chi', 'd', 'delta', 'e', 'epsilon', 'eta', 'f', 'g', 'gamma', 'h', 'i', 'iota', 'j', 'k', 'kappa', 'l', 'm', 'mu', 'n', 'nu', 'o', 'omega', 'omicron', 'p', 'phi', 'pi', 'psi', 'q', 'r', 'rho', 's', 'sigma', 't', 'tau', 'theta', 'u', 'upsilon', 'v', 'w', 'x', 'xi', 'y', 'z', 'zeta']
```
If you want control over the assumptions of the variables, use `Symbol()` and `symbols()`.

Lastly, it is recomended that you not use `I` or `E` for variable or symbol names, as those are used for the imaginary unit (\(i\)) and the base of the natural logarithm (\(e\)), respectively.  Python will not prevent you from overriding default SymPy names or functions, so be careful.  To get a full list of all default names in SymPy do:

```py
>>> import sympy
>>> dir(sympy)      # doctest: +SKIP
#A big list of all default sympy names and functions follows.  Ignore everything that starts and ends with __.
```

If you have iPython installed and use isympy, you can also press the TAB key to get a list of all built in names and to autocomplete.  See [this page](http://kogs-www.informatik.uni-hamburg.de/~meine/python_tricks) for a trick for getting tab completion in the regular Python console.

See also the [[FAQ]] (#What_is_the_best_way_to_create_symbols?).
