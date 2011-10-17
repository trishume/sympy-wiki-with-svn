This is a list of little tips for SymPy.  Feel free to edit this page and add some. They can be just basic things or advanced tips.  If we get enough of them, we might do something with them.

- You can define many numbered symbols at once using the slice syntax of symbols. `symbols('a4:10')` will create symbols `a4` through `a9` and `symbols('a:3')` will give 3 symbols: `a0`, `a1`, `a2`.  You can also do `symbols('a:z')` to create the symbols `a`, `b`, ..., `z`.

- You can convert any string into a symbolic expression using the `sympify()` function.  This will automatically define variables for you, so for example, you can type `sympify("a^2 + cos(b)")` and it will just work.

- Got a long expression that you want to copy from a console? Often, long expressions wrap at unintelligible places (like in the middle of a number). You can use python's textwrap module to help with this. In the example below, the breaks in the first output of `eq` are as they were in a cmd window of Windows.

```python
>>> eq=((x+1)**20).expand()
>>> eq
x**20 + 20*x**19 + 190*x**18 + 1140*x**17 + 4845*x**16 + 15504*x**15 + 38760*x**
14 + 77520*x**13 + 125970*x**12 + 167960*x**11 + 184756*x**10 + 167960*x**9 + 12
5970*x**8 + 77520*x**7 + 38760*x**6 + 15504*x**5 + 4845*x**4 + 1140*x**3 + 190*x
**2 + 20*x + 1
>>> print '\\\\\n'.join(textwrap.wrap(str(eq)))
x**20 + 20*x**19 + 190*x**18 + 1140*x**17 + 4845*x**16 + 15504*x**15 +\
38760*x**14 + 77520*x**13 + 125970*x**12 + 167960*x**11 + 184756*x**10\
+ 167960*x**9 + 125970*x**8 + 77520*x**7 + 38760*x**6 + 15504*x**5 +\
4845*x**4 + 1140*x**3 + 190*x**2 + 20*x + 1
>>> print '\\\\\n'.join(textwrap.wrap(str(eq), 50))
x**20 + 20*x**19 + 190*x**18 + 1140*x**17 +\
4845*x**16 + 15504*x**15 + 38760*x**14 +\
77520*x**13 + 125970*x**12 + 167960*x**11 +\
184756*x**10 + 167960*x**9 + 125970*x**8 +\
77520*x**7 + 38760*x**6 + 15504*x**5 + 4845*x**4 +\
1140*x**3 + 190*x**2 + 20*x + 1
```