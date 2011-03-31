## Symbolic Clebsch-Gordon coefficients/Wigner symbols and Implementing Addition of Spin Angular Momenta

***

This is still a draft, if anyone has any comments or suggestions, please feel free to let me know.

## About me

* Name: Sean Vig
* Current physics and math undergrad at University of Minnesota, will be graduating the spring and going to the University of Illinois at Urbana-Champaign this fall.
* IRC: flacjacket on freenode
* Email: sean.v.775 gmail.com

## Background

Spin dynamics is an important part of dealing with quantum systems. The current implementation of spin in Sympy covers single spin states and the operators that can act on them; however, there is no means of dealing with spin states in multiple particle systems. A key to understanding these systems is Clebsch-Gordon coefficients and its generalizations to systems of more than two particles. These coefficients give the expansion of coupled spin states as a sum of product states and vice versa. Sympy currently has functions capable of calculating these coefficients numerically; this project will focus on implementing a symbolic means of manipulating these coefficients and expand the spin implementation to utilize these coefficients.

## Project Overview

The basis of this project is the implementation of symbolic Clebsch-Gordon coefficients/Wigner symbols. To implement this, I will create coefficients as a subclass of Expr, which allows us to create symbolic expressions based on input parameters. In this case, the Clebsch-Gordon coefficients would take 6 parameters, 2 for each of the two particles in the product basis and 2 for the particle in the coupled basis. This can be extended to the coupling of more than two particles with Wigner-6j/9j/... symbols; these will be added if time allows, though this project will develop the framework that could be extended to include these objects. Numerical calculation of the coefficients will be possible by invoking the current numerical methods, but of note will be the implementation of symbolic manipulation and simplification by the various symmetries and properties that have been developed for evaluating Clebsch-Gordon coefficients (see Varshalovich, "Quantum Theory of Angular Momentum", pp 244-264 as a sample of the available relations). There are many such relations that could be implemented, and the how many are implemented will be based on the amount of time available determined in discussions with my mentor.

With the Clebsch-Gordon coefficients implemented, I will improve the spin algebra to utilize these terms. The first component of this will be to modify the treatment of spin states to be able to utilize product and coupled bases. This would be implemented such that if given a coupled state |j,m>, it could be written as the sum of tensor products of spin states with the appropriate Clebsch-Gordon cofficient and if given a tensor product of spin states, it could written as a sum of coupled states, again with the appropriate Clebsch-Gordon coefficient.

The next stage of this project would be to integrate the use of coupled and product bases with the spin operators. The spin operators as they are currently implemented are designed to act on single spin states. This can be immediately applied to the spin operators of the coupled basis acting on coupled states. What would need to be implemented for this project would be spin operators in one of the tensor product bases. In addition, all the spin operators would need to implement methods for acting on tensor product states. In implementing these things, I would use the methods developed for moving states between the coupled and product bases using the Clebsch-Gordon coefficients.

My plan for this project would be to first implement this for coupling between two spin states. Once this is done, I would extend these methods to include coupling between more states. The current numerical implementation includes up to Wigner-9j symbols, which gives coupling between 4 spin states. My goal would be to implement the necessary spin algebra to include coupling between at least this many states.

## Code Implementation

TODO

## Timeline

The specifics of each of these steps is outlined in the implementation.

During the official time frame of the Summer of Code, I have no other serious commitments and can easily commit to the required 40 hours of work per week and I'll put as much free time as I can into working this project because of the interesting subject matter.

**Before official start**

Review the current source code and begin integrating with the community. Work with my mentor to finalize a plan of action and formulate a project design, then begin preliminary coding work on the project.

**Weeks 1-3**

Work on implementing the Clebsch-Gordon class. This would include developing the basic functionality of the class, such as evaluation, use in equations and printing, but would also include the symbolic manipulation through the symmetry relations and properties of the Clebsch-Gordon coefficients.

Documentation on how to create and manipulate the coefficients will be done as the features are implemented. You can see above for more information regarding the CG class and how it will be fully implemented. The documentation will also include examples as shown below. Tests that these coefficients obey the properly relations and evaluate properly, also below, will be added to the code as they are implemented.

At this point, the implementation of the Clebsch-Gordon coefficients should be available for merging. While these coefficients are most useful in the context of coupled and product bases, they can stand alone and I will work to begin merging these at this time

**Weeks 4-5**

Expand the spin states to work with both product and coupled spin states.

With this addition, I will add documentation on how to define spin states in the coupled and uncoupled bases in addition to how to rewrite states in terms of one or the other basis. Tests will be implemented to test that these conversions are performed as expected (see below).

**Weeks 6-7**

Modify spin operators to work with the new formulation of spin states. Prepare for midterm evaluation.

During this phase, I will be adding documentation for defining spin operators that act in the various bases and acting them on spin states on these bases. The tests that will be added at this point will verify both that these operators function as expected on various spin states, but that this works with the above implemented conversions between bases.

**Week 8**
Midterm evaluation

Around this time, I should be finishing the spin states and operators that utilize the Clebsch-Gordon coefficients. I will begin merging the implementation, documentation and tests for these at this time. This should allow for the solving of any problem involving the coupling of two spin angular momenta.

**Weeks 8-10**

Implement terms for coupling between more spin states, i.e. Wigner 6j and 9j symbols.

I will try to merge these as I complete the implementation for them, i.e. when the 6j symbols are implemented with working coupling of 3 spin states and the corresponding operators functioning properly, that would be merged.

Documentation and tests for these symbols will be included as the symbols are developed. The documentation will expand the previously written documentation for defining spin states and operators and how these interact in the various bases. Tests similar to those for the two spin coupling case will be included, verifying that symbols obey the symmetry relations, states can be properly converted between bases and operators acting on these states can incorporate this functionality.

**Week 11-12**

Finalize project, merging any final documentation, tests and bug fixes, and pencils down.

## Test cases and examples

TODO

## Current code patches

**Open pull requests**

**Closed pull requests**

[Fix Rotation.d function](https://github.com/sympy/sympy/pull/153) addressing a bug I found in evaluating elements of the Rotation operator

[Bug fix for evaluating J2 on a Jz ket](https://github.com/sympy/sympy/pull/155) addressing a bug I found in evaluating the J2 operator on a Jz eigenket.

[Change apply_operators to qapply](https://github.com/sympy/sympy/pull/152) addressing [Bug #2223](http://code.google.com/p/sympy/issues/detail?id=2223)

[Fixing the printing of the CNOT gate](https://github.com/sympy/sympy/pull/167) addressing [Bug #2188](http://code.google.com/p/sympy/issues/detail?id=2188)

[Fixing the Matrix.is_upper,.is_lower and .is_upper functions](https://github.com/sympy/sympy/pull/157) addressing [Bug #2220](http://code.google.com/p/sympy/issues/detail?id=2220)

## Bio

I am a senior at the University of Minnesota and will be graduating this spring in physics and math and will begin graduate physics work next fall at the University of Illinois at Urbana-Champaign. While a student, I have taken several classes in programming; the classes I took covered C/C++ and parallel programming with CUDA. Also of note for this project are the physics classes I have taken, which include the 2 semester graduate level quantum mechanics sequence, which I will be completing this spring. Out of the classroom, I spent last summer working on developing a parallel implementation of the zlib compression library using CUDA. As for my experience with Python, beyond hobby coding, I am using Python, mainly using the PyROOT module, to do the analysis as a part of research for my senior physics thesis. While this will be the first time I will be working on an open source project, I am excited to get the chance to use my extensive physics training as a stepping stone to developing software with the Sympy community.