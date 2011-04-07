## Symbolic Clebsch-Gordon coefficients/Wigner symbols and Implementing Addition of Spin Angular Momenta

## About me

* Name: Sean Vig
* Current physics and math undergrad at University of Minnesota, will be graduating the spring and going to the University of Illinois at Urbana-Champaign this fall.
* IRC: flacjacket on freenode
* Email: sean.v.775 gmail.com

## Background

Spin dynamics is an important part of dealing with quantum systems. The current implementation of spin in Sympy covers single spin states and the operators that can act on them; however, there is no means of dealing with spin states in multiple particle systems. A key to understanding these systems is Clebsch-Gordon coefficients and its generalizations to systems of more than two particles (Wigner 3nj symbols). These coefficients give the expansion of coupled spin states as a linear combination of product states and product states as the linear combination of coupled states. Sympy currently has functions capable of calculating these coefficients numerically; this project will focus on implementing a symbolic means of manipulating these coefficients and expand the spin implementation to utilize these coefficients.

## Final product

* Clebsch-Gordon module: Implement a new class which allows for the creation of Clebsch-Gordon coefficients and the symbolic manipulation of these coefficients
* Coupled spin states: Extend the functionality of the current Jx/Jy/Jz spin states which will allow the state to be defined as coupled spin states of multiple particles.
* Uncoupled spin states: Work with existing Jx/Jy/Jz states and expand the implementation such that taking the TensorProduct of states will represent that these states are written in the uncoupled basis.
* Integration of coefficients with spin algebra: Implement functions such that states can be projected between the coupled and uncoupled bases, allowing calculations such as the evaluation of innerproducts.
* Integration of new bases with spin operators: Make spin operators act properly on the new spin states, which includes implementing a means of defining the basis and space over which spin operators act.
* Wigner 6j/9j/... symbols: Time allowing, implement the coefficients similar to the Clebsch-Gordon coefficient for larger numbers of particles.

## Project Overview

The basis of this project is the implementation of symbolic Clebsch-Gordon coefficients/Wigner symbols. To implement this, I will create coefficients as a subclass of Expr, which allows us to create symbolic expressions based on input spin parameters. In this case, the Clebsch-Gordon coefficients would take 6 parameters, 2 for each of the two particles in the product basis and 2 for the particle in the coupled basis, and are expressed as \(CG^{jm}_{j_1m_1j_2m_2}\). This can be extended to the coupling of more than two particles with Wigner-6j/9j/... symbols; these will be added if time allows, though this project will develop the framework that could be extended to include these objects. Numerical calculation of the coefficients will be possible by invoking the current numerical methods, but of note will be the implementation of symbolic manipulation and simplification by the various symmetries and properties that have been developed for evaluating Clebsch-Gordon coefficients (see Varshalovich pp 244-264 as a sample of the available relations). There are many such relations that could be implemented, and the number of relations that are implemented will be based on the amount of time available determined in discussions with my mentor.

With the Clebsch-Gordon coefficients implemented, I will improve the spin states and spin algebra to fully utilize these terms. The first component of this will be to modify the treatment of spin states to be able to utilize product and coupled bases. This would involve using the current spin state implementation and tensor products to define uncoupled spin states and creating a new class inheriting from the current spin state classes to define coupled spin states. The coupled spin state classes would expand the current spin state states to include the spins of the corresponding uncoupled states. The algebra would be implemented such that if given a coupled state |j,m>, it could be written as the sum of tensor products of spin states with the appropriate Clebsch-Gordon cofficient and if given a tensor product of spin states, it could written as a sum of coupled states, again with the appropriate Clebsch-Gordon coefficient. Doing this allows calculations such as inner products between spin states to be evaluated.

The next stage of this project would be to integrate the use of coupled and product bases with the spin operators. The spin operators as they are currently implemented are designed to act on single spin states. This can be immediately applied to the spin operators of the coupled basis acting on coupled states. What would need to be implemented for this project would be spin operators in one of the tensor product bases. In addition, all the spin operators would need to implement methods for acting on tensor product states. In implementing these things, I would use the methods developed for moving states between the coupled and product bases using the Clebsch-Gordon coefficients.

My plan for this project would be to first implement this for coupling between two spin states. Once this is done, I would extend these methods to include coupling between more states. The current numerical implementation includes up to Wigner-9j symbols, which gives coupling between 4 spin states. My goal would be to implement the necessary spin algebra to include coupling between at least this many states. See the timeline for specifics of how I intend to complete this project.

## Code Implementation

* CG module

The Clebsch-Gordon and Wigner-3nj symbols will be placed in a separate module within sympy.physics.quantum. I would choose to do this because these coefficients have uses outside of spin projection, such as in integrating spherical harmonics, and since there are possible projects in getting spherical harmonics working in physics.quantum, having these available would be useful.

Within the CG module, the main class will likely be Wigner3j, as many of the symmetry relations are best described by the Wigner-3j symbols; this class will inherit from the Expr class. The `__new__` method will take 6 parameters (j,m,j1,m1,j2,m2) to define the symbol. This class would have @properties defined to retrieve these parameters. The `doit()` method would be used to evaluate the coefficients numerically, which would employ the algorithms currently in sympy.physics.wigner. In addition, there would be functions to properly print out the Wigner symbol.

The CG class, which would inherit from the Wigner3j class, would create a Wigner3j object and would override methods such that the appropriate pre-factor is applied to the Wigner-3j symbol in evaluation and symbolic manipulation.

An important method which would be in the CG module would be a `cg_simp()` function (similar to `tensor_product_simp()` in sympy.physics.quantum.tensorproduct). This method would take as its parameter an expression involving Clebsch-Gordon and Wigner coefficients. This method would apply symmetry relations and known properties between things such as sums and products of coefficients to simplify the input expression. In developing this module, this will likely be what is most time consuming to implement and test.

In addition, when the rest of the Wigner-3jn symbols are implemented, they too would implemented as subclasses of Expr and would be placed in this module with the simplification method modified to include the simplification of these coefficients.

* Spin states

First, coupled spin states will be implemented using the current Jx/Jy/Jz eigenstates. The coupled states will be specified by passing a parameter `coupled` to the new method which will be a tuple giving the j1,j2,... quantum numbers of the spin states that are coupled together. The changes for how these states interact with other states is given below.

The uncoupled states will be implemented by taking tensor products of the currently implemented Jx/Jy/Jz spin states, and thus will not require changes to how these states are created.  The changes for how these states interact with other states is given below.

As for the functions for the spin states classes, there will be required changes to the printing of the states, but more important are the changes to how these spin states are projected. In the parent SpinState class, I will implement a `_represent_base_coupled` and `_represent_base_uncoupled`. These will be used to write the input spin states as vectors in the new basis and will use the CG coefficients developed earlier. These will be invoked by the spin kets when the represent(basis=SpinOp) is called on the state. Furthermore, the SpinState class will implement `_rewrite_basis_coupled` and `_rewrite_basis_uncoupled`, which will be called from the SpinState class by functions such as `_rewrite_basis_as_J2`, `_rewrite_basis_as_Jz`, etc. These methods will utilize the vector expansion of the states in the `_represent_base` functions to rewrite the state. The spin state kets will also implement `_eval_innerproduct` functions that call the `_represent_base` functions to evaluate inner products between states in different bases. In addition to these means of numerically expanding the states, symbolic methods will be implemented to expand states as arbitrary sums (see "Test cases and examples").

If you see the "Current code work" under the spin_improvements branch, I have done some work implementing functions similar to those mentioned above, only for representing spin states in terms of Jx/Jy/Jz states. The code for the coupled and uncoupled states has been described to mirror this implementation.

* Spin operators

Spin operators must be changed to account for the new definitions of spin states. Spin operators as they currently stand will default to being operators in the coupled basis. In this way, any state created with or without the coupled parameter will be taken to be diagonalized in the basis of the spin operator. Spin operators will, however, need a `__new__` method that will check for a `space` parameter, which will set which space of the product basis the spin operator acts on.

The way spin operators act will need to account for this new definition. The default operator acting on a coupled state or a single state will use the current implementation. When the `space` parameter is set, the evaluation of the operator on these states, which occurs in the `_apply_operator` methods, will need to utilize the `_represent` functions defined for the spin states to change the basis of the spin states, then allowing it to call the `_apply_operator` function for uncoupled states, described below.

Furthermore `_apply_operator` methods will need to be developed to allow for uncoupled spin states to be acted on by the operator. In these methods, when the operator is coupled, the method will invoke the `_represent` functions of the spin states to rewrite the state in the proper basis, then allowing it to invoke the `_apply_operator` methods for the coupled basis. In the uncoupled basis, the operator will act on only the state which is defined by the `space` parameter (e.g. an operator with the parameter`space=1` will only act on the first state in the tensor product), and will act on this state by invoking the currently implemented `_apply_operator` methods.

## Timeline

The specifics of each of these steps is outlined in the overview and implementation.

During the official time frame of the Summer of Code, I have no other serious commitments and can easily commit to the required 40 hours of work per week and I'll put as much free time as I can into working this project because of the interesting subject matter. I may be taking a 1 week vacation to go camping in the BWCA in the first week of June, but will be able to make up time between starting early and working beyond 40 hrs/week while I am in town the rest of the summer. Classes in the fall will begin on August 22, the firm pencils down date, and I should be able to complete any final evaluation by this time. Because this is mostly complete, it should be easily completable in the lead-in to the Summer of Code.

**Before official start**

Review the current source code and begin integrating with the community. Work with my mentor to finalize a plan of action and formulate a project design, then begin preliminary coding work on the project. I will be busy through the end of the school year, which extends through May 14, but would have no problem starting early on the project after this time.

Also, before work begins on this project, some of the work done on representing Jx/Jy/Jz basis elements in terms of each other should be finished, documented and merged. The beginnings of this work can be seen in the spin_improvements branch linked in "Current code work" below. This project fills in the remaining algebra for working with the currently implemented spin states and will work within the current implementation without any of the CG/Wigner algebra this project develops. This work should be done before work is started on this project because it establishes the syntax for projecting between bases.

** Weeks 1-3 **

Work on implementing the Clebsch-Gordon class. This would include developing the basic functionality of the class, such as evaluation, use in equations and printing, but would also include the symbolic manipulation through the symmetry relations and properties of the Clebsch-Gordon coefficients.

Documentation on how to create and manipulate the coefficients will be done as the features are implemented. You can see above for more information regarding the CG class and how it will be fully implemented. The documentation will also include examples as shown below. Tests that these coefficients obey the properly relations and evaluate properly, also below, will be added to the code as they are implemented.

At this point, the implementation of the Clebsch-Gordon coefficients should be available for merging. While these coefficients are most useful in the context of coupled and product bases, they can stand alone and I will work to begin merging these at this time

** Weeks 4-5 **

Expand the spin states to work with both product and coupled spin states.

With this addition, I will add documentation on how to define spin states in the coupled and uncoupled bases in addition to how to rewrite states in terms of one or the other basis. Tests will be implemented to test that these conversions are performed as expected (see below).

** Weeks 6-7 **

Modify spin operators to work with the new formulation of spin states. Prepare for midterm evaluation.

During this phase, I will be adding documentation for defining spin operators that act in the various bases and acting them on spin states on these bases. The tests that will be added at this point will verify both that these operators function as expected on various spin states, but that this works with the above implemented conversions between bases.

** Week 8 - Midterm Evaluation**

Around this time, I should be finishing the spin states and operators that utilize the Clebsch-Gordon coefficients. I will begin merging the implementation, documentation and tests for these at this time. This should allow for the solving of any problem involving the coupling of two spin angular momenta.

** Weeks 8-10 **

Implement terms for coupling between more spin states, i.e. Wigner 6j and 9j symbols.

I will try to merge these as I complete the implementation for them, i.e. when the 6j symbols are implemented with working coupling of 3 spin states and the corresponding operators functioning properly, that would be merged.

Documentation and tests for these symbols will be included as the symbols are developed. The documentation will expand the previously written documentation for defining spin states and operators and how these interact in the various bases. Tests similar to those for the two spin coupling case will be included, verifying that symbols obey the symmetry relations, states can be properly converted between bases and operators acting on these states can incorporate this functionality.

** Week 11-12 **

Finalize project, merging any final documentation, tests and bug fixes, and pencils down.

** Beyond GSoC **

After the Summer of Code, I would stick around to finalize, debug and document any remaining pieces of the project and future extensions to the framework this project implements. I'd love to continue to develop the physics code base in SymPy into the future as my coursework and outside research schedule would allow.

## Test cases and examples

* Clebsch-Gordon symmetries

Symmetry relations on the coefficients should hold, such as
```python
CG(j,m,j1,m1,j2,m2)==(-1)**(j1+j2-j)*CG(j,-m,j1,-m1,j2,-m2)
```
In addition, expressions involving sums and products of Clebsch-Gordon coefficients should be simplified where possible by implemented relations:
```python
CG(0,m,1/2,1/2,1/2,-1/2)*CG(0,mprime,1/2,1/2,1/2,-1/2)+CG(0,m,1/2,-1/2,1/2,1/2)*CG(0,mprime,1/2,-1/2,1/2,1/2)==KroneckerDelta(m,mprime)
```
These can also be evaluated using the existing means of evaluation.
```python
CG(1,0,1/2,1/2,1/2,-1/2).doit() == 1/sqrt(2)
```

* Projecting states

One of the main uses of the Clebsch-Gordon coefficients is being able to rewrite states in terms of different bases. First, projecting coupled states onto the upcoupled basis:
```python
JzKet(3/2,1/2,coupled=(1,1/2)).rewrite('Jz') == CG(3/2,1/2,1,1,1/2,-1/2)*TensorProduct(JzKet(1,1),JzKet(1/2,-1/2))+GC(3/2,1/2,1,0,1/2,1/2)*TensorProduct(JzKet(1,0),JzKet(1/2,-1/2))
```
Similarly for acting from the product space back to the coupled space:
```python
TensorProduct(JzKet(1,1),JzKet(1,-1)).rewrite('J2') == CG(2,0,1,1,1,-1)*JzKet(2,0,coupled=(1,1))+CG(1,0,1,1,1,-1)*JzKet(1,0,coupled=(1,1))+CG(0,0,1,1,1,-1)*JzKet(0,0,coupled=(1,1))
```
This would allow innerproducts between states to be evaluated:
```python
Innerproduct(JzKet(1,0,coupled=(1/2,1/2)),TensorProduct(JzKet(1/2,1/2),JzKet(1/2,-1/2))) == CG(1,0,1/2,1/2,1/2,-1/2)
```
Ideally, this operation would be implemented symbolically so that we could take arbitrary states and recover the expansion in term of a sum:
```python
j,m,j1,j2 = symbols('j m j1 j2')
JzKet(j,m,coupled=(j1,j2)).rewrite('Jz') == Sum(CG(j,m,j1,m1,j2,m2)*TensorProduct(JzKet(j1,m1),JzKet(j2,m2)),(m1,-j1,j1),(m2,-j2,j2))
```

* Acting operators on states

Operators will be modified so they act properly on coupled and uncoupled states, both in states that are diagonalized and not diagonalized:
```python
J2*JzKet(1,0,coupled=(1,1)) == hbar**2*2*JzKet(1,0,coupled=(1,1))
Jplus(space=2)*TensorProduct(JzKet(1,1),JzKet(1,0)) == hbar*sqrt(2)*TensorProduct(JzKet(1,1),JzKet(1,1))
Jz(space=1)*JzKet(2,1,coupled=(1,1)) == hbar*CG(2,1,1,1,1,0)*TensorProduct(JzKet(1,1),JzKet(1,0))
```

* Example: Spin-Orbit coupling

If we have some Hamiltonian that goes as \(\omega J_1\cdot J_2\). If we want to find the expectation value of the Hamiltonian in an uncoupled state, we will need to use the tools developed by this project. We note \(J_1\cdot J_2 = \frac{1}{2}(J^2+J_1^2+J_2^2)\). If the initial state is \(|1,1;1,-1\rangle\), then we have as the input:
```python
1/2*TensorProduct(JzBra(1,1),JzBra(1,-1))*(J2+J2(space=1)+J2(space=2))*TensorProduct(JzKet(1,1),JzKet(1,-1))
```
If we have this evaluate, the kets will be projected into the coupled basis so that they can be acted upon by the J2 operator. After being acted on by the operators, they will be converted back to the product basis so the inner product can be evaluated. This gives as a result:
```python
(3*hbar**2+2*hbar)*CG(2,0,1,1,1,-1)**2+(hbar**2+2*hbar)*CG(1,0,1,1,1,-1)**2+2*hbar*CG(0,0,1,1,1,-1)
```

* Example: Zeeman effect

If we take a hydrogen atom in a uniform magnetic field, we will get interactions between the electron and the field. Take for this only the Zeeman effect and the coupling of the electron and proton spin, such that the Hamiltonian is given as \(g\mu J_e\cdot B+4WJ_e\cdot J_p\). Taking the magnetic field in the z direction, we have \(g\mu B J_{e,z}+2W(J^2+J_e^2+J_p^2)\). We can see what this does to a state in the coupled basis \(|1,1\rangle\). We give the input of this as
```python
g, mu, B, W = symbols('g mu B W'
(g*mu*Jz(space=1)+2*W*(J2+J2(space=1)+J2(space=2))*JzKet(1,1,coupled=(1/2,1/2))
```
The second part of this Hamiltonian can be evaluated directly from this basis, however, the first part will require that the basis is switched to the product basis. Converting back then gives the result:
```python
(hbar*g*mu/2+14*W*hbar**2/2)*JzKet(1,1,coupled=(1/2,1/2))
```
Note `CG(j,m,j1,j1,j-j1,j-j1) == 1`.

## Current code work

**Closed pull requests**

[Fix Rotation.d function](https://github.com/sympy/sympy/pull/153) addressing a bug I found in evaluating elements of the Rotation operator

[Bug fix for evaluating J2 on a Jz ket](https://github.com/sympy/sympy/pull/155) addressing a bug I found in evaluating the J2 operator on a Jz eigenket.

[Change apply_operators to qapply](https://github.com/sympy/sympy/pull/152) addressing [Bug #2223](http://code.google.com/p/sympy/issues/detail?id=2223)

[Fixing the printing of the CNOT gate](https://github.com/sympy/sympy/pull/167) addressing [Bug #2188](http://code.google.com/p/sympy/issues/detail?id=2188)

[Fixing the Matrix.is_upper,.is_lower and .is_upper functions](https://github.com/sympy/sympy/pull/157) addressing [Bug #2220](http://code.google.com/p/sympy/issues/detail?id=2220)

**Open pull requests**

**Work in progress**

[spin_improvements branch](https://github.com/flacjacket/sympy/tree/spin_improvements) Work done that allows for converting between the Jx, Jy and Jz bases, which are the currently implemented eigenstates. Also implements innerproducts between states in the Jx, Jy and Jz bases and writing states as vectors in these bases. Note that this is similar to my proposed project, as I will be working on projecting between bases, but it is not the same as this is filling in the algebra for bases that are already implemented.

[spin_tests branch](https://github.com/flacjacket/sympy/tree/spin_tests) Implementing additional tests that the elements currently implemented in the spin module should be able to pass.

## Biography

I am a senior at the University of Minnesota and will be graduating this spring in physics and math and will begin graduate physics work next fall at the University of Illinois at Urbana-Champaign. As a student, I have taken several classes in programming; the classes I took covered C/C++ and parallel programming with CUDA. Also of note for this project are the physics classes I have taken, which include the 2 semester graduate level quantum mechanics sequence, which I will be completing this spring. Out of the classroom, I spent last summer working on developing a parallel implementation of the zlib compression library using CUDA. As for my experience with Python, beyond hobby coding, I am using Python, mainly using the PyROOT module, to do the analysis as a part of research for my senior physics thesis. As for my coding environment, I run GNU/Linux as my primary operating system. I primarily run Gentoo, but I have setup a virtual machine that runs Arch on which I do all coding and development work; this environment has Python 2.7.1. While this will be the first time I will be working on an open source project, I am excited to get the chance to use my extensive physics training as a stepping stone to developing software with the Sympy community.

## References

Varshalovich, D.A. "Quantum Theory of Angular Momentum", World Scientific Publishing, 1988.

Zare, Richard. "Angular Momentum", John Wiley & Sons, 1988.

Shankar, Ramamurti. "Principles of Quantum Mechanics, 2nd ed", Springer, 1994.