#GSoC 2011 Application - Luis Garcia - Solovay-Kitaev algorithm
## Abstract
The Solovay-Kitaev algorithm is an important step in the building of quantum computing as it provides a way of _compiling_ quantum algorithms with arbitrary \(U\) gates in \(SU(d)\) into sequences composed of gates from a fixed, finite set. The algorithm runs in \(polylog(1/e)\) time on a classical computer and returns a sequence of \(polylog(1/e)\) length, where \(e\) is the aimed accuracy. This algorithm requires a preparatory stage that is run once for each value of \(d\) required.

## Introduction
Quantum computing has been an active field of study in the twenty to thirty years, with a marked increase in activity after the introduction of Shor’s factoring algorithm. Great strides have been made in the development of the quantum computing and information theory, bringing validity and feasibility to the construction of quantum computing hardware. Quantum-error-correction codes were a huge milestone against criticisms of the impossibility of having completely isolated machines to avoid decoherence. 

Another step forward to the construction of quantum computer is the Solovay-Kitaev theorem proves that any gate \(U\) in \(SU(d)\) can be approximated to a given accuracy \(e\) with a sequence \(S\) of gates \(g_n\) from a set \(G\) that fills \(SU(d)\) densely. The implications of this theorem are that any unitary gate used by a quantum algorithm can be constructed with a set of available gates. The gates on the available set would ideally be fault-tolerant, and constructable. With this you can tackle the issue of oracle and blackbox gates common in quantum algorithms and break them down into a sequence of known gates.

In order to find the decomposition of an arbitrary \(U\) gate, the Solovay-Kitaev algorithm can be computed on a classical computer and it will give back the sequence \(S\) approximation for the desired accuracy. 

## Project Details
I plan to implement the Solovay-Kitaev algorithm based on a first approach on Nielsen and Dawson [0] and implementing the preparatory stage based on Nagy [1]. Based on Brian Granger's hint my first approach will be to port Paul Pham's implementation [4] into SymPy. Pham's implementation breaks it into three stages: generation, preparatory stage, where you generate the \(e_0\) approximations for arbitrary \(U\), build of search tree (this is needed for the actual algorithm), and finally the actual algorithm. The generation of the \(e_0\) sequences and the search tree is time consuming so Pham stores both as files and loads them into memory when they are needed.

The default set G would be defined to be the Clifford group (Hadamard, CNOT, Pauli) and \(\pi/8\) gate. However if time allows I would like to allow for the user to specify a different set to use, given it complies with the requirements. That is all gates from the set are in \(SU(d)\) as well as their conjugated transpose and the set generates \(SU(d)\). It follows that if the user wishes to define a set, he/she would have to run the preparatory stage in order to use the SK algorithm. The idea would be to test this with \(SU(2)\) and \(SU(4)\) while having the implementation support \(d>4\) but not recommend it for the time being.

Besides [0] and [1], my first approach would be to read as much information as possible about the theorem/algorithm. One of my other references would be Nielsen and Chuang [3]. I am currently taking a Quantum Information Processing class and we use [3] as our textbook so I’m familiar with it. In the class we cover quantum algorithms(Shor, Grover, Deutsch, Deutsch-Jozsa) , quantum circuits (QFT), adiabatic quantum computing, quantum information, compression, quantum entropy, quantum communication, quantum channels, quantum error correction, qkd, among others.

As part of my school’s graduation reqs I need to work jointly with a professor on a project over the period of about one year and I plan on working with my QIP professor in quantum computing related research. So having sympy.physics.quantum as a tool would really help me. I plan on continuing to collaborate on SymPy well after the summer and continue to improve work in the quantum module but also on the other parts of SymPy.

## Schedule
**Week 0 and before:** Read as much as possible about the Solovay-Kitaev algorithm, get a more in depth knowledge of the sympy's codebase. This would also work as a community bonding period. I finish with all my school related things by the beginning of May so before that I'll be working with limited time.

### Beginning of program
**Week 1:** Definition of class structure, methods, and general, broad breakdown of the implementation. This requires to have a very good idea of SymPy's organization and the resources available to see what I can reuse and what needs to be done from scratch. On a general perspective I plan to divide work into two big the preparation stage and the actual algorithm. My idea right now is having   
**Week 2:**  
**Week 5-7:**  
###Midterms
**Week 8-9:**  
**Week 10-11:**  
**Week 12(-13):**  

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
[3]Nielsen, Chuang. [Quantum Computation and Quantum Information](http://www.amazon.com/Quantum-Computation-Information-Cambridge-Sciences/dp/0521635039)