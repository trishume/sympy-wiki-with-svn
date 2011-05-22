Random variables are like any other variable except that rather than taking on a single value they take on several, each with a certain probability. For example, we could say that the value of a roll of a die is either 1,2,3,4,5 or 6, each with probability 1/6th. Random Variables are defined in SymPy much how they are in mathematics, as function on probability spaces. 

# Abstract Definition
## Mathematical Formalism
To define Random variables we must first define probability spaces. A Probability Space consists of the following: 

* A Sample Space - a set of possible values of some process ({1,2,3,4,5,6} in the above example)

* A set of Events ({{1}, {2}, {1,2}, {2,4,6}, ... }, subsets of the sample space.

* A measure P which assigns probabilities to events ( P({1,3,5}) = 1/2 ). 

## Python Formalism
We implement this formalism with the following constructs. 

The Sample Space is simply a SymPy Set. 

Events are enhanced Sets. They must also encode from which Sample Space they come so that we may differentiate between die one being odd ({1,3,5}, die1) and die two being odd ({1,3,5}, die2).

A Probability Measure is a mapping of events to the positive reals under various conditions (P(Sample Space) = 1, P>0 , P(A+B) = P(A)+P(B)-(A Intersect B), etc...)

A Random Variable is then a function on the sample space with all of the probability space formalism attached. The following are examples of random variables given a probability space, die1. 

`X = Identity(die1)`

`X = die1**2`

`X = die1 > 3`

`X = die1 % 2 == 0`

## Why Abstract?

We define Random Variables abstractly first so that future implementations can interact nicely and so that a standard formalism is maintained in the future. The abstract class handles mixing of different implementations. 
Imagine a sports team deciding if it should practice given two random variables Rain (Discrete) and Temp (Continuous) defined on different probability spaces. 

`Practice =  Rain==False or Temp > 20`

Both (Rain==False) and (Temp > 20) are Events on their respective spaces (conditionals turn Random Variables into Events). (Rain==False or Temp > 20) is an event on the Cartesian product of these two spaces which is itself another probability space. One could consider Compound Random Variables which mix several types of different implementations. 

# Implementations
## Discrete Random Variable
A Discrete Random Variable is a function on a countable sample space. Common examples include the result of a die {1,2,3,4,5,6}, a coin toss {'H', 'T'}, or The number of Heads before a Tails on a sequence of coin tosses {0,1,2,3, ... }. 

Events are simple discrete Sets. 

The Probability Measure is encoded trivially as an assignment of a probability to each elementary element of the set. 

## Continuous 1D Random Variable
Our first implementation of a Continuous 1D Random Variable is a function on the real numbers as a sample space. Common examples include the time a radioactive isotope takes to decay, the height of a person, wait time in line at the grocery store. 

Events are restricted to be Unions of SymPy Intervals such as (0,1) or (a,b). 

The Probability Measure is commonly encoded as either a CDF or PDF. Given an event/interval one can compute the probability either by asking for values of the CDF at the interval endpoints or by performing a SymPy integral on the PDF over the intervals. 

## Multivariate Normal Random Variable
Much active statistics research acts on multivariate random variables. These are generally functions from R^n to R^m. Common examples include the state of the weather (all of it), risk of diabetes given weight, glucose levels, age, etc.... 

Multivariate Normal Random Variables are commonly used because they can be encoded simply as a mean vector and a covariance matrix. 
