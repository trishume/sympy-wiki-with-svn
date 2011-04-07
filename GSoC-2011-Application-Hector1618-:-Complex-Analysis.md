**Title** : Extending the domain of integration to complex plane and enabling SymPy to handle more  physics and engineering problems.

**Abstract** :  SymPy is an open source python library used for symbolic mathematics. Although lots of algorithms has been implemented at the time being, there is a scope of improvement in some of the areas, and complex analysis is one of them. I am proposing to improve integration functionality of SymPy by enabling it to do complex integration. But it is not only related to integration, for integration to be feasible, I have to add some other functions to SymPy which will help dealing with complex numbers and functions with complex variables. Once this is done, my next step would be to add Laplace and Fourier transformation to SymPy, as they are widely used in many physics and engineering applications.This will take SymPy one step closer to become a full featured CAS library. 


##Contact Information : 
* Name : TALE PRAFULLKUMAR P.
* Institute : Indian Institute of Technology Roorkee
* Email : hector1618@gmail.com 
* IRC : hector on freenode
* Contact : +91-9760197719 / +91-9970057858



##Contribution to SymPy : 
Since I started using SymPy, I tasted the real flavor of open source and enjoyed working with it. Till now, I have submitted four pull requests. One of them has been accepted, two are marked as 'NeedsReview' and the last one needs improvement from my side.

* Pull request( accepted ) : A small step to start with. I added a doc-string to Plot function. It was hidden under the class description. It took me considerable time to fix it but because of that, I learned a lot about coding structure in SymPy.

* Pull request #201 : Added arbitrary function to final result of integration. This change is under review and once it gets pulled in, integrate() can have an additional keyword named arbitrary_function which will give the following results:

```ipython

In [2]: integrate(1+y,x,arbitrary_function=True)
Out[2]: x*(1 + y) + f(y)

In [3]: integrate(1+y*z,x,arbitrary_function=True)
Out[3]: x*(1 + y*z) + f(y,z)
 
```
I believe this will be very helpful in ODE and PDE solvers.

* Pull request #165 : I added integration by parts ( with a condition so that it doesn't go in infinite loop) to solve some of the integration which are not solvable by current methods. For example, integrate(x*sqrt(1+2*x),x) is not solvable. But with this improved code, it will give following result-

```ipython
In [7]: integrate(x*sqrt(1+2*x),x)
Out[7]: x*(1+2*x)**(3/2)/3 - (1+2*x)**(5,2)/15
```
After adding a pull request, some of the critical issues were pointed out and now I am working on it.

##Proposal :
When I was going through the issues, I found somethings which were commonly used in mathematics and engineering but SymPy provides very little support for that. Complex integration is one of it. Only very elementary functions present to deal with complex numbers. Others are Laplace and Fourier transformations. Once complex integration is implemented, it will help in improving some of the existing methods for real functions also. 

My summer project proposal has been divided into two stages - first ( and major ) is to write functions for handling complex analysis and second is to write functions related to Laplace and Fourier transformations.

### **Complex Analysis**:

Complex analysis is useful in many branches of pure and applied mathematics as well as in physics mainly for  hydrodynamics, thermodynamics and electrical engineering. Complex analysis is described as one of the most beautiful as well as useful branches of mathematics. Yet SymPy has very limited functions dealing with it. The current functions in this domain includes - defining complex numbers, functions returning real and imaginary part, absolute value, argument and conjugate of complex numbers. The 'roots' function in SymPy can only solve the polynomials in complex variable and returns the roots which are only expressible by radicals. As far as integrations are concerned, only function that can be used is 'line integrals' function.

To reach at complex integration, I need to define some other functions and it will be very useful if I make them available to end users. And there are some other functions which are not directly related to complex integration, but will be useful to form the basic of complex analysis in SymPy. I would like to add following functions in SymPy -

* **Analytic Functions** : Complex analysis is particularly concerned with the analytic functions of complex variables and hence analytic functions are studied widely and hence whether a given function is analytic or not would be topic of interest for most of the mathematicians. And this function would serve the purpose.

* **Zeros** : As I mentioned, currently only polynomials with complex variable are solvable in SymPy. I want to extend this to make sure that every function which is solvable by any other CAS system will be solvable by SymPy. Precisely I am targeting on polynomials, exponential and trigonometric functions.  

* **Poles** : Ones we had a function to find the roots, it would not be very difficult to make a program to find poles and their multiplicity. 

* **Residues** : This is one of the important functions we will be needing to apply Cauchy Residue theorem. I believe we need to consider two separate cases, namely - Residues at finite point and residue at the point of infinity. There is an already implemented residue function for elementary functions, so it will be easy for me to expand it.

* **Singularities** : This function will return the singularities of given function, and if possible, I will write a code to classify them. 

* **Limit** : The currently implemented limit function is only restricted to real line. This functions only checks limits in one direction ( +ve or -ve). Clearly we can't use this function in case of complex variables. I need to rewrite the code to find limit of functions with complex variables. This code can also be used to find limit of bi-variant function.

* **Continuity** : Once the limit has been found, we can talk about the continuity and its type (removable or non-removable) at a given point. 

* **Derivative** : This function is required to form the basic set of tools to handle complex analysis and it will not be very difficult to complete, once code for above two functions get completed.

* **Integration** : With the above tools, and existing line integration, I can write a program for complex integration using Cauchy's integral formula. Extending this idea of complex integrals, I am planning to implement Cauchy's Residue theorem which will serve as a powerful tool for solving complex integration. I will incorporate this function to handle integration of real valued functions which are not solvable or feasible to solve with current implementation methods.

    And if the time permits some of the other functions like Gaussion Integers, Random Complex number generators, etc.

### **Laplace and Fourier transformation**:
 
Laplace and Fourier transformations are widely used linear transformations which has many important applications over science and engineering. Once the complex integration of a function has been accomplished, my next step would be to introduce these topics in SymPy and try to add the relevant transformations like - inverse Laplace, Bilateral Laplace, inverse Fourier, Fourier Sin, Fourier Cosine, etc. 

## **Benefits** : 

Aim of my project is to create a platform for the development of functions in SymPy which can be used to work in complex analysis. With this new tools, new doors for handling various mathematical problems with sympy will be opened. Sympy will be enriched with Laplace and Fourier transformation which are one of the most useful techniques in engineering related problems. Some of currently implemented techniques can be improved with this. As complex analysis forms the crucial base in applied mathematics, these new functions will serve the same purpose in sympy.


## Time line (Tentative) : 

Following is the tentative time table I will be following during my summer.

* **Before the beginning** :
My final exams will get over by 13th May and I want to start coding well before official date. I have some exposure to SymPy and have a general idea about coding style, conventions, methods used in coding SymPy and also in reporting issues, discussing patches, adding pull requestes, etc. I can right away start with work for my project.

* **During coding period** :

Early starting will give me 4 weeks before 1st mid-term evaluations and I am planning for :

* Week 1 & 2 : Working on limit, continuity and differentiability of complex function. (and try to incorporate them for 'bi-variate function' in real plane)
Function to determine whether a given function is analytic (and Harmonic) or not.

* Week 3 : Roots and poles of function with complex variables.

* Week 4 & 5 : Finding singularities and types of singularities

* Week 6 : Moving complex functions out of functions/elementary/complex.py and to make it a module so that it will be easy for modifying in the future.

* Week 7 : Buffer time.

**Mid-term Evaluations**

* Week 8 & 9 : Working on residue and complex integration

* Week 10,11 & 12 : Laplace and Fourier transformations

* Week 13 : Buffer time

* Week 14 : Completing documentation and final touch.

**Final Evaluations**

* **After the end** : I will be, along with other people, maintaining complex module of sympy and fixing any bugs that will arise in it, while dealing with other issues of SymPy and continue my journey in open source world.


Buffer of 2 weeks has been kept in case of some unpredictable delay. 
In my institute, no one precisely work with open source and algorithms and hence I will be spending most of my summer at Institute of Mathematical Science - Chennai (India). The institute is ready to host me and it  will be helpful in nourishing my knowledge in theoretical computer science.

## **Educational Background** : 
I am a 4th year student of Integrated M.Sc. in Applied Mathematics at IIT Roorkee. It is 5 year integrated course, offering graduate and post-graduate degree in mathematics. Although, I spend most of my time in writing algorithms for various mathematical problems, I love pure maths. Following are some of the courses I had done in my academic curriculum which are directly related to project or will help me understanding basic mathematics behind it.

* Complex Analysis and Partial Differential Equations
* Linear Algebra
* Real Analysis-I ( Riemann integrals, Metric space )
* Real Analysis-II( Riemann Stieltje’s & Lebesgue integrals, Measure theory )
* General Topology
* Mathematical Methods ( Laplace and Fourier Transforms )
* Theory of Partial Differential Equations
* Theory of Ordinary Differential Equations
* Advanced Complex Analysis
* Functional Analysis
      
## **Programming Background** : 
I have been coding since last 2&1/2 years. I like coding for mathematical problems and spend most of my time doing the same. Initially I spent 1&1/2 years coding in MATLAB, before finally switching to Python. After attending 'Sage Days 25' and 'SciPy 2010', I became a big fan of open source and would like to contribute in its progress. Following are the courses I had taken, which gave me a solid foundation in programming : 

* Fundamentals of Object Oriented Programming
* Database Management System 
* Data Structure and Algorithms
* Number Theory		                          
* Abstract Algebra                
* Graph Theory                       
* Discrete Mathematics

Here is the brief description of my project work.

* Algorithms for computing all cliques in undirected Graph.
I did this project in last summer at Indian Statistical Institute - Kolkata. All coding was done in Python.

* Prime-factorization of a given number using concept of trees.
This was a semester long project as a part of academic curriculum. Coding of this was done in C++.

* Implementing numerical methods to solve real life problem using MatLab.
During this, I wrote MatLab programs for elementary numerical analysis methods considering practical level input data size.