This is a list of little tips for SymPy.  Feel free to edit this page and add some. They can be just basic things or advanced tips.  If we get enough of them, we might do something with them.

# Basic

- You can define many numbered symbols at once using the slice syntax of symbols. `symbols('a4:10')` will create symbols `a4` through `a9` and `symbols('a:3')` will give 3 symbols: `a0`, `a1`, `a2`.  You can also do `symbols('a:z')` to create the symbols `a`, `b`, ..., `z`.

- You can convert any string into a symbolic expression using the `sympify()` function.  This will automatically define variables for you, so for example, you can type `sympify("a^2 + cos(b)")` and it will just work.

- The best method to test equality is to use the simplify function to check whether the difference of two expressions is 0. For example, to check the equality of (x-1)**2 and x**2 - 2*x + 1, print simplify((x-1) ** 2 - (x**2 - 2*x + 1)) and see if it equals 0.

- Some SymPy trig functions are named differently than their counterparts in other systems. In particular, SymPy inverse functions are asin, acos, and atan (the standard in the programming world), while most mathematical systems/humans refer to them as either sin/cos/tan**-1 or arcsin/cos/tan.

- To create a list of values, assign a variable to a list enclosed by brackets (e.g. x = [1,2,3,4,5]). To get the i-th value in x, you use x[i - 1]. Note that this means that to access the first value in the list, you must use x[0], so that print x[0] outputs 1, print x[1] outputs 2, and so on.

- If you need help, the quickest resource is using the built in help tool by entering help(functionname). For example, if you need to find out what sin(x) does, type help(sin), or alternatively, sin? if using IPython.

# Intermediate

- Got a long expression that you want to copy from a console? Often, long expressions wrap at unintelligible places (like in the middle of a number). You can use python's textwrap module to help with this. In the example below, the breaks in the first output of `eq` are as they were in a cmd window of Windows.

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

- If you have some functions in an expression that you don't want, you can get rid of them by using `expr.replace(function, Id)`.  This will replace all instances of the function `function`, with `Id`, which is just the identity function.  For example, if your expression is `sin(Abs(x)) + cos(Abs(x))`, and you don't want the absolute values, you can do `expr.replace(Abs, Id)` to get rid of them.  This gives `sin(x) + cos(x)`. (Notice that you have to use `Abs`, `abs` is the Python built-in and will not work.)

- When defining a variable in terms of a symbol with an assignment (=) sign, the assigned variable will not change even if the variable containing the symbol does. When you type x = Symbol('x'), y = x, and x = 25, printing y will still give x, not 25.

- SymPy allows you to use the Python method of writing functions in SymPy itself. You declare a function with def functionname(varlist). Make sure your functions have return values. Sample function:
```
def add(n1, n2):
    return n1 + n2
```

- SymPy has a lovely Geometry tool. To declare points, use <pointname> = Point(x, y). Most other objects are self-explanatory, such as Triangle(point1, point2, point3), and Circle(centerpoint, radius).

# Advanced

- You can use a dictionary to map text keys to values (syntax: sampledict = {'var1':2, 'var2':4). This is particularly useful if you want to write a function that returns a list of variables, as the user can simply query the dictionary for some key representing a variable to get a value (query syntax: myvar = sampledict['var1']).

- SymPy can manipulate boolean logic variables. And is represented by &, or by |, and implication by >> or <<. Alternatively, you can use textual representation of operations (ex. Or(true, false)). There are many other boolean algebra functions: check the documentation for a full listing.

- If you're particularly curious about the inner workings of SymPy, try entering the function source(functionname). This will print the mess that's known as source code.