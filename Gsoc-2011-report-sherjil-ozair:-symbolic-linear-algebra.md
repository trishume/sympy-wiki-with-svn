About
=====
I'm Sherjil Ozair, studying Computer Science and Engineering at the Indian Institute of Technology. I enjoy programming and mathematics. A senior of mine, who recognized my passion for coding, suggested me I should apply for GSoC 2011. I looked through previous list of organizations, and SymPy caught my attention, dealing with algorithms and mathematics.

Overview
========
My project consisted of writing a new sparse symbolic matrix class for SymPy, consisting of sparse symbolic algorithms. SymPy had a pseudo-sparse implementation which used dense algorithms, and further mpmath had sparse matrix for numerics only.
A further part of my project was to make the coefficients of matrices belong to specific domains, which would ease the computation and increase SymPy's overall speed. This would allow Matrices over Integers, or Matrices over fields like the Galois Field. Such types of Matrices are particularly useful in some areas of Mathematics.
Finally, I had to merge the sparse matrices with the previous dense matrix implementation, so that the high level Matrix class would be seamless for the user to use.

The Project
==========

Sparse Matrix Data Structures and Algorithms
---
For sparse matrices, two implementations were needed. The List of List DS(LIL) and the Dictionary of Keys(DOK). Python's dictionary is quite fast, and I used that in the implementation of DOK. The DOK representation was superior when it comes to construction of matrix and element access. However, Iterating over elements was not supported natively. The Cholesky decomposition and its variant LDL decomposition was implemented in DOK since the algorithm assumed a set-structured matrix. The implementation worked neatly. But more natural algorithms like the Gaussian Elimination could not be implemented. As algorithms like the Gaussian elimination and Gauss-Jordan are row-structured, the row-based LIL representation supports a very fast implementation of GE. Thus with a combination of LIL and DOK, almost all the fundamental matrix operations, i.e. Inverse of a matrix, Solving Ax=B, determinant of a matrix, were implemented.

Matrix under domains and GMPY
----
Since SymPy is a symbolic library, it would be a useful asset to have matrices defined under various domains like integers, reals, fractions, polynomials, finite fields like Zp, expression fields. This was comparatively easy. SymPy matrices make use of a function, which all elements pass through to make it SymPy-recognizable. This function could be replaced by any other function, could also be provided by the user in the parameters.

Merging with dense matrices and a common API
------------------------------------------
TODO

Looking Back
==============================
TODO