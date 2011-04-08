#GSoC 2011 Application Luis Garcia: Solovay-Kitaev algorithm
## Abstract
The Solovay-Kitaev algorithm is an important step in the building of quantum computing as it provides a way of _compiling_ quantum algorithms with arbitrary \(U\) gates in \(SU(d)\) into sequences composed of gates from a fixed, finite set. The algorithm runs in \(polylog(1/e)\) time on a classical computer and returns a sequence of \(polylog(1/e)\) length, where \(e\) is the aimed accuracy. This algorithm requires a preparatory stage that is run once for each value of \(d\) required.

## Introduction
Quantum computing has been an active field of study in the twenty to thirty years, with a marked increase in activity after the introduction of Shor’s factoring algorithm. Great strides have been made in the development of the quantum computing and information theory, bringing validity and feasibility to the construction of quantum computing hardware. Quantum-error-correction codes were a huge milestone against criticisms of the impossibility of having completely isolated machines to avoid decoherence. 

Another step forward to the construction of quantum computer is the Solovay-Kitaev theorem proves that any gate \(U\) in \(SU(d)\) can be approximated to a given accuracy \(e\) with a sequence \(S\) of gates \(g_n\) from a set \(G\) that fills \(SU(d)\) densely. The implications of this theorem are that any unitary gate used by a quantum algorithm can be constructed with a set of available gates. The gates on the available set would ideally be fault-tolerant, and constructable. With this you can tackle the issue of oracle and blackbox gates common in quantum algorithms and break them down into a sequence of known gates.

In order to find the decomposition of an arbitrary \(U\) gate, the Solovay-Kitaev algorithm can be computed on a classical computer and it will give back the sequence \(S\) approximation for the desired accuracy. 

## Project Details
I plan to implement the Solovay-Kitaev algorithm based on a first approach on Nielsen and Dawson [0] and implementing the preparatory stage based on Nagy [1].

The preparatory stage implies on finding constant gate sequences up to length \(l_0\) that work as the base approximation upon which the Solovay-Kitaev algorithm builds recursively. Details of this can be found in [0]. This preparatory stage only needs to run once for a given set of gates \(G\) for \(SU(d)\).

The default set G would be defined to be the Clifford group (Hadamard, CNOT, Pauli) and \(Pi/8\) gate. However if time allows I would like to allow for the user to specify a different set to use, given it complies with the requirements. That is all gates from the set are in \(SU(d)\) as well as their conjugated transpose and the set generates \(SU(d)\). It follows that if the user wishes to define a set, he/she would have to run the preparatory stage in order to use the SK algorithm.

Besides [0] and [1], my first approach would be to read as much information as possible about the theorem/algorithm. One of my other references would be Nielsen and Chuang [3]. I am currently taking a Quantum Information Processing class and we use [3] as our textbook so I’m familiar with it. In the class we cover quantum algorithms(Shor, Grover, Deutsch, Deutsch-Jozsa) , quantum circuits (QFT), adiabatic quantum computing, quantum information, compression, quantum entropy, quantum communication, quantum channels, quantum error correction, qkd, among others.

As part of my school’s graduation reqs I need to work jointly with a professor on a project over the period of about one year and I plan on working with my QIP professor in quantum computing related research. So having sympy.physics.quantum as a tool would really help me. I plan on continuing to collaborate on SymPy well after the summer and continue to improve work in the quantum module but also on the other parts of SymPy.

## Schedule
**Week 0 and before:** Read on the 

## Me
* **Name:** Luis Garcia
* **University:** Physics major in Tec de Monterrey (Mexico)
* **Email:** ppn (dot) online (at) me (dot) com
* **Github:** ppn
* **IRC handle:** ppn

My completed coursework so far has  included: Classical mechanics, Electromagnetic Theory, Calculus,  Vector Calculus, Mathematical methods for Physics, ODE/PDE,  Computational Physics (a numerical methods class applied to Physics,  we coded almost entirely in Matlab), Linear Algebra, Data Structures.  Some of my current classes are: Quantum Mechanics, Quantum Information  Processing, Electrodynamics. I've grown quite fond of QM and quantum  computing so far and I am excited to see that SymPy has projects for  both areas. On the technical side I have mainly coded in Java, C#, C++, Matlab and I've played around for a bit with Python, PHP, HTML, CSS. The past two summers I've been an intern with Microsoft, first on the Servers and Tools division and then in a team within the  Office org.

My platform of choice is Mac OS X but also work on Windows and Linux. My distro of choice is Fedora.

## References
