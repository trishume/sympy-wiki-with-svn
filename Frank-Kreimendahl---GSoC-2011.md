# Bio

Name: Frank Kreimendahl  
University: 1st year PhD candidate at University of New Hampshire  
Contact: ylfchild@gmail.com  
Short Bio: Around the time that I completed my undergraduate studies in mathematics, I realized that the types of problem solving that I enjoyed in math are more prevalent in computer science. I recently returned to school to pursue a PhD in computer science and I have found myself more engaged in the material than I had been before.


# Motivation

SymPy does not currently have a way to handle large matrices, and its matrix implementation and interface are not separated. The first goal of my project is to separate the interface from the back end, which will allow simpler updates in the future. The next goal is to implement sparse storage structures, and accompanying functions that will be available to users. The motivation for this goal is to give users an interface that specifies the storage type of a matrix. The user can then call functions of the matrix without worrying about the storage type. This second goal will require algorithms that apply to sparse numerical matrices, but may not work as efficiently with symbolic ones. I will write tests to compare the execution times of different algorithms, compared to each other, as well as to dense matrix algorithms that are currently implemented. (This also includes verifying that storage type conversions are running as fast as they should.) The sparse storage structures will be designed with fast access in mind, rather than fast insertion.


# Background

Since my first data structures course, I have been fascinated with data structures that have been optimized for specific applications, and their accompanying algorithms. For the course's final project, I wrote a Huffman encoder/decoder, with an emphasis on minimizing both the runtime and output file size. As an independent project for on object oriented course, I wrote an STL-style container that efficiently stored key-value pairs where either value of the pair could act as the key. Last fall, I heard a short lecture from one of the members of Matlab's sparse matrix team, and I was immediately fascinated by the problems that were presented. I looked into the clever ways that sparse matrices were stored and accessed, as well as some of the efficient algorithms that Matlab uses on sparse matrices.


I have an undergraduate degree in mathematics, including two semesters of linear algebra and two semesters of differential equations. I have taken a data structures course and two systems programming courses, which have given me insight into implementing data structures for both space and time efficiency. For this project, I have identified several helpful algorithms books (three of which are in my office right now).


# Schedule

I plan on devoting at least 40 hours a week over the summer to this project. For projects that I am intellectually invested in, this often means that I spend my free time also researching and trying to improve my work.


Community bonding period: 
I have several large goals during the bonding period. The first goal, obviously, is to interact with my mentor and the rest of SymPy's community. The next goal is to become comfortable with using github for version control. I have played around with git on my own, but I haven't used it in a multi-user setting before. The last, and most important, goal, is to familiarize myself with python. I am quite comfortable with C, C++, and Java. My first courses in both C and Java 'required' prerequisites that I didn't have, and I had no trouble catching up with the mechanics of either language. From the past two weeks of reading and poking around in SymPy's codebase, I am confident that I can learn python's syntax and coding style within the bonding period.

Weeks 1 and 2:
Rewrite matrices to use polys ground types and abstract the matrix interface to lay groundwork for sparse implementations.
This includes abstracting matrix functions so that users don't have to worry about the matrix storage type. Implement a block constructor(bug #342) and collapse rref and solve_linear_system into one(bug #1850).

Week 3:
Implement a sparse matrix data structure (compressed sparse row, to start with) and provide functions for users to convert between matrix types. Users would call m.toCSR() or m.toDense() and the appropriate conversion will be chosen. Calling toDense() on a matrix that was already dense would do nothing. At the end of this week, all that a sparse matrix would do is reduce storage size. All matrices, dense or sparse, would call the functions for dense matrices.

Weeks 4 and 5:
Begin writing more efficient algorithms for sparse matrices. Start with simple operations, like addition, multiplication, transposition, and conjugate transposition. Set up a testbed to compare sparse algorithm runtimes with dense versions.  
Choosing and writing these algorithms will take some trial and error, as there is very little literature on approaches for specifically symbolic sparse matrices.
Also, note that once the transposition of a CSR matrix is implemented, we have a compressed sparse column(CSC) implementation.  
Multiplying a sparse matrix by a vector is a particularly useful function - its algorithm should run in O(n) time (for n elements in the matrix), because we're not concerned with any 0s. Likewise, matrix-matrix multiplication should speed up because we can ignore a significant amount of 0s.

Week 6:
Add another sparse data structure - list of lists(LIL). Write conversion functions between matrix storage types. Start to implement Cholesky factorization, which will give solutions to symmetric linear systems. This includes a preordering algorithm to preserve sparsity, and analysis. I want to use an LDL^T factorization rather than LL^T factorization to avoid taking square roots of expressions.

Midterm Goals: Abstracted matrix interface, several storage types(dense, CSC, CSR, LIL), simple matrix operations, conversion functions, testbed.

Week 7:
Continue implementing and testing an efficient Cholesky factorization algorithm.

Weeks 8 and 9:
Implement pivoting LU decomposition for solutions to more general linear systems than Cholesky factorization allows for. This 

Week 10-12: Implement QR factorization, research and implement sparse matrix algorithms for eigenvalue and eigenvector solutions. Implement any remaining simple functions and write documentation for matrix interface.


## Reference books:
Direct Methods for Sparse Matrices: Duff, Erisman and Reid  
Direct Methods for Sparse Linear Systems: Davis  
Sparse Matrix Technology: Pissanetsky  
Direct Methods for Sparse Matrices: Østerby and Zlatev  