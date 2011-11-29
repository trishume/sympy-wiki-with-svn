This is a list of little tips for SymPy.  Feel free to edit this page and add some. They can be just basic things or advanced tips.  If we get enough of them, we might do something with them. If you have a short tip try to keep it under 140 characters. We may create a SymPy daily tips twitter stream. 

# Basic

- You can define many numbered symbols at once using the slice syntax of symbols. `symbols('a4:10')` will create symbols `a4` through `a9` and `symbols('a:3')` will give 3 symbols: `a0`, `a1`, `a2`.  You can also do `symbols('a:z')` to create the symbols `a`, `b`, ..., `z`.

- I, E, S, N, C, O, or Q are special variables which already have values; It's best not to overwrite them.

- SymPy, like Python, has no implied multiplication. I.e. `2x` would not work but `2*x` would.

- You can convert any string into a symbolic expression using the `sympify()` function.  This will automatically define variables for you, so for example, you can type `sympify("a^2 + cos(b)")` and it will just work.

- You can store special values in normal variables. so that you don't have to add ".evalf()" when you use the value.
ex. `x=pi.evalf()` or `y=E.evalf()`

- The best method to test equality is to use the simplify function to check whether the difference of two expressions is `0`. For example, to check the equality of `(x-1)**2` and `x**2 - 2*x + 1`, print `simplify((x-1) ** 2 - (x**2 - 2*x + 1))` and see if it equals `0`.

- `=` is used to assign values to variables; `==` checks for equality. More info can found at the Documentation Tutorial [here](http://docs.sympy.org/0.7.1/gotchas.html#equals-signs).

- Some SymPy trig functions are named differently than their counterparts in other systems. In particular, SymPy inverse functions are asin, acos, and atan not arcsin/arccos/arctan.

- To create a list of values, assign a variable to a list enclosed by brackets (e.g. `x = [1,2,3,4,5]`). To get the i-th value in `x`, you use `x[i - 1]`. Note that this means that to access the first value in the list, you must use `x[0]`, so that `print x[0]` outputs `1`, `print x[1]` outputs `2`, and so on.

- Tuples are like lists, but are less easy to use. They are created in the same way, just with parentheses instead of bracket. For example, `x = (2,3,4)`. There are two other differences from lists. The major difference is that you cannot change values in tuples after creating them. This may be useful if you don't want to overwrite the data. 

```python
>>> y = (1,3,5)
>>> y
(1, 3, 5)
>>> y[1] = 10
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```
The last difference is that if you want a tuple with only only one element, you must put a comma after the element, e.x. `x = (1,)`. 

- The `Dummy()` command can be used to take place of an undetermined variable that cannot be equal to anything else. `Dummy('x') == Symbol('x')` and `Dummy('x') == Dummy('x')` would both return false because each Dummy symbol is unique.

- If you need help, the quickest resource is using the built in help tool by entering `help(functionname)`. For example, if you need to find out what `sin(x)` does, type `help(sin)`, or alternatively, `sin?` if you are using IPython.

- Because multiplication and division have equal priority, these operators are evaluated from left to right.
Addition and subtraction work in the same way. This occurs because Sympy uses [Python's precedence rules](http://docs.python.org/reference/expressions.html#summary), which evaluates them this way.

- If you want to divide integers, it's a good idea to use `from __future__ import division`. This prevents Python from truncating the answer by stopping it from using the `floor()` command.

- If you want to use integer division after you've already imported `division` from `__future__`, you can use a `//` in place of the `/`

- Have an equation and a value for the variable(s)? Use the substitution method. For example, if you have: `x + 14` and you know `x` = `1`, do `(x + 14).subs(x, 1)` to get `15`.

- You can also use the substitution method to change variables. For example, if you have `pi - 17*x` and want to switch `x` for `y`, then `(pi - 17*x).subs(x, y)` produces `pi - 17*y`.

- Remember that all variables must first be defined. You must do `r = Symbol('r')` before using the variable `r`.

- Want to have your result printed in LaTeX? Just use the built-in `latex()` function. For example, `latex(exp(x))` will print out `e^x` in LaTeX.

- If you have pyglet, you can use the `plot()` command to plot a function in up to three dimensions.

- Have a function plotted and want to easily zoom in and out without changing the window? Use the '-' and '+' keys on the number pad or the 'r' and 'f' keys.

- Want to have SymPy print out numeric results? Use `expr.evalf()` or `N(expr)`.  For example, `N(pi)` will return `3.14159265358979` instead of `pi`.

- Want to do definite integration? Use the `integrate()` function. The arguments are `integrate(function, (variable, bottom bound, top bound))`. For example, `integrate(sin(x), (x, 0, pi/2))` will return `1`.

- The expand method works not only for algebraic functions, but also for trigonometric functions. For example, `sin(x + y).expand(trig=True)` will return `sin(x)*cos(y) + sin(y)*cos(x)`.

- Want SymPy to print in Pretty Print? Use the Pretty Print function. To print out `x/y` in Pretty Print, do `pprint(x/y)`. Alternatively use the isympy console. 

# Intermediate

- Have a long expression that you want to copy from a console? Often, long expressions wrap at unintelligible places (like in the middle of a number). You can use python's textwrap module to help with this. In the example below, the breaks in the first output of `eq` are as they were in a cmd window of Windows.

```python
>>> from sympy.abc import x
>>> eq=((x+1)**20).expand()
>>> eq
x**20 + 20*x**19 + 190*x**18 + 1140*x**17 + 4845*x**16 + 15504*x**15 + 38760*x**14 + 77520*x**13 + 125970*x**12 + 167960*x**11 + 184756*x**10 + 167960*x**9 + 125970*x**8 + 77520*x**7 + 38760*x**6 + 15504*x**5 + 4845*x**4 + 1140*x**3 + 190*x**2 + 20*x + 1
>>> import textwrap
>>> print '\\\\\n'.join(textwrap.wrap(str(eq)))
x**20 + 20*x**19 + 190*x**18 + 1140*x**17 + 4845*x**16 + 15504*x**15 +\\
38760*x**14 + 77520*x**13 + 125970*x**12 + 167960*x**11 + 184756*x**10\\
+ 167960*x**9 + 125970*x**8 + 77520*x**7 + 38760*x**6 + 15504*x**5 +\\
4845*x**4 + 1140*x**3 + 190*x**2 + 20*x + 1
>>> print '\\\\\n'.join(textwrap.wrap(str(eq), 50))
x**20 + 20*x**19 + 190*x**18 + 1140*x**17 +\\
4845*x**16 + 15504*x**15 + 38760*x**14 +\\
77520*x**13 + 125970*x**12 + 167960*x**11 +\\
184756*x**10 + 167960*x**9 + 125970*x**8 +\\
77520*x**7 + 38760*x**6 + 15504*x**5 + 4845*x**4 +\\
1140*x**3 + 190*x**2 + 20*x + 1
```

- If you have some functions in an expression that you don't want, you can get rid of them by using `expr.replace(function, Id)`.  This will replace all instances of the function `function`, with `Id`, which is just the identity function.  For example, if your expression is `sin(Abs(x)) + cos(Abs(x))`, and you don't want the absolute values, you can do `expr.replace(Abs, Id)` to get rid of them.  This gives `sin(x) + cos(x)`. (Notice that you have to use SymPy's `Abs`, and not the python built-in `abs` function.)

- When defining a variable in terms of a symbol with an assignment (=) sign, the assigned variable will not change even if the variable containing the symbol does. When you type `x = Symbol('x')`, `y = x`, and `x = 25`, printing `y` will still give `x`, not `25`.

- SymPy allows you to use the Python method of writing functions in SymPy itself. You declare a function with `def functionname(varlist):`. Make sure your functions have return values. Sample function:
```python
def add(n1, n2):
    return n1 + n2
```

- SymPy has a lovely Geometry tool. To declare points, use `pointname = Point(x, y)`. Most other objects are self-explanatory, such as `Triangle(point1, point2, point3)`, and `Circle(centerpoint, radius)`.

- Want to combine fraction terms? Use the together function. For example, `together(1/x + 1/y + 1/z)` will return 
`(x*y + x*z + y*z)/(x*y*z)`.

# Advanced

- You can use a dictionary to map text keys to values (syntax: `sampledict = {'var1':2, 'var2':4}`). This is particularly useful if you want to write a function that returns a list of variables, as the user can simply query the dictionary for some key representing a variable to get a value (query syntax: `myvar = sampledict['var1']`).

- SymPy can manipulate boolean logic variables. And is represented by `&`, or by `|`, and implication by `>>` or `<<`. Alternatively, you can use textual representation of operations (ex. `Or(x, y)`). There are many other boolean algebra functions: check the documentation for a full listing.

- If you're particularly curious about the inner workings of SymPy, try entering the function `source(functionname)`. This will print the mess that's known as source code. You can also use `functionname??` if you are using IPython.