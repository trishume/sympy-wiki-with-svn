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
* I work under Windows 7 (32-bit) and use PyScripter for programming in Python. I also have installed Eclipse with PyDev plugin for SymPy development. Msysgit is installed on my PC. 

SymPy: Improving multivariate polynomials
-----------------------------------------

## Status

SymPy is an open source computer algebra system (CAS) written in Python. Support for multivariate polynomials is an important tool in algebra systems, very useful by its own, also used in symbolic integration algorithms, simplification of expressions, partial fractions, etc. Currently SymPy has quite efficient implementation of multivariate polynomials. Nevertheless there is a space where polynomial module can be improved. 

## Idea

The objective of the project is significantly acceleration of calculations for sparse multivariate polynomials and extension of multivariate polynomials capabilities in SymPy.

Support for polynomials was significantly improved in SymPy over the past year. Most notably Wang's multivariate factorization EEZ algorithm [EEZ-Wang] was implemented. At this stage it looks naturally to implement EEZ-GCD algorithm [EEZ-GCD] which can improve computation of GCDs of sparse multivariate polynomials over integers and rationals (current implementations for computing GCDs are based on subresultants approach and Gröbner bases).

It would be also useful to implement coefficient prediction sub-algorithm of EEZ for iterations 2..n [EEZ-Wang] (supposed to give huge speed ups for large sparse polynomials).

The next step is implementing algorithms for polynomial arithmetics based on heaps [Monagan, Monagan2]. Experimental data reveals that this is currently the best approach to compute with sparse polynomials in many variables (which is actually the most important case when computing with polynomials) [Monagan3][Paprocki]. Such approach implies using of distributed multivariate polynomials internal representation along with current recursive dense representation.

I see further development in implementing efficient multivariate factorization over finite fields [Bernardin].

Next steps may be aimed on support of non-commutative polynomials [Cohen].

Majority of ideas was derived from Mateusz Paprocki [Paprocki]. 

## My Qualifications

* I choose this idea because here I should implement several math algorithms and this side of programming is one of the most attractive for me. 
* Classes that I had related to the project: 
    - Algorithms and Data Structures;
    - Linear Algebra;
    - Polynomials;
    - Calculus Mathematics;
    - Software Design;
    - Programming Paradigms. 
* I've graduated Academy of Modern Software Engineering. 
* I had a Polynomials course in school and read book Polynomials (Algorithms and Computation in Mathematics) by Victor V. Prasolov. So I familiar with multivariate polynomials, Groebner bases, Buchberger algorithm that are connected with the topic. I also had a course of calculus mathematics where I particularly implemented various math methods and algorithms. This experience was interesting and successful.

## Schedule

* I have to finish my master project at last days of May and need to work hard on it before this dates. But after that, in June I will be free from any work and studies. It means that I will have a lot of time for GSoC. 
According to this I see the following time distribution for GSoC: 
    - April - May - 8-10 hours per week. 
    - June  - August - 40-50 hours per week. 

* Plan 
    * April - May 
        - read documentation, learn the sources of SymPy, especially _polys_ module. 
        - read the resources that I will need to implement the algorithms (see _Sources_ paragraph). 
        - figure out how to use and configure git for work, make some patches (add tests, fix bugs, push EasyToFix pathces and patches related to polys module).
        - think out and come to agreement with mentor about design of effective multivariate polynomials with different representations - dense recursive and distributed. 

    * June - August
        - start with implementing Karatsuba's polynomial multiplication algorithm. Althought this algorithm manipulates with univariate polynomials I think this is a good start point of improving _polys_ module. Implementing of well-known algorithm helps me to concentrate here on commit procedure rules, common development workflow in SymPy and prepares me for future more complicated commits. 
        - integrate Karatsuba's polynomial multiplication algorithm instead of classic multiplication algorithm where it brings profit. 
        - implement EEZ-GCD algorithm. 
        - implement coefficient prediction sub-algorithm of EEZ. 
        - implement arithmetic, i.e. addition, subtraction, multiplication and division of multivariate polynomials with usage of dynamic arrays, heaps and packed exponent vectors data structures. 
        - integrate above arithmetic algorithms for sparse multivariate polynomials. 
        - implement efficient multivariate polynomial factorization over finite fields. 
        - continue work with _polys_ module. Implement support of non-commutative polynomials. 

## Current Community Activity

- [[https://github.com/sympy/sympy/pull/214]]  (Submit a patch for Issue 760: property is_number fixed; pushed in)
- [[https://github.com/sympy/sympy/pull/208]]  (Submit a patch for Issue 604: write tests for p = x**3+2*x**2+8; pull request)
- [[http://code.google.com/p/sympy/issues/detail?id=694#c25]]  (Submit a patch. Add tests from "Review of CAS mathematical capabilities", by Michael Wester)
- [[http://code.google.com/p/sympy/issues/detail?id=1095#c8]]  (Ask a question about need of test)
- [[http://code.google.com/p/sympy/issues/detail?id=834#c8]] (Discussion about need of @property)
- [[http://code.google.com/p/sympy/issues/detail?id=1464#c2]] (Docs: adding instructions how to get stuff working on windows)
- [[http://code.google.com/p/sympy/issues/detail?id=2111#c1]]  (Send bug report)


## Sources

[EEZ-Wang] P. S. Wang. An Improved Multivariate Polynomial Factoring Algorithm. Mathematics of Computation, Vol. 32, Oct. 1978, pp. 1215-1231. 

[EEZ-GCD] P. S. Wang. The EEZ-GCD algorithm. http://portal.acm.org/citation.cfm?id=1089228

[Monagan] M. Monagan, R. Pearce. Polynomial multiplication and division using heap. http://www.cecm.sfu.ca/CAG/papers/SDMPheap08.pdf

[Monagan2] M. Monagan, R. Pearce. Polynomial Division Using Dynamic Arrays, Heaps, and Packed Exponent Vectors. Proceedings of CASC 2007, Springer (2007) 295-315.

[Monagan3] M. Monagan, R. Pearce. Sparse Polynomial Multiplication and Division in Maple 14. http://www.cecm.sfu.ca/CAG/papers/SDMPmaple14.pdf

[Bernardin] L. Bernardin, M. Monagan. Efficient Multivariate Factorization over Finite Fields. http://portal.acm.org/citation.cfm?id=677201

[Cohen] A. Cohen. Non-commutative Polynomial Computations. http://www.win.tue.nl/~amc/pub/grobner/gbnp.pdf

[Paprocki] M. Paprocki. SymPy: Master’s Thesis. http://mattpap.github.com/masters-thesis/html/index.html