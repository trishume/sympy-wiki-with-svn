# Release Notes for SymPy 0.7.1
These are the release notes for SymPy 0.7.1.

## Major changes

- Python 2.4 is no longer supported.  SymPy will not work at all in
Python 2.4.  If you still need to use SymPy under Python 2.4 for some
reason, you will need to use SymPy 0.7.0 or earlier.

- The Pyglet plotting library is now an (optional) external dependency. 
Previously, we shipped a version of Pyglet with SymPy, but this was old
and buggy.  The plan is to eventually make the plotting in SymPy much
more modular, so that it supports many backends, but this has not been
done yet.  For now, still only Pyglet is directly supported.  Note that
Pyglet is only an optional dependency and is only needed for plotting. 
The rest of SymPy can still be used without any dependencies (except for
Python).
