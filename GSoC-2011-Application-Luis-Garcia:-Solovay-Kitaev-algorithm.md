#GSoC 2011 Application - Luis Garcia - Solovay-Kitaev algorithm
## Abstract
The Solovay-Kitaev algorithm is an important step in the building of quantum computing as it provides a way of _compiling_ quantum algorithms with arbitrary \(U\) gates in \(SU(d)\) into sequences composed of gates from a fixed, finite set. The algorithm runs in \(polylog(1/e)\) time on a classical computer and returns a sequence of \(polylog(1/e)\) length, where \(e\) is the aimed accuracy. This algorithm requires a preparatory stage that is run once for each set \(G\) that generates \(SU(d)\).

## Introduction
Quantum computing has been an active field of study in the twenty to thirty years, with a marked increase in activity after the introduction of Shor’s factoring algorithm. Great strides have been made in the development of the quantum computing and information theory, bringing validity and feasibility to the construction of quantum computing hardware. Quantum-error-correction codes were a huge milestone against criticisms of the impossibility of having completely isolated machines to avoid decoherence. 

Another step forward to the construction of quantum computer is the Solovay-Kitaev theorem proves that any gate \(U\) in \(SU(d)\) can be approximated to a given accuracy \(e\) with a sequence \(S\) of gates \(g_n\) from a set \(G\) that fills \(SU(d)\) densely. The implications of this theorem are that any unitary gate used by a quantum algorithm can be constructed with a set of available gates. The gates on the available set would ideally be fault-tolerant, and constructable. With this you can tackle the issue of oracle and blackbox gates common in quantum algorithms and break them down into a sequence of known gates.

In order to find the decomposition of an arbitrary \(U\) gate, the Solovay-Kitaev algorithm can be computed on a classical computer and it will give back the sequence \(S\) approximation for the desired accuracy. 

## Project Details
I plan to implement the Solovay-Kitaev algorithm using Nielsen and Dawson [0], Nagy [1], Nielsen and Chuang [2] as references, among others. Based on Brian Granger's hint my first approach will be to port Paul Pham's implementation [3] into SymPy. Pham's implementation breaks it into three stages: generation, preparatory stage, where you generate the \(e_0\) approximations for arbitrary \(U\), build of search tree (this is needed for the actual algorithm), and finally the actual algorithm. The generation of the \(e_0\) sequences and the search tree is time consuming so Pham stores both as files and loads them into memory when they are needed.

The default set \(G\) would be defined to be \(H\), \(T\), and \(T^{-1}\) for \(SU(2)\) and for \(SU(4)\) the same set but adding the \(CNOT\) gate. However if time allows I would like to allow for the user to specify a different set to use, given it complies with the requirements. That is all gates from the set are in \(SU(d)\) and their conjugated transpose is also in the set, and the set generates \(SU(d)\). It follows that if the user wishes to define a set, he/she would have to run the preparatory stage in order to use the SK algorithm. The idea would be to test this with \(SU(2)\) and \(SU(4)\) while having the implementation be extensible to \(d>4\) but not recommend it for the time being given the memory and time requirements.

The idea is porting Pham's implementation in Python/numpy into Python/SymPy removing as much numpy dependencies as possible. This is possible since sympy.physics.quantum already has classes for gates, operators, and related methods. A possible class breakdown based on Pham's would be something as follows:  

* **quantum[.skc]generatesu2:** this would define the default set for \(SU(2)\) and the associated settings for the preparatory stage. The settings include simplification rules, corresponding hilbert space, size of the eye.  
* **quantum[.skc].generatesu4:** same as the last but for \(SU(4)\).  
* **quantum[.skc].generate:** build the basic approximations and save the generations into files using the settings specified in one of the two modules before.  
* **quantum[.skc].buildtree:** process the generations produced into a kd tree and save into a file to allow search during the sk algorithm.  
* **quantum[.skc].searchtree:** for a given gate \(U\) it will search the tree for the generation that gives the best approximation using the operator norm as the distance.  
* **quantum[.skc].simplify:** Engine to simplify gate sequences, since the basic approximation are all the possible permutation of the gates within the set \(G\) less than a length \(l_0\), simplification is needed to avoid having sequences that are equivalent.  
* **quantum[.skc].bgcdecomposition:** This module will do a balanced group commutation decomposition with \(UU^{-1}\) as input. The result would ve \(V\),\(W\) such that \(VWV^{-1}W^{-1}=U\).  
* **quantum[.skc].skc:** This will be the module someone would use to get an approximation \(S\) for an arbitrary gate \(U\). So this is the module where the sk algorithm is actually implemented.  

Besides this there are some things that need implementation for example an implementation of kdtree, not sure where we would put this in SymPy since it is not something specific for sympy.physics.quantum. I would be leveraging quantum.tensorproduct quantum.gate, quantum.hilbert, quantum.dagger, quantum.matrixutils, quantum.operator and others. The operator norm would need to be added to quantum.operator since it it the basic condition in the algorithm. Further experimenting and exploration of SymPy's and Pham's codebase will help me refine the class structure and understand what is missing on SymPy to make the Solovay-Kitaev compiling to work.

## Why this? Why me? Why I care?
Besides [0], [1], and [2], my first approach would be to read as much information as possible about the theorem/algorithm. I am currently taking a Quantum Information Processing class and we use [2] as our textbook so I’m familiar with it. In the class we cover quantum algorithms(Shor, Grover, Deutsch, Deutsch-Jozsa) , quantum circuits (QFT), adiabatic quantum computing, quantum information, compression, quantum entropy, quantum communication, quantum channels, quantum error correction, qkd, among others.

As part of my school’s graduation reqs I need to work jointly with a professor on a project over the period of about one year and I plan on working with my QIP professor in quantum computing related research. So having sympy.physics.quantum as a tool would really help me. I plan on continuing to collaborate on SymPy well after the summer and continue to improve work in the quantum module but also on the other parts of SymPy.

## Schedule
**Week 0 and before:** Read as much as possible about the Solovay-Kitaev algorithm, get a more in depth knowledge of the sympy's codebase. This would also work as a community bonding period. I finish with all my school related things by the beginning of May so before that I'll be working with limited time. After being done with school I should be able to allocate 40-50 hrs/week. I mention the main modules in the schedule and things like the operator norm, modifications to existing modules, etc. would be implemented on a need basis. The idea would be to work as modular as possible to have various push ins throughout the summer. I work with a test driven approach, where I generate the basic test cases in the beginning so by the end of the implementation the basic tests pass and the testing after the dev phase is diminished.

### Beginning of program
**Week 1-2:** Implementation of kd tree based on Matej Drame's python implementation.  
**Week 3:** Testing of kd tree, documentation, and getting code review to push in. Work on simplify.  
**Week 4-5:** Work on generate, generatesu2, generatesu4.  
**Week 6-7:** Work on buildtree, searchtree.
###Midterms
**Week 8:** Work on bgcdecomposition.  
**Week 9:** Work skc.  
**Week 10-11:** Testing and work on examples for documentation.  
**Week 12(-13):** Code review, last bug fixes, finish pushing in everything.  

## Me
* **Name:** Luis Garcia
* **University:** Physics major in Tec de Monterrey (Mexico)
* **Email:** ppn (dot) online (at) me (dot) com
* **Github:** ppn
* **IRC handle:** ppn

My completed coursework so far has  included: Classical mechanics, Electromagnetic Theory, Calculus,  Vector Calculus, Mathematical methods for Physics, ODE/PDE,  Computational Physics (a numerical methods class applied to Physics,  we coded almost entirely in Matlab), Linear Algebra, Data Structures.  Some of my current classes are: Quantum Mechanics, Quantum Information  Processing, Electrodynamics. I've grown quite fond of QM and quantum  computing so far and I am excited to see that SymPy has projects for  both areas. On the technical side I have mainly coded in Java, C#, C++, Matlab and I've played around for a bit with Python, PHP, HTML, CSS. The past two summers I've been an intern with Microsoft, first on the Servers and Tools division and then in a team within the  Office org.

My platform of choice is Mac OS X but also work on Windows and Linux. My distro of choice is Fedora.

## References
[0]Dawson, Nielsen. The Solovay-Kitaev Algorithm. arXiv:quant-ph/0505030v2  
[1]Nagy. On an implementation of the Solovay-Kitaev algorithm. arXiv:quant-ph/0606077v1  
[2]Nielsen, Chuang. [Quantum Computation and Quantum Information](http://www.amazon.com/Quantum-Computation-Information-Cambridge-Sciences/dp/0521635039)  
[3] [Phalm's implementation](http://sourceforge.net/p/quantumcompiler/home/)