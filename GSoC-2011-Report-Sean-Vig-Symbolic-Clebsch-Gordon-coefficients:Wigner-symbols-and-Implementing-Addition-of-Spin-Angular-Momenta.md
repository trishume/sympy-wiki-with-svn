## About Me

My name is Sean Vig. This last spring, I completed my undergrad at the University of Minnesota, with degrees in physics and math. This fall, I'm attending the University of Illinois at Urbana-Champaign in their physics graduate program.

## Introduction

For my project, my goal was to implement symbolic Clebsch-Gordan coefficients, then use these symbolic objects to implement coupled spin algebra. This would include implementing the code to use uncoupled states and operators with the existing TensorProduct class, creating new classes for coupled spin states and defining the algebra to go back and forth between these and apply operators to states.

My initial application can be seen here: [[GSoC 2011 Application Sean Vig Symbolic Clebsch Gordon coefficients:Wigner symbols and Implementing Addition of Spin Angular Momenta]]. My progress over the course of the summer is documented on my blog [here](http://seanvig.blogspot.com)

## GSoC Project

### Cartesian spin bases

The initial plan had me finishing some preliminary work with the x/y/z spin state bases, allowing states to be rewritten in any basis, as the previous implementation only worked for rewriting to the Jz basis and representation only worked for j=1/2. While much of the preliminary work for this was done very early in the summer, there were problems in the evaluation of the Wigner D-matrix, which was being used to move between bases.

While it ultimately turned out to be related to an issue with the domain of the Wigner d-function, this part of the project ended up taking much longer than anticipated. However, due to this, an extensive set of tests were put in place, for both symbolic and numerical values of both the Wigner D-matrix and the Wigner small-d function. In addition, while this was being worked on, I created a Wigner D class, which would be returned when the Rotation.D and Rotation.d methods were called, allowing for symbolic manipulation of these elements.

The pull requests for this can be seen [here](https://github.com/sympy/sympy/pull/431) and [here](https://github.com/sympy/sympy/pull/462).

### Symbolic CG/Wigner-3j

The next key component needed in developing my project was the creation of the symbolic coefficients. The actual class for the coefficients themselves were simple simple to implement, as the evaluation of the coefficients is already covered by the `sympy.physics.wigner module`. Most of the code here is written for the `cg_simp` method, which simplifies sums of Clebsch-Gordan coefficients.

After some work, this eventually settled on the use of a helper function which would be passed the terms that need to be checked and would check the terms of the sum using `Wild` and `.match()` to match terms. This was done for several simplifications of sums of products of one and two Clebsch-Gordan terms. While there are only a couple simplifications in place, at the time this was being worked on, I'd fallen behind schedule and in the interest of time, proceeded with the coupled states, as further work did not depend on this working. With the methods currently in place, implementing additional simplifications should be relatively easy.

The pull request for this can be seen [here](https://github.com/sympy/sympy/pull/453).

### Coupled and uncoupled states and operators

With a symbolic Clebsch-Gordan coefficient in place, the next step was to implement a way of representing coupled and uncoupled states. The uncoupled states and operators are simply given as TensorProducts of the states and operators. The first attempt at implementing this had the coupling and uncoupling being done with `.rewrite()` and `represent()`, however, in order to keep the coupling code out of non-spin modules, this functionality was removed and separate coupling and uncoupling methods were implemented; the representation and rewriting worked as expected using the normal TensorProduct methods.

The first implementation also had the normal states take an additional parameter, jvals, to set the j values of a coupled state, and when it was not set, the state would be taken as a normal state. However, in the interest of keeping the base spin states free from information of coupled states, this functionality was moved to a separate class, identical to the previous class with Coupled appended to the end, e.g. JzKetCoupled. These classes had explicit parameters for the j values of the coupled spaces.

Acting the operators on the states with qapply was very straightforward. With uncoupled states and operators, some code in `qapply.py` was modified to check if two TensorProduct's are acting on each other, one being an operator and the other being a state, then applying corresponding components of each. The coupled states interact with operators in the same way as normal states, so similar methods were implemented which retain the j values of the coupled spaces in the resulting eigenstates. Representation of coupled states had to be altered, as these states are in a Hilbert space which is the direct sum of the Hilbert spaces of all possible j values given the j values of the coupled spin spaces, e.g. states with j1=1 and j2=1/2 would be in a Hilbert space of j=1/2 + j=3/2, where + is the direct sum of the two spaces. This, however, could be easily accomplished by taking the representation of the normal state with the same j and m value and putting this representation in a slice of the vector representing the state.

### Coupling and Uncoupling States

The last part of the project was coupling and uncoupling of states, which is the part of the project that uses the Clebsch-Gordan coefficients. The methods `couple()` and `uncouple()` were created to move back and forth between coupled and uncoupled states. The `coupled()` method takes either a coupled spin state or a normal spin state and the j values of the states that coupled spaces and this method returns a linear combination of TensorProduct's of states. The `uncoupled()` method takes a TensorProduct of states and returns a coupled state corresponding to the coupling of the state. Currently, these methods and states only work for coupling of two spin spaces.

The pull request for the first implementation of coupled spin spaces, addressing both coupling/uncoupling and coupled and uncoupled spin states and operators can be seen [here](https://github.com/sympy/sympy/pull/524).

## Evaluating progress

Looking back at what I'd set out to do at the beginning of the summer, I think I have done most of the things I set out to finish and did so with quality, well tested code. There are some things, like the content in cg.py, which turned out about roughly like I expected, and some other stuff, like the implementation of coupled spin states, that have changed drastically from my initial application to their implementation. The only thing that is still missing that I had in my application is to get coupling working for arbitrary numbers of spin spaces. However, given the amount of work that went into getting other parts of the code to work correctly and to get the code properly documented and tested, I am pleased with the work I completed during the project.

## Conclusion and looking forward

While I accomplished a great deal during this project, it wasn't without its setbacks and pitfalls. Right off the bat, between not knowing how to start and then going out of town for a week, I had a very slow start. However, with the push to work out the issues with the Rotation.D and Rotation.d functions, I was able to rally myself and get my bearings with the codebase. Working out the issues with the Wigner D functions was surely one of the biggest issues faced during the summer, with much of the rest proceeding fairly straightforward. While there is still a question as to the derivation of some of the equations that were used, having worked through this, I am confident in the results the function now returns.  One thing I do regret is my low level of interaction with the rest of the community. I was able to get some questions answered and get some help with some code review, but especially with the project ending, this is something I wished I'd forced myself to be more active on. That said, seeing that these were worked through and the output that was produced, I would say overall, this was a successful endeavor.

Beyond this GSoC project, the immediate goal with the spin code is to get the code for coupling multiple spin spaces in. This is still a work in progress, and can be found [here](https://github.com/flacjacket/sympy/tree/multi_coupled). Some things, like the `uncouple()` method are working, if in a messy way, and the `couple()` method still has to be rewritten. Another possible continuation of this project would be to make possible evaluating expressions with coupled and uncoupled components, which is currently not handled. Time permitting with school and other commitments, I'll try to finish up these last components to this project.