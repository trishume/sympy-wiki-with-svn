## About Me

My name is Tomo Lazovich. I just completed my undergraduate degree in Physics at Harvard University and am currently a 1st year in their PhD program. 

## Introduction

Before the start of this year's GSOC, SymPy had much functionality in place for working in discrete spin bases to do symbolic quantum mechanics. In fact, a whole symbolic quantum computing framework had been built on top of this foundation. One area where SymPy was lacking, however, was the ability to represent symbolic quantum states or operators in continuous bases, such as position and momentum. The goal of my project was to implement a base framework for such functionality, and example systems in multiple coordinate systems if possible. The original proposal is here: [[GSoC 2011 Application Tomo Lazovich: Position and Momentum Bases for QM]]. My blog cataloging progress over the summer is [here](http://lazovichsympy.wordpress.com).

## GSoC Project

### Modifications to represent.py

The first and most important portion of my project was introducing modifications to the represent.py module to allow for representations in continuous bases. The rationale in represent is now a multi-step process based on a general heuristic one might follow to calculate a representation when doing it by hand. The idea is to insert so-called unity operators (an outer product of some particular ket and its dual state, integrated over all possible eigenvalues for that state) and then use those so-called "dummy" states to calculate representations in the appropriate coordinates, finally integrating over any of the dummy variables. The majority of my summer was actually spent working out the subtleties of this process, and the details can only be explained once some more specific pieces are talked about. After talking about some specific pieces, we can come back to the overall represent program flow. 

### DifferentialOperator and Wavefunction

Representations of states in the position or momentum basis usually take the form of some sort of function (for example, a sine in the case of a particle in the box eigenstate). Additionally, operators when represented in these bases can be in the form of derivatives (for example, the representation of the momentum operator in position space). To facilitate the expression of these continuous representations, the DifferentialOperator and Wavefunction classes were created. The Wavefunction object is designed to hold a symbolic expression which is the eigenfunction representation of a state in a particular basis. The object has much desirable built in functionality, including functions for calculating the normalization. Wavefunction objects are also callable, so that the functional expression can immediately be evaluated at different values. DifferentialOperator inherits from Operator and gives the ability to specify an arbitrary expression involving derivatives. Any Wavefunction object that this DifferentialOperator is applied to then has its contents substituted into the differential expression, and a new Wavefunction is returned. 

### Default states and operators

As mentioned previously, the representation in continuous bases works by inserting dummy states into the expression and then integrating over their coordinates. One desired piece of functionality, then, was to have the user to be able to specify simply the class of the basis they wish to represent in, and then have default dummy states instantiated based on that class. As a result, a default argument infrastructure was introduced for the states in sympy.physics.quantum. This allows for someone to simply instantiate a state or operator (such as XOp()) without any arguments, and have the default arguments for that class be used to instantiate the object. This is very convenient, and aids in the making of dummy states for insertion into the expression. 

### Changes to basis methodology and addition of operator <-> state mapping

Previously in represent, there was a specified API for building representations of a specific basis into a given state or operator class. The API involved writing a _represent_Operator type method in the class. Particularly, the Operator class for a basis was used to specify which basis to represent in. A more natural choice, particularly for continuous bases, though, is to specify the basis state to represent in, rather than specifying an operator class. Thus, one change made to pre-existing classes was to shift all _represent_Operator methods to _represent_State methods.

Additionally, when a user is calling the represent function on some expression, they specify a basis option, usually the class or object of the basis they want to represent. We thought it would be desirable to be able to specify either the basis state or the operator (or set of operators) corresponding to the basis state you with to represent in. As a result, a module operatorset.py has been added to allow for state <-> operator mapping, and it contains a dictionary which maps each basis state to an operator or set of operators. 

### Final represent program flow

The final behavior for the represent function in continuous bases is as follows:

* Call internal ``_represent_FooBasis`` method on the given ``QExpr``,
passing an index with the options. The resulting expression will be a
Wavefunction, DifferentialOperator, or DiracDelta expression.
* If the original expression in the recursion tree was a Mul, then combine
all of the resulting expressions multiplicatively.
* Integrate over any unities (|x_1><x_1|) that resulted in a DiracDelta
function being produced.
* Combine any subsequent Wavefunctions in the Mul into a single
Wavefunction, so that DifferentialOperator can be applied appropriately.
* Call qapply on the expression, so the DifferentialOperators are applied to
Wavefunctions.
* Unwrap any remaining Wavefunction objects to get their contained
expressions, so that they can be integrated.
* Integrate over any remaining unities.
* Collapse the indices of the dummy coordinates to the lowest
available. This is so that you don't end up with expressions in terms of x_2
or higher indices if you had many ``QExpr``s in your original expression.
* Wrap a single Wavefunction object around the resulting expression if it is
still a function. Otherwise, return the Expr as is.

## Conclusion

In conclusion, many new features have been added to facilitate representing in continuous bases. While I was unable to implement many different coordinate systems as originally planned, I think alot of good work has gone into a making a robust and general framework that will work with many different systems. Some interesting final results can be found on the blog [here](http://lazovichsympy.wordpress.com/2011/08/13/cool-results-in-represent/). I still have one branch waiting to be merged in that still needs a few more changes, but after these are put in I think a very solid framework will be in place. 

