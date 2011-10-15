This is a list of little tips for SymPy.  Feel free to edit this page and add some. They can be just basic things or advanced tips.  If we get enough of them, we might do something with them.

- You can define many numbered symbols at once using the slice syntax of symbols. `symbols('a0:10')` will create symbols `a0` through `a9`.  You can also do `symbols('a:z')` to create the symbols `a`, `b`, ..., `z`.

- You can convert any string into a symbolic expression using the `sympify()` function.  This will automatically define variables for you, so for example, you can type `sympify("a^2 + cos(b)")` and it will just work.