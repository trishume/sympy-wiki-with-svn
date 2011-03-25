# GSoC 2011 Proposal Random Variables
This will be a project proposal for GSoC 2011 by [Matthew Rocklin](http://people.cs.uchicago.edu/~mrocklin). Any and all advice/feedback is welcome either via this wiki, the sympy mailing list, or direct e-mail at mrocklin cs uchicago edu. 

##Basics
Name: Matthew Rocklin

E-Mail: MRocklin cs uchicago edu

Occupation: PhD Student at University of Chicago

Webpage: http://people.cs.uchicago.edu/~mrocklin


Title: Random Variables in SymPy

Abstract: We develop the statistics functionality in SymPy, an open sounce Computer Algebra System in Python. We implement a Random Variable type and integrate it into existing SymPy functionality. By using the behavior of random variables and by leveraging the existing functionality in SymPy we hope to start a powerful statistical modeling language. 

## General Introduction 
Statistics is more important than we thought. Scientific and social research is scrambling add statistics to past experiments and theories. Computational systems are also struggling to keep up - previously neglected statistical packages are dusted off and found to be lacking. Now is a time for development. 

Current solutions are usually numeric, data-centric (R, SAS), or behind commercial/closed source barriers (Maple, Mathematica). Statistical researchers however often think and work symbollically (Beta = Lx + noise) and do not have a good language to encode and assist in their work. 

A substantial part of statistical modeling can be reconciled with traditional modeling if random variables can be freely interchanged with traditional ones. I propose to build and integrate a Random Variable type and integrate it into SymPy. I hope that by leveraging the existing SymPy functionality on random variables we can build a well developed and powerful statistical modeling language. 

## Background
### Random Variables

[Random variables](http://en.wikipedia.org/wiki/Random_variable) are basic building blocks of statistics and probability. They are useful in basic probability theory as well as applications where measurement error or uncertainty occurs. This uncertainty can be mathematically described as a probability distribution over a space of possible outcomes. Often we are concerned with functions on these outcomes, such as money won/lost by getting a number which is black on a roulette wheel or the expected damage done by an earthquake with value of 9 or greater on the Richter scale. These functions are random variables. Like traditional variables they can interact with functions (like sin, cos) and each other (X+Y). 

The rules for these interactions however can be quite different. They are taught briefly in school and, while they are clear to express mathematically, they involve challenging algebraic manipulations which are tedious for students. Random variables are usually treated with entirely abstract or entirely numerical methods. Given our strength in performing tedious algebraic manipulations this seems like a textbook use case for computer algebra systems.

### Previous Work

Random Variables have been implemented in the popular commercial CAS languages, [Maple](http://www.maplesoft.com/support/help/Maple/view.aspx?path=Statistics/RandomVariable) and [Mathematica](http://reference.wolfram.com/legacy/v5_2/Add-onsLinks/StandardPackages/Statistics/ContinuousDistributions.html) as well as in specialized though less popular statistical languages such as [APPL](http://www.math.wm.edu/~leemis/2001amstat.pdf).   None of these systems are freely accessible to the general public. 

This problem has been approached in the open source Python community from the numerical side. Motivation for this project was taken from the [Uncertainties Package](http://packages.python.org/uncertainties/index.html) which enhances numeric Python floats with single parameter uncertainty information (standard deviation). This is handy in a laboratory setting where measurements are often described by a simple x = 2 +- .3. A simple example taken from their website is printed below
```python
>>> x = ufloat((1, 0.1))  # x = 1+/-0.1
>>> print 2*x
2.0+/-0.2
>>> sin(2*x)  
0.90929742682568171+/-0.083229367309428481
```

## Work

I argue above for the importance of statistical code and I express hopes that we can build a "powerful statistical modeling language." This hope is far beyond the scope of a single summer. In this section I state concrete goals.

Schedule:
### Prior to Code Start Date, May 23
* Identify those in the SymPy community who are interested or knowledgeable in this subject
* Familiarize myself with the existing code structure of SymPy. 
* Decide on a clear and general definition of Random Variables which fits well into this structure. 
* Collect algorithms for future coding. 
* Collect uses cases and requirements from statisticians and educators

### Prior to First Review, July 15
At this point I hope to have a working and self consistent implementation of Random Variables. I do not expect it to be fully integrated with all parts of SymPy nor fully tested. Basic support should include: 
* Discrete and Continuous RVs
* Binary Operations like +, *, inv, Relationals (no longer bools!)
* Standard Unary Functions like (Sin, Exp, Log) and their compositions
* RV's defined on multi-dimensional probability spaces
* Ensure all common distributions accounted for (Normal, Uniform, Discrete, Correlated Multivar, Pareto, T, ..., see [scipy.stats](http://docs.scipy.org/doc/scipy/reference/stats.html)) 

### Prior to Second Review, August 15
Integrate Random Variables gracefully into other parts of SymPy. The goal is to leverage existing SymPy functionality to make Random Variables powerful. This is likely to be the most challenging part of the project. This work will likely continue past the Summer.
* Linear algebra
* Physics / Quantum 
* Numerical Evaluation / Code generation 
* Logic, Hypothesis testing

## References
[Wikipedia Article](http://en.wikipedia.org/wiki/Random_variable)

[Wolfram Mathworld Article](http://mathworld.wolfram.com/RandomVariable.html)

[Current SymPy Statistics Functionality](http://docs.sympy.org/dev/modules/statistics.html)

[Uncertainties in Python](http://packages.python.org/uncertainties/)

[Maple Random Variables Help page](http://www.maplesoft.com/support/help/Maple/view.aspx?path=Statistics/RandomVariable)

[Mathematica Continuous Probability Distributions Help page](http://reference.wolfram.com/legacy/v5_2/Add-onsLinks/StandardPackages/Statistics/ContinuousDistributions.html)

[SciPy Stats Reference Page](http://docs.scipy.org/doc/scipy/reference/stats.html)

[Algorithm to Handle Multiplication of Continuous Random Variables](http://www.math.usma.edu/people/glen/Publications/product.pdf)

[APPL, A Probability Programming Language](http://www.math.wm.edu/~leemis/2001amstat.pdf)

## Uses Cases
Please add any fun use cases you can think of

* Educational examples with dice. Make three dice, plot the PDF. What is the probability of an even roll?
* Uncertainty Quantification in simple systems. Provides analytical base to test numerical methods.
* For simple systems an analytical description of how uncertainty evolves may allow for clear statement about how to minimize that uncertainty. 
* Clear description of experiments, with statistical variation. 
* Quantum Mechanical states can be thought of as random variables with complex wave functions rather than distributions. Perhaps there is some crossover. 