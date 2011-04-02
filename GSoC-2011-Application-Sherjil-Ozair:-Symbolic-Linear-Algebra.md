EDIT : The latest updated application can be found in the google-melange page. Click [here](http://www.google-melange.com/gsoc/proposal/review/google/gsoc2011/sherjilozair/1).

Title : Symbolic Linear Algebra

Abstract 
SymPy is an open-source Python library for symbolic mathematics. Its current Linear Algebra module is criticized as being slow, and also does not have an efficient sparse matrix implementation. My proposal is to write an efficient sparse matrix implementation and to re-write the current Matrix class to add support for multi-precision ints using GMPY.

Name and Contact Info

Sherjil Ozair

Email: sherjilozair@gmail.com

Institute : Indian Institute of Technology Delhi

IRC: sherjilozair on freenode

Phone: +91 9811939858

 

Benefits to Community

SymPy's Linear Algebra module is used by many other parts of SymPy like quantum mechanics, integration, etc. So it is critically important that the module is highly-efficient. Very sparse systems of hundreds of equations need to be solved, and the current dense implementation fails to do so. 

Linear Algebra is a very important subject particularly useful in computation, physics, data compression, algebraic coding, not to mention elementary algebra itself. A complete linear algebra module would take SymPy to the direction of a complete open source CAS.

>>> A = SMatrix(100,100,lambda i,j : 1 * isprime( i+2*j ) )

>>> A.nonzero_col(2)

[(1,2,1),(3,2,1),(7,2,1),(9,2,1), ...... ]

>>> B = SMatrix(10,10, [(4,4,7 + x),(7,7,9*I),(9,4,2)])

>>> B.nonzero_diag(0)

[(4,4,7+x), (7,7,9*I)]

>>> C = DiagonalMatrix([x**2,16*I,0,0,14,y+x])

>>> C.nonzero_row(1)

[(1,1,x**2)]

>>> D = PermutationMatrix([1,4,2,5,3])

>>> D

[1, 0, 0, 0, 0]

[0, 0, 0, 1, 0]

[0, 1, 0, 0, 0]

[0, 0, 0, 0, 1]

[0, 0, 1, 0, 0]

 

Deliverables

1. Complete Sparse Matrix implementation consisting of a sparse storage scheme and essential algorithms.

I will use the Dictionary of Keys scheme, along with a row-sorted and a column sorted list of keys. According to me, this is a reasonable data structure for sparse symbolic matrices. The two lists will be helpful to write efficient iterators and for multiplication. Whether to maintain a list or to calculate when needed will depend on benchmarking tests.

My data structure is effectively a combination of DOK and COO.

Matrix constructors
Addition, Multiplication
Elementary row/column operations 
Solving Ax=B using Gaussian Elimination, for square matrix [0]
Method of least squares, for non-square matrix
Sub-matrices
Iterators
Editing matrices
Co-factors and minors and associated matrices
Determinant using Gaussian Elimination
Inverses
Eigenvectors and Eigenvalues
 

Note : The above algorithms are only trivial for a dense implement. Algorithms for a sparse data structure require some thoughts to remove complexity dependency on N.

It is to be noted that all the above components will have to coded from scratch. It won't be possible to re-use code from the dense implementation as the data structure is very different.

 

2. GMPY integration

 

3. Special Types of Sparse Matrices like PermutationMatrix, DiagonalMatrix, etc.

 

Description (by timeline)

April 25: Accepted student proposals announced

Community Bonding period

May 6: College major exams end.

May 23: Official 'Coding starts' day

July 15: Mid-term evaluation

July 25: College classes start

August 15 : Suggested Pencils down

August 22 : Firm Pencils down

August 26: Final Evaluation

 

My college summer schedule starts early but ends early too.

It starts 17 days before Google's Official 'coding starts' day.

Summer ends 20 days before the suggested pencils down day

I'll have a head start of 20 days before the dates in the Google timeline.

I plan to start coding after my college exams end on May 6. That will give me 10 weeks before mid-term evaluation.

I intend to finish my project by mid-term evaluation. I leave the time after evaluation for review and documentation. 

Tests and profiling will be carried out while coding.

 

Here is a tentative week-by-week timeline. 

Week 1 : Matrix constructors, addition, multiplication, transpose

Week 2 : Editing matrices, iterators, element access and editing, slicing, sub-matrices

Week 3 : Co-factors, Minors, Co-factor matrix, Adjoint/Inverse using adjoint, Eigenvector and Eigenvalues

Week 4, 5, 6 : Elementary Row/Column operations, Gaussian Elimination, Solving Ax=B using Gaussian Elimination, Method of Least Squares, Determinant using Gaussian Elimination

Week 7 : Miscellaneous functions like the is_something functions, and other such trivial functions. Personal Code Review.

By the end of 7th week, I will have a working and tested efficient Sparse Matrix implementation.

Week 8, 9 : Re-writing the Matrix class. Freeze function to solve mutability/immutability problem. GMPY integration for DenseMatrix and SparseMatrix. Writing special types of sparse matrix classes like DiagonalMatrix, PermutationMatrix, etc.,

 

 

Biographical Information

I'm a first year undergraduate student pursuing Bachelors in Technology in the Indian Institute of Technology Delhi, in the department of Computer Science and Engineering. 

Relevant course I have taken are:

◆CSL201 : Data Structure and Algorithms

◆MAL124 : Introduction to Abstract Algebra and Matrix Analysis

In a previous course, CSL102, I had designed RSA encryption for 64-bit ints in python.

As an assignment for CSL201, I had successfully designed and implemented Sparse Matrix multiplication algorithm in java, with time complexity O( L1 * L2 )

 

References

[0] www.eecis.udel.edu/~saunders/papers/sffge/it5.ps 