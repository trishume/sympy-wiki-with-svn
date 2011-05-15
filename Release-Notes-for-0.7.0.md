This is the changelog for the 0.7.0 release. This is a draft.  Please help fill it out.

# Backwards compatibility breaks

* This will be the last release of SymPy to support Python 2.4.  Dropping support for Python 2.4 will let us move forward with things like supporting Python 3, and will let use things that were introduced in Python 2.5, like with statement context managers.
* no longer support creating matrices without brackets (see: issue 930)
* Rename sum() to summation() (see: 3e763a8, issues 1376, 1727).  This was changed so that it no longer overrides the built-in sum().  The unevaluated summation is still called Sum().
* Rename abs() to Abs() (see: 64a12a4, issue 1727).  This was also changed so that it no longer overrides the built-in abs().  Note that because of __abs__ magic, you can still do abs(expr) with the built-in abs(), and it will return Abs(expr).
* Rename max_, min_ to now Max, Min (see: 99a271e, issue 2153)
* Change behavior of symbols(); symbols('xyz') is now a single symbol, not three (see: f6452a8).  Use symbols('x, y, z') or symbols('x y z').
* Split class Basic into new classes Expr, Boolean (see: a0ab479, 635d89c).  Classes that are designed to be part of standard symbolic expressions (like x**2*sin(x)) should subclass from Expr.  More generic objects that do not work in symbolic expressions but still want the basic SymPy structure like .args and basic methods like .subs() should only subclass from Basic.
* ... ?

# Major Changes
## Polys (TODO)
Mateusz, can you write this?
 
 * Improved Gröbner bases algorithm (see: ff65e9f, 891e4de, 310a585)
 * New internal representations of dense and sparse polynomials (see: 31c9aa4)
 * Implemented algorithms for real and complex root isolation (see: 3acac67, 4b75dae, fa1206e)
 * Field isomorphism algorithm (see: b097b01, 08482bf)
 * Implemented efficient orthogonal polynomials (see: b8fbd59)
 * Added configuration framework for polys (see: 33d8cdb)
 * Function for computing minimal polynomials (see: 88bf187, f800f95)
 * Function for generating Viete's formulas (see: 1027408)
 * roots() supports more classes of polynomials (e.g. cyclotomic) (see: d8c8768)
 * Added a function for recognizing cyclotomic polynomials (see: b9c2a9a)
 * Added a function for computing Horner form of polynomials (see: 8d235c7)
 * Added a function for computing symmetric reductions of polynomials (see: 6d560f3)
 * Added generators of Swinnerton-Dyer, cyclotomic, symmetric, random and interpolating polynomials (see: dad03dd, 6ccf20c, dc728d6, 2f17684, 3004db8)
 * Added a function computing isolation intervals of algebraic numbers (see: 37a58f1)
 * 

## Quantum (TODO)
Brian, can you and your students write this?

* Added qubit, hilbert, Matrix support for Dagger, QFT and Shor's algorithm... I got lost already :)

## What other major changes?

# Everything else

* Implement symarray, providing numpy nd-arrays of symbols.
* update mpmath to 0.16
* Add a tensor module (see: [[http://code.google.com/p/sympy/wiki/CodeGenerationReport]])

* Assumptions:
 * Refine 
 * Add Predicates (see: 7c0b857, 53f0e1a, d1dd6a3..)
 * Implement a SAT solver (see: [[http://code.google.com/p/sympy/wiki/SuperchargingAssumptionsReport]], 2d96329, acfbe75, etc.)

* Core:
 * Split Atom into Atom and AtomicExpr (see: 965aa91)
 * Various sympify improvements
 * Added functionality for action verbs (many functions can be called both as global functions and as methods e.g. a.simplify() == simplify(a))
 * Improve handling of rational strings (see: 053a045, issue 1778)
 * Major changes to factoring of integers (see: 273f450, issue 2003)
 * Optimized has() (see: c83c9b0, issue 1980; d86d08f)
 * Improvements to power (see: c8661ef, issue 1963)
 * Added range and lexicographic syntax to `symbols()` and `var()` (see: f6452a8, 9aeb220, 957745a)

* Logic
 * implies object adheres to negative normal form
 * Create new boolean class, logic.boolalg.Boolean
 * Added XOR operator (^) support 
 * Added the dpll algorithm

* isympy
 * fix the -p switch
 * Caching can be disabled
 * lexicographic order is now the default.  Now finally things will print as x**2 + x + 1 instead of 1 + x + x**2.  You can get the old order (and other orderings) by setting the -o option to isympy.

* Functions:
 * Added Piecewise, B-splines
 * Spherical Bessel function of the second kind implemented
 * Add series expansions of multivariate functions (see: d4d351d)

* Series:
 * Implement a function to calculate residues, residue()
 * Implement nseries and lseries to handle x0!=0, series should be more robust now (see: 2c99999, issues 2122-2124)
 * Improvements to Gruntz algorithm

* Matrices:
 * Add elementwise product (Hadamard product)
 * Extended QR factorization for general full ranked mxn matrices
 * Remove deprecated functions zero(), zeronm(), one() (see: 5da0884)

* Geometry:
 * Various improvements to Ellipse
 * Updated documentation to numpy standard
 * Polygon and Line improvements
 * Allow all geometry objects to accept a tuple as Point args

* Solvers:
 * ODE improvements (see: d12a2aa, 3542041; 73fb9ac)

* Integrals:
 * Various improvements (see eg. issues 1772, 1999, 1992, 1987.. etc)
 * Hydrogen radial wavefunctions added
 * Ported wigner from Sage

* Utilities:
 * Improve cartes, for generating the Cartesian product (see: b1b10ed)
 * Major improvements to the Fortran code generator (see: [[http://code.google.com/p/sympy/wiki/CodeGenerationReport]], 3383aa3, 7ab2da2, etc.)

In addition to the more noticeable changes listed above, there have been numerous other smaller additions, improvements and bug fixes in the ~2000 commits in this release. See the git log for a full list of all changes. You can also see the issues closed since the last release [here](http://code.google.com/p/sympy/issues/list?can=1&q=closed-after%3A2010%2F3%2F17+closed-before%3A2011%2F5%2F14+&sort=closed&colspec=ID+Type+Status+Priority+Milestone+Owner+Summary+Stars+Closed&cells=tiles). (TODO: change closed-before date with the actual date of the release)