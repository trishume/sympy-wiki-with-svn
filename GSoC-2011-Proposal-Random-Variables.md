sympy random variables
# GSoC 2011 Proposal Random Variables
This will be a project proposal for GSoC 2011 by [Matthew Rocklin](http://people.cs.uchicago.edu/~mrocklin). Any and all advice/feedback is welcome either via this wiki, the sympy mailing list, or direct e-mail at mrocklin cs uchicago edu. 

##Basics
Name: Matthew Rocklin

E-Mail: MRocklin cs uchicago edu

Occupation: PhD Student at University of Chicago

Webpage: http://people.cs.uchicago.edu/~mrocklin


Title: Random Variables in SymPy

Abstract: We develop the statistics functionality in SymPy, an open sounce Computer Algebra System in Python. We implement a Random Variable type and integrate it into existing SymPy functionality. By using the behavior of random variables and by leveraging the existing functionality in SymPy we hope to start a powerful statistical modeling language. 

## Introduction 
Statistics is more important than we thought. In both social and scientific research we’re scrambling to quantify and reduce error in past experiments and theories. Computational systems are also struggling to keep up with this changing paradigm - previously neglected statistical packages are dusted off and found to be lacking. Now is a time for active development. 

Numerically most solutions approach this from a data-analytic view (R, SAS, STATA, scipy.stats) or by sampling (Monte Carlo). Many statistical researchers however consider problems from a modeling perspective (regression, signals/processes, uncertainty evolution) and think symbolically (Beta = Lx + noise) and are unaware that computers could handle these symbolic problems. 

Statistical mathematical modeling can be reconciled with traditional mathematical modeling if random variables can be freely interchanged with traditional ones. I propose to build and integrate a Random Variable type and integrate it into SymPy. I hope that by leveraging the existing SymPy functionality on random variables we can build a well developed and powerful statistical modeling language. 

## Random Variables

[Random variables](http://en.wikipedia.org/wiki/Random_variable) are basic building blocks of statistics and probability. They are useful in basic probability theory as well as applications where measurement error or uncertainty occurs. This uncertainty can be mathematically described as a probability distribution over a space of possible outcomes. Often we are concerned with functions on these outcomes, such as money won/lost by getting a number which is black on a roulette wheel or the expected damage done by an earthquake with value of 9 or greater on the Richter scale. These functions are random variables. Like traditional variables they can interact with functions (like sin, cos) and each other (X+Y). 

The rules for these interactions however can be quite different. They are taught briefly in school and, while they are clear to express mathematically, they involve challenging algebraic manipulations which are tedious for students for anything beyond the most basic problems. Traditionally after a few simple homework problems students switch to treating random variables as entirely abstract or entirely numerical methods. Given our strength in performing tedious algebraic manipulations this seems like a textbook use case for computer algebra systems.

## Background
Motivation was taken from the [Uncertainties Package](http://packages.python.org/uncertainties/index.html) which enhances numeric Python floats with single parameter uncertainty information (standard deviation). This is handy in a laboratory setting where measurements are often described by a simple x = 2 +- .3. A simple example taken from their website is printed below
```python
>>> x = ufloat((1, 0.1))  # x = 1+/-0.1
>>> print 2*x
2.0+/-0.2
>>> sin(2*x)  
0.90929742682568171+/-0.083229367309428481
```

The rules for functions of random variables can be found in any standard textbook or, in some cases,  [on Wikipedia](http://en.wikipedia.org/wiki/Random_variable#Functions_of_random_variables). 

Previous CAS work has been done by [Maple](http://www.maplesoft.com/support/help/Maple/view.aspx?path=Statistics/RandomVariables) at least. Mathematica doesn't seem to have a very advanced implementation (although I looked only briefly). 

## Work

How to mathematically define Random Variables is clear. How to code and integrate them into SymPy is not. I separate the work into solving two main problems:

### Defining Random Variables

There are two goals:

* Define Random Variables as generally as possible

* Ensure that Random Variables are as intuitive to use and efficient to compute as possible. 

For example we could decide only to treat Continuous random variables and focus on optimizing operations on continuous probability density functions (PDFs). Alternatively, we could define arbitrary spaces of events (allowing for say the number of dots on a six sided die or a space of functions), distributions on these spaces (unifomly ⅙ in the die example)  and then define random variables as functions on the space of events. How about Cartesian products of these spaces? Multivariable target spaces? What are the best choices here which balance intuitive use and mathematical clarity?

#### Continuous Random Variables
#### Discrete Random Variables

### Integration into SymPy

I suspect that implementing a clean, efficient and intuitive Random Variable type will take up at most half my time. The other half will be in integration with existing SymPy mechanics. 
SymPy was designed to function on traditional variables, not random ones. Random Variables require different dynamics (such as easily computable inverses of functions) and will provide different responses. 

It’s difficult for me to give a rich response here without understanding the core of SymPy at a deeper level. 

## Uses
Please add any fun use cases you can think of

* Educational examples with dice. Make three dice, plot the PDF. What is the probability of an even roll?

* Uncertainty Quantification in simple systems. Provides analytical base to test numerical methods.

* For simple systems an analytical description of how uncertainty evolves may allow for clear statement about how to minimize that uncertainty. 

* Clear description of experiments, with statistical variation. 

* Quantum Mechanical states can be thought of as random variables with complex wave functions rather than distributions. Perhaps there is some crossover. 


## Requirements from SymPy
* I'll probably need to augment sympy.probability.distributions

* Applying Functions to Probability Distributions requires that they have inverses. Maybe I'm not aware of the correct syntax here but (cos(sin(x**2))).inverse() yields just "acos" and not the expected result. Are inverses of compositions possible? The inline documentation suggests that this is only a feature of sympycore. Is this easily portable?
  * The way functions are currently designed is a problem. There's basically no good way to represent a specific non built-in function, cf [issue 1688](http://code.google.com/p/sympy/issues/detail?id=1688). And this `inverse` method is seriously broken. --Ronan  
  * Is it broken beyond repair? I anticipate that I'll need to enhance other parts of SymPy to integrate Random Variables. Is fixing 'inverse' doable? --Matt


## Further Directions

