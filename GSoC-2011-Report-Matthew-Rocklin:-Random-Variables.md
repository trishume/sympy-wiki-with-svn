## About Me

My name is Matthew Rocklin. I'm a 4th year PhD student in computer science at the University of Chicago. My research is in numerical methods in applied problems, particularly efficient evolution of probability distributions in dynamical systems. 

## Introduction

The goal of this project was to enable statistical computations in SymPy by introducing a Random Variable type. This can be further split into a general framework for Random Expressions, and three implementations:

* Finite/Discrete Random Variables
* Continuous Univariate Random Variables
* Multivariate Normal Random Variables

Queries on expressions of these three types of random variables yield an expression in a different part of SymPy. 

* Finite RVs depend on SymPy Sets and Generators
* Continuous RVs depend on SymPy Integrals
* Multivariate Normal RVs depend on SymPy Matrix Expressions

The first and third of these required further contributions from this project. The second was fortunately being augmented by another GSoC student during the same Summer. 

## Main Work

### Random Variable Interface

A SymPy Expr may contain a RandomSymbol (class). A RandomSymbol acts like a like a traditional SymPy Symbol (such as Symbol('x')) except that it is connected to a PSpace (short for ProbabilitySpace). 

A PSpace consists of a probability density function over a set of variables. An example is that PSpace p might dictate that the variable x is normally distributed with mean 0 and variance 1. The RandomSymbol X is the representative of x within SymPy expressions. There is a clear division between lower-case x, which is used to describe densities, probabilities, etc... and upper-case X which represents x in SymPy Expressions. This division allows all existing SymPy
mechanics (calculus, inference, etc...) to integrate cleanly with the random mechanics. 

After expressions are made and manipulated by SymPy the user can ask statisical questions using a few key functions 

* E(expression) # Expectation
* P(condition) # Probability that condition is True
* Density(expression) # Probability density of the expression
* Where(condition) # Domain where condition is True
* Given(expression, given_condition) # A new conditional Probability Space is created

These few operations can express most statistical queries. All three implementations (finite, continuous, multivariate normal) try to implement these operations as best as possible. 

### Finite Random Variables

Finite/Discrete Random Variables are used to describe events with distinct possibilities - the canonical example is the roll of several dice. To answer the above questions each possibility of the expression is considered. Finite Random Variables depend heavily on Python generator expressions and SymPy FiniteSets

Finite Random Variables support all operations listed above. They do not fail to produce an answer but, in the case of expressions involving many variables may take prohibitively long to supply an answer. 

### Continuous Random Variables

Continuous Random Variables describe events that can take on a continuum of values such as the expected amount of rainfall in the month of June. To answer these questions complex integrals are formed and hopefully solved. 

Continuous Random Variables support all operations listed above with some conditions. For example conditional probabilities may be computed but not in the case where different random variables are compared to each other i.e. P(X given X>Y**2), X,Y both normally distributed. Additionally the integration routine may fail to produce a result in which case the unevaluated integral is returned. 

### Multivariate Normal Random Variables

Multivariate Normals are common in statistics and applied research. Normality and linearity are common assumptions to make in a high-dimensional setting. Multivariate Normals produce expressions involving matrices which in turn describe other Multivariate Normals. 

Multivariate Normals are the most restrictive of the three implementations. They only support the Expectation, Density, and Given operations. They fail on any expression which is not linear in the RandomSymbols. Given these conditions though they always compute and compute quickly. MVN's simply expose the mathematics of the Kalman Filter. 

## Supplementary Work

### Sets

SymPy Sets now contain a FiniteSet class which mimics the Python set and support cartesian products of sets. This, combined with the previous work describing Intervals and Unions makes describing complex sets in Rn very intuitive. 

### Matrix Expressions

Matrices in SymPy are currently only represented explicitly. Matrix Expressions allow for the representation of Expr's containing matrices, their inverses, and transposes. MatrixExpr classes pass basic flattening rules onto the traditional Expr classes but add rules for Matrix Identies and Zeros. Additionally, for the Multivariate Normal RVs block matrices were formed. 

## Status of Current Work

Matrix Expressions are in. 

The Random Variables branch is waiting for Tom Bachmann's integration code to enter SymPy before a pull is submitted. 

The Multivariate Normal branch depends on the previous two and is also not yet a pull. 

Sets and various smaller bug-fix branches have been merged into SymPy master. 

There are a few miscellaneous errors or errata that are present in issues. 

## Conclusion and Future Work

We now have a Random Variable type that integrates smoothly with the rest of SymPy. It is capable of reproducing a number of results in statistics. On the simple side it can computing general means and variances of well known expressions, the sort of which are found in elementary statistics books. As a case study it was used in [this blogpost](http://sympystats.wordpress.com/2011/07/02/a-lesson-in-data-assimilation-using-sympy/) to illustrate univariate data assimilation. Additionally the Multivariate Normals are capable of reproducing the Kalman Filter, a fundamental and well used result, as shown in [this blogpost](http://sympystats.wordpress.com/2011/07/19/multivariate-normal-random-variables/). 