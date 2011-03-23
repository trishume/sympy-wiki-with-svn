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

### random numbers from distributions of arbitrary form in N dimensions

Suppose one has a function in N dimensions that is non-negative and normalized to 1,
so that we can treat it like a probability density (of 4-momentum of the relativistic
particle for example). The idea is to be able to generate N-dimensional points
according to that distribution.

Actually this technique is widely used in Monte-Carlo simulations in particle physics
and is mostly related to numerical methods than symbolic calculation, however is
extremely interesting nevertheless.

to be continued ...