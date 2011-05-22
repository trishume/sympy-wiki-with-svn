What is a random variable? Random variables are just like any other variable except that rather than take on a single value they take on several, each with a certain probability. For example, we could say that the value of a roll of a die is either 1,2,3,4,5 or 6, each with probability 1/6th. Random Variables are defined in SymPy much how they are in mathematics, as function on probability spaces. 

# Abstract Definition

To define Random variables we must first define probability spaces. A Probability Space consists of the following: 

* A Sample Space - a set of possible values of some process ({1,2,3,4,5,6} in the above example)

* A set of Events ({{1}, {2}, {1,2}, ... }, 

* A measure P which assigns probabilities to events ( P({1,3,5}) = 1/2 ). 


We implement this formalism with the following constructs. 

The Sample Space is simply a SymPy Set. 

Event inherit from Sets. They also encode from which Sample Space they come so that we may differentiate between die one being odd ({1,3,5}, die1) and die two being odd ({1,3,5}, die2).

A Probability Measure is a mapping of events to the positive reals under various conditions (P(Omega) = 1, P>0 , P(A+B) = P(A)+P(B)-(A \Cap B), etc...)

A Random Variable is then a function on the sample space with all of the probability space formalism attached. The following are examples of random variables given a probability space, die1. 

`X = Identity(die1)`

`X = die1**2`

`X = die1 > 3`

`X = die1 % 2 == 0`


We define Random Variables abstractly first so that future implementations can interact nicely and so that a standard formalism is maintained in the future. The abstract class handles mixing of different implementations. 
Imagine a sports team deciding if it should practice given two random variables Rain (Discrete) and Temp (Continuous) defined on different probability spaces. 

`Practice =  Rain==False or Temp > 20`

Both (Rain==False) and (Temp > 20) are Events on their respective spaces (conditionals turn Random Variables into Events). (Rain==False or Temp > 20) is an event on the Cartesian product of these two spaces which is itself another probability space. One could consider Compound Random Variables which mix several types of different implementations. 