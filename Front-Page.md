

!SymPy is a Python library for symbolic mathematics. It aims to become a full-featured computer algebra system (CAS) while keeping the code as simple as possible in order to be comprehensible and easily extensible. !SymPy is written entirely in Python and does not require any external libraries.


## News

!SymPy is participating in *Google Summer of Code 2011*. See our [https://github.com/sympy/sympy/wiki/GSoC-2011-Ideas ideas page].

  * *29 Jul 2011* Version 0.7.1 released ([https://github.com/sympy/sympy/wiki/Release-Notes-for-0.7.1])
  * *28 Jun 2011* Version 0.7.0 released ([https://github.com/sympy/sympy/wiki/Release-Notes-for-0.7.0])
  * *18 Mar 2011* SymPy is accepted as a [http://www.google-melange.com/gsoc/org/show/google/gsoc2011/sympy mentoring organization] for Google Summer of Code 2011
  * *23 Oct 2010* New website launched at sympy.org
  * *18 Oct 2010* The final page about the [http://code.google.com/p/sympy/wiki/GSoC2010 Google Summer of Code 2010 in SymPy] is available.
  * *17 Mar 2010* Version 0.6.7 released ([http://code.google.com/p/sympy/wiki/Changes changes])
  * *20 Dec 2009* Version 0.6.6 released ([http://code.google.com/p/sympy/wiki/Changes changes])
  * * 26 Sep 2009* Final page about the [http://code.google.com/p/sympy/wiki/GSoC2009 2009 Google Summer of Code 2009 in SymPy] is available.
  * * 23 May 2009* !SymPy is participating in the Google Summer of Code 2009. See [http://code.google.com/p/sympy/wiki/GSoC2009 GSoC2009]
  * *17 Jul 2009* Version 0.6.5 released ([http://sympy.blogspot.com/2009/07/sympy-065-released.html changes])
  * *16 Jul 2009* Version 0.6.5.rc2 released ([http://groups.google.com/group/sympy/browse_thread/thread/cdbfc9e95a8ce140 changes])
  * *11 Jul 2009* Version 0.6.5.rc1 released ([http://groups.google.com/group/sympy/browse_thread/thread/2fb2bd459fbaf936 changes])
  * *25 Jun 2009* Version 0.6.5-beta2 released ([http://code.google.com/p/sympy/wiki/Changes changes])
  * *4 Apr 2009* Version 0.6.4 released ([http://code.google.com/p/sympy/wiki/Changes changes], [http://sympy.blogspot.com/2009/04/sympy-0.html release notes])
  * *29 Mar 2009* Version 0.6.4.beta3 [http://groups.google.com/group/sympy/browse_thread/thread/b798743505304a2 released]
  * *11 Mar 2009* Version 0.6.4.beta2 [http://groups.google.com/group/sympy/browse_thread/thread/50ed6ecdb1709405/ released]
  * *9 Feb 2009* Version 0.6.4.beta1 [http://groups.google.com/group/sympy/browse_thread/thread/7f2db9097a3bfa37 released]
  * *19 Nov 2008* Version 0.6.3 released ([http://code.google.com/p/sympy/wiki/Changes changes])
  * *18 Nov 2008* Version 0.6.3.beta2 [http://groups.google.com/group/sympy/browse_thread/thread/f96c98545a3fdf25 released]
  * *17 Nov 2008* Version 0.6.3.beta1 [http://groups.google.com/group/sympy/browse_thread/thread/3ee19d16871e1c0d released]
  * *17 Aug 2008* Version 0.6.2 released ([http://code.google.com/p/sympy/wiki/Changes changes])
  * *22 Jul 2008* Version 0.6.1 released ([http://code.google.com/p/sympy/wiki/Changes changes])
  * *7 Jul 2008* Version 0.6.0 released ([http://code.google.com/p/sympy/wiki/Changes changes])
  * *24 May 2008* Version 0.5.15 released ([http://code.google.com/p/sympy/wiki/Changes changes])
  * *19 May 2008* online !SymPy shell at [http://live.sympy.org live.sympy.org] created
  * *26 Apr 2008* Version 0.5.14 released ([http://code.google.com/p/sympy/wiki/Changes changes])

OlderNews

!SymPy is easy to install and get started with. See the [http://code.google.com/p/sympy/wiki/DownloadInstallation?tm=2 download instructions] and [http://docs.sympy.org/tutorial.html tutorial] for more information. It works everywhere, where Python 2.4 or newer is installed (Linux, Windows, Mac OS X, ...).

If you found a bug, please report it in [http://code.google.com/p/sympy/issues/list Issues] or the [http://groups.google.com/group/sympy mailinglist]. 

  * [http://docs.sympy.org/ docs.sympy.org]: Documentation
  * [http://wiki.sympy.org wiki.sympy.org]: we encourage you to edit/improve/add anything to the wiki, it's open to everyone.
  * [http://live.sympy.org live.sympy.org]: try !SymPy online now

## Downloads

Use "Featured Downloads" on the right hand side. For more options and information, go to the [http://code.google.com/p/sympy/wiki/DownloadInstallation?tm=2 Downloads] tab.

git repository (you can track current progress in there): http://github.com/sympy/

## Documentation

All documentation is at: http://docs.sympy.org/

For the documentation of the development version see: http://certik.github.com/sympy/

## Features

Currently, !SymPy core has around 13000 lines of code (including extensive comments and docstrings) and its capabilities include:

  * basic arithmetics `*,/,+,-,**`
  * basic simplification (like `a*b*b + 2*b*a*b  -> 3*a*b^2`)
  * expansion (like `(a+b)^2 -> a^2 + 2*a*b + b^2`)
  * functions (exp, ln, ...)
  * complex numbers (like `exp(I*x).expand(complex=True)  -> cos(x)+I*sin(x)`)
  * differentiation
  * taylor (laurent) series
  * substitution (like x -> ln(x), or sin -> cos)
  * arbitrary precision integers, rationals and floats
  * noncommutative symbols
  * pattern matching
 
Then there are !SymPy modules (73000 lines including documentation) for these tasks:

  * more functions (sin, cos, tan, atan, asin, acos, factorial, zeta, legendre)
  * limits (like `limit(x*log(x), x, 0) -> 0`)
  * integration using extended Risch-Norman heuristic
  * polynomials (division, gcd, square free decomposition, groebner bases, factorization)
  * solvers (algebraic, difference and differential equations, and systems of equations)
  * symbolic matrices (determinants, LU decomposition...)
  * Pauli and Dirac algebra
  * geometry module
  * plotting (2D and 3D)


There are extensive tests (15000 lines in 142 files) for every single feature in !SymPy. 

### Related projects

  * [http://sagemath.org/ Sage]: an open source alternative to Mathematica, Maple, Matlab and Magma (!SymPy is included in Sage)
  * [http://code.google.com/p/mpmath/ mpmath]: a Python library for arbitrary-precision floating-point arithmetic (included in !SymPy)
  * [http://pyglet.org pyglet]: a fast cross-platform windowing and multimedia library in pure Python, that we use in !SymPy for 2D and 3D stuff
  * [http://code.google.com/p/sympycore/ sympycore]: another Python CAS (see SymPyCore for more information)
  * [http://code.google.com/p/symbide/ symbide]: GUI for !SymPy in PyGTK
  * [http://code.google.com/p/sfepy/ sfepy]: Full featured finite element library written in Python and C
  * [http://code.google.com/p/symfe/ symfe]: Lightweight symbolic finite element calculations in Python (sfepy will use symfe in the future)
  * [http://scipy.org/ scipy.org]: !SciPy + !NumPy
  * [http://code.google.com/p/sympy/ rSymPy]: SymPy in [http://www.r-project.org/ R].

The community around all these tools is wonderful, feel free to join the respective lists of these projects and also share your code, so that we can build on each other's work.

### Things we are working on

See our roadmap: http://wiki.sympy.org/wiki/Plan_for_SymPy_1.0

  * Make !SymPy very easy to use with [http://www.sagemath.org/ Sage], [http://scipy.org/ NumPy], [http://ipython.scipy.org ipython], [http://matplotlib.sourceforge.net/ matplotlib] and similar tools...
  * See also [http://code.google.com/p/sympy/issues/list Issues]
  * You can also check our blogs: [http://planet.sympy.org/ PlanetSympy]
  * Or join us at #sympy on irc.freenode.net (see our [http://wiki.sympy.org/wiki/FAQ#How_to_connect_to_our_IRC_channel.3F FAQ] for instructions how to connect)

But generally, we are trying to polish things, fix bugs, improve documentation, make !SymPy reliable and faster. It's very important for us, that you grab
the tarball and it just works (if it doesn't, it's a bug and please report it).
Until we reach the 1.0 version, the internal structure of !SymPy can change,
as we are still investigating the most efficient ways of doing symbolic manipulation
in Python, but from the user point of view, the API shouldn't change much, unless
there is a very good reason for it.

### Some ideas for future development

  * improve the integration algorithm, so that !SymPy can integrate anything that can be integrated.
  * improve series expansion
  * asymptotic expansion
  * objects with indices (tensors) 
  * rewrite the core to C++ or C or Cython, and use it as an optional module, if the user would like to speed things up (in any case the Python core will always be the default)

and more... Feel free to tell us your ideas in Issues or the mailinglist.

## Motivation

Why another CAS? What is the !SymPy's relationship to Sage?

Everything is explained in the [http://code.google.com/p/sympy/wiki/Motivation Motivation].

## Usage

Example in the python interpreter:
```
>>> from sympy import Symbol, cos
>>> x = Symbol('x')
>>> e = 1/cos(x)
>>> print e.series(x, 0, 10)
1 + (1/2)*x**2 + (5/24)*x**4 + (61/720)*x**6 + (277/8064)*x**8 + O(x**10)
```

There is a nice console `isympy` (in the `bin` directory, or if you installed the `deb`, it will be in `/usr/bin/isympy`) which just imports sympy and defines symbols x,y,z for you, so the above thing can be achieved by starting `isympy` and typing this one line:
```
In [1]: (1/cos(x)).series(x, 0, 10)
Out[1]: 
     2      4       6        8           
    x    5*x    61*x    277*x            
1 + ── + ──── + ───── + ────── + O(x**10)
    2     24     720     8064            
```

Read the [http://docs.sympy.org/tutorial.html tutorial] for more examples.


## Development

If you wrote anything interesting using !SymPy, please donate your code back to the project, so that other people can easily use it and we can grow as the community.
You are welcomed to join the development. If you find a bug or just want to say what you think, tell us on the [http://groups.google.com/group/sympy mailinglist] (or put your comment/bug report into the [http://code.google.com/p/sympy/issues/list Issues]). We are interested in your opinions if you think the !SymPy's interface is not
as you would expect or if you created some algorithm using !SymPy and would like it to become part of !SymPy (so that others can easily use your code as well).

More information can be found in SympyDevelopment.

See also the list of [http://docs.sympy.org/aboutus.html contributors].