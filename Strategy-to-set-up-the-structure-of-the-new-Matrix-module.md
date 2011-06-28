This would be my strategy to set up the structure of the new Matrix module.

1. [New code] Add code that I have written to SparseMatrix.


2. [Removing code duplication] Observe which functions can be used by both Matrix and SparseMatrix and put them in a super Matrix class, call it _Matrix for now. _Matrix will derive from object. Remove those functions from Matrix and SparseMatrix(if they're there).


3. [SparseMatrix and Matrix derive from a common super class _Matrix]Make SparseMatrix derive from _Matrix rather than Matrix. This will make a lot of tests fail probably. Fix those tests. If that test was written for a SparseMatrix object using a dense algorithm, then that test is not good, and should be removed. User should use the dense matrix for dense algorithms. If a test is for a functionality that dense matrix shares, then that function could be put in the super _Matrix class. _Matrix class can be thought of as a collection of functions that do not depend on the representation of the matrix. It can also define some interfaces that a a subclass should have.


4. [Structuring] Put the three classes in separate files, and also split the test file. Change imports accordingly.


5.a. [Renaming] Rename Matrix to DenseMatrix, _Matrix to Matrix, SparseMatrix to DOKMatrix. This might break tests all over sympy, but solution is most likely to be trivial. Fix those tests.
5.b. Because of the renaming Matrix(...) constructor won't work. A small getaway as of now would be to write a __new__method which will divert the construction to the DenseMatrix constructor. (This will be changed later.)


6. [More tests] Now that SparseMatrix is a respected working separate class in its own right, write tests for old and new functionality.

> At this point, We have DOKMatrix(Matrix), DenseMatrix(Matrix), and Matrix(object) in three separate files, with tests written in separate files for each. Matrix(...) is working and returns a DenseMatrix object. isinstance(A, Matrix) also works. Only after this is complete, I will add another file lilmatrix.py which will have the LILMatrix class deriving from Matrix.

7. [LILMatrix] Add LILMatrix code that I have written. Write tests for it.

8. [Misc] Write miscellaneous functions and ensure all operations can be done on both the sparse matrices even if that algorithm has not been written.

( Note: One major example is that LILMatrix does not support an efficient matrix multiplication algorithm, If a user calls LILmatrix * LILmatrix, both the matrices will be converted to a DOKMatrix and then multiplied and then return the product DOKMatrix. Note that LILMatrix * LILMatrix --> DOKMatrix. But I don't think that is a problem since even if the user assumes the product to be a LILMatrix and carries out an operation of LILMatrix, if the DOKMatrix does not have that operation, then it will be converted back to LILMatrix and that operation performed. In short, Matrix interconversions would be implicit. Of course, the user will also be given explicit conversion functions like .to_dokmatrix.)

> At this point three matrix representations will be have been implemented along with tests.

9. [Domainifying] Add the `domain` kwarg to relevant constructors and functions. Write some more tests to check for matrix functionality over some domains from polys like QQ, FF(q), etc. Write some random matrix generator function over such domains. A small experiment I did indicated that this is reasonably easy, but generates some random bugs. Fixing bugs depends on changing Polys code and for this reason might be slow.

10.[Putting it all together] Write the Matrix constructor, which will take into account 1. the domain specified and 2. the sparsity of the data passed to it. If the domain is not explicitly specified, I would use construct_domain to set the domain. The user can also explicitly state that he wants his matrix to have no domain i.e. domain=object. If the given data is sparse enough, the data will be passed to one of the sparse matrices.

11+. Uncharted.

Many of these steps can also be carried out in parallel, but those that cannot reply on the completion of the previous steps. I will need the help of the community here to review each step and tell me when according to them, a step has been 'completed', so that I can confidently move to the next step. Lack of this is causing me to be in a slight state of confusion regarding what should I work on next.

Things have also been a little slow lately due to the above problem and also due to my lack of experience with git. I have never contributed to open source before, and have no expertise in handling large collection of commits. I'm learning fast though with the help of Vinzent.

I hope to get much of this done by mid-term evaluation. But I think (I'm not sure, though) all these steps 1 - 10 will take some 10 - 15 days more than 15th july.

Suggestions are most welcome.