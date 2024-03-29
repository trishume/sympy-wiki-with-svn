# GSoC 2011 Application Oleksandr Gituliar

## About me

Here is [my introduction to SymPy community at the discussion group](http://groups.google.com/group/sympy/browse_thread/thread/bfd38c7d28afe669/7729ff463e00ae41#7729ff463e00ae41).

And here -- not a complete list of courses I took during my MSc and PhD studies
(both in theoretical physics) that may help me with ideas I propose:

* classical QM (2 semesters, undergrad);
* QFT + QED (1 + 1 semesters, undergrad);
* QM (2 semesters, grad);
* nuclear physics (1 semester, grad);
* particle physics (1 semester, grad);

* mathematical analysis (2 semesters, undergrad);
* differential equations (1 semester, undergrad);
* vector and tensor analysis (2 semesters, undergrad);

I have 3 years expierense programming in Python and C/C++. Currently I use Mac OS X
as my primary OS, however have experience with FreeBSD, Ubuntu, ArchLinux.


## GSoC 2011 ideas

Being encouraged by my QM classes and ["Structure and Interpretation of Classical Mechanics"](http://mitpress.mit.edu/SICM/)
book in particular I was thinking for quite long time about the combination of
both in order to have an environment for performing and demonstrating solutions
of physical problems. For sure, this task is almost undoable for a single person
ans requires a lot of time (luck of which an every student has) and resources of
different kinds. However, SymPy seems a descent starting point for such tool
or at least a very interesting project to contribute in in that direction. Thus
I'd like to present this list of ideas in order to share my opinion concerning
the features such kind of tools is likely to have.

Note, a general idea is not to have just a programming libriray, module or set
of classes. The idea is to get a final answer (a solution of a problem) using
those tools, that's why a starting point for each of my idea is a physical problem
instead of set of abstract tools. (I do not insist on that approach and it is not
the only one I have, thus do not judge it too strict. :) ).

Follow [gituliar/sympy/qunatum2 branch](https://github.com/gituliar/sympy/tree/quantum2) where some
rudiments of proposed ideas are supposed to be implemented.


### basic QM notation

It seems without a descent implementation of the following features none of the
further ideas could be fully functional, thus treat it as a starting point for
them.

* both discrete and continuous Hilbert spaces with operators (in matrix and
  differential forms respectively)
* basic operations with states and operators: superposition, measurements (averaging
  over sates) as well as building complex states like spin*momentum etc.

Idealy the following problems should be easily solved:

* what is an average momentum of an electron with +1/2 projection of spin on X
  direction (Y and Z for the same state considered that we know it)?
* what is an average spin projection on X (Y and Z) of an electron with a given
  momentum? A kind of inverse problem to the previous.


### perturbative schemes

It would be definitely worth to have some of [the approximation methods](http://en.wikipedia.org/wiki/Perturbation_theory_(quantum_mechanics\)#Second-order_and_higher_corrections)
to be implemented in SymPy since they can be applied to a wide range of problems.
[Variational method](http://en.wikipedia.org/wiki/Variational_method) seems extremely
interesting since SymPy has enough power to solve it analytically.


### rotation group representations + multi-particle (iso)spin states

The point here is to implement a rotation group SO(3) (or even Lorentz SO(1,3)
group) representations for SU(N) with arbitrary N so that one could "rotate" spin
states as well. Seems extremely interesting especially in symbolic implementation.

Currently, HilbertSpace and State classes are implemented in quantum2 branch, however
that is enough to build a simple implementation of rotation group on top of it. An idea
is that states are not a first-class objects, however belong to some HilbertSpace,
thus every Hilbert space knows all its states and can transform them once some rotation
is mode with it. For example:
```python
from sympy.physics.quantum2 import HilbertSpace

h2 = HilbertSpace(2)  # a 2-dimensional Hilbert space

s1 = h2.state(...)    # make some bra/ket states in h2
s2 = h2.state(...)
s3 = h2.state(...)

h2.rotate(Pi/4, 0, Pi/8)   # make a rotation using for example Euler angles convention
```

Note, that after the last line of code was executed all states that belong to h2 (in this example s1, s2, and s3) has changed according to SU(2) representation of rotaion group. Moreover all the details of rotation group representations are hidden in HilbertSpace.rotation method that of course is not trivial to implement for arbitrary N (integer or oo for continuous spaces).

The idea can be extended even further if one will consider direct sum of several Hilbert spaces (Momentum + Spin + Angular Momentum). In that case all spaces should be transformed as well as states/wavefunctions and their arguments (that is a non-trivial task especially in a symbolic form).

### random numbers from distributions of arbitrary form in N dimensions

Suppose one has a function in N dimensions that is non-negative and normalized to 1,
so that we can treat it like a probability density (of 4-momentum of the relativistic
particle for example). The idea is to be able to generate N-dimensional points
according to that distribution.

It might look like this idea is more appropriate for some numerical system, however
making it general/good enough requires to perform an analytical analysis of the density
function that SymPy could easily do.

Once implemented such module could be very useful standalone as a general random number
generator as well as a component for a Monte-Carlo integrator.

to be continued ...