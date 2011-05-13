This is the changelog for the 0.7.0 release. This is a draft.  Please help fill it out.

# Backwards compatibility breaks
WARNING: Python 2.4 will not be supported any more after this release

* no longer support creating matrices without brackets (see: issue 930)
* Renamed ode_renumber to constant_renumber
* Rename sum() to summation() (see: 3e763a8, issues 1376, 1727)
* Rename abs() to Abs() (see: 64a12a4, issue 1727)
* Rename max_, min_ to now Max, Min (see: 99a271e, issue 2153)
* Change behavior of symbols(); symbols('xyz') is now a single symbol, not three (see: f6452a8)
... ?

# Major Changes
## Polys (TODO)
Mateusz, can you write this?
## Quantum (TODO)
Brian, can you and your students write this?
* Added qubit, hilbert, Matrix support for Dagger, QFT and Shor's algorithm... I got lost already :)

# Everything else

* Implement symarray, providing numpy nd-arrays of symbols.
* update mpmath to 0.16
* Add a tensor module (see: [[http://code.google.com/p/sympy/wiki/CodeGenerationReport]])
* Don't import runtests or pytest when importing sympy (see: 7ba29a1)

* Assumptions:
 * Refine 
 * Add Predicates (see: 7c0b857, 53f0e1a, d1dd6a3..)
 * Implement a SAT solver (see: [[http://code.google.com/p/sympy/wiki/SuperchargingAssumptionsReport]], 2d96329, acfbe75, etc.)

* Core:
 * Split class Basic into new classes Expr, Boolean (see: a0ab479, 635d89c)
 * Split Atom into Atom and AtomicExpr (see: 965aa91)
 * Various sympify improvements
 * Added functionality for action verbs (can be called both as global functions and as methods e.g. a.simplify() = simplify(a) )
 * Improve handling of rationals (see: 053a045, issue 1778)
 * Major changes to factoring of integers (see: 273f450, issue 2003)
 * Optimized has() (see: c83c9b0, issue 1980; d86d08f)
 * Improvements to power (see: c8661ef, issue 1963)

* Logic
 * implies object adheres to negative normal form
 * Create new boolean class, logic.boolalg.Boolean
 * Added XOR operator (^) support 
 * Added the dpll algorithm

* isympy
 * fix the -p switch
 * Caching can be disabled

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
 * ODE improvements (see: d12a2aa, 3542041; 73fb9ac

* Integrals:
 * Various improvements (see eg. issues 1772, 1999, 1992, 1987.. etc)
 * Hydrogen radial wavefunctions added
 * Ported wigner from Sage

* Utilities:
 * Improve cartes, for generating the Cartesian product (see: b1b10ed)
 * Major improvements to the Fortran code generator (see: [[http://code.google.com/p/sympy/wiki/CodeGenerationReport]], 3383aa3, 7ab2da2, etc.)

In addition to the more noticeable changes listed above, there have been numerous other smaller additions, improvements and bug fixes in the ~2000 commits in this release. 