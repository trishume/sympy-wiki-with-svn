# Expanding on the ODEs
##Abstract

ODEs have various applications in the engineering and scientific communities. Currently, Sympy's ODE
capabilities are lacking and incomplete. Further, it is currently unable to solve systems of ODEs. And lastly, use of the methods already in place is not quite user-friendly. This summer, I would like to develop an ODE class for Sympy that takes the arguments needed to solve an ODE, organizes the information, and works with the methods of the ode module to get the solution when necessary. Whilst creating this class, I would like to work on and expand the ode module capabilities, and implement the solving of basic systems of ODEs.

##About Me

Name: Gregory Ksionda  
School: University of Arizona  
Email: ksiondag846@gmail.com  
IRC handle: ksiondag (freenode authenticated)  
Phone: (520) 576-8331  

### Background
I am currently in my junior year studying computer engineering. Math-wise, I have learned up to undergraduate differential equations which includes knowledge of linear algebra, integration, ODEs, and PDEs. In programming, I have taken classes using the C, Java, and Python languages. The C class was an introduction to programming, the Java an introduction of object-oriented programming, and the Python class about solving complex mathematical problems (via python-xy).

Most of my experience with CAS has been through the use of MATLAB in various classes. Recently, I have had some exposure to Sage.

### My Programming Experience

The languages I code in include C, Java, and Python (for current project purposes) as well as MIPS, C++, and Verilog (still learning the languages). C is used in the programming of a micromouse via MPLab on Windows XP, Java for the creation of a game via Eclipse on Mac OS X, and Python for various all-purpose work (calculating, figuring out problems, working on new programming ideas) lately written via vim on Ubuntu Linux.

## Support

Currently ironing out issue 2068 [0] with pull request 204 [1].

## The Project

Simply put, during the summer I would like to implement a ODE class in Sympy.

This class will have a similar function to that of the Integral function already provided in Sympy. Upon creation, ODE will be fed the differential equation or a system of differential equations, the dependent variables in the equation, and the independent variables in the equation, with added possible options of initial conditions and the choice of calculated or exact answers.

### Qualifications

I have had two semesters worth of undergraduate differential equations education, which taught the basic problem-solving skills for application towards ordinary differential equations. From finding the homogeneous solution, to the use of variation of parameters, to the use of eigenvalues and eigenvectors to solve systems of ODEs. These basics, I believe, provide a solid foundation to begin the development of an ODE class as well as give me a starting point to dissect and absorb the ode module code.

### Basic Timeline

#### Before the summer coding begins

I will review and master the relevant content already learned from the mentioned classes through rereading the books and redoing various problems. At the same time, I will familiarize myself with the Sympy ode module, looking for gaps in its methods that I can fill, and finding gaps in my knowledge I need to research. I also plan to gain more intuitive knowledge of several of the classes on Sympy already (certain significant ones being Integral for structural understanding; Symbol, Matrix, and mpmath.odefun for usage understanding). I will do this via issue tracking and working on small snippets of the Sympy code.

#### During the summer coding

I currently have no other work or educational plans for the summer of 2011. I am fully willing and able to work 40+ hours per week on this project. Though every summer I tend to do a small amount of traveling (to visit friends and family), there is always Internet connection where I go and generally the people I visit have full-time jobs and school giving me ample time to work.

#### The plan  

May 24th - 30th:  
Acquire a more complete understanding of the ode module, checking its completeness against that of Maple, Mathematica, etc. Cross-check other python based software (Sage, python-xy, scipy) for their means of usage. Get a good idea of what the ODE class would be able to use, and what missing methods would be necessary for a more useful class. Consider the methods by which ODEs are set up and solved in other languages, and how the user may want them to be set up.

May 31st - June 8th:  
Begin design for setup of ODE class. Examine the possible means of sending the ordinary differential equation information and the form the data can take itself. Consider implementation of dy(x)/dx = A*y(x) + B*g(x) where y and g are eigenvectors (and A, B are matrices), and planning the implementation of solving systems of ODEs.

June 8th - June 15th:  
Begin having ODE class interact with ode module. Implement classify_ode, ode_simp, ode_sol_simplicity, dsolve, etc. as per appropriate.

June 16th - June 23rd:  
Have minimal implementation of ODE setup and basic solving. Have working solver method that outputs the given ODEs solution (much like Integral's doit).

June 24th - June 30th:  
Whilst working on gaining increasing functionality of basic ode solver methods, begin implementation of solving systems of ODEs.

July 1st - July 8th:  
Have ODE capable of outputting solutions to basic systems of ODEs, as well as have it output itself when it can not find a solution.

July 9th - July 16th:  
Work on expanding to full usage of ode module, and/or expanding the type of problems ode can handle.

July 17th - July 24th:  
Work on expanding possible ODE solution output for homogeneous, particular, and initial conditions.

July 25th - July 31st:  
Have ODE capable of outputting homogeneous, particular , and initial condition solutions.

August 1st - August 7th:  
Expand tests of ODE class and ode module significantly to shake out all the hiding bugs.

August 8th - August 15th:  
Run through and polish code. Expand tests to the limits of the code. Clearly list what ODE class/ode module currently can and can not do.
   
August 16:  
Submit completed code of ODE class and expanded ode module

#### Post Summer of Code
After the summer session has ended, assuming all has gone well, I would like to continue expanding the usability of the code, probably at a much slower pace. Perhaps I could work on implementing numerical solutions to ODEs given that have no found solution.

##Links  

[0] http://code.google.com/p/sympy/issues/detail?id=2068  
[1] https://github.com/sympy/sympy/pull/204