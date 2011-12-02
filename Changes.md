

# Introduction

This page documents the major changes made to !SymPy in each release and git (small bugfixes are not included here).

<wiki:comment>
We try to mimic http://kernelnewbies.org/LinuxChanges
</wiki:comment>

## git

You can see all changes in the git repository here:

http://git.sympy.org/?p=sympy.git;a=summary

Find the latest release tag and see what is new since then.

## 0.7.1
date: 29 July 2011

You can see the release notes for this release at https://github.com/sympy/sympy/wiki/Release-Notes-for-0.7.1.

## 0.7.0
date: 28 June 2011

You can see the release notes for this release at https://github.com/sympy/sympy/wiki/Release-Notes-for-0.7.0.

## 0.6.7

date: 17 March 2010

  * fix a bug where bin/test and bin/doctest would be installed into /usr/bin
  * fix an example for recent matplotlib versions
  * some fixes for Python 2.4 and 2.5
  * try to expand integrand if integration fails
  * improved isprime() (pseudoprimes were falsely reported as being prime)
  * runtests.py prints less when testing documentation
  * ODE code clean-up and fixes
  * runtests.py is now more verbose about expected failures to avoid confusion
  * update mpmath to version 0.14
  * improvements to second quantization module and coupled cluster example
  * implement visual factorint()
  * implement symarray(): numpy array of sympy symbols
  * documentation fixes and some bugfixes

The following 7 people have contributed patches to this release:

  * Aaron Meurer
  * Chris Smith
  * Fernando Perez
  * Øyvind Jensen
  * Ronan Lamy
  * Toon Verstraelen
  * Vinzent Steinberg

The following 5 people helped reviewing patches:

  * Aaron Meurer
  * Chris Smith
  * Ondrej Certik
  * Ronan Lamy
  * Vinzent Steinberg

## 0.6.6

date: 20 December 2009

  * many documentation improvements, including docstrings and doctests
  * new assumptions system (GSoC) (See [http://docs.sympy.org/modules/assumptions.html assumptions documentation] for more information or have a look at [http://fseoane.net/blog/?cat=16 Fabian's blog].)
    * Note: This is going to replace the old assumption system. It is encouraged to use it for new code, however it is not completely finished and parts of sympy have yet to be rewritten to use it; this scheduled for the 0.7 release. 
  * improvements to test runner
  * printing improvements (especially LaTeX, but also mathml and pretty printing)
  * discriminant of polys 
  * block diagonal methods for matrices
  * vast improvements to solving of ODEs (GSoC) (See [http://docs.sympy.org/modules/solvers/ode.html ODE documentation] for full details or [http://asmeurersympy.wordpress.com/ Aaron's blog]). 
  * logcombine function
  * improvements to sets
  * better trigonometric simplification
  * improvements to piecewise functions
  * improvements to solve() and nsolve()
  * improvements to as_numer_denom()
  * much better quartic and cubic polynomial rootfinding
  * code refactoring and cleanup
  * physics: coupled clusters and wick expansion
  * matrices: symbolic QR solving
  * mpmath updated
  * pyglet updated
  * many, many bug fixes and small improvements

The following 22 people have contributed patches to this release (sorted alphabetically):

  * Aaron Meurer
  * Alan Bromborsky
  * Andy R. Terrel
  * Bill Flynn
  * Chris Smith
  * Eh Tan
  * Fabian Pedregosa
  * Fredrik Johansson
  * Jorn Baayen
  * Julio Idichekop Filho
  * Kevin Goodsell
  * Łukasz Pankowski
  * Luke Peterson
  * Øyvind Jensen
  * Ondrej Certik
  * Oscar Benjamin
  * Priit Laes
  * Renato Coutinho
  * Ronan Lamy
  * Ryan Krauss
  * Ted Horst
  * Toon Verstraelen
  * Vinzent Steinberg

The following 10 people helped reviewing patches:

  * Aaron Meurer
  * Andy R. Terrel
  * Chris Smith
  * Fabian Pedregosa
  * Fredrik Johansson
  * Luke Peterson
  * Mateusz Paprocki
  * Ondrej Certik
  * Ronan Lamy
  * Vinzent Steinberg

## 0.6.5

date: 17 July 2009

This release has been marked by improved documentation,
C code generation, solve and dsolve improvements, mpmath update, a new
logic module and the start of Google's Summer of Code program.

Source distribution can be downloaded from
http://sympy.googlecode.com/files/sympy-0.6.5.rc2.tar.gz

Windows binaries can be downloaded from
http://sympy.googlecode.com/files/sympy-0.6.5.rc2.win32.exe

Major changes include:

  * Geometric Algebra Improvements
    * Upgrade GA module with left and right contraction operations
    * Add intersection test for the vertical segment, reimplementation of convex_hull (Florian Mickler)
  * Implement series() as function (Barry Wardell)
  * Core improvements
     * Refactor Number._eval_power (Fabian Pedregosa)
     * fix bugs in Number._eval_power (Chris Smith)
  * Matrix improvements:
     * Improve jacobian function, introduce vec and vech (Ben Goodrich)
  * Solver improvements:
     * solutions past linear factor found in tsolve (Chris Smith)
     * refactor sympy.solvers.guess_solve_strategy (Fabian Pedregosa)
     * Small cleanups to the ODE solver and tests. (Priit Laes)
     * Fix corner case for Bernoulli equation. (Priit Laes)
  * Improvements on partial differential equations solvers (Priit Laes)
    * Added separation of variables for PDEs (Priit Laes)
  * Expand improvements (Aaron Meurer)
     * Refactoring
     * exp(x) exp(y)  is no longer automatically combined into exp(x+y), use powsimp for that
  * Documentation improvements:
     * Test also documentation under doc/ (Fabian Pedregosa)
     * Added many docstrings
     * Fix Sphinx complaints/warnings/errors (Priit Laes)
     * Doctest coverage (Ondrej Certik)
  * New logic module (Fabian Pedregosa)
     * Efficient DPLL algorithm (Fabian Pedregosa)
  * LaTeX printer improvements:
     * Handle standard form in the LaTeX printer correctly (Freddie Witherde)
     * Latex: _print_Mul fix (issue 1282) (Nicolas Pourcelot)
     * Robust printing of latex sub and superscripts (Toon Verstraelen)
     * sorting _print_Add output using a main variable (Ryan Krauss)
     * Matrix printing improvements (Ryan Krauss)
  * MathML printing improvements:
     * MathML's printer extended (Thomas Sidoti)
  * Testing framework improvements
     * Make tests pass without the "py" module (Ondrej Certik)
  * Polynomial module improvements:
     * Fixed subresultant PRS computation and ratint() (Mateusz Paprocki)
     * Removed old module sympy.polynomials (Priit Laes)
  * limit fixes:
     * Compute the finite parts of the limit of a sum by direct substitution (Ronan Lamy)
  * Test coverage script (Ronan Lamy)
  * Code quality improvements (remove string exceptions, code quality test improvements) (Tomasz Buchert)
  * C code generation (Toon Verstraelen)
  * Update mpmath (Fredrik Johansson, Vinzent Steinberg)

The following people submitted code for this release (sorted by number of patches):

  *	Fabian Pedregosa
  *	Ondrej Certik
  *	Priit Laes
  *	Vinzent Steinberg
  *	Toon Verstraelen
  *	Tomasz Buchert
  *	Nicolas Pourcelot
  *	Aaron Meurer
  *	Florian Mickler
  *	Jochen Voss
  *	Alan Bromborsky
  *	Barry Wardell
  *	Riccardo Gori
  *	Chris Smith
  *	Freddie Witherden
  *	Ben Goodrich
  *	Ronan Lamy
  *	Akshay Srinivasan
  *	Johann Cohen-Tanugi
  *	Luke Peterson
  *	Mateusz Paprocki
  *	Ted Horst
  *	Thomas Sidoti
  *	Vinay Kumar

## 0.6.4

date: 4 April 2009

  * robust and fast (still pure Python) multivariate factorization
  * sympy works with pickle protocol 2 (thus works in ipython parallel)
  * `./sympy test` now uses our testing suite and it tests both regular tests and doctests
  * examples directory tidied up
  * more trigonometric simplifications
  * polynomial roots finding and factoring vastly improved
  * mpmath updated
  * many bugfixes (more than 200 patches since the last release)

The following 21 people have contributed patches to this release (sorted by the number of patches):

  *  Ondrej Certik
  *  Mateusz Paprocki
  *  Fabian Seoane
  *  Andy R. Terrel
  *  Freddie Witherden
  *  Robert Kern
  *  Priit Laes
  *  Riccardo Gori
  *  Fredrik Johansson
  *  Aaron Meurer
  *  Alan Bromborsky
  *  Brian E. Granger
  *  Felix Kaiser
  *  Kirill Smelkov
  *  Vinzent Steinberg
  *  Akshay Srinivasan
  *  Andrew Docherty
  *  Andrew Straw
  *  Henrik Johansson
  *  Kaifeng Zhu
  *  Ted Horst

The following people helped review patches:

  * Riccardo Gori
  * Fabian Seoane
  * Vinzent Steinberg
  * Gael Varoquaux
  * Fredrik Johansson
  * Robert Kern
  * Alan Bromborsky
  * Ondrej Certik

## 0.6.3

date: 19 November 2008

  * port to python2.6 (all tests pass)
  * port to jython (all tests pass except those depending on the "ast" module)
  * true division fixed (all tests pass with "-Qnew" Python option)
  * [http://buildbot.sympy.org/ buildbot.sympy.org] created, sympy is now regularly tested on python2.4, 2.5, 2.6 on both i386 and amd64 architectures.
  * py.bench -- py.test based benchmarking added
  * bin/test -- simple py.test like testing framework, without external dependencies, nice colored output
  * most limits now work
  * factorization over `Z[x]` greatly improved
  * Piecewise function added
  * nsimplify() implemented
  * symbols and var syntax unified
  * C code printing
  * many bugfixes

The following 17 people have contributed patches to this release:

  * Andy R. Terrel
  * Kirill Smelkov
  * Stepan Roucka
  * Riccardo Gori
  * Fabian Seoane
  * Fredrik Johansson
  * Mateusz Paprocki
  * Sebastian Kreft
  * Sebastian Krämer
  * Vinzent Steinberg
  * Boris Timokhin
  * Alan Bromborsky
  * Henrik Johansson
  * Hubert Tsang
  * Konrad Meyer
  * Robert (average.programmer)
  * Ondrej Certik

The following people helped review patches:

  * Andy R. Terrel
  * Riccardo Gori
  * Fredrik Johansson
  * Vinzent Steinberg
  * Fabian Seoane
  * Kirill Smelkov
  * Sebastian Krämer
  * Mateusz Paprocki
  * Stepan Roucka
  * Friedrich Hagedorn
  * Brian Granger
  * Ondrej Certik

## 0.6.2

date: 17 August 2008

##### user-visible changes:

  * !SymPy is now 50% faster on average (cache:on) and 130% (cache:off) compared to previous release.
  * adaptive and faster evalf() ([http://hg.sympy.org/sympy/rev/f2603e998194 commit 1], [http://hg.sympy.org/sympy/rev/16104562dc53 2], [http://hg.sympy.org/sympy/rev/77e7ddf1e3f4 3], [http://hg.sympy.org/sympy/rev/ee9372681a64 4], [http://hg.sympy.org/sympy/rev/e61438b324d3 5])
  * evalf: numerical summation of hypergeometric series ([http://hg.sympy.org/sympy/rev/40b3cff7b9ff commit])
  * evalf: fast and accurate numerical summation ([http://hg.sympy.org/sympy/rev/95eca1e72c47 commit 1], [http://hg.sympy.org/sympy/rev/f0f06daa11e7 2], [http://hg.sympy.org/sympy/rev/ef0395c6b6c4 3])
  * evalf: oscillatory quadrature ([http://hg.sympy.org/sympy/rev/353584ecf19d commit])
  * integrals now support variable transformation ([http://hg.sympy.org/sympy/rev/32a178e2a8b9 commit])
  * we can now integrate(f(x)⋅diff(f(x),x), x) ([http://hg.sympy.org/sympy/rev/4810adeada5c commit 1], [http://hg.sympy.org/sympy/rev/ce9a981c8c64 2], [http://hg.sympy.org/sympy/rev/73be255e7992 3])
  * we can now solve a⋅cos(x)=y ([http://hg.sympy.org/sympy/rev/953090f5209e comit]) and exp(x)+exp(-x)=y ([http://hg.sympy.org/sympy/rev/61478855c294 commit 1], [http://hg.sympy.org/sympy/rev/b43beaab3bb1 2])
  * printing system refactored ([http://hg.sympy.org/sympy/rev/d56cca1785c5 commit 1], [http://hg.sympy.org/sympy/rev/d8c5c92db412 2], [http://hg.sympy.org/sympy/rev/db09ebd06fb4 3], [http://hg.sympy.org/sympy/rev/b13d7cb0fde2 4], [http://hg.sympy.org/sympy/rev/c7fd2ed49ec3 5], [http://hg.sympy.org/sympy/rev/58eade7e7944 6], [http://hg.sympy.org/sympy/rev/786a5c7b7dfa 7], [http://hg.sympy.org/sympy/rev/0e69a491ac1d 8], [http://hg.sympy.org/sympy/rev/5cb4de19cc66 9], [http://hg.sympy.org/sympy/rev/a735af6bfe76 10], [http://hg.sympy.org/sympy/rev/d04abe71fd96 11], [http://hg.sympy.org/sympy/rev/8512eff4ce57 12], [http://hg.sympy.org/sympy/rev/b996f9beb406 13], [http://hg.sympy.org/sympy/rev/c4188be75ff5 14], [http://hg.sympy.org/sympy/rev/2f2fea6ab447 15], [http://hg.sympy.org/sympy/rev/ca74a684946c 16], [http://hg.sympy.org/sympy/rev/6809c89c8913 17], [http://hg.sympy.org/sympy/rev/6f7e70376ba3 18], [http://hg.sympy.org/sympy/rev/4b31dc02128c 19], [http://hg.sympy.org/sympy/rev/45bb843aa79a 20], [http://hg.sympy.org/sympy/rev/5a03af88b9a2 21])
  * pprint: new symbol for multiply in unicode mode(x*y -> x⋅y) ([http://hg.sympy.org/sympy/rev/96b3bd3dbb39 commit])
  * pprint: matrices now look much better ([http://hg.sympy.org/sympy/rev/0460ebc36574 commit]) + example ([http://hg.sympy.org/sympy/rev/7c36e4e62552 commit 1], [http://hg.sympy.org/sympy/rev/77ba6e02c3b9 2])
  * printing of dicts and sets are now more human-friendly ([http://hg.sympy.org/sympy/rev/d2142abff624 commit 1], [http://hg.sympy.org/sympy/rev/88c92a032421 2], [http://hg.sympy.org/sympy/rev/210c0b2c41f3 3], [http://hg.sympy.org/sympy/rev/52013020a48d 5])
  * latex: now supports sub- and superscripts in symbol names ([http://hg.sympy.org/sympy/rev/2e99982a94f4 commit])
  * !RootSum.doit, now works on all roots ([http://hg.sympy.org/sympy/rev/16ecba299530 commit])
  * Wild can now have additional predicates ([http://hg.sympy.org/sympy/rev/af81bfff9c5f commit])
  * numpy-like zeros and ones functions ([http://hg.sympy.org/sympy/rev/3ff3349e6df1 commit 1], [http://hg.sympy.org/sympy/rev/a87f81d5b17f 2], [http://hg.sympy.org/sympy/rev/4c866cf85b39 3], [http://hg.sympy.org/sympy/rev/945423d11129 4])
  * var('x,y,z') now works ([http://hg.sympy.org/sympy/rev/1030f3b48a9e commit])
  * many bug fixes

##### changes that affected speed:

  * `((x+y+z)**50).expand()` is now 4.8x faster ([http://hg.sympy.org/sympy/rev/af4887673d3d commit 1], [http://hg.sympy.org/sympy/rev/a8b30539405e 2] + following changes which all summed up)
  * big assumptions cleanup and rewrite ([http://hg.sympy.org/sympy/rev/282cd00aaaa1 commit1], [http://hg.sympy.org/sympy/rev/a8301bbe56fc 2], [http://hg.sympy.org/sympy/rev/d455e5d19826 3], [http://hg.sympy.org/sympy/rev/27890fc7df0a 4], [http://hg.sympy.org/sympy/rev/913d34d179c5 5], [http://hg.sympy.org/sympy/rev/78f62e09c6b3 6], [http://hg.sympy.org/sympy/rev/2686e5b35812 7], [http://hg.sympy.org/sympy/rev/44046f890462 8], [http://hg.sympy.org/sympy/rev/2f6b3d5cc571 9], [http://hg.sympy.org/sympy/rev/a6ddc80bd679 10], [http://hg.sympy.org/sympy/rev/86fb85c10898 11], [http://hg.sympy.org/sympy/rev/27bf7b1fcf51 12], [http://hg.sympy.org/sympy/rev/3da1ce1a590d 13], [http://hg.sympy.org/sympy/rev/ac93092655ce 14], [http://hg.sympy.org/sympy/rev/7fd4ccbf8177 15], [http://hg.sympy.org/sympy/rev/07d1d690579c 16], [http://hg.sympy.org/sympy/rev/8a93cd729d4b 17], [http://hg.sympy.org/sympy/rev/ac803c9988d1 18], [http://hg.sympy.org/sympy/rev/7077bdb157ad 19], [http://hg.sympy.org/sympy/rev/960c13f64fbc 20], [http://hg.sympy.org/sympy/rev/65694f0c4930 21], [http://hg.sympy.org/sympy/rev/37e7c1592ee4 22], [http://hg.sympy.org/sympy/rev/929e567d9d59 23], [http://hg.sympy.org/sympy/rev/37f28f01a0a8 24], [http://hg.sympy.org/sympy/rev/f082b056f0ef 25])
  * access to all object attributes is now ~2.5 times faster ([http://hg.sympy.org/sympy/rev/f5aa87669950 commit])
  * we try not to let 'is_commutative' to go through (slow) assumptions path ([http://hg.sympy.org/sympy/rev/ee75a18ca7b2 commit 1], [http://hg.sympy.org/sympy/rev/de81757d7898 2])
  * Add/Mul were optimized (for some cases significantly) ([http://hg.sympy.org/sympy/rev/66657a9d94f4 commit 1], [http://hg.sympy.org/sympy/rev/3950c0a9c67f 2], [http://hg.sympy.org/sympy/rev/964fd3f4314d 3], [http://hg.sympy.org/sympy/rev/3b39ffb44b3a 4], [http://hg.sympy.org/sympy/rev/be61828f7a46 5], [http://hg.sympy.org/sympy/rev/8a31d8eebe32 6])

##### general cleanup:

  * isympy and sympy.interactive code were merged ([http://hg.sympy.org/sympy/rev/d0d91349a007 commit])
  * multiple inheritance removed (!NoArithMeths, !NoRelMeths, !RelMeths, !ArithMeths are gone) ([http://hg.sympy.org/sympy/rev/06cad30fdaef commit 1], [http://hg.sympy.org/sympy/rev/aaf5c230783e 2], [http://hg.sympy.org/sympy/rev/79d490a601ab 3], [http://hg.sympy.org/sympy/rev/fa9012e14995 4], [http://hg.sympy.org/sympy/rev/05e95f08f3c5 5], [http://hg.sympy.org/sympy/rev/8744641b59a3 6])
  * .nseries() is now used as default in .series()
  * doctesting was made more robust ([http://hg.sympy.org/sympy/rev/955d16bc63d3 commit 1], [http://hg.sympy.org/sympy/rev/bf338ee0722f 2], [http://hg.sympy.org/sympy/rev/ceb485e51516 3], [http://hg.sympy.org/sympy/rev/f09b630df594 4], [http://hg.sympy.org/sympy/rev/490a46fa2482 5])

The following 11 people have contributed patches to this release:


  * Sebastian Krämer
  * Fredrik Johansson
  * Ondřej Čertík
  * Mateusz Paprocki
  * Stefano Maggiolo
  * Robert Cimrman
  * Sebastian Krause
  * Bastian Weber
  * Sebastian Kreft
  * Štěpán Roučka
  * Kirill Smelkov

The following people helped review patches:

  * Riccardo Gori
  * Fredrik Johansson
  * Kirill Smelkov
  * Ondřej Čertík
  * Mateusz Paprocki

## 0.6.1

date: 22 July 2008

##### user-visible changes:

  * almost all functions and constants can be converted to Sage ([http://hg.sympy.org/sympy/rev/414880e1c8be commit 1], [http://hg.sympy.org/sympy/rev/245efb21d82f 2])
  * univariate factorization algorithm was fixed ([http://hg.sympy.org/sympy/rev/1bf5f90b3a97 commit])
  * .evalf() method fixed, pi.evalf(10**6) calculates 1 000 000 digits of pi ([http://hg.sympy.org/sympy/rev/c46eed7e289f commit 1])
  * @threaded decorator ([http://hg.sympy.org/sympy/rev/c45b351e93cf commit 1], [http://hg.sympy.org/sympy/rev/26ac349099d2 2], [http://hg.sympy.org/sympy/rev/affb2ee1be2d 3])
  * more robust solvers, polynomials and simplification (about 60 patches from Mateusz, see the hg history)
  * better simplify, that makes a solver more robust ([http://hg.sympy.org/sympy/rev/93a2ec3a7651 commit])
  * optional compiling of functions to machine code ([http://hg.sympy.org/sympy/rev/8af2d333319c commit])
  * msolve: solving of nonlinear equation systems using Newton's method ([http://hg.sympy.org/sympy/rev/c70e9302f0d4 commit])

##### changes that affected speed:

  * `((x+y+z)**50).expand()` is now 3 times faster ([http://hg.sympy.org/sympy/rev/16cfc09420ee commit])
  * caching was removed from the Order class: 1.5x speedups in series tests ([http://hg.sympy.org/sympy/rev/c23f4a589832 commit 1], [http://hg.sympy.org/sympy/rev/aee6b586dbca 2], [http://hg.sympy.org/sympy/rev/e192c4e04e2e 3], [http://hg.sympy.org/sympy/rev/ff575d1e085b 4], [http://hg.sympy.org/sympy/rev/d09500d91a83 5])

The following 8 people have contributed patches to this release:

  * Mateusz Paprocki
  * Vinzent Steinberg
  * Fredrik Johansson
  * Riccardo Gori
  * Kirill Smelkov
  * Štěpán Roučka
  * Ali Raza Syed
  * Ondřej Čertík

The following people helped review patches:

  * Riccardo Gori
  * Fredrik Johansson
  * Kirill Smelkov
  * Ondřej Čertík
  * Mateusz Paprocki

## 0.6.0

date: 7 July 2008

##### user-visible changes:

 * all documentation wiki pages moved to [http://docs.sympy.org/ docs.sympy.org]
 * mpmath was integrated in !SymPy, numerics module removed
 * mpmath can use gmpy optionally, thus [http://wiki.sympy.org/wiki/Million_digits_of_pi calculating] 1000000 digits of pi in 7.5s
 * Common subexpression elimination implemented ([http://hg.sympy.org/sympy/rev/f26c5d4fd984 commit 1], [http://hg.sympy.org/sympy/rev/d799b0e232f2 2], [http://hg.sympy.org/sympy/rev/a899701f1e4f 3], [http://hg.sympy.org/sympy/rev/841260b1596e 4]), see [http://docs.sympy.org/modules/rewriting.html#module-sympy.simplify.cse_main docs]
 * roots, !RootsOf, !RootSum implemented ([http://hg.sympy.org/sympy/rev/a620a8af6134 commit])
 * lambdify() now accepts Matrices ([http://hg.sympy.org/sympy/rev/f5000a5a06df commit])
 * Matrices polished and spedup ([http://hg.sympy.org/sympy/rev/3d48d6181a30 commit 1], [http://hg.sympy.org/sympy/rev/62fd8a6aebca 2], [http://hg.sympy.org/sympy/rev/5ce3cdd10ed0 3], [http://hg.sympy.org/sympy/rev/22e3cedc3386 4], [http://hg.sympy.org/sympy/rev/9c285548be1a 5], [http://hg.sympy.org/sympy/rev/0842457787a9 6], [http://hg.sympy.org/sympy/rev/c6e57bb8de9a 7], [http://hg.sympy.org/sympy/rev/ccebd03423df 8], [http://hg.sympy.org/sympy/rev/86b9ff6c04f5 9])
 * source command implemented ([http://hg.sympy.org/sympy/rev/c81de1a03811 commit 1], [http://hg.sympy.org/sympy/rev/c0b091408696 2])
 * Polys were made the default polynomials in !SymPy ([http://hg.sympy.org/sympy/rev/a45312e68f12 commit 1], + many following commits)
 * Add, Mul, Pow now accept evaluate=False argument ([http://hg.sympy.org/sympy/rev/c51330c0f3da commit])

The following 12 people have contributed patches to this release:

  * Mateusz Paprocki
  * Fredrik Johansson
  * Robert Kern
  * Riccardo Gori
  * Sebastian Krämer
  * Case Van Horsen
  * Vinzent Steinberg
  * Roberto Nobrega
  * Friedrich Hagedorn
  * David Roberts
  * Kirill Smelkov
  * Ondřej Čertík

The following people helped review patches:

  * Kirill Smelkov
  * Mateusz Paprocki
  * Robert Kern
  * Vinzent Steinberg
  * Fredrik Johansson
  * Sebastian Krämer
  * Ondřej Čertík

## 0.5.15

date: 24 May 2008

##### user-visible changes:

  * all !SymPy functions support vector arguments, e.g. sin([1, 2, 3]) ([http://hg.sympy.org/sympy/rev/3cff481efa3b commit 1], [http://hg.sympy.org/sympy/rev/0b48760c55f9 2])
  * lambdify can now use numpy/math/mpmath ([http://hg.sympy.org/sympy/rev/e513289b6a6b 1], [http://hg.sympy.org/sympy/rev/99999069151e 2], [http://hg.sympy.org/sympy/rev/7b1100a86d25 3])
  * the order of lambdify arguments has changed ([http://hg.sympy.org/sympy/rev/7cc82cfb14fc commit])
  * all !SymPy objects are pickable ([http://hg.sympy.org/sympy/rev/f94ae6e9875e commit 1], [http://hg.sympy.org/sympy/rev/e57b07581a31 2], [http://hg.sympy.org/sympy/rev/fa515a8867af 3])
  * simplify improved and made more robust ([http://hg.sympy.org/sympy/rev/e470371c5aae commit])
  * broken limit_series was removed, we now have just one limit implementation ([http://hg.sympy.org/sympy/rev/8c54a835ad73 commit 1], [http://hg.sympy.org/sympy/rev/9f0c92ddfebd 2], [http://hg.sympy.org/sympy/rev/9dae4855ec6f 3])
  * limits now use .nseries ([http://hg.sympy.org/sympy/rev/993079823dfe commit])
  * .nseries() improved a lot ([http://hg.sympy.org/sympy/rev/e627c389bf35 commit 1], [http://hg.sympy.org/sympy/rev/04a4fff3127f 2], [http://hg.sympy.org/sympy/rev/2917e1061a1b 3])
  * Polys improved ([http://hg.sympy.org/sympy/rev/518fc875fed3 commit])
  * Basic kronecker delta and Levi-Civita implementation ([http://hg.sympy.org/sympy/rev/1d61eb463510 commit])

The following 8 people have contributed patches to this release:

  * Sebastian Krämer
  * Friedrich Hagedorn
  * Mateusz Paprocki
  * Saroj Adhikari
  * Vinzent Steinberg
  * David Roberts
  * Nimish Telang
  * Ondřej Čertík

## 0.5.14

date: 26 Apr 2008

##### user-visible changes:

  * !SymPy is now 25% faster on average compared to the previous release (see below)
  * Documentation was improved a *lot* ([http://hg.sympy.org/sympy/rev/26d75a5b7dbc commit 1], [http://hg.sympy.org/sympy/rev/a0a01fc08c63 2], [http://hg.sympy.org/sympy/rev/526612998a02 3]). See http://docs.sympy.org/
  * `rsolve_poly` & `rsolve_hyper` fixed ([http://hg.sympy.org/sympy/rev/191d906f553b commit 1], [http://hg.sympy.org/sympy/rev/95722c586c3c 2])
  * subs and subs_dict unified to .subs() ([http://hg.sympy.org/sympy/rev/c78c01651791 commit 1], [http://hg.sympy.org/sympy/rev/cf7db1715d61 2])
  * faster and more robust polynomials module ([http://hg.sympy.org/sympy/rev/eae5a978e965 commit 1], [http://hg.sympy.org/sympy/rev/a2b46b6a9339 2], [http://hg.sympy.org/sympy/rev/068fe612ab61 3], [http://hg.sympy.org/sympy/rev/94ce7584098a 4],  [http://hg.sympy.org/sympy/rev/e4e392eebac5 5],  [http://hg.sympy.org/sympy/rev/d8110613024e 6],  [http://hg.sympy.org/sympy/rev/58d8d9eb2cfa 7],  [http://hg.sympy.org/sympy/rev/911965062220 8],  [http://hg.sympy.org/sympy/rev/d3fd80444cb6 9],  [http://hg.sympy.org/sympy/rev/ac727777a83a 10],  [http://hg.sympy.org/sympy/rev/176de6403477 11],  [http://hg.sympy.org/sympy/rev/a9fc641351aa 12],  [http://hg.sympy.org/sympy/rev/4a71cecc65f4 13], [http://hg.sympy.org/sympy/rev/90caafd36b5a 14], ..., look into the hg history)
  * improved Matrix.det(), implemented Berkowitz algorithm ([http://hg.sympy.org/sympy/rev/c8cbb6c5e78d commit 1], [http://hg.sympy.org/sympy/rev/6ab14eeeda3e 2])
  * improved isympy (interactive shell for !SymPy) ([http://hg.sympy.org/sympy/rev/075af554b091 commit 1], [http://hg.sympy.org/sympy/rev/01b152988acb 2], [http://hg.sympy.org/sympy/rev/194752e14bd7 3], [http://hg.sympy.org/sympy/rev/58cddca75b8f 4], [http://hg.sympy.org/sympy/rev/397a1bf465b9 5], [http://hg.sympy.org/sympy/rev/82d6521722e9 6])
  * pretty-printing improved ([http://hg.sympy.org/sympy/rev/16f56992f467 commit 1], [http://hg.sympy.org/sympy/rev/31c518a87450 2], [http://hg.sympy.org/sympy/rev/e12accf6a9d1 3])
  * Rel, Eq, Ne, Lt, Le, Gt, Ge implemented ([http://hg.sympy.org/sympy/rev/4bb011af2d0c commit 1])
  * Limit class represents unevaluated limits now ([http://hg.sympy.org/sympy/rev/936e73c6bafd commit 1]) 
  * Bailey-Borwein-Plouffe algorithm (finds the nth hexidecimal digit of pi without calculating the previous digits) implemented ([http://hg.sympy.org/sympy/rev/6d73013adce3 commit 1])
  * solver for transcendental equations added ([http://hg.sympy.org/sympy/rev/e2db18455951 commit 1])
  * .nseries() methods implemented (more robust/faster than .oseries) ([http://hg.sympy.org/sympy/rev/81f8e2c98500 commit 1], [http://hg.sympy.org/sympy/rev/a2eed9dc6a91 2])
  * multivariate Lambdas implemented ([http://hg.sympy.org/sympy/rev/0097b68ac3c5 commit 1])
  
##### changes that affected speed:

  * `__eq__`/`__ne__`/`__nonzero__` returns True/False directly so dict lookups are not expensive anymore ([http://hg.sympy.org/sympy/rev/1f52bd36839c commit 1], [http://hg.sympy.org/sympy/rev/d9965888a005 2], [http://hg.sympy.org/sympy/rev/9e7131a4533b 3], [http://hg.sympy.org/sympy/rev/76542a035dd6 4], [http://hg.sympy.org/sympy/rev/92af27a9e8bd 5], [http://hg.sympy.org/sympy/rev/edcd763c6999 6])
  * `sum(x**i/i,i=1..400)` is now 4.8x faster ([http://hg.sympy.org/sympy/rev/9fa720169ed9 commit 1], [http://hg.sympy.org/sympy/rev/15fc2acb7231 2], [http://hg.sympy.org/sympy/rev/a602e5369326 3], [http://hg.sympy.org/sympy/rev/2e496abeb32b 4], [http://hg.sympy.org/sympy/rev/4962f6641827 5])
  * `isinstance(term, C.Mul)`  was replaced by `term.is_Mul` and similarly for other basic classes ([http://hg.sympy.org/sympy/rev/f83106bc39a5 commit 1], [http://hg.sympy.org/sympy/rev/a522f77cd5e9 2])

The following 15 people have contributed patches to this release:

    * Mateusz Paprocki
    * Fredrik Johansson
    * James Aspnes
    * Friedrich Hagedorn
    * Pan Peng
    * Abderrahim Kitouni
    * Nimish Telang
    * Jurjen N.E. Bos
    * Elrond der Elbenfuerst
    * Rizgar Mella
    * Felix Kaiser
    * Roberto Nobrega
    * David Roberts
    * Ondřej Čertík
    * Kirill Smelkov

## 0.5.13

date: 6 Mar 2008

##### user-visible changes:

  * !SymPy is now 2x faster in average compared to the previous release (see below)
  * `integrate()` can handle most of the basic integrals now ([http://hg.sympy.org/sympy/rev/045f9b4d28e1 commit])
  * interactive experience with isympy was improved through adding support for [], () and {} to pretty-printer, and switching to it as the default ipython printer ([http://hg.sympy.org/sympy/rev/1952e5872712 commit 1], [http://hg.sympy.org/sympy/rev/8b8d52652bc8 2], [http://hg.sympy.org/sympy/rev/9d872c1768b2 3])
  * new `trim()` function to map all non-atomic expressions, ie. functions, derivatives and more complex objects, to symbols and remove common factors from numerator and denominator. also `cancel()` was improved ([http://hg.sympy.org/sympy/rev/b36abe849cae commit 1], [http://hg.sympy.org/sympy/rev/2c7a8f13af0c 2])
  * `.expand()` for noncommutative symbols fixed ([http://hg.sympy.org/sympy/rev/f3841bb49aba commit])
  * bug in `(x+y+sin(x)).as_independent()` fixed ([http://hg.sympy.org/sympy/rev/6e53d4e4f31b commit])
  * `.subs_dict()` improved ([http://hg.sympy.org/sympy/rev/6d82fc2f132a commit])
  * support for plotting geometry objects added ([http://hg.sympy.org/sympy/rev/81b5ea2f798f commit])
  * bug in `.tangent_line()` of ellipse fixed ([http://hg.sympy.org/sympy/rev/7a4895d2a5c6 commit 1], [http://hg.sympy.org/sympy/rev/7e931942af76 2])
  * new `atan2` function and assotiated fixes for `.arg()` and expanding rational powers ([http://hg.sympy.org/sympy/rev/6b122f035a59 commit 1], [http://hg.sympy.org/sympy/rev/59e098c67d2a 2], [http://hg.sympy.org/sympy/rev/730666b691ab 3])
  * new `.coeff()` method for returning coefficient of a poly ([http://hg.sympy.org/sympy/rev/fe28b857f840 commit 1], [http://hg.sympy.org/sympy/rev/823a98e61f39 2], [http://hg.sympy.org/sympy/rev/2462e919c263 3])
  * pretty-printer now uses unicode by default ([http://hg.sympy.org/sympy/rev/3287de8a4632 commit])
  * recognition of geometric sums were generalized ([http://hg.sympy.org/sympy/rev/46592846838b commit])
  * `.is_positive` and `.is_negative` now fallback to evalf() when appropriate ([http://hg.sympy.org/sympy/rev/22824466ecc3 commit])
  * as the result `oo*(pi-1)` now correctly simplifies to `oo` ([http://hg.sympy.org/sympy/rev/595807013bfc commit])
  * support for objects which provide `__int__` method was added ([http://hg.sympy.org/sympy/rev/499b40d2b273 commit])
  * we finally started !SymPy User's Guide ([http://hg.sympy.org/sympy/rev/fdf6ca3287f9 commit 1], [http://hg.sympy.org/sympy/rev/18ad24318344 2])




##### changes that affected speed:

  * first patches with 25% speedup ([http://hg.sympy.org/sympy/rev/5db289e227f9 commit 1], [http://hg.sympy.org/sympy/rev/b8a3f509123d 2], [http://hg.sympy.org/sympy/rev/2146efe6d6ed 3], [http://hg.sympy.org/sympy/rev/9ae600a3134f 4])
  * Basic.cos et. al. removed, use C.cos instead ([http://hg.sympy.org/sympy/rev/fa487034bbb1 commit 1], [http://hg.sympy.org/sympy/rev/add2007e2df6 2], [http://hg.sympy.org/sympy/rev/5393aaff17f0 3], [http://hg.sympy.org/sympy/rev/7b94988ea0fc 4])
  * sympy.core now uses direct imports ([http://hg.sympy.org/sympy/rev/ad1660d022eb commit 1], [http://hg.sympy.org/sympy/rev/9fefd2f55cca 2])
  * sympifyit decorator ([http://hg.sympy.org/sympy/rev/0ff293ced56e commit 1], [http://hg.sympy.org/sympy/rev/09af91e6d0f5 2], [http://hg.sympy.org/sympy/rev/e41996ef5e80 3], [http://hg.sympy.org/sympy/rev/8bff90e3d9be 4], [http://hg.sympy.org/sympy/rev/cf70b0b2ef8b 5], [http://hg.sympy.org/sympy/rev/141d4a8de633 6], [http://hg.sympy.org/sympy/rev/91ab79697a8c 7])
  * speedup Integers creation and arithmetic ([http://hg.sympy.org/sympy/rev/710dd41fdbfc commit 1], [http://hg.sympy.org/sympy/rev/97558045dae6 2])
  * speedup unary operations for singleton numbers ([http://hg.sympy.org/sympy/rev/ea74c5f5c8c7 commit])
  * remove silly slowdowns from fast-path of __mul__ and __div__ ([http://hg.sympy.org/sympy/rev/89925b6ebf7b commit 1], [http://hg.sympy.org/sympy/rev/5598327b36c3 2])
  * significant speedup was achieved by reusing dummy variables ([http://hg.sympy.org/sympy/rev/5056059c2d74 commit 1], [http://hg.sympy.org/sympy/rev/5d242cf4a6cf 2], [http://hg.sympy.org/sympy/rev/c9e5d083a61d 3], [http://hg.sympy.org/sympy/rev/213ab1bc4cd7 4])
  * `is_dummy` is not an assumption anymore ([http://hg.sympy.org/sympy/rev/532e467b57a3 commit 1], [http://hg.sympy.org/sympy/rev/6a36b59d6558 2])
  * Symbols & Wilds are cached ([http://hg.sympy.org/sympy/rev/8bdffd52db99 commit 1], [http://hg.sympy.org/sympy/rev/c374fbd5b444 2], [http://hg.sympy.org/sympy/rev/6d57d8846471 3])
  * `((2+3*I)**1000).expand()` is now at least 100x faster ([http://hg.sympy.org/sympy/rev/83fd6783459b commit])
  * `.expand()` was made faster for cases where an expression is already expanded ([http://hg.sympy.org/sympy/rev/dcdb94326a38 commit])
  * rational powers of integers are now computed more efficiently ([http://hg.sympy.org/sympy/rev/7ad4283378aa commit])
  * unknown assumptions are now cached as well as known assumptions ([http://hg.sympy.org/sympy/rev/c54cd4b2c5aa commit])


##### general cleanup:

  * !BasicMeths merged into Basic ([http://hg.sympy.org/sympy/rev/652651dc90e5 commit 1], [http://hg.sympy.org/sympy/rev/a95ff37e15a1 2], [http://hg.sympy.org/sympy/rev/5b77303888e2 3], [http://hg.sympy.org/sympy/rev/241e2f20a139 4], [http://hg.sympy.org/sympy/rev/31044aa38e49 5], [http://hg.sympy.org/sympy/rev/20a6ba547347 6], [http://hg.sympy.org/sympy/rev/f4630ac97369 7], [http://hg.sympy.org/sympy/rev/873665a234e3 8])
  * cache subsystem was cleaned up -- now it supports only immutable objects ([http://hg.sympy.org/sympy/rev/0a53991871e4 commit 1], [http://hg.sympy.org/sympy/rev/3fbb7fe833ba 2], [http://hg.sympy.org/sympy/rev/d42933e9bdeb 3], [http://hg.sympy.org/sympy/rev/aea7205bb832 4], [http://hg.sympy.org/sympy/rev/1e7b490b3a7b 5])

The following 8 people have contributed patches to this release:

    * Mateusz Paprocki
    * Saroj Adhikari
    * Fredrik Johansson
    * Jaroslaw Tworek
    * Robert Kern
    * Pauli Virtanen
    * Ondřej Čertík
    * Kirill Smelkov

## 0.5.12

date: 27 Jan 2008

  * !SymPy works with !NumPy out of the box ([http://hg.sympy.org/sympy/rev/82e8ff0a8a3e commit 1], [http://hg.sympy.org/sympy/rev/1f8444d3a4c8 2])
  * !RootOf implemented ([http://hg.sympy.org/sympy/rev/8463c5d8a2de commit])
  * Lambda support works now ([http://hg.sympy.org/sympy/rev/bc07efdd1346 commit])
  * heuristic Risch method improved ([http://hg.sympy.org/sympy/rev/8463c5d8a2de commit 1], [http://hg.sympy.org/sympy/rev/2b6f19782b23 2], [http://hg.sympy.org/sympy/rev/e3fbd8889807 3], [http://hg.sympy.org/sympy/rev/d26feb6f929b 4], [http://hg.sympy.org/sympy/rev/543c897e454b 5])
  * cancel function implemented ([http://hg.sympy.org/sympy/rev/82b0caf68372 commit])
  * sqrt(x) is now equivalent to `x**(1/2)` ([http://hg.sympy.org/sympy/rev/bb8fef4b5bc6 commit 1], [http://hg.sympy.org/sympy/rev/5f2d030a8436 2])
  * Derivative is now unevaluated ([http://hg.sympy.org/sympy/rev/0c3e9db6004f commit])
  * `list2numpy()` implemented ([http://hg.sympy.org/sympy/rev/b63450f364bc commit])
  * series expansion of hyperbolic functions fixed ([http://hg.sympy.org/sympy/rev/10bcdd558957 commit])
  * sympify('lambda x: 2*x') works, plus other fixes ([http://hg.sympy.org/sympy/rev/3a6e51e4cb01 commit 1], [http://hg.sympy.org/sympy/rev/058cf905cdca 2], [http://hg.sympy.org/sympy/rev/c993a8d68dfa 3])
  * simple maxima parser implemented ([http://hg.sympy.org/sympy/rev/94e3b53cc0a2 commit])
  * `sin(x)[0]` idiom changed to `sin(x).args[0]` ([http://hg.sympy.org/sympy/rev/68f51f8e6532 commit])
  * `sin(x).series(x, 5)` idiom changed to `sin(x).series(x, 0, 5)` ([http://hg.sympy.org/sympy/rev/91de32b1b7f2 commit])
  * caching refactored ([http://hg.sympy.org/sympy/rev/8f04a0dbf0e9 commit 1], [http://hg.sympy.org/sympy/rev/53faf3605222 2], [http://hg.sympy.org/sympy/rev/5d05d3d87712 3], [http://hg.sympy.org/sympy/rev/3e298ca616a3 4], [http://hg.sympy.org/sympy/rev/926cd30629fc 5], [http://hg.sympy.org/sympy/rev/7ddd0e97eecf 6], [http://hg.sympy.org/sympy/rev/fdca1475fb92 7], [http://hg.sympy.org/sympy/rev/65ef69b91e73 8], [http://hg.sympy.org/sympy/rev/91d3e101046f 9])
  * integration of trigonometry expressions improved ([http://hg.sympy.org/sympy/rev/1d1fc98b2a44 commit])
  * pretty-print for list and tuples implemented ([http://hg.sympy.org/sympy/rev/de6494d36b36 commit])
  * Python printing implemented ([http://hg.sympy.org/sympy/rev/d0ae0c3f38e1 commit])
  * 2D plots now don't rotate in 3D, but translate instead ([http://hg.sympy.org/sympy/rev/03b3348eac8a commit])
  * many bug fixes, see the Mercurial history for details

The following 10 people have contributed patches to this release:

    * Mateusz Paprocki
    * Fredrik Johansson
    * Jaroslaw Tworek
    * Saroj Adhikari
    * Andrej Tokarčík
    * David Marek
    * Or Dvory
    * Bernhard R. Link
    * Ondřej Čertík
    * Kirill Smelkov

## 0.5.11

date: 07 Jan 2008

  * `./setup.py install` installs pyglet correctly now ([http://hg.sympy.org/sympy/rev/e01db9e8b6e6 commit])
  * `var("k")` fixed ([http://hg.sympy.org/sympy/rev/6d226ac58d84 commit])
  * script for automatic testing of plotting in pure environment added ([http://hg.sympy.org/sympy/rev/79ff83053040 commit 1], [http://hg.sympy.org/sympy/rev/535bde464363 2])

## 0.5.10

date: 04 Jan 2008

  * `view` renamed to `preview`, `pngview`, `pdfview`, `dviview` added ([http://hg.sympy.org/sympy/rev/49161c434035 commit])
  * latex printer was rewritten, `preview` uses builtin pyglet instead of pygame ([http://hg.sympy.org/sympy/rev/5cf8987d6744 commit 1], [http://hg.sympy.org/sympy/rev/2cbb895ae8b3 2])
  * square root denesting implemented ([http://hg.sympy.org/sympy/rev/f794a01195b7 commit])
  * parser of simple Mathematica expressions added ([http://hg.sympy.org/sympy/rev/54c7ceb12a75 commit])
  * !TeXmacs interface written ([http://hg.sympy.org/sympy/rev/9c1293a56e3d commit])
  * some integration fixes ([http://hg.sympy.org/sympy/rev/9a7ba9499c43 commit 1], [http://hg.sympy.org/sympy/rev/0a57a070f8ee 2], [http://hg.sympy.org/sympy/rev/c660cc8d6201 3])
  * line width in 2D plotting can be specified ([http://hg.sympy.org/sympy/rev/06fbc18a5837 commit])
  * README was updated ([http://hg.sympy.org/sympy/rev/07f59495f136 commit 1], [http://hg.sympy.org/sympy/rev/a9e246fbd464 2])
  * `pyglet` and `mpmath` were updated and moved to sympy/thirdparty ([http://hg.sympy.org/sympy/rev/35ea4723788e commit 1], [http://hg.sympy.org/sympy/rev/7e62d0d6a179 2], [http://hg.sympy.org/sympy/rev/931e4bbbec07 3], [http://hg.sympy.org/sympy/rev/f17e3ff93118 4], [http://hg.sympy.org/sympy/rev/df56f8070da9 5])
  * all `sys.path` hacks were moved to just 2 places - pyglet and examples ([http://hg.sympy.org/sympy/rev/ccd8afb93124 commit 1], [http://hg.sympy.org/sympy/rev/b62b512edd2f 2], [http://hg.sympy.org/sympy/rev/2c5c759d4eed 3])
  * !SymPy objects should work in `numpy` arrays now ([http://hg.sympy.org/sympy/rev/23473c1194e4 commit 1], [http://hg.sympy.org/sympy/rev/ab960e55ee42 2])
  * hand written sympify() parser was rewritten and simplified using Python AST ([http://hg.sympy.org/sympy/rev/ad3704adbd53 commit])
  * known issues
    * 3D plotting doesn't work in this release if you install it using `./setup.py install`. It only works if you use it directly without installing. Fixed in 0.5.11.

## 0.5.9

date: 22 Dec 2007

  * Differential solvers were polished ([http://hg.sympy.org/sympy/rev/fed3bf172cd5 commit 1], [http://hg.sympy.org/sympy/rev/31bf80b8afb4 2], [http://hg.sympy.org/sympy/rev/6aaa2e4e40af 3])
  * `isympy` now predefines `f` as a function ([http://hg.sympy.org/sympy/rev/aded3f85df9b commit])
  * Matrix printing improved ([http://hg.sympy.org/sympy/rev/9c2a2ccc5929 commit 1], [http://hg.sympy.org/sympy/rev/a603a56661ea 2], [http://hg.sympy.org/sympy/rev/506201f33afd 3], [http://hg.sympy.org/sympy/rev/f95b75a13dea 4])
  * Printing internals were documented ([http://hg.sympy.org/sympy/rev/5636b9da4297 commit])

## 0.5.8

  * `_eval_apply()` was renamed to `canonize()`
  * Added `var` from [http://www.sagemath.org SAGE]
  * Added more number theory functions
  * Spherical harmonics (Ylm) implemented
  * Functions interface simplified (`SingleValuedFunction` removed, `nofargs -> nargs`)
  * Draw negative powers in denominator nicely
  * Integration of polynomials is 10x faster
  * pyglet updated to 1.0beta2

People who contributed to this release:
  * Goutham Lakshminarayan
  * Ondřej Čertík
  * Kirill Smelkov

## 0.5.7

  * `isympy` now uses 2D unicode PrettyPrinting by default
  * Convergence acceleration / extrapolation methods for series and sequences
  * !SymPy was made ready to work nicely with SAGE
  * known issues:
      * the series expansion fails for some more complex expressions (the same problem since !SymPy 0.5.0), see the relevant [http://code.google.com/p/sympy/issues/list?can=2&q=%22series+bug%22 issues].

People who contributed to this release:
  * Fredrik Johansson
  * Ondřej Čertík
  * Kirill Smelkov

## 0.5.6

  * `_sage_()` methods implemented to convert any !SymPy expression to a SAGE expression.
  * `isympy` fixed so that it always tries the local unpacked sympy first (the one in the directory where `isympy` sits) and only then the system wide installation of sympy (Debian package for example)
  * issues fixed: 439, 436
  * known issues:
      * the series expansion fails for some more complex expressions (the same problem since !SymPy 0.5.0), see the relevant [http://code.google.com/p/sympy/issues/list?can=2&q=%22series+bug%22 issues].

## 0.5.5

  * `sympy.abc` module for quickly importing predefined symbols
  * nice pretty printing when a unicode terminal is available
  * `isympy -c python` now also supports true division
  * documentation improved (sympy module, bin/isympy and isympy's man page)
  * a lot of problems with series expansion fixed
  * patched pyglet to conform to Debian policy
  * known issues:
      * the series expansion fails for some more complex expressions (the same problem since !SymPy 0.5.0), see the relevant [http://code.google.com/p/sympy/issues/list?can=2&q=%22series+bug%22 issues].

## 0.5.4

  * `Log` and `ApplyLog` classes were simplified to `log`, as was in the 0.4.3 version (the same for all other classes, like `sin`, `cos`, etc.), for the current uptodate documentation see SymPySvn.
  * limits algorithm was fixed and it works very reliably (there are some bugs in the series facility though that make some limits fail), see this [http://groups.google.com/group/sympy/browse_thread/thread/98a044bd5ac537ca post] for more details
  * all functions arguments are now accessed using the `sin(x)[:]` idiom again, as in the 0.4.3 version (instead of the old `sin(x)._args` or `sin(x).args` which was briefly introduced in the 0.5.x series), see SymPySvn, section _accessing parameters_
  * known issues:
      * the series expansion fails for some more complex expressions (the same problem since !SymPy 0.5.0), see this [http://groups.google.com/group/sympy/browse_thread/thread/98a044bd5ac537ca post] for more details

## 0.5.3

  * faster `import sympy` statement
  * using the `integrate(3*t**2, (t,0,x))` syntax again (as was in the 0.4.3 version)
  * using true division in `isympy` (1/2 returns 0.5 instead of 0, [http://groups.google.com/group/sympy/browse_thread/thread/b59d9b6da69de886 example])
  * plotting module can `saveimage()`
  * implemented extended Risch-Norman heuristic
  * full partial fraction decomposition via `apart()`
  * added a complete set of rewrite rules for trigonometric and hyperbolic functions
  * `ComplexInfinity` renamed to `zoo`
  * known issues:
     * there are many problems in the limits module that needs to be refactored (see the  [http://code.google.com/p/sympy/issues/detail?id=298 issue 298]), but all tests pass correctly (fixed in 0.5.4)
     * the series expansion fails for some more complex expressions

## 0.5.2

  * concrete mathematics module written
  * geometry module
  * make the tarball conform to Debian policy
  * many small bugs fixed, see Issues for details
  * known issues: 
     * there are many problems in the limits module (needs to be refactored), but all tests pass correctly (fixed in 0.5.4)
     * `import sympy` is slow again (fixed in 0.5.3)
     * the series expansion fails for some more complex expressions

## 0.5.1

  * importing sympy (`import sympy`) was made a lot faster (2.4s against 0.1s)
  * known issues: 
     * there are many problems in the limits module (needs to be refactored), but all tests pass correctly (fixed in 0.5.4)
     * the series expansion fails for some more complex expressions

## 0.5.0

  * new core (from 10x to 100x speedup compared to 0.4.3)
  * multivariate functions
  * pattern matching uses the Wild and !WildFunction classes (see the [http://code.google.com/p/sympy/wiki/Tutorial Tutorial] for usage)
  * `numerics` module for fast arbitrary-precision numerical computations (much faster than the Python int and Decimal)
  * `plotting` module improved (colormaps, middle mouse button for zooming and more)
  * `sympy/modules/*` was moved to `sympy/*` and the `sympy/modules` directory was deleted
  * known issues: 
     * there are many problems in the limits module (needs to be refactored), but all tests pass correctly (fixed in 0.5.4)
     * the series expansion fails for some more complex expressions

## 0.4.3

  * assumptions improved
  * plotting module uses pyglet (no more hangups) and more improvements
  * caching Rationals -1, 0, 1, resulting in 35% speedup of tests
  * closed and pretty forms for simple summations and products
  * new term rewriting functions: collect() and together()
  * enhanced solver of polynomial equations
  * preliminary support for binary arithmetics
  * more special functions (zeta, incomplete gamma etc.) 

## 0.4.2

  * augmented matrix manipulation including 2d slicing
  * general matrix inversion
  * LU decomposition (& associated linear solver)
  * sparse matrix implementation via python dictionaries
  * hessian, jacobian of matrices, cross/dot products
  * QR decomposition & the Gram-Schmidt procedure
  * geometry module enhanced
  * factorization ( `factor(x**6-1)` )

## 0.4.1

  * added `sympy.modules.plotting.renderables` and `sympy.modules.plotting.scene` modules

## 0.4.0

  * determinants
  * groebner bases (initial implementation). multivariate division, gcd
  * Fraction free Gaussian elimination
  * resultant of polynomials
  * graphing support
  * geometry module
  * prime numbers
  * special functions (factorials)
  * renamed arguments is_commutative to commutative, is_dummy to dummy
  * MathML refactoring, renamed to __mathml__ and now uses xml.dom.minidom
  * ratsimp() for simplifying fractions added to sympy.modules.simplify
  * `exp(x+y).expand()` and `(exp(x)*exp(y)).combine()`, the same for `log`.
  * pretty printing
  * `infty` renamed to `oo`
  * Experimental plotting support via matplotlib
  * Removed class NCSymbol, use Symbol(name, is_commutative=False) instead
  * Matrix now (optionally) accepts a generating function: Matrix(2, 2, lambda i,j: i*j )
  * The class Order added
  * Pattern matching implemented (see the match() method)
  * A table of integrals implemented
  * Basic equations solving, algebraic (solve) and differential (dsolve)

## 0.3

  * symbolic matrices (normal operations like `+`, `*`, dirac and pauli matrices)
  * Pauli algebra implemented using the NCSymbol class
  * polynomials (division, gcd, square free decomposition)
  * moved printing advanced stuff out of the core (see http://code.google.com/p/sympy/wiki/PrintingMathML)
  * implemented slices on sympy's objects. Slices are now the recomended way to access all of sympy's nested objects. Examples: 
    * know the arguments of a function: `sin(x*y)[:] -- > (x*y,)`
    * arguments of Mul, Add, Pow, etc. : `(1+x)[:] --> (1,x)`
    * see also the new Basic.atoms function
  * Derivative and Limit class
  * easy usage (differentiation and other stuff) of unknown functions, see examples/relativity.py
  * complex numbers work for `exp(I*x)` and stuff. evalc() method 
  * Initial support for assumptions (for example: x = Symbol('x', is_real=True) )
  * a lot of refactorings and small fixes (the c() was renamed to Basic.sympify())
  * debian package

## 0.2

This is the first release.