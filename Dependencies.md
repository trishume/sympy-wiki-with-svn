_Please add to this page all the optional dependencies for SymPy (not development dependencies).  See [issue 2160](http://code.google.com/p/sympy/issues/detail?id=2160)_

Dependencies
------------

One of the fundamental design decisions behind SymPy is that it should not have any external dependencies besides Python to install.  Therefore, the only real "dependency" of SymPy is an installation of Python 2.4, 2.5, 2.6, or 2.7 (note that Python 2.4 support is deprecated and will no longer work in the next release).

However, there are several packages that are not required to use SymPy, but that will enhance SymPy if they are installed.  These packages are:

- IPython (http://ipython.scipy.org/moin/).  IPython is a third party Python interactive shell that has many more features over the built-in Python interactive shell, such as tab-completetion and [what other important features should I mention here?].  If IPython is installed, isympy will automatically use it.  Otherwise, it will fall back to the regular Python interactive shell.  You can override this behavior by setting the -c option to isympy, like `isympy -c python`.

- gmpy (http://code.google.com/p/gmpy/). gmpy is a Python wrapper around the GNU Multiple Precision Arithmetic Library (GMP). If gmpy is installed, it may make certain operations in SymPy faster, because it will use gmpy as the ground type instead of the built-in Python ground types.  If gmpy is not installed, it will fall back to the default Python ground types.  You can override this behavior by setting the SYMPY_GROUND_TYPES environment variable, such as `SYMPY_GROUND_TYPES=python isympy`. [Note: this should be an option to isympy!]

- Cython. [What exactly is the situation with Cython?]

- Numpy. [Ditto]

- Scipy. [Ditto]

- [Code generation dependencies?]

- [Other dependencies?]

Note that mpmath and pyglet, our floating point and plotting libraries respectively, are included with SymPy, so it is unnecessary to install them.  Indeed, SymPy will always use the version of mpmath or pyglet that comes with SymPy, even if a newer version is installed in the system.  This is done for compatibility reasons.
