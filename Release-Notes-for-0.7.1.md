# Release Notes for SymPy 0.7.1
These are the release notes for SymPy 0.7.1.

## Major changes

- Python 2.4 is no longer supported.  SymPy will not work at all in
  Python 2.4.  If you still need to use SymPy under Python 2.4 for some
  reason, you will need to use SymPy 0.7.0 or earlier.

- The Pyglet plotting library is now an (optional) external dependency. 
  Previously, we shipped a version of Pyglet with SymPy, but this was
  old and buggy.  The plan is to eventually make the plotting in SymPy
  much more modular, so that it supports many backends, but this has not
  been done yet.  For now, still only Pyglet is directly supported. 
  Note that Pyglet is only an optional dependency and is only needed for
  plotting. The rest of SymPy can still be used without any dependencies
  (except for Python).

- isympy now works with the new IPython 0.11.

- mpmath has been updated to 0.17.  See the corresponding mpmath release
  notes at http://mpmath.googlecode.com/svn/trunk/CHANGES.

- Added a Subs object for representing unevaluated substitutions.  This
  lets us finally represent derivatives evaluated at a point, i.e.,
  `diff(f(x), x).subs(x, 0)` returns `Subs(Derivative(f(_x), _x), (_x,), (0,))`.
  This also means that SymPy can now correctly compute the chain rule
  when this functionality is required, such as with `f(g(x)).diff(x)`.

## Hypergeometric functions/Meijer G-Functions
_Tom, can you fill this out?_

## Sets
_Matthew, can you fill this out?_

## Iterables
_Chris and/or Saptarshi, can you fill this out?_

## Solvers/Simplify
_Chris and/or Nicolas, can you fill this out?_

## xyz bases
_Sean and/or Ondrej, can you fill this out?_

## Other changes

- We now use MathJax in our docs. MathJax renders LaTeX math entierly in
  the browser using Javascript.  This means that the math is much more
  readable than the previous png math, which uses images.  MathJax is
  only supported on modern browsers, so LaTeX math in the docs may not
  work on older browsers.

- nroots() now lets you set the precision of computations

- Added support for gmpy and mpmath's types to sympify()

- Fix a some bugs with lambdify()

- Fix a bug with as_independent and non-commutative symbols.

- Many fixes relating to porting SymPy to Python 3.  Thanks to our GSoC
  student Vladimir Perić, this task is almost completed.

- Some people were retroactively added to the AUTHORS file.

- Added a solver for a special case of the Riccati equation in the ODE
  module.

- Iterated derivatives are pretty printed in a concise way.

- Fix a bug with integrating functions with multiple DiracDeltas.

- Add support for Matrix.norm() that works for Matrices (not just vectors).

- Improvements to the Groebner bases algorithm.

- Plot.saveimage now supports a StringIO outfile

- Expr.as_ordered_terms now supports non lex orderings.

- diff now canonicalizes the order of differentiation symbols.  This is
  so it can simplify expressions like `f(x, y).diff(x, y) - f(x,
  y).diff(y, x)`.  If you want to create a Derivative object without
  sorting the args, you should create it explicitly with `Derivative`,
  so that you will get `Derivative(f(x, y), x, y) != Derivative(f(x, y), y, x)`.
  Note that internally, derivatives that can be computed are always
  computed in the order that they are given in.

- Added functions `ordered_iter()` and `iterable()` for determining if
  something is an ordered iterable or normal iterable.
