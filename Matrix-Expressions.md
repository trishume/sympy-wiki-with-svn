# Introduction 

Matrices can be expressed in two ways using SymPy. They can be expressed explicitly as Matrix objects or they can be expressed as SymPy Symbols. The first is matrix specific but requires explicit representation. The second does not require explicit representation but is not specialized to matrices. 

This page discusses a possible Matrix Expression type in SymPy. 

# Uses

How are Matrix Expressions used mathematically? What should a SymPy implementation support?

How are Matrix Expressions used mathematically? 

* Representation of linear algebra programs / code generation
* Symbolic statistics
* _Add more here and below_

What should a SymPy implementation support?

* Matrix Symbol object
* ImmutableMatrix (explicitly represented Matrix which is also Basic)
* Mixture of the two objects above in the same expression
* Shape checking
* Matrix specific Functions (Transpose, Inverse, Determinant)
* Block Matrices

# Challenges

What is holding us back? What are some issues we should consider before moving forward?

* Subclassing Expr is hard
* Matrix Expressions will be used in a variety of ways. How can we assure our solution is sufficiently general?

# Next Steps

How do we continue from here? 

# Narratives

It was suggested that to address use cases we collect hypothetical narratives that contain desired features and reasons. 

## Symbolic Statistics
I'd like purely symbolic matrices so I can represent equations in statistics. I'm interested in both linear regression and Gaussian mixtures. For regressions I could probably get by with regular SymPy Symbols but for Gaussian mixtures I really need block matrices. 

## Code generation
All of my computation can be represented as applications and solves of (sparse) matrices. I'm using (numpy, theano, numexpr) now for fast computation but would like to represent my equations at a higher level first and only put data in afterwards. It would be nice to reason about my expressions so that I can choose different algorithms at runtime, i.e. "is this matrix positive semi-definite so I can use conjugate gradient?" I'd also really appreciate a way to subs numpy matrices into my expression and then dump down to a numerical level. Would it be possible to have SymPy organize the operations so that they're more efficient or should I take that work to one of the numerical linear algebra systems?

## Teaching/Printing
I teach linear algebra and love using SymPy. Printing linear algebra Expressions never works out well though. A**-1 comes out as 1/A and I find this frustrating. 