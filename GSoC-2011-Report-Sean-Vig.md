WIP

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



## Conclusion and Future Work

Conclusion