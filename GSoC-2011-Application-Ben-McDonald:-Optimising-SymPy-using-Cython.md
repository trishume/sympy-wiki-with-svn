GSoC 2011 Application Ben McDonald: Optimising SymPy using Cython
=================================================================

Abstract
------------------
The SymPy linear algebra library is extensive and has many tools. The extensive tool set can be used for a large range of problems (signal processing, physics, computational chemistry). Yet the application of SymPy to problems can be limited by the slow performance of the CPython interpreter it makes use of.

This project aims to unshackle SymPy from the slow CPython compiler so it can be applied to computationally intensive problems such as physics simulations and image processing. This project will make use of the Cython language, which allows a compiler to generate efficient C code from Python code. The generated code could potentially increase the performance of SymPy 100-1000 times [1].
1. http://thread.gmane.org/gmane.comp.python.cython.devel/4602/focus=4619

Deliverables
------------------
 * Increase the performance of SymPy
 * Create tests and benchmarks for compiled Cython code.
 * Create a mature build system for Cython in SymPy that will produce binaries on all major platforms.

In addition to improvements to SymPy performance, I hope to produce a lasting infrastructure to compile Cython code on SymPy. This infrastructure will be able to compile Cython code, test and distribute it. This will allow the painless addition of Cython code to the SymPy project in the future.


Schedule
------------------
I am able to commit to 40 hours per week during the Google Summer of Code period. I will also be committing to 6 hours per week tutoring Python and algorithm classes during this period.

**Before April 25:**

 * Familiarize myself with SymPy’s code, community and community procedures.
 * Familiarize myself with SymPy’s currently Cython usage and build system.
 * Research ways to add Cython support (headers, decorators, etc.).

**April 25 – May 23 (Before the official coding time):**

 * I will stay in constant contact with my mentor and the SymPy community using email, voice chat and instant messaging. I will participate in community discussions during this time on SymPy’s usage of Cython, SymPy’s build system or on SymPy’s performance. This will let become integrated in the community and give me an understanding of the current direction of SymPy.
 * I will make use of this time to prioritise SymPy modules for optimisation. I will weigh community opinion, module dependence [], module performance and stability of a module’s code to build a case for a prioritised list of modules to be optimised. To do this, I will search through the Google Groups page and the FreeNode logs for mentions of performance and Cython. I already have examples where SymPy members have expressed the need for performance improvements in certain modules []. 
 * Lastly, I will report my approach of optimisation and prioritised list of modules to be optimised to the SymPy community. I will then review the  feedback.

**May 23 – June 11 (Official coding period starts):**

 * Write Cython code for chosen SymPy modules.
 * Compile Cython and test code as I go.
 * Write tests for Cython support, include benchmarks so performance improvements can be measured.
 * Documentation of my implementation will be added to the SymPy wiki. This information will be useful to other developers writing Cython for SymPy.
 * I will tweet completion of milestones,  challengers encountered and comments as I go.

**JULY 15th MID TERM EVALUATION**

**July 15 – August 15:**

 * The second half of the project will focus on code stability. I will test the build system's ability to produce code that passes all test and to compile code on all major platforms.
 * I will estimate the progress I can make in completing the optimisation of modules and focus on completing modules so none are left nearly finished.


**July 15 – August 15:**

 * Rigorous testing and bug fixes.

**August 15– August 26:**

 * Documenting, testing and cleaning up of code.
 * Complete documentation of Cython’s usage in SymPy on the wiki.

If time permits
------------------
Create code samples that make use of an optimised SymPy. For example, use PIL and an optimised SymPy to perform image processing. I have worked as a researcher in the area of computer vision and I could use my experience to enable computer vision tasks in Sympy. Matlab is capable of computer vision and image processing tasks. We could also have the same in an optimised SymPy.

Coding Skills
------------------

Tutor Python in undergraduate classes
...

Relevant Personal Projects
------------------
_Python Shell for Google Chrome_

Relevant Languages: Python, SymPy

Link: [[https://chrome.google.com/webstore/detail/gdiimmpmdoofmahingpgabiikimjgcia]]
***

_A silhouette based technique for locating and rendering foot movements over a plane_

Relevant Languages: C++

Link: [[http://scholar.google.co.nz/scholar?hl=en&q=A+silhouette+based+technique+for+locating+and+rendering+foot+movements+over+a+plane+Ben+McDonald&btnG=Search&as_sdt=0%2C5&as_ylo=&as_vis=0]]

TODO
---------------
* Submit a patch

Optimising SymPy using Cython
------------
The core is being updated so work depended on it is being postponed until the replacement core is available [http://groups.google.com/group/sympy/browse_thread/thread/6cf7ece92746bcdc].
Other parts of SymPy may be good candidates for optimisation logic code (like the SAT solver), matrices, polys (work already started), physics [http://groups.google.com/group/sympy/browse_thread/thread/6cf7ece92746bcdc]

The cythonized decorator is currently being used in the polys module
An alternative methods is to use Cython header files (.pyx). See http://wiki.cython.org/pure

### Community Discussion on Cython
Decorators and header files have both been suggested. http://groups.google.com/group/sympy/browse_thread/thread/5eccee5e2d02aa1a/d6671be18f5c11ab?lnk=gst&q=Cython#d6671be18f5c11ab
Cython improves performance significantly http://groups.google.com/group/sympy/browse_thread/thread/5eccee5e2d02aa1a/d6671be18f5c11ab?lnk=gst&q=Cython#d6671be18f5c11ab
sympy.physics requires increased performance http://groups.google.com/group/sympy/browse_thread/thread/5eccee5e2d02aa1a/d6671be18f5c11ab?lnk=gst&q=Cython#d6671be18f5c11ab


http://groups.google.com/group/sympy/browse_thread/thread/aa3f4263bc3f7e23

### Complexities
Cython compiles to platform dependent binaries. SymPy with Cython optimisation will need to be build on the platform it is to be run on, or binaries for each platform will need to be distributed with SympPy.


About Me
------------------
Name: Ben McDonald

Computer Science student completing my Master’s thesis at the University of Canterbury, New Zealand. 

Email/GTalk: mcdonald.ben@gmail.com

IRQ: BenM on FreeNode

Skype: mcdonald.ben

Google Groups Profile: [[http://groups.google.com/groups/profile?enc_user=XdP78RYAAAC340FUqOWWVVJI19mL7Wvio4cocwWvDVg2RHsu8f1bCg]]
