GSoC 2011 Application Pavel Fedotov: Multivariate polynomials and factorization
================================================================================

About me
--------

* Pavel Fedotov, 22 years old. 
* I'm sixth year student at Saint Petersburg State University of Information Technologies, Mechanics and Optics ([SPbSU ITMO](http://en.ifmo.ru/)). 
* I graduated from Saint Petersburg Lyceum 239 that specializes in mathematics and physics in 2005. In 2009 I've got bachelor degree on apply math at SPbSU ITMO and at this time I'm working on my master's project at SPbSU ITMO. I have rather solid math and algorithms background. 
* Classes that I had related to the project: 
    - Algorithms and Data Structures;
    - Linear Algebra;
    - Polynomials;
    - Calculus Mathematics;
    - Software Design;
    - Programming Paradigms. 
* Email: fedotovp@gmail.com

Coding Skills
-------------

* My primary language is Java. I developed several rather big projects, you can see examples of my code here: 
   - [[http://rain.ifmo.ru/~fedotov/pub/GraphEditor.html]];  
   - [[http://rain.ifmo.ru/~fedotov/pub/Noplag.html]]. 
* I'm also expirienced with Python, C, C++, C#, Matlab, Maple, Delphi, Haskell, MPS. 
* At this time I'm mostly interested in Python as a language that is suitable for a lot of areas. 
* I work under Windows 7 (32-bit) and use PyScripter for programming in Python. I also have installed Eclipse with PyDev plugin for SymPy development. 

My Project
----------

* SymPy: Improving multivariate polynomials. 
* Status: Factorization of multivariate polynomials is an important tool in algebra systems, very useful by its own, also used in symbolic integration algorithms, simplification of expressions, partial fractions, etc. Currently multivariate factorization algorithm is based on Kronecker's method, which is impractical for real life problems. Undergo there is implementation of Wang's algorithm, the most widely used method for the task.
* Idea: Start with implementing efficient multivariate polynomial arithmetics and GCD algorithm. You do this by improving existing code, which is based on recursive dense representation or implement new methods based on your research in the field. There are many interesting methods, like Yan's geobuckets or heap based algorithms (Monagan & Pearce). Having this, implement efficient GCD algorithm over integers, which is not a heuristic, e.g. Zippel's SPMOD, Musser's EZ-GCD, Wang's EEZ-GCD. Help with implementing Wang's EEZ factorization algorithm or implement your favourite method, e.g. Gao's partial differential equations approach. You can go further and extend all this to polynomials with coefficients in algebraic domains or implement efficient multivariate factorization over finite fields.
* I choose this idea because here I should implement several math algorithms and this side of programming is one of the most attractive for me. 
* I had a Polynomials course in school and read book Polynomials (Algorithms and Computation in Mathematics) by Victor V. Prasolov. So I'm familiar with multivariate polynomials, Groebner bases, Buchberger algorithm that are connected with the topic. I also had a course of calculus mathematics where I particularly implemented different math methods and algorithms. This experience was interesting and successful. 
* I have to finish my master project at first days of June and need to work hard on it before this dates. But after 5-th of June I will be free from any work and studies. It means that I'm ready to a lot of time on GSoC. 
I see the following plan for me: 
    - April - June 5 - 8-10 hours per week. 
    - June 6 - August 30 - 40-50 hours per week. 
* TODO. Schedule. First steps. 
    - I've started with installing git and studying how to work with it. 
    - Then I'll clone repository of sympy and I'll write some tests for some parts of sympy or submit other EasyToFix patch. 
    - Then I will deep inside polys module looking for things that could be improved in easy way. 
    - After I'll get closer with algorithms and methods listed in _Idea_ paragraph and polys module I will choose one of the method provided efficient multivariate polynomial arithmetics and GCD algorithm and implement it. 