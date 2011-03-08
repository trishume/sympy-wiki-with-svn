Draft of our roadmap.

The items in each block represent what we should work on in each version and what needs to be finished in order to bump the version.

## sympy 0.6.0 ##

* good numpy and mpmath integration
* good Sage integration + tests (so that things like {{issue|881}}, {{issue|882}} or {{issue|924}} never occur again)
* All useful SymPy modules and all important features should be documented at http://docs.sympy.org/, so that anyone who tries to find if SymPy can do something, can easily find it in docs.
* assumptions

## sympy 0.7.0 ##

The next release after 0.6.7 should be a 0.7 release.

* Merge in the new Polys module. 
* Merge in the 2010 Google Summer of Code projects (Risch integration, SAT solving, quantum mechanics, code generation)
* After 0.7.0, we will drop Python 2.4 support.

## sympy 0.8.0 ##

* complete new assumptions (finally replacing the old assumptions).
* Python 3 support.
* merge our experimental core [http://groups.google.com/group/sympy/browse_thread/thread/aa3f4263bc3f7e23 sympyx], that basically should make sympy as fast as sympycore (or nearly as fast)
* speed sympy to the level of sympycore, merge all important things
* maybe add some (optional!) C/Cython module for speed
* all important things working, general polishing of things
* full test coverage (using tools like [http://darcs.idyll.org/~t/projects/figleaf/doc/ figleaf])

## sympy 0.9.0 ##

* Begin to implement a more complete type system that includes coercion/casting, sets+elements, etc.

## 1.0 ##

Well tested  product. This is not the end, rather the opposite. Just a milestone on the way to be a good CAS in Python.

## notes ##

All other improvements will just bump the third number, i.e. 0.6.1, 0.6.2, 0.6.3, ... The priority is to merge all useful (and stable) things that anyone contributes immediatelly and also that sympy is usable and robust right now. The above plan is just the general direction, so that we know where we are standing.
