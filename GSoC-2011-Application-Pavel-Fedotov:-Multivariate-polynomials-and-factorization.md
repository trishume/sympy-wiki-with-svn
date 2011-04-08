GSoC 2011 Application Pavel Fedotov: Improving Multivariate Polynomials
=======================================================================

About me
--------

* Pavel Fedotov, 22 years old. 
* I'm sixth year student at Saint Petersburg State University of Information Technologies, Mechanics and Optics ([SPbSU ITMO](http://en.ifmo.ru/)). 
* I graduated from Saint Petersburg Lyceum 239 that specializes in mathematics and physics in 2005. In 2009 I've got bachelor degree on apply math at SPbSU ITMO and at this time I'm working on my master's project at SPbSU ITMO. I have rather solid math and algorithms background. 
* Email: fedotovp@gmail.com

Coding Skills
-------------

* My primary language is Java. I developed several rather big projects, you can see examples of my code here: 
   - [[http://rain.ifmo.ru/~fedotov/pub/GraphEditor.html]];  
   - [[http://rain.ifmo.ru/~fedotov/pub/Noplag.html]]. 
* I'm also expirienced with Python, C, C++, C#, Matlab, Maple, Delphi, Haskell, MPS. 
* At this time I'm mostly interested in Python as a language that is suitable for a lot of areas. Among Python's many benefits is the fact that it is very easy to use, requiring fewer man-hours of coding time per output than just about any other programming language.
* I work under Windows 7 (32-bit) and use PyScripter for programming in Python. I also have installed Eclipse with PyDev plugin for SymPy development. 
* I've graduated Academy of Modern Software Engineering. 

SymPy: Improving multivariate polynomials
-----------------------------------------

## Status

SymPy is an open source computer algebra system (CAS) written in Python. Support for multivariate polynomials is an important tool in algebra systems, very useful by its own, also used in symbolic integration algorithms, simplification of expressions, partial fractions, etc. Currently SymPy has quite efficient implementation of multivariate polynomials. Nevertheless there is a space where polynomial module can be improved. 

## Idea

Support for polynomials was significantly improved over the past year. Most notably Wang's multivariate factorization EEZ algorithm [EEZ-Wang] was implemented. At this stage it looks naturally to implement EEZ-GCD algorithm [EEZ-GCD] which can improve computation of GCDs of sparse multivariate polynomials over integers and rationals (current implementations for computing GCDs are based on subresultants approach [Subresultant] and Gröbner bases [Gröbner]).

It would be also useful to implement coefficient prediction sub-algorithm of EEZ for iterations 2..n [Wang] (supposed to give huge speed ups for large sparse polynomials). 

The next step is implementing algorithms for polynomial multiplication and division based on heaps [Monagan2007heaps]. Experimental data reveals that this is currently the best approach to compute with sparse polynomials in many variables (which is actually the most important case when computing with polynomials). This approach implies using of distributed multivariate polynomials internal representation along with current recursive dense representation. 

I see further development in implementing efficient multivariate factorization over finite fields [Bernardin].

Majority of ideas was derived from Mateusz Paprocki [Mattpap]. 

## My Qualifications

* I choose this idea because here I should implement several math algorithms and this side of programming is one of the most attractive for me. 
* Classes that I had related to the project: 
    - Algorithms and Data Structures;
    - Linear Algebra;
    - Polynomials;
    - Calculus Mathematics;
    - Software Design;
    - Programming Paradigms. 
* I had a Polynomials course in school and read book Polynomials (Algorithms and Computation in Mathematics) by Victor V. Prasolov. So I'm familiar with multivariate polynomials, Groebner bases, Buchberger algorithm that are connected with the topic. I also had a course of calculus mathematics where I particularly implemented different math methods and algorithms. This experience was interesting and successful. 

## Schedule [not finished yet]

* I have to finish my master project at first days of June and need to work hard on it before this dates. But after 5-th of June I will be free from any work and studies. It means that I'm ready to a lot of time on GSoC. 
I see the following plan for me: 
    - April - May - 8-10 hours per week. 
    - June  - August 30 - 40-50 hours per week. 
* Schedule. First steps. 
    - I've started with installing git and studying how to work with it. 
    - Then I'll clone repository of sympy and I'll write some tests for some parts of sympy or submit other EasyToFix patch. 
    - Then I will deep inside polys module looking for things that could be improved in easy way. 
    - After I'll get closer with algorithms and methods listed in _Idea_ paragraph and polys module I will choose one of the method provided efficient multivariate polynomial arithmetics and GCD algorithm and implement it. 

## Sources

[Mattpap] http://mattpap.github.com/masters-thesis/html/index.html

[EEZ-Wang]

[EEZ-GCD]

[Subresultant]

[Gröbner]

[Monagan]

[Bernardin, Monagan]