

# Introduction

This page is intended for sketches and design ideas related to the code generation features of Sympy which I (Øyvind) will improve during the GSOC 2010 project http://socghop.appspot.com/gsoc/student_project/show/google/gsoc2010/python/t127230762991 .  

Everyone should feel free to add comments, suggestions and corrections.

I am thinking aloud here, so don't expect everything to be 100% clever.  On the contrary, expect that anything I write on this page can be substantially revised in the future, as my understanding evolves.  I will use this page as a working document and try to keep it up to date both with my current understanding of the issues and the actual implementation, so that in the end of the summer I can convert this page into documentation of the implemented code.  

# Details

## Examples

A simple example of the functionality is a low-level implementation of a matrix vector product.  We may express the matrix-vector product as

```
y(i) = M(i,j)*x(j)                (implicit sum over repeated indices)
```

The corresponding code should include the following loop:

```
y = 0
do i=1, dim_1
  do j = 1, dim_2
    y(i) = y(i) + M(i, j)*x(j)
  end do
end do
```

Here, dim_1 and dim_2 should be input arguments that must be supplied to the routine at runtime along with the arrays y, M and x.   The integers i,j are local variables.

## Math interpretation step

Before the code can be generated, it is necessary to have a clear idea of what the symbolic relation is supposed to express.  The math expression that implement a mathematical statement in code may not correspond directly with the hand written form, as exemplified by the matrix vector loop above.  Each element y(i) is calculated as a sum over j where the terms are added one at a time.   In order to implement the loop as above, `y(i)` must be added to the right hand side expression, `M(i,j)*x(j)` in an "interpretation step".

I am unsure whether the interpretation step should be implemented in the Printers or in the codegen utility:  The modification of right hand side must go hand in hand with proper initialization of the result vector.  What is the correct initialization depends on whether it is identified as an InOutArgument or an OutputArgument, and currently this information is only available in codegen.  On the other hand, what the Printers are doing is of course interpreting math to code, so it would also naturally belong there.

Alternatively, the loop can be implemented in a slightly different way:
```
do i=1, dim_1
  temp = 0
  do j = 1, dim_2
    temp = temp + M(i, j)*x(j)
  end do
  y(i) = temp
end do
```

This has an advantage of simplicity and it does not require initialization of y, so it would no doubt belong in the Printers.  The disadvantage is that the loops must be ordered such that all left hand side indices are in the outer loops, and this may hinder loop optimizations.  For instance, the above loop is optimized for C where arrays are column-first, but cannot easily be optimized for Fortran row-first arrays.  That would require reordering indices of the array.


## Code generation step

Fortran and C code printers will be used

Scalar arguments are already implemented, but we need a mechanism to handle array arguments.  This is my current focus, and here is a tentative plan along with thoughts about some decisions that must be made:

  * In order to handle large arrays, it is necessary to pass arrays by reference.  This is always the case in Fortran, and in C this corresponds to passing a memory address to a pointer.  In this sense, array arguments are actually just scalar arguments, but in order to access the array correctly in the subroutine it is necessary to also communicate information about how the array is stored in memory, i.e. rank and dimensions.  (Let's call it 'array metadata')

  * Before the array metadata can be communicated to the subroutine, it must also be extracted from the mathematical expression.  This functionality could go into the code printers, the math objects themselves (by adding methods to Expr) or it could be determined by a standalone function in the codegen module.  My current conclusion is that since rank information of an object can be determined without knowing the context, but dimensions need to be synchronized across an equation, 1) Expr should get a property .array_rank, 2)  a standalone function should determine dimensions.  Aaron suggested using assumptions to store array metadata.  

*Update:* I created Indexed and Idx classes, inspired from GiNaC, and they work very well for generating the loops.  I now think this is the way to go, so that in order to generate code with arrays, you will need to use Indexed objects from the point of setting up and manipulating the equations.  However, the Indexed and Idx classes are lightweight and general, so they can easily be subclassed for different applications.  I still like the idea of using assumptions on Symbols because it is an elegant user interface.  When the Idx based approach stabilizes, an assumption based approach can be implemented simply as a call to a conversion function.  Codegen can be set up to always call convert_assumed_shape_to_Idx(expr) before processing.

  * A standalone function to determine dimensions must be able to synchronize the dimensions of the objects in the expression.  E.g. for a matrix A and vectors x and b it must be able to determine and distribute dimensions m,n, such that an equation b=Ax would result in code with arrays declared something like A <=> a(m,n), x <=> x(n) and b <=> b(m)

  * I am considering whether array indices should be represented as objects of an 'Index' class ~~that inherits from Symbol~~.  Each Index instance would keep track of its own range, so that it carries the information needed to construct a loop over its full range.  The function that determines dimensions should insert Index objects into the expression before it is handed over to the Code generators.

  * The codegen utility implements a class 'Argument' with a subclass 'InputArgument'.  It is meant for scalar arguments, and I am not sure if I should put the array arguments in a subclass on its own, or simply extend InputArgument to handle arrays as well.

  * I need to to implement corresponding classes for 'OutputArgument' and 'InOutArgument', so that we can have more than one return object.  This will be needed for instance to return both eigenvectors and eigenvalues in one call.

  * We should have a way to to optimize loops over arrays.  Since Fortran and C  store arrays row-wise and column-wise, respectively, the loop order must be determined in the sub-classes of CodeGen.

### More about the Index class

Motivation:

In the process of code generation, the symbolic math expressions need to be converted to a numerical expression. The problem must be discretized, dimensions must be specified and the problem formulation looses some generality.  I want to keep the expression as general as possible as long as possible.  In particular, I want to decide dimensions of arrays after the binary has been compiled, and pass them as arguments when calling the subroutine.  This is the reason I believe I need an Index class.  I think this would be similar to the Idx class in GiNaC.

Implementation:

The Index instances will store a label as well as upper and lower bounds of its range.  The upper and lower bounds will typically be Symbol objects, and the code generator must detect them and add them to the list of input arguments.  

Index objects are not atomic since they contain other symbols, so it would not make sense to inherit from Symbol.

## Code compilation step

The plan is to have a ~~singleton~~ compiler object that encapsulates system resources such as compilers and libraries (blas, lapack etc.) and creates compiled binaries with python bindings.  

Luckily, we don't need to start from scratch, some options are

### compilers
   1. CCompiler from distutils
   1. scipy_distutils is extended to handle fortran compilation (used by f2py)
   1. fwrap has compilation functionality (also based on scipy_distutils?) 

### python bindings
   1. Cython can create python bindings to C
   1. fwrap can create python bindings to Fortran
   1. swig can be used to make python bindings to C
   1. f2py can be used to make python bindings to Fortran