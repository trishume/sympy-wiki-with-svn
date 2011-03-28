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



## Project Implementation

The basis of this project is the implementation of symbolic Clebsch-Gordon coefficients/Wigner symbols. To implement this, I will create coefficients as a subclass of Expr, which allows us to create symbolic expressions based on input parameters. In this case, the Clebsch-Gordon coefficients would take 6 parameters, 2 for each of the two particles in the product basis and 2 for the particle in the coupled basis. This can be extended to the coupling of more than two particles with Wigner-6j/9j/... symbols; these will be added if time allows, though this project will develop the framework that could be extended to include these objects. Numerical calculation of the coefficients will be possible by invoking the current numerical methods, but of note will be the implementation of symbolic manipulation and simplification by the various symmetries and properties that have been developed for evaluating Clebsch-Gordon coefficients (see Varshalovich, "Quantum Theory of Angular Momentum", pp 244-264 as a sample of the available relations). There are many such relations that could be implemented, and the how many are implemented will be based on the amount of time available determined in discussions with my mentor.

With the Clebsch-Gordon coefficients implemented, I will improve the spin algebra to utilize these terms. The first component of this will be to modify the treatment of spin states to be able to utilize product and coupled bases. This would be implemented such that if given a coupled state |j,m>, it could be written as the sum of tensor products of spin states with the appropriate Clebsch-Gordon cofficient and if given a tensor product of spin states, it could written as a sum of coupled states, again with the appropriate Clebsch-Gordon coefficient.

The next stage of this project would be to integrate the use of coupled and product bases with the spin operators. The spin operators as they are currently implemented are designed to act on single spin states. This can be immediately applied to the spin operators of the coupled basis acting on coupled states. What would need to be implemented for this project would be spin operators in one of the tensor product bases. In addition, all the spin operators would need to implement methods for acting on tensor product states. In implementing these things, I would use the methods developed for moving states between the coupled and product bases using the Clebsch-Gordon coefficients.

My plan for this project would be to first implement this for coupling between two spin states. Once this is done, I would extend these methods to include coupling between more states. The current numerical implementation includes up to Wigner-9j symbols, which gives coupling between 4 spin states. My goal would be to implement the necessary spin algebra to include coupling between at least this many states.

## Timeline

The specifics of each of these steps is outlined in the implementation.

During the official time frame of the Summer of Code, I have no other serious commitments and can easily commit to the required 40 hours of work per week and I'll put as much free time as I can into working this project because of the interesting subject matter.

**Before official start**

Review the current source code and begin integrating with the community. Work with my mentor to finalize a plan of action and formulate a project design, then begin preliminary coding work on the project.

**Weeks 1-3**

Work on implementing the Clebsch-Gordon class. This would include developing the basic functionality of the class, such as evaluation, use in equations and printing, but would also include the symbolic manipulation through the symmetry relations and properties of the Clebsch-Gordon coefficients.

**Weeks 4-5**

Expand the spin states to work with both product and coupled spin states.

**Weeks 6-7**

Modify spin operators to work with the new formulation of spin states. Prepare for midterm evaluation.

**Week 8**
Midterm evaluation

**Weeks 8-10**

Implement terms for coupling between more spin states, i.e. Wigner 6j and 9j symbols.

**Week 11-12**

Finalize project, adding any final documentation and tests, and pencils down.

## Bio

I am a senior at the University of Minnesota and will be graduating this spring in physics and math and will begin graduate physics work next fall at the University of Illinois at Urbana-Champaign. While a student, I have taken several classes in programming; the classes I took covered C/C++ and parallel programming with CUDA. Also of note for this project are the physics classes I have taken, which include the 2 semester graduate level quantum mechanics sequence, which I will be completing this spring. Out of the classroom, I spent last summer working on developing a parallel implementation of the zlib compression library using CUDA. As for my experience with Python, beyond hobby coding, I am using Python, mainly using the PyROOT module, to do the analysis as a part of research for my senior physics thesis. While this will be the first time I will be working on an open source project, I am excited to get the chance to use my extensive physics training as a stepping stone to developing software with the Sympy community.