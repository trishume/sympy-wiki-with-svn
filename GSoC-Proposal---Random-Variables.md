# Random Variables
## Introduction

This will be a project proposal for GSoC 2011 by [Matthew Rocklin](http://people.cs.uchicago.edu/~mrocklin). Any and all advice/feedback is welcome either via this wiki, the sympy mailing list, or direct e-mail at mrocklin cs uchicago edu. 
This is not currently a proposal however. It is currently a presentation of ideas to generate interest and feedback to make sure that this idea is of use and has a place in SymPy. Many sections created here will not be included in a final proposal. Also, this is rough and has not been proofread. I'm of the shoot-before-looking mentality when it comes to wikis. 


[Random variables](http://en.wikipedia.org/wiki/Random_variable) are basic building blocks of statistics and probability. They are useful in basic probability theory as well as applications where measurement error or uncertainty occurs. This uncertainty can be mathematically described as a probability distribution over a space of possible outcomes. Often we are concerned with functions on these outcomes, such as money won/lost by getting "Black" on a roulette wheel or the damage done by a value of 9 or greater on the Richter scale. These functions are random variables. They can be manipulated by standard functions and by each other. 

My academic interest is in Uncertainty Quantification. Most talks in Uncertainty Quantification start out as follows:
_"Given a set of inputs and a complex system we compute outputs. If we have a probability distribution describing uncertainty in inputs (random variables) then things become more complicated. We would like to quantify how this uncertainty affects uncertainty in the outputs. Doing this analytically is hard so instead we'll do numerical sampling method X, Y, and Z"_

Analytically this problem is quite challenging. The rules for how random variables interact with functions and other random variables involve inverses, derivatives, and convolutions. These algebraic manipulations  quickly become unmanageable for even a skilled statistician. ([Other CAS systems](http://www.maplesoft.com/support/help/Maple/view.aspx?path=Statistics/RandomVariables)) have implementations with varying usability. 

## Background
Motivation was taken from the [Uncertainties Package](http://packages.python.org/uncertainties/index.html) which enhances numeric Python floats with single parameter uncertainty information (standard deviation). This is handy in a laboratory setting where measurements are often described by a simple x = 2 +- .3. A simple example taken from their website is printed below
> >>> x = ufloat((1, 0.1))  # x = 1+/-0.1

> >>> print 2*x

> 2.0+/-0.2

> >>> sin(2*x)  # In a Python shell, "print" is optional

> 0.90929742682568171+/-0.083229367309428481


The rules for functions of random variables can be found [here](http://en.wikipedia.org/wiki/Random_variable#Functions_of_random_variables). The rules for combination of random variables with each other can be found in a standard statistics textbook (I haven't found a good online source yet). 

## Proposal

I propose to implement Random Variables and integrate them into the existing SymPy framework. This would allow for the following example 
> >>> A = Normal(mean=0, std=1) 

> >>> A.pdf(x) 

> 2**(1/2)*exp(-x**2/2)/(2*pi**(1/2)) 

> >>> print (2*A).std()

> 2

> >>> sin(A).pdf(x) 

> 2**(1/2)*exp(-asin(x)**2/2)/(2*pi**(1/2)*(1 - x**2)**(1/2)) 

> >>> B = Binomial(p=.3) + Binomial(p=.4)

> >>> C = sin(A)+B/5

> >>> Plot(C.cdf(x))

> >>> print C.expectedValue()

> ...

> >>> print C.kurtosis()

> ...


There will be several implementation issues I'm sure. Feel free to add questions or concerns here. 
*
*

## Uses
Please add any fun use cases you can think of
* Educational examples with dice. Make three dice, plot the PDF. What is the probability of an even roll?

* Rules for optics and other mechanical systems can be written down analytically. We could compute 
analytical spread functions of telescopes. An analytical for may allow for optimization. 
* Uncertainty Quantification in simple systems. Provides analytical base to test numerical methods.

* Quantum Mechanical states can be thought of as random variables with complex wave functions rather than distributions. Perhaps there is some crossover. 


## Requirements from SymPy
* I'll probably need to augment sympy.probability.distributions

* Applying Functions to Probability Distributions requires that they have inverses. Maybe I'm not aware of the correct syntax here but (cos(sin(x**2))).inverse() yields just "acos" and not the expected result. Are inverses of compositions possible? The inline documentation suggests that this is only a feature of sympycore. Is this easily portable?


## Further Directions

