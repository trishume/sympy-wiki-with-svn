# GSoC 2011 Application Jack McCaffery: Improved Series

John (Jack)  McCaffery

University of Louisiana at Lafayette

[[jpmccaffery@gmail.com]]

##Bio: 

I attended [Michigan Technological University](http://www.mtu.edu) as an undergraduate and completed a B.S. In physics. My primary area of interest was quantum mechanics and mathematical physics. I then went on to finish my masters degree in mathematics at the [University of Alabama](http://www.ua.edu). While there my primary research area was real and complex analysis. I am currently finishing my third year as a PhD student in the [cognitive science](http://ics.louisiana.edu) program at the [University of Louisiana at Lafayette](http://www.louisiana.edu). My primary research interest is machine learning and probabilistic reasoning.

This project is ideal for me. My deepest interest in mathematics is in limits and complex functional analysis. Because of this and my strong background, I will be able to generalize the series expansion functionality in sympy in a way that is mathematically consistent (producing minimal errors due to competing limits, etc...) and in a way that will readily generalize to more advanced series manipulation in future releases.

##Programming: 
My primary language right now is Python. I often code in C++ and until a few years ago, this was my primary language. In my research I have often needed to use Matlab so I am familiar with its core functionality. I love programming in Haskell but it has been several years since I've used it.

##Abstract:
(This proposal primarily addresses issues [1639](http://code.google.com/p/sympy/issues/detail?id=1639&q=label%3ASeries&colspec=ID%20Type%20Status%20Priority%20Milestone%20Owner%20Summary%20Stars), [1038](http://code.google.com/p/sympy/issues/detail?id=1038&q=label%3ASeries&colspec=ID%20Type%20Status%20Priority%20Milestone%20Owner%20Summary%20Stars) and [1300](http://code.google.com/p/sympy/issues/detail?id=1300&q=label%3ASeries&colspec=ID%20Type%20Status%20Priority%20Milestone%20Owner%20Summary%20Stars)) 

The existing series expansion function in sympy covers a broad range of situations but is lacking some simple functionality and will need to be generalized as more specific functions are defined. In particular, series() lacks the ability to evaluate Taylor series directly by evaluating derivatives of the function being expanded. Additionally, Taylor series are just one of many useful series expansions. Laurent series provide expansions for complex functions that do not have Taylor expansions and Puiseux series provide simple expansions for inverse trigonometric and inverse hyperbolic functions.

This project will lay the framework for sympy to express functions with different types of expansions, efficiently manipulate series expansions. This will allow future developers to include more robust and efficient series expansions of complex functions and make sympy more competitive with existing computer algebra systems. The existing state of affairs are detailed [here](https://github.com/sympy/sympy/wiki/Function-expansions-and-series).

**Immediate benefits:** 

* Faster series expansions
* Series expansions for a broader class of functions ( e.g. \(\exp(\frac{1}{x})\) or \(\exp(x)/x\) )
* Laurent series support
* Implementation of \(\csc(x)\), \(\sec(x)\), acsc\((x)\), asec\((x)\), csch\((x)\), sech\((x)\), acsch\((x)\), asech\((x)\) (see [issue 564](http://code.google.com/p/sympy/issues/detail?id=564&can=5&colspec=ID%20Type%20Status%20Priority%20Milestone%20Owner%20Summary%20Stars))

**Long term benefits:**

* Ability to implement more sophisticated functions
* A framework in which more general types of expansions can be included
* Improved functionality of series() without unnecessary additional complexity for the end user

#Schedule:

##April 25 – May 23
(5 hours per week)

During this period I will be getting to know the larger sympy community. I will be communicating with active members who are familiar with the workings of sympy's differentiation, limit evaluation and series expansion. This will also be a good time to familiarize myself with some of the more obscure bugs relating to series, and limits. This will help me to avoid common problems during development, see issue [1300](http://code.google.com/p/sympy/issues/detail?id=1300&q=label%3ASeries&colspec=ID%20Type%20Status%20Priority%20Milestone%20Owner%20Summary%20Stars) for example.

I will also continue to clean up the specific value tests of the trigonometric and hyperbolic functions. Once this is complete I can submit my already written cosecant, secant, arccsc, arcsec, csch, sech, acsch and asech functions. Because of their dependence on existing functions, they are not quite ready for submission at this point.

##May 23 – July 15
(40-50 hours per week)

During the first period I will be working to implement something like dseries as described in issue [1038](http://code.google.com/p/sympy/issues/detail?id=1038&q=label%3ASeries&colspec=ID%20Type%20Status%20Priority%20Milestone%20Owner%20Summary%20Stars). Following this a new heuristic will need to be defined to identify when dseries is appropriate. This will need to be generalizable for when Laurent and other series expansions are included. During this period I will also be implementing a smart multiplier for things like \(\sin(x)*\cos(x)\).series() = \(\sin(x)\).series( )\(*\cos(x)\).series( )).

I will also be cataloging all the existing functions and their:

1. Taylor series. Exists? Is a Laurent series? Is something else?
2. Differentiation functions.


**Week1:** Cataloging and familiarization with existing taylor series.

**Week2:** Implement dseries for differentiable functions.

**Week3-4:** Integrate dseries with series and taylor_series. 

**Week5:** Implement smart multiplication and other optimzations for series.

**Week6-7:** Define laurent_series and integrate with series, dseries and taylor_series. This should now form a coherent series expansion framework.

**Week8:** Testing

##Halfway Check: 

Bottom line: Is dseries running and is series ready to integrate different types of series expansions in a smart and graceful way. This should be the expectation at this point.

##July 15 – August 26
(40-50 hours per week)

**Week9-10:** Add Laurent series functionality for existing function base. For example, some composite functions like \(\exp(\frac{1}{x})\) have do not have a Taylor series about 0 but do have a Laurent series. Right now sympy treats this expansion the same way it treats any Taylor series.

**Week11:** Additional series expansions. Puiseux series for example allow for \(\log(x)\) terms and can be used to define acosh\((x)\). This functionality would be a nice addition.

**Week12:** Wiggle room. There should be plenty to do at this point.

**Week13:** Pencils down. Finalize code documentation and perform final debugging.


##Final Check: 

Bottom line: At this point we should absolutely have dseries, laurent_series and taylor_series as three separate entities, all unified under series. These three series expansions should be applied to all existing functions wherever appropriate.

##Links:

[Wikipedia: Taylor Series](http://en.wikipedia.org/wiki/Taylor_series)

[Wikipedia: Laurent Series](http://en.wikipedia.org/wiki/Laurent_series)

[Mathworld: Puiseux Series](http://mathworld.wolfram.com/PuiseuxSeries.html)

[Mathworld: Trigonometric Functions](http://mathworld.wolfram.com/TrigonometricFunctions.html)

[Mathworld: Hyperbolic Functions](http://mathworld.wolfram.com/HyperbolicFunctions.html)

##References:

Stein, E. M. and Shakarchi, R. (2003). _Princeton Lectures in Analysis II: Complex Analysis_. Princeton University Press, Princeton, NJ, USA.

Wade, W. R. (1999). _An Introduction to Analysis, Second Edition_. Prentice Hall.


**Note:** The patch that I've submitted can be found here ([issue 2243](http://code.google.com/p/sympy/issues/detail?id=2243)). My pull request is number [190](https://github.com/sympy/sympy/pull/190).
