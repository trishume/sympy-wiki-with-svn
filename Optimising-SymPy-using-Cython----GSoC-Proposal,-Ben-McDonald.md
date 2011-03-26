Optimising SymPy using Cython
==============================

About Me
------------------
* Ben McDonald
* Computer Science student completing my Master’s thesis at the University of Canterbury, New Zealand. 
* Email/GTalk: mcdonald.ben@gmail.com

Coding Skills
------------------
todo

TODO
---------------
* Submit a patch

Optimising SymPy using Cython
------------
The core is being updated so work depended on it is being postponed until the replacement core is available [http://groups.google.com/group/sympy/browse_thread/thread/6cf7ece92746bcdc].
Other parts of SymPy may be good candidates for optimisation. logic code (like the SAT solver), matrices ,polys (work already started) , physics [http://groups.google.com/group/sympy/browse_thread/thread/6cf7ece92746bcdc]

The cythonized decorator is currently being used in the polys module
An alternative methods is to use Cython header files (.pyx). See http://wiki.cython.org/pure

### Community Discussion on Cython
Decorators and header files have both been suggested. http://groups.google.com/group/sympy/browse_thread/thread/5eccee5e2d02aa1a/d6671be18f5c11ab?lnk=gst&q=Cython#d6671be18f5c11ab
Cython improves performance significantly http://groups.google.com/group/sympy/browse_thread/thread/5eccee5e2d02aa1a/d6671be18f5c11ab?lnk=gst&q=Cython#d6671be18f5c11ab
sympy.physics requires increase performance http://groups.google.com/group/sympy/browse_thread/thread/5eccee5e2d02aa1a/d6671be18f5c11ab?lnk=gst&q=Cython#d6671be18f5c11ab


http://groups.google.com/group/sympy/browse_thread/thread/aa3f4263bc3f7e23

### Complexities
Cython compiles to platform dependent binaries. SymPy with Cython optimisation will been to be build on the platform it is to be run on, or binaries for each platform will need to be distributed with SympPy.