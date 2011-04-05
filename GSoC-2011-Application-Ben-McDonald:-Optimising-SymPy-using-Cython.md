## Abstract

>The SymPy linear algebra library is extensive and has many tools. The extensive tool set can be used for a large range of problems (solving linear systems, physics, statistics problems, ...). Yet the application of SymPy to problems can be limited by the slow performance of the CPython interpreter it makes use of.

>This project aims to unshackle SymPy from the slow CPython compiler so it can be applied to computationally intensive problems such as physics simulations and image processing. This project will make use of the Cython language, which allows a compiler to generate efficient C code from Python code. The generated code could potentially increase the performance of SymPy 100-1000 times [[ref](http://www.google.com/url?q=http%3A%2F%2Fthread.gmane.org%2Fgmane.comp.python.cython.devel%2F4602%2Ffocus%3D4619&sa=D&sntz=1&usg=AFQjCNFHDU86V04yV21-UTQg-efARGkuUg)]. 
## Deliverables

 * Increase the performance of SymPy.
 * Add Cython code to chosen modules.
 * Create tests and benchmarks for compiled Cython code.
 * Create a mature build system for Cython in SymPy that will produce binaries on major platforms.


>In addition to improving to SymPy performance, I hope to produce a lasting infrastructure to compile, test and distribute Cython code on SymPy. Such an infrastructure will allow the painless addition of Cython code to the SymPy project in the future.
## Schedule

I am able to commit to 40 hours per week during the Google Summer of Code period. I will also be committing to 6 hours per week tutoring Python and algorithm classes during this period.

**Before April 25:**

 * Familiarise myself with SymPy’s code, community and procedures.
 * Familiarise myself with SymPy’s current Cython use and build system.
 * Research ways to add Cython support (headers, decorators, etc.).

**April 25 – May 23 (Before the official coding time):**

 * I will stay in constant contact with my mentor and the SymPy community using email, voice chat or instant messaging. I will participate in community discussions during this time on SymPy’s build system, use of Cython or performance. This will allow me to become a part of  the community and give me an understanding of the current direction of SymPy.
 * I will make use of this time to prioritise SymPy modules for optimisation. I will weigh community opinion, module dependence, module performance and stability of a module’s code to build a case for a prioritised list of modules to be optimised. To aid my understanding of community opinion, I will search through the Google Groups page and the FreeNode logs for mentions of performance and Cython. I already have examples where SymPy members have expressed the need for performance improvements in certain modules [[ref](http://www.google.com/url?q=http%3A%2F%2Fgroups.google.com%2Fgroup%2Fsympy%2Fbrowse_thread%2Fthread%2F5eccee5e2d02aa1a%2Fd6671be18f5c11ab%3Flnk%3Dgst%26q%3DCython%23d6671be18f5c11ab)].
 * Lastly, I will report my approach of optimisation and prioritised list of modules to be optimised to the SymPy community. I will then review the feedback.

**May 23 – June 11 (Official coding period starts):**

 * Write Cython code for chosen SymPy modules.
 * Write tests for Cython support, including benchmarks to measure performance improvements.
 * I will tweet completion of milestones, challenges encountered and comments as I go.

**MID TERM EVALUATION**

**July 15 – August 15:**

The second half of the project will focus on code stability.

 * I will estimate the progress I can make in completing the optimisation of modules and focus on completing modules so none are left nearly completed.
 * Compile and test code on major platforms
 * Document my Cython implementation on the SymPy wiki. This information will be useful to other developers writing Cython for SymPy.
 * Work with the Cython open source project to fix bugs and optimise code if necessary.
 * Rigorous testing and bug fixes.

**August 15– August 26:**

 * Testing and cleaning up of code.
 * Completing documentation.

## Cython


#### HOW CYTHON BENEFITS SYMPY


1. Improves performance.

1. Generates static code that finds type errors.
1. Adds functionality to the Python language (calling C code, constants).

>Also, Cython does not require any rewriting of Python code. This is beneficial in two ways. First, this leaves a pure Python base that can be ported to other Python platforms such as Jython, IronPython, and Google App Engine. Second, it does not bind the original code to Cython. If SymPy moves to other optimisation techniques, there are no development costs to de-couple SymPy from Cython.   

#### CURRENT STATE OF CYTHON IN SYMPY

>Cython is currently used only in the poly module. The poly module makes use of the ‘cythonized’ decorator from the utilities module, which declares specified local variables as ‘cython.int’ types. This implementation is efficient in increasing performance but only uses a subset of Cython's features.

>An alternative to decorators are Cython header files (.pyx). See http://wiki.cython.org/pure. Decorators and header files have both been suggested by SymPy members [[ref](http://www.google.com/url?q=http%3A%2F%2Fgroups.google.com%2Fgroup%2Fsympy%2Fbrowse_thread%2Fthread%2F5eccee5e2d02aa1a%2Fd6671be18f5c11ab%3Flnk%3Dgst%26q%3DCython%23d6671be18f5c11ab)].

>SymPy’s core module is being updated so work depended on it is being postponed until the replacement core is available [[ref](http://www.google.com/url?q=http%3A%2F%2Fgroups.google.com%2Fgroup%2Fsympy%2Fbrowse_thread%2Fthread%2F6cf7ece92746bcdc)]. Other parts of SymPy may be good candidates for optimisation (logic code, SAT solver, matrices, polys, physics) [[ref](http://www.google.com/url?q=http%3A%2F%2Fgroups.google.com%2Fgroup%2Fsympy%2Fbrowse_thread%2Fthread%2F6cf7ece92746bcdc), [ref](http://www.google.com/url?q=http%3A%2F%2Fgroups.google.com%2Fgroup%2Fsympy%2Fbrowse_thread%2Fthread%2F5eccee5e2d02aa1a%2Fd6671be18f5c11ab%3Flnk%3Dgst%26q%3DCython%23d6671be18f5c11ab)].

#### Priority of Modules to Optimise

#### Cythonizing Methods

# About Me

>Name: Ben McDonald

>Computer Science student completing my master’s thesis at the University of Canterbury, New Zealand.

>Email/GTalk: mcdonald.ben@gmail.com

>IRQ: BenM on FreeNode

>Skype: mcdonald.ben

>Google Groups Profile: [link](http://www.google.com/url?q=http%3A%2F%2Fgroups.google.com%2Fgroups%2Fprofile%3Fenc_user%3DXdP78RYAAAC340FUqOWWVVJI19mL7Wvio4cocwWvDVg2RHsu8f1bCg)

>Coding platform: Ubuntu distribution called lubuntu with Wing IDE or Windows 7 with notepad++

>Python is currently my language of choice. I use Python in my studies and also tutor first-year university Python. I authored the [Python Shell for Google Chrome](http://www.google.com/url?q=https%3A%2F%2Fchrome.google.com%2Fwebstore%2Fdetail%2Fgdiimmpmdoofmahingpgabiikimjgcia) that allows you to execute Python code in a drop-down console in Google Chrome. The shell also includes the SymPy module so that calculations can be done in your browser. People spend more time in their browser now days  and this shell allows quick access to Python and mathematics tools.

>I would like to be active in one of the open source project I frequently make use of. Large projects can be daunting to get your head around and require time, which is not always available, to learn a code base. I hope that my participation in Google Summer of Code will allow me the time to understand the SymPy project’s structure and to become a contributing member of this open source project. I have an enthusiasm for learning and hope to become a better programmer through working with a knowledgeable community.

>I have an interest in the project to optimise the core using Cython because it is a technique that I found useful in my own Master’s project. Cython allowed me to increase the performance of my code while leaving the original Python code unchanged. I added Cython headers (.pyx) to modules to allow the Python code to be converted into C++, adding significant performance, while not changing the Python modules, leaving a portable, pure Python base. This technique would be useful to any software library which requires processor/memory intensive methods.

>I am a dedicated programmer. Programming is a useful tool to build the software that interests me. The challenges in solving complex problems is what keeps me interested and I am passionate about the things I can create with computer code.

#### Code patches

 * Working on [Issue 834](http://www.google.com/url?q=http%3A%2F%2Fcode.google.com%2Fp%2Fsympy%2Fissues%2Fdetail%3Fid%3D834)


## Relevant Personal Projects

#### PYTHON SHELL FOR GOOGLE CHROME

Online Python shell for the Google Chrome browser.

Relevant Languages: Python, SymPy

[Link](http://www.google.com/url?q=https%3A%2F%2Fchrome.google.com%2Fwebstore%2Fdetail%2Fgdiimmpmdoofmahingpgabiikimjgcia)
#### A SILHOUETTE BASED TECHNIQUE FOR LOCATING AND RENDERING FOOT MOVEMENTS OVER A PLANE

A project to locate and render an athlete's foot placements using a static camera.

Relevant Languages: C++

[Link](http://www.google.com/url?q=http%3A%2F%2Fscholar.google.co.nz%2Fscholar%3Fhl%3Den%26q%3DA%2Bsilhouette%2Bbased%2Btechnique%2Bfor%2Blocating%2Band%2Brendering%2Bfoot%2Bmovements%2Bover%2Ba%2Bplane%2BBen%2BMcDonald%26btnG%3DSearch%26as_sdt%3D0%252C5%26as_ylo%3D%26as_vis%3D0)


#### Code Examples
 1. [Optimised Rectangle class](https://gist.github.com/900337)
 1. [Optimised Color class](https://gist.github.com/900332)