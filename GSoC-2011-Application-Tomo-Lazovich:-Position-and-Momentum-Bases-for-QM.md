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
* **Modified HilbertSpace**: need to add functionality for representing an infinite number of dimensions
* Implementations of position and momentum operators in **Cartesian, cylindrical, and spherical** coordinates in **1D, 2D, and 3D**. 
* **Example systems**: implement particle in a box, simple harmonic oscillator, hydrogen atom, etc. in varying numbers of dimensions
* **Symbolic Schrodinger equation solver** (time permitting): if everything goes as planned, it might be possible to incorporate a PDE solver for solving the Schrodinger equation with symbolic Hamiltonians in these bases.