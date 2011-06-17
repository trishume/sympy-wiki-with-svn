Random variables are like any other variable except that rather than taking on a single value they take on several, each with a certain probability. For example, we could say that the value of a roll of a die is either 1,2,3,4,5 or 6, each with probability 1/6th. Random Variables are defined in SymPy much how they are in mathematics, as function on probability spaces. 

# Abstract Definition
## Mathematical Formalism
To define Random variables we must first define probability spaces. A Probability Space consists of the following: 

* A Sample Space - a set of possible values of some process ( such as {1,2,3,4,5,6})

* A set of Events ({{1}, {2}, {1,2}, {2,4,6}, ... }, subsets of the sample space.

* A measure P which assigns probabilities to events ( such as P({1,3,5}) = 1/2 ). 

A Random Variable is then a function on the sample space with all of the probability space formalism attached. Such as the square of the die roll or the value mod 2. 

Conditionals on Random Variables such as X > 3 are again events  which have defined probabilities under the measure, P(die > 3) == 1/2. 

## Python Formalism

Mathematical sets are represented by SymPy Sets. 

ProbabilityMeasures are implemented directly for finite (as a dict) and continuous real sets (as a pdf/cdf expression). 

ProbabilitySpaces contain a sample_space (Set) and a ProbabilityMeasure.

Events contain a Set and a ProbabilitySpace. This lets us differentiate between die one being odd (die1 in {1,3,5}) and die two being odd (die2 in {1,3,5}).

Random Variables do not have a class. They are represented by SymPy Exprs when that Expr contains a RandomSymbol. A RandomSymbol is just like ordinary SymPy Symbol except that it points back to a ProbabilitySpace. This is made more clear by an example:

`>>> d = Die(6) # An intuiitve probability space`

`>>> X = d.value # a RandomSymbol which represents this space in expressions`

`>>> X**2+1 # A normal SymPy Expr containing a RandomSymbol - we think of this Expr as a random variable`

`>>> expectation(X**2+1) # Special functions know to look for RandomSymbols within SymPy Exprs`

`    8`



## Why Abstract?

We define Random Variables abstractly first so that different implementations can interact nicely and so that a standard formalism is maintained in the future. The abstract class will be mainly an empty interface with logic to handle heterogeneous combinations of variables. 

# Implementations
## FiniteProbabilitySpace
Common examples include the result of a die {1,2,3,4,5,6}, a coin toss {'H', 'T'}. This does not include countably infinite spaces such as the number of Heads before a Tails on a sequence of coin tosses {0,1,2,3, ... }. 

Event sets are FiniteSets or Unions thereof. 

The Probability Measure is encoded as a dict assigning a probability to each elementary element of the sample_space. 

## Continuous Probability Space
Common examples include the time a radioactive isotope takes to decay, the height of a person, wait time in line at the grocery store, etc.... 

Event sets are Intervals or Unions thereof. 

The Probability Measure is encoded as either a PDF (generally) or a CDF. 

## Product Probability Spaces
Elementary Probability Spaces are assumed independent. Statements on multiple spaces invoke ProductProbabilitySpaces. 

## Multivariate Normal Random Variable
TODO

Much active statistics research acts on multivariate random variables. These are generally functions on R^n. Common examples include the state of the weather, the position of an airplane, noisy measurements of the position of an airplane (the noise has it's own probability space), risk of diabetes given weight, glucose levels, age, etc.... 

Multivariate Normal Random Variables are commonly used because they can be encoded with only a mean vector and a covariance matrix. 

[A diagram of the class structure](http://people.cs.uchicago.edu/~mrocklin/class_diagram.pdf)