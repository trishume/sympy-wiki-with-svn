# Linear Algebra Module

## Introduction

The SymPy linear algebra module is an easy-to-learn, functional library for matrix manipulation. The module includes the ability to use symbolic variables.

For a more general tutorial remember to read the general.

## Creating Matrices

The linear algebra module is designed to be as simple as possible. First, we import and declare our first Matrix object:

    >>> from sympy import *
    >>> from sympy.matrices import Matrix
    >>> Matrix([ [1,0], [0,1] ])


This is the standard manner one creates a matrix, i.e. with a list of appropriately-sizes lists. !SymPy also supports more advanced methods of matrix creation including a single list of values and dimension inputs:

    >>> Matrix(2, 3, [1, 2, 3, 4, 5, 6])


More interestingly (and usefully), we can use a 2-variable function (or lambda) to make one. Here we create an indicator function which is 1 on the diagonal and then use it to make the identity matrix:


    >>> def f(i,j):
    ...     if i == j:
    ...             return 1
    ...     else:
    ...             return 0
    ...
    >>> Matrix(4, 4, f)

Finally let's use lambda to create a 1-line matrix with 1's in the even permutation entries:

    >>> Matrix(3, 4, lambda i,j: 1 - (i+j) % 2)
    [1, 0, 1, 0]
    [0, 1, 0, 1]
    [1, 0, 1, 0]

There are also a couple of special constructors for quick matrix construction - `eye` is the identity matrix, `zeros` matrix functions, `ones`, and `diag`:

    >>> eye(4)
    [1, 0, 0, 0]
    [0, 1, 0, 0]
    [0, 0, 1, 0]
    [0, 0, 0, 1]
    
    >>> zeros(2)
    [0, 0]
    [0, 0]

    >>> zeros([2,5])
    [0, 0, 0, 0, 0]
    [0, 0, 0, 0, 0]

    >>> ones(2)
    [1, 1]
    [1, 1]

    >>> diag(1, 4*ones(2), 3)
    [1, 0, 0, 0]
    [0, 4, 4, 0]
    [0, 4, 4, 0]
    [0, 0, 0, 3]


# Basic Manipulation

While learning to work with matrices, let's choose one where the entries are readily identifiable. One useful thing to know is that while matrices are 2-dimensional, the storage is not and so it is allowable - though one should be careful - to access the entries as if they were a 1-d list.

    >>> M = Matrix(2, 3, [1, 2, 3, 4, 5, 6])
    >>> M[4]
    5
    >>> M
    [1, 2, 3]
    [4, 5, 6]


Now, the more standard entry access is a pair of indices:

    >>> M[1,2]
    6
    >>> M[0,0]
    1
    >>> M[1,1]
    5

Since this is Python we're also able to slice submatrices:

    >>> M[0:2,0:2]
    [1, 2]
    [4, 5]
    
    >>> M[1:2,2:2]
    []

    >>> M[:,2]
    [3]
    [6]

Remember in the 2nd example above that slicing 2:2 gives an empty range and that, as in python, a 4 column list is indexed from 0 to 3. In particular, this mean a quick way to create a copy of the matrix is:

    >>> M2 = M[:,:]
    >>> M2[0,0] = 100
    >>> M
    [1, 2, 3]
    [4, 5, 6]

See? Changing M2 didn't change M. Since we can slice, we can also assign entries:

    >>> M = Matrix(([1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]))
    >>> M
    [ 1,  2,  3,  4]
    [ 5,  6,  7,  8]
    [ 9, 10, 11, 12]
    [13, 14, 15, 16]
    >>> M[2,2] = M[0,3] = 0
    >>> M
    [ 1,  2,  3,  0]
    [ 5,  6,  7,  8]
    [ 9, 10,  0, 12]
    [13, 14, 15, 16]

    as well as assign slices:

    >>> M = Matrix(([1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]))
    >>> M[2:,2:] = Matrix(2,2,lambda i,j: 0)
    >>> M
    [ 1,  2, 3, 4]
    [ 5,  6, 7, 8]
    [ 9, 10, 0, 0]
    [13, 14, 0, 0]

All the standard arithmetic operations are supported:

    >>> M = Matrix(([1,2,3],[4,5,6],[7,8,9]))
    >>> M - M
    [0, 0, 0]
    [0, 0, 0]
    [0, 0, 0]
    
    >>> M + M
    [ 2,  4,  6]
    [ 8, 10, 12]
    [14, 16, 18]

    >>> M * M
    [ 30,  36,  42]
    [ 66,  81,  96]
    [102, 126, 150]

    >>> M2 = Matrix(3,1,[1,5,0])
    >>> M*M2
    [11]
    [29]
    [47]

    >>> M**2
    [ 30,  36,  42]
    [ 66,  81,  96]
    [102, 126, 150]

    As well as some useful vector operations:

    >>> M.row_del(0)
    >>> M
    [4, 5, 6]
    [7, 8, 9]

    >>> M.col_del(1)
    >>> M
    [4, 6]
    [7, 9]

    >>> v1 = Matrix([1,2,3])
    >>> v2 = Matrix([4,5,6])
    >>> v3 = v1.cross(v2)
    >>> v1.dot(v2)
    32
    >>> v2.dot(v3)
    0
    >>> v1.dot(v3)
    0

Recall that the `row_del()` and `col_del()` operations don't return a value - they simply change the matrix object. We can also *glue* together matrices of the appropriate size:

    >>> M1 = eye(3)
    >>> M2 = zeros(3)
    >>> M1.row_join(M2)
    [1, 0, 0, 0, 0, 0]
    [0, 1, 0, 0, 0, 0]
    [0, 0, 1, 0, 0, 0]


    >>> M1.col_join(M2)
    [1, 0, 0]
    [0, 1, 0]
    [0, 0, 1]
    [0, 0, 0]
    [0, 0, 0]
    [0, 0, 0]

## Operations on entries

We are not restricted to having multiplication between two matrices:

    >>> M = eye(3)
    >>> M*2
    [2, 0, 0]
    [0, 2, 0]
    [0, 0, 2]
    >>> 3*M
    [3, 0, 0]
    [0, 3, 0]
    [0, 0, 3]

but we can also apply functions to our matrix entries using applyfunc(). Here we'll declare a function that double any input number. Then we apply it to the 3x3 identity matrix:

    >>> f = lambda x: 2*x
    >>> eye(3).applyfunc(f)
    [2, 0, 0]
    [0, 2, 0]
    [0, 0, 2]

One more useful matrix-wide entry application function is the substitution function. Let's declare a matrix with symbolic entries then substitute a value. Remember we can substitute anything - even another symbol!:

    >>> x = Symbol('x')
    >>> M = eye(3) * x
    >>> M
    [x, 0, 0]
    [0, x, 0]
    [0, 0, x]

    >>> M.subs(x, 4)
    [4, 0, 0]
    [0, 4, 0]
    [0, 0, 4]

    >>> y = Symbol('y')
    >>> M.subs(x, y)
    [y, 0, 0]
    [0, y, 0]
    [0, 0, y]

## Linear algebra

Now that we have the basics out of the way, let's see what we can do with the actual matrices. Of course the first things that come to mind are the basics like the determinant:

    >>> M = Matrix(( [1, 2, 3], [3, 6, 2], [2, 0, 1] ))
    >>> M.det()
    -28
    >>> M2 = eye(3)
    >>> M2.det()
    1
    >>> M3 = Matrix(( [1, 0, 0], [1, 0, 0], [1, 0, 0] ))
    >>> M3.det()
    0

and the inverse. In SymPy the inverse is computed by Gaussian elimination by default but we can specify it be done by LU decomposition as well:

    >>> M2.inv()
    [1, 0, 0]
    [0, 1, 0]
    [0, 0, 1]

    >>> M2.inv("LU")
    [1, 0, 0]
    [0, 1, 0]
    [0, 0, 1]

    >>> M.inv("LU")
    [-3/14, 1/14,  1/2]
    [-1/28, 5/28, -1/4]
    [  3/7, -1/7,    0]

    >>> M * M.inv("LU")
    [1, 0, 0]
    [0, 1, 0]
    [0, 0, 1]

We can perform a QR factorization which is handy for solving systems:

    >>> A = Matrix([ [1,1,1],[1,1,3],[2,3,4] ])
    >>> Q, R = A.QRdecomposition()
    >>> Q
    [6**(1/2)/6, -3**(1/2)/3, -2**(1/2)/2]
    [6**(1/2)/6, -3**(1/2)/3,  2**(1/2)/2]
    [6**(1/2)/3,  3**(1/2)/3,           0]

    >>> Q*R
    [1, 1, 1]
    [1, 1, 3]
    [2, 3, 4]


In addition to the solvers in the solver.py file, we can solve the system Ax=b by passing the b vector to the matrix A's LUsolve function. Here we'll cheat a little choose A and x then multiply to get b. Then we can solve for x and check that it's correct:

    >>> A = Matrix([ [2, 3, 5], [3, 6, 2], [8, 3, 6] ])
    >>> x = Matrix(3,1,[3,7,5])
    >>> b = A*x
    >>> soln = A.LUsolve(b)
    >>> soln
    [3]
    [7]
    [5]

There's also a nice Gram-Schmidt orthogonalizer which will take a set of vectors and orthogonalize then with respect to another another. There is an optional argument which specifies whether or not the output should also be normalized, it defaults to False. Let's take some vectors and orthogonalize them - one normalized and one not:

    >>> L = [Matrix((2,3,5)), Matrix((3,6,2)), Matrix((8,3,6))]
    >>> out1 = GramSchmidt(L)
    >>> out2 = GramSchmidt(L, True)

Let's take a look at the vectors:

    >>> for i in out1:
    ...     print i
    ...
    [2]
    [3]
    [5]
    [ 23/19]
    [ 63/19]
    [-47/19]
    [ 1692/353]
    [-1551/706]
    [ -423/706]
    >>> for i in out2:
    ...      print i
    ...
    [2*(1/38)**(1/2)]
    [3*(1/38)**(1/2)]
    [5*(1/38)**(1/2)]
    [(23/19)*19**(1/2)*(1/353)**(1/2)]
    [(63/19)*19**(1/2)*(1/353)**(1/2)]
    [ -47/19*19**(1/2)*(1/353)**(1/2)]
    [(12/353)*706**(1/2)]
    [ -11/706*706**(1/2)]
    [  -3/706*706**(1/2)]

We can spot-check their orthogonality with `dot()` and their orthogonality with `norm()`:

    >>> out1[0].dot(out1[1])
    0
    >>> out1[0].dot(out1[2])
    0
    >>> out1[1].dot(out1[2])
    0
    >>> out2[0].norm()
    1
    >>> out2[1].norm()
    1
    >>> out2[2].norm()
    1

So there is quite a bit that can be done with the module including eigenvalues, eigenvectors, nullspace calculation, cofactor expansion tools, and so on. From here one might want to look over the matrices.py file for all functionality.


## A Sample Workspace

Ignoring that fact that there is an eigenvalue function, let's consider the task of taking a matrix and calculating a set of orthonormal vectors for it's eigenspace. For more info take a look at [http://en.wikipedia.org/wiki/Eigenvalue this page]. We'll first declare the matrix then use charpoly to get it's characteristic polynomial. Because we're working with polynomials we'll need the symbol module:

    >>> from sympy import Symbol
    >>> from sympy.matrices import *
    >>> x = Symbol('x')
    >>> M = Matrix(( (5,0,2), (3,2,0), (0,0,1) ))
    >>> f = M.charpoly(x)
    >>> f
    (1 - x)*(2 - x)*(5 - x)

Now we can use the handy solver from the polynomial module to get our roots:

    >>> from sympy.polynomials import roots
    >>> r = roots(f, x)
    >>> r
    [1, 2, 5]

Now that we have our eigenvalues we need the eigenvectors. What we need to do is find the basis vectors for the nullspace of the system

    (A - kI) x = 0,

where the k's are the eigenvalues. Luckily we have a handy nullspace function and we'll make use of that.

    >>> M = Matrix(( (5,0,2), (3,2,0), (0,0,1) ))
    >>> r = [1,2,5]
    >>> vlist = []
    >>> for vals in r:
    ...     nlsp = (M-vals*eye(3)).nullspace()
    ...     for vect in nlsp:
    ...             vlist.append(vect)
    ...
    >>> for i in vlist:
    ...     print i.T
    ...
    [-1/2, 3/2, 1]
    [0, 1, 0]
    [1, 1, 0]

The last print we used the transpose operation for readability. So we're almost there, now we just call the GramSchmidt procedure to orthogonalize:

    >>> normal = GramSchmidt(vlist, True)
    >>> for i in normal:
    ...     print i.T
    ...
    [-14**(1/2)/14, 3*14**(1/2)/14, 14**(1/2)/7]
    [3*70**(1/2)/70, 70**(1/2)/14, -3*70**(1/2)/35]
    [2*5**(1/2)/5, 0, 5**(1/2)/5]

And that's it. At this point, one should continue to experiment with the module: read the matrices.py file, try and interact with the other modules such as solvers.py and polynomials.

## Working with *in progress* software

Even though SymPy has some really great functionality, one should always keep in mind that !SymPy is a work in progress and so, while the code you wrote may be correct, it may not always do what you have in mind.

Let's take an example. Now, at any time this may no longer be a problem but for now let's play with the [http://en.wikipedia.org/wiki/Vandermonde_matrix Vandermonde Matrix]. First, let's use our Matrix to find the determinant

    >>> x, y, z = symbols("xyz")
    >>> V = Matrix( [ [1, x, x**2], [1, y, y**2], [1, z, z**2] ] )
    >>> V
    [1, x, x**2]
    [1, y, y**2]
    [1, z, z**2]

    >>> V.det()
    x*y**2 + y*z**2 + z*x**2 - x*z**2 - y*x**2 - z*y**2

Clearly, this is not the canonical form we're looking for. We're really trying to find:

    >>> L = [x, y, z]
    >>> det = 1
    >>> for i in range(len(L)): det *= L[i] - L[i-1]
    ...
    >>> det
    (x - z)*(y - x)*(z - y)

But notice that if we use the expression expansion function, we can see that they are equal:

    >>> det.expand()
    x*z**2 + y*x**2 + z*y**2 - x*y**2 - y*z**2 - z*x**2

So what is the message? This is your opportunity to contribute. When you come across an inconsistency, see if you can figure out what kind of bug it is. Then help us out by posting an issues on the  [issues list](http://code.google.com/p/sympy/issues/list "issues list").