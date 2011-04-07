
					GSOC Proposal by Aashish Mishra

Name:
Aashish Mishra

Contact Information:
  IRC Nick at Freenode: 
     admish
  Email: 
     aashishduttmishra@gmail.com
  Blog: 
     http://www.techo2.blogspot.com/
  Cell: 
     +91-9680129010
 

Title:
                Extended symbolic Framework for Quantum Computation in Sympy
 

Synopsis:
Sympy is a powerful mathematical library to perform mathematical operations over data. Sympy is built on Python that can do symbolic manipulations of complicated mathematical expressions in a human-readable manner which seems easy to the user. This library has been extended up to some physics calculation too. Quantum Computation is an emerging field which will potentially revolutionize the field of computation by providing practical polynomial-time algorithms to many NP problems, this will allow problems that would normally take impractical periods of time to be solved quickly. A symbolic simulation of “qubits” and “quantum gates” on a classical computer using SymPy would be invaluable to the study and understanding of quantum computation. 

This project will create classes and functions within SymPy that will extend the functionality of qubits, the quantum gates that operate on them and various measurement and calculations schemes. The idea here is to inherit the powerful properties of the sympy.core.expr.Expr and other SymPy classes to create symbolic representations of the mathematical and physical entities relevant in quantum computing. Users will be able to manipulate the resulting Python objects in a simple way that will be similar to the syntax of hand-written physics. The clarity this will provide will allow individuals studying quantum computation to focus on the mathematical and physics aspects of quantum computers rather than on the minutiae of how a quantum computer is represented on a classical computer.

Benefits to Community:
The study of quantum computation is an interesting multidisciplinary problem involving physics, mathematics and computer science disciplines. Being able to quickly construct, manipulate and even visualize quantum computations in SymPy will allow researchers in the field to focus on their research and will provide students with a new tool for learning the field. Ultimately, this may allow individuals to develop new computer aided proofs, create new quantum algorithms and simulate non-trivial quantum computations. This work may also help in the creation of quantum computer compilers that use classical machines to convert a single unitary gate into a series of universal gates; the ability to convert a large unitary operation into a series of small and simple gates will be highly practical when a many qubit quantum computer is actually created.
Description:
A series of n qubits is represented by a  column matrix. These qubits are operated on by quantum gates which map their amplitudes in a known way; this operation is represented by multiplying the column vector by a x Unitary matrix. To start my project, I will develop the general single quibit class as well as the 2x2 matrices which represent the most frequently used single qubit quantum gates. I will also create a framework that can deal with varying basis sets for the qubits and gates. Objects that are subclasses of Expr are capable of symbolically simplifying an expression automatically upon creation. Part of the difficulty will be determining exactly when automatic simplification should occur. For example, a phase matrix multiplied by itself is the same as a Pauli-Z matrix. It is my duty to determine if this simplification should occur. Here are the classes that I will develop as well as the parents they will inherit from:

class Qbit(Expr):
class Gate(Expr):
class HadamardGate(Gate):
class XGate(Gate):
class YGate(Gate):
class ZGate(Gate):
class PhaseGate(Gate):
class TGate(Gate):

The next portion of the project will increase the complexity so that the code, given enough time and memory, can handle an arbitrary number of quibits. Along with this, I will incorporate a number of common multi-qubit gate operators. These gate operators will be set up to work on a subset of a larger set of qubits; which is to say, I would make it so that the 4x4 CNOT gate can act on two qubits within a set of any size.

class QBitState(Expr):
class CNOT(Gate):
class ControlledZ(Gate):
class Swap(Gate):

It can be shown that the single qubit and CNOT gates are universal for quantum computers. This fact means that we can use these gates alone to implement any quantum computation; this is akin to the universality of the NAND gate in classical computing. That is to say, a set of CNOT gates and a set of single qubit gates can approximate any quantum computational system to any desired degree of accuracy. Since many of our large gate matricies are going to be sparse with only a few non-zero entries, it would be impractical and inefficient to store all of the zeros in a matrix.  Instead, I will investigate the best way to store the data in a way that makes matrix multiplication fast without sacrificing memory. Just like with the one qubit classes, we need to be able to transform the qubits and gates into different bases; in addition, we will need to be able to specify which qubits we will measure and how. We will also want to model the POVM form of measurement as it has a higher chance of returning a conclusive result. 

The last step of development will involve the implementation of common algorithms in quantum computation, namely the Quantum Fourier Transform; this transform is essential to many other important processes such as Shor's algorithm for integer factorization.

class QFourierTransform(Function):

Deliverables:  
During the summer I will keep up with the following schedule, and communicate (in person or by email) weekly with my mentor on my progress. After each phase of the schedule, I intend to merge my branches with the rest of the Sympy project; to do this, I will first submit it to be reviewed by the Sympy community and then address any criticisms they may have. I will create a github account where I will publicly host my branches and base these branches off the main Sympy repository at http://git.sympy.org/?p=sympy.git;a=summary. During the development phase, I will create testing classes that will ensure proper functionality of the code under all cases; this will make sure the physics is correct. I will use good documentation making sure my code is clean and can be easily read and understood. Throughout this time, I will blog weekly about my project and invite all of my physics and computer science friends, as well as the SymPy developers, to follow my blog. 
Phase I (Weeks 1-3):
Initial Design Phase
During this time, I will further develop my understanding of Quantum computation. I will do this by reading through the book "Quantum Computation and Quantum Information" by Michael Nielsen and Isaac Chaung; this book discusses at great length the mathematical theory of quantum computation and its context within the field of computation as a whole. I will especially focus on getting a feel for the implementation of Quantum Fourier Transforms as well as other quantum algorithms. I will still be in school during this phase, so much of my study will be focused on learning theoretical and quantum mechanics for my physics classes; the learning here will be essential for completing the project. I will spend some time hammering out the exact structure of the project.

Phase II (Weeks 4-6)
Single Qubits and their Gates
School is finished now and I will implement the classes necessary for a single qubit and the common operators (gates) on the single qubit. This will include allowing qubits and gates to be represented in different bases.  Different measurement schemes (projective, POVM) will also be implemented.

Phase III (Week 7-9):
Multiple Qubits and their Gates
Here, I will build on the previous effort to represent single qubit machines and implement the classes necessary to represent an arbitrarily sized collection of qubits.  As with the single qubit work, this phase will include the development of code for handling basis sets and measurements of multi-qubit states.

Phase IV (Week 10-12):
Quantum Algorithms
This phase will use the code established before to begin to implement the common algorithms of quantum computation. In particular, I will work on implementing a Quantum Fourier Transform routine. In an actual quantum computer, this routine would be essential to fast integer factorization which is of great importance to cryptography as many public key encryption schemes rely on the difficulty of factoring large numbers with few prime factors.  
 
Related Works:
jQuantum and libquantum are two open-source libraries for Java and C respectively that implement numerical simulations of quantum computers. My project will bring some of this functionality in addition to symbolic manipulations to Sympy. Since Sympy is incredibly human-readable, with a syntax almost identical to the way one would write a problem on a chalkboard, this will make the use of the library more intuitive. Thus, an implementation of a symbolic quantum computer under Sympy will abstract away many of the particulars allowing anyone studying quantum computation to focus on studying the computers themselves.
   
http://jquantum.sourceforge.net/ 
http://www.libquantum.de/
 
Biographical Information:
 I'm a third year physics major with a strong interest in computer science and computational physics. I currently have a 3.6 GPA and have a strong experience in Quantum Mechanics, Linear Algebra and Computer Science.
 
I have taken an introductory series in computer science and am currently taking an upper division course in Systems Programming. During my computer science classes, I have used git version control software on projects and other assignments. While I am only starting to learn Python, I am quite skilled in the C, Java, and Matlab programming languages. In addition, I am capable of programming at a lower abstraction level, having learned how to code for the LC-3 Assembly ISA. I use the Ubuntu Linux operating system at home and am competent in Unix-like operating systems. I intend to continue to learn Python during the spring quarter so that I will be ready to use it during the summer.
 
I am currently taking an upper division course in Quantum Mechanics, which will increase my knowledge in the subject giving me the necessary skills to complete this project. I have already taken courses in linear analysis and complex analysis which will be essential to this project as quantum mechanics and quantum computation are written in the language of linear algebra and complex numbers. In addition, I am taking a course in mathematical methods of theoretical physics which will help solidify my knowledge of the mathematics necessary to complete this project.

As I don't have many significant time obligations ever since Battlestar Galactica was canceled, I see no reason why I would not be able to spend 40 or more hours a week on this project after I finish school in the third week. Before the third week, I plan on spending as much time as I can spare working on the project, with my classes in quantum mechanics helping me better understand the topic.
