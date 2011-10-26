## About Me

My name is Tomo Lazovich. I just completed my undergraduate degree in Physics at Harvard University and am currently a 1st year in their PhD program. 

## Introduction

Before the start of this year's GSOC, SymPy had much functionality in place for working in discrete spin bases to do symbolic quantum mechanics. In fact, a whole symbolic quantum computing framework had been built on top of this foundation. One area where SymPy was lacking, however, was the ability to represent symbolic quantum states or operators in continuous bases, such as position and momentum. The goal of my project was to implement a base framework for such functionality, and example systems in multiple coordinate systems if possible. The original proposal is here: [[GSoC 2011 Application Tomo Lazovich: Position and Momentum Bases for QM]]. My blog cataloging progress over the summer is [here](http://lazovichsympy.wordpress.com).

## GSoC Project

### Modifications to represent.py

The first and most important portion of my project was introducing modifications to the represent.py module to allow for representations in continuous bases. The rationale in represent is now a multi-step process based on a general heuristic one might follow to calculate a representation when doing it by hand. The idea is to insert so-called unity operators (an outer product of some particular ket and its dual state, integrated over all possible eigenvalues for that state) and then use those so-called "dummy" states to calculate representations in the appropriate coordinates, finally integrating over any of the dummy variables. The majority of my summer was actually spent working out the subtleties of this process, and the details can only be explained once some more specific pieces are talked about. After talking about some specific pieces, we can come back to the overall represent program flow. 

### DifferentialOperator and Wavefunction

Representations of states in the position or momentum basis usually take the form of some sort of function (for example, a sine in the case of a particle in the box eigenstate). Additionally, operators when represented in these bases can be in the form of derivatives (for example, the representation of the momentum operator in position space). To facilitate the expression of these continuous representations, the DifferentialOperator and Wavefunction classes were created. 


## Evaluating progress


## Conclusion and looking forward

