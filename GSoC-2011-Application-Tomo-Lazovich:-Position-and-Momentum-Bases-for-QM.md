GSoC 2011 Application Tomo Lazovich: Position and Momentum Bases for QM
==============================

## My information

* Name: Tomo Lazovich
* University / current enrollment: Harvard University (graduating May 2011)
* Bio/background: I am a physics major with a CS minor at Harvard and am about to graduate this May. My main research has been in particle physics. I spent one summer working at Fermilab on the CDF experiment and two summers on the ATLAS experiment at CERN. My experience is in writing software for data analysis at these experiments. As a physics major, I also have much experience with quantum mechanics, having taken all of the undergraduate courses on QM offered as well as courses with applications of QM, such as solid state physics. I also have experience in C++, C, Python, Java, and many web programming technologies. I believe that I am qualified to write the necessary code for sympy and to understand the quantum mechanics of the systems that will be represented. 
* Email: lazovich [at] NOSPAM gmail [dot] com
    
    
## My coding platform

My current setup is an Ubuntu system. I have been programming in Python for two years now. I am familiar with both SVN and git so I will be able to work in the open source setting. 

## Getting to know the community/codebase

I forked the git repository and began to tackle this issue: [[http://code.google.com/p/sympy/issues/detail?id=2186&q=label%3Aquantum]]

to become familiar with the code base, particularly in sympy.physics.quantum. After introducing myself to the list and privately to Brian Granger, the physics project mentor, as well as asking some questions about how to handle operators that are both Hermitian and Unitary, I came up with a potential solution. After changing HermitianOperator to handle the special case where the operator is also Hermitian, I submitted my first pull request here: [[https://github.com/sympy/sympy/pull/160]]

That request is still under review!

## My Project

### Goal

Currently in sympy, there is support for discrete Hilbert spaces, which are quite useful for spin calculations or symbolic quantum computing. However, there is only very preliminary support for continuous Hilbert spaces. The goal of this project would be to implement position/momentum representations for operators and eigenstates in various coordinate systems, including cartesian, cylindrical, and spherical. After adding support for these operators, we will be able to easily represent many of the "textbook" quantum mechanics systems, including particle in a box, simple harmonic oscillator, hydrogen atom, etc. 

### Motivation

By thinking about how to represent operators that depend on continuous variables, we can open up a whole new area of functionality for the sympy.physics.quantum module. Beyond implementing the standard textbook quantum mechanical systems, support for continuous bases is a big step towards being able to solve the Schrodinger equation symbolically in these coordinate systems. It represents the completion of a big missing piece of the quantum module. The representation of operators as matrices in discrete Hilbert spaces works quite well, and the implementation of the continuous spaces will greatly increase the number of quantum mechanical calculations possible with SymPy.

### Project deliverables
* **Modified represent.py**: some operators (for example, momentum), when represented in another basis, actually take on a representation as a derivative of that basis variable (i.e. p ~ d/dx). Represent currently has no way of dealing with this
* Implementations of position and momentum operators in **Cartesian, cylindrical, and spherical** coordinates in **1D, 2D, and 3D**. 
* **Example systems**: implement particle in a box, simple harmonic oscillator, hydrogen atom, etc. in varying numbers of dimensions
* **Symbolic Schrodinger equation solver** (time permitting): if everything goes as planned, it might be possible to incorporate a PDE solver for solving the Schrodinger equation with symbolic Hamiltonians in these bases.

### Timeline

* **Startup period** (April 25-May 27): Become more familiar with the quantum code base; sketch out a more detailed design of the modules which will implement the proposed functionality and discuss with the sympy community (Note that while the GSoC period technically starts on May 23rd, I am in school until the 27th so only after this will I be able to work full time).
* **Phase 1** (May 28-June 18): Modify the pre-existing codebase; change represent to be able to deal with arbitrary representations of operators, including derivatives; will most likely have to somehow incorporate the sympy diff function; there will certainly be many subtleties involved in this portion
* **Phase 2** (June 18-July 16): Implementation of the key position and momentum bases; first modify the already existent 1D cartesian classes to include representations of momentum operator in the position basis and vice-versa. Then add 2D and 3D cartesian operators, as well as cylindrical and spherical equivalents;
* **Phase 3** (July 16-August 6): Go crazy! Implement as many textbook QM systems as possible with the new framework that is in place! Topics include particle in a box in 1D, 2D, and 3D, both with infinite and finite potential walls, simple harmonic oscillator, hydrogen atom, delta function potential, etc.
* **Phase 4** (August 6-August 22): This can act as a buffer period in case the other pieces take longer than expected. If everything goes as planned, however, this could potentially be used to investigate writing a solver for symbolic Schrodinger equations in the bases that were implemented.

### Some implementation details
* **Code design**: A good question to ask is how the position and momentum bases in the various coordinate systems will actually be implemented. I will attempt to model the structure after the cartesian.py file written by Brian Granger. The basic idea is to have classes such as XOp and POp for operators and XKet and PKet for the corresponding kets. The operator classes will implement methods such as ```_eval_hilbert_space ``` and ```_apply_operator_XKet ```. These functions define the space on which the operator is defined and the behavior of the operator when applied to a wavefunction in a particular basis. An example of functionality that is not implemented, even in the example code, is given in the POp class. POp has a ```_apply_operator_PKet``` function but not an ```_apply_operator_XKet``` function. Applying the operator to an XKet requires taking a derivative, so such a function could only be implemented after having defined how we will represent derivatives in the modified represent.py

* **Eigenstates**: The eigenstates, when represented in their bases, will actually take the form of functions in position or momentum space. Let's consider, for example, the classic particle in a box system, implemented as an example in piab.py. When represented in the X basis, it takes the form of a sine wave at different energy levels. Thus, part of the project will be characterizing these representations in the various bases. It would also be useful to be able to use sympy integration modules to transform between x and p space.

* **Example systems**: Here I will provide a more complete list of the different example systems that I think are feasible to be implemented: Free particle in 1D, 2D, and 3D; Particle in an infinite potential well and particle in a finite potential well in 1D, 2D, and 3D; delta function potential; rectangular potential barrier (tunneling effect); quantum harmonic oscillator in 1D, 2D, and 3D, including creation and annihilation operators; hydrogen atom in spherical coordinates.




