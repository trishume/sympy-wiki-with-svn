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

SymPy's Linear Algebra module is used by many other parts of SymPy like quantum mechanics, integration, etc. So it is critically important that the module is highly-efficient. Very sparse systems of hundreds of equations need to be solved, and the current dense implementation fails to do so efficiently. 

Linear Algebra is a very important subject particularly useful in computation, physics, data compression, algebraic coding, not to mention elementary algebra itself. A complete linear algebra module would take SymPy to the direction of a complete open source CAS.

 

Deliverables

As yet, there are many ideas regarding what to do with the linear algebra module. It probably needs more work than any other module of SymPy, keeping in mind that it is a widely-used module. For sure, my project will change over the summer. Ideas will be discussed, added and deleted. There maybe be more than one students working in the Linear Algebra project, and we might have to share work. What I lay down here are basic essentials that I think the Linear Algebra module can't do without. It is essentially a project focussing on making ONE sparse storage scheme completely self-sufficient and 100% working with efficient sparse aglorithms.

I will list out a schedule, but it is only a very rough guideline. Linear Algebra has lots of work to be done in it, like code generation, matrix expressions, abstract matrices that I will look into when the current deliverables finish. These topics are better suited for the end of the summer as these require a very good familiarity with SymPy. I might also implement another sparse scheme, if need dictates.

 

1. Complete Sparse Matrix implementation consisting of a sparse storage scheme and essential algorithms.

I will use the Dictionary of Keys scheme, along with a row-sorted and a column sorted list of keys. According to me, this is a reasonable data structure for sparse symbolic matrices. The two lists will be helpful to write efficient iterators and for multiplication. Whether to maintain a list or to calculate when needed will depend on benchmarking tests.

My data structure is effectively a combination of DOK and COO.

Matrix constructors
Addition, Multiplication
Elementary row/column operations 
Gaussian Elimination [0]
Symbolic Cholesky Factorization [1] [2]
Method of least squares, for non-square matrix
Sub-matrices
Iterators
Editing matrices
Co-factors and minors and associated matrices
Determinant using Gaussian Elimination
Inverses
Eigenvectors and Eigenvalues
Diagonalization methods like exponentiation
 

Note : The above algorithms are only trivial for a dense implement. Algorithms for a sparse data structure require some thoughts to remove complexity dependency on N, the dimension of matrix.

It is to be noted that all the above components will have to coded from scratch. It won't be possible to re-use code from the dense implementation as the data structure is different.

I'm confident I will be able to think of algorithms by my own. I coded in the Cholesky Decomposition, a sizebale chunk of my project, and the corresponding solve algorithm. I implemented it for dense matrices, though essentially it is a very good symbolic sparse algorithm. To implement it in Sparse Matrices would require a better interface than the SMatrix class currently has. [3] 

2. GMPY integration

3. Special Types of Sparse Matrices

Matrices like PermutationMatrix, DiagonalMatrix, TriDiagonalMatrix etc. are often-use sparse matrices. I will research and implement these matrices as sub-classes of the sparse matrix class, with overrided more-efficient functions.

4. Ground-work for matrix expressions and code generation


Some Design Ideas

Sympy's motivation involves 'doing more writing less' and aims to implement algorithms with minimum number of lines possible. But the Linear Algebra module is a widely used module, and thus needs to be highly-optimized.

Some ideas related to the design principles I'll follow:

Dynamic Programming Or Why Calculate Twice When You Can Re-use
Oft-needed properties of a matrix, like the determinant, will be stored after computing once, for re-use. 
Why Store When You Can Compute:
Often, a Matrix is constructed using a function. If the matrix is very large, the class can store the function and not the individual elements, to save space.
Low - level and High - level Functions (idea borrowed from SciPy)
Some functions will be written twice, one safe/high-level function which contains error-checks and will be available to the user, and 
Another unsafe/low-level function which will be used internally by this module and possibly other parts of Sympy. This unsafe version will be fully-optimized, without error-checks.
The high-level function will perform error checks and then call the low-level function. There won't be any code-duplication.
Polymorphism
Classes like DenseMatrix, SparseMatrix, etc. will be implemented separately, but will be called by only one user-available class Matrix.
Similarly SparseMatrix class can return its subclasses, when the sparse matrix is analysed to be of any of the special types of sparse matrices.
 

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

 

My college summer schedule starts early but ends early too. It starts 17 days before Google's Official 'coding starts' day. Summer ends 20 days before the suggested pencils down day I'll have a head start of about 20 days before the dates in the Google timeline. I plan to start coding after my college exams end on May 6. That will give me 10 weeks before mid-term evaluation. I intend to finish most of my project by mid-term evaluation. Testing, profiling and benchmarking will be carried out side by side coding. 

Here is a tentative week-by-week timeline. 

Week 1 (9th May - 15th May)

Matrix data structure, Matrix constructors, addition, multiplication, transpose

Week 2 (16th May - 22nd May)

Matrix element handlers, slicing and submatrices (__setitem__ and __getitem__)

Iterators. #Needs to be discussed

Week 3 (23rd May - 29th May)

Co-factors, Minors, Co-factor matrix, Adjoint, Inverse.

Week 4 (30th May - 5th June)

Eigenvalues, Eigenvector, Diagonalization-based methods like exponentiation ( Matrix**Integer and Integer**Matrix )
Week 5 (6th June - 12th June)

Elementary Row/Column operations, Gaussian Elimination, Solving Ax=B using Gaussian Elimination, Method of Least Squares, Determinant using Gaussian Elimination.

Week 6 (13th June - 19th June)

Symbolic Cholesky Decomposition for sparse matrices. I've already coded in two versions of this pre-GSoC. But this variant is most efficient. Coding this would require a good set of iterators and some auxiliary functions.

Week 7 (20th June - 26th June)

Miscellaneous functions like the is_something functions, and other such trivial functions. Personal Code Review.

By the end of 7th week, I will have a working and tested efficient Sparse Matrix implementation.

Week 8 (27th June - 3rd July)

Freeze function to solve mutability/immutability problem. GMPY integration for DenseMatrix and SparseMatrix. 

Week 9 (4th July - 10th July)

Writing special types of sparse matrix classes like DiagonalMatrix, PermutationMatrix, etc., 

Week 10 (11th July - 17th July)

Final touches, reviewing. Buffer.

Mid-Term Evaluation (15th July)

Weeks 8th, 9th and 10th have been kept light so that any work left of the previous weeks can be completed now.

Week 11 and 12 (18th July - 31tst July)

Will add more functionalities that I come across later, through the mailing list or through my mentor.

Will lay ground-work for matrix expressions and code generation.

Week 13 (1st August - 7th august)

Documentation.

Work on matrix expressions and code generation will continue after GSoC, though I admit at a slower pace. More sparse representations can also be added after this GSoC or in the next GSoC. 

Do note that this is a tentative timeline. This schedule might change, subject to later discussions with my mentor and SymPy community.

I will be in touch with my mentors and with the community in a daily basis, and before first week will have a final schedule as to what needs to be done. I might also have to collaborate with another GSoC student, according to Andy. 

More than 40hours/week of work is assured. I have nothing planned for the summer except for a 3-4 day trip after mid-term evaluation.

 

Biographical Information

I'm a first year undergraduate student pursuing Bachelors in Technology in the Indian Institute of Technology Delhi, in the department of Computer Science and Engineering. 

Relevant course I have taken are:

◆ CSL201 : Data Structure and Algorithms

◆ MAL124 : Introduction to Abstract Algebra and Matrix Analysis

In a previous course, CSL102, I had implemented RSA encryption for 64-bit ints in python.

As an assignment for CSL201, I had designed and implemented COO Sparse Matrix multiplication algorithm in java, with time complexity O( L1 * L2 )

I work in Mac OSX architecture and have also experience in Linux/Ubuntu.

References

[0] www.eecis.udel.edu/~saunders/papers/sffge/it5.ps 

[1] http://en.wikipedia.org/wiki/Symbolic_Cholesky_decomposition

[2] http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.163.7506&rep=rep1&type=pdf

[3] https://github.com/sympy/sympy/pull/184