## Abstract
Python 3 represents the future of the language. If SymPy is to be used as a library, it will have to be ported to Python 3. In order to accomplish this, a system for automatic testing will need to be established. A robust test system will ensure no regression happen and will ease the maintaining of a dual code-base. After the main porting is done, my goal is to attempt to support alternative Python compilers, to further ensure compatibility and reduce reliance on implementation details. 


## Synopsis

The first priority is to (re)establish a buildbot-based system for automated testing across platforms and Python versions. This will ease current development, as some care already needs to be put into support Python 2.4 - 2.7, and will ensure no regressions happen as the porting commences. Afterward, porting will commence following the steps outlined in [this guide](http://techspot.zzzeek.org/2011/01/24/zzzeek-s-guide-to-python-3-porting/): use the -3 flag to root out obvious issues, and then run the 2to3 tool in a private branch and choose the right method of handling the problems that arise. In parallel, I will attempt to educate the current developers (and GSoC students) on writing Python 3 compatible code during their work, to minimize the chances of problems with integrating new code. I plan to use a dual code-base, which means that the 2to3 tool will be run automatically when the Python 3 version will be built; this is the most practical method of supporting a vast range of Python versions, which is necessary for a library.

After the main porting is completed and any bugs found ironed out, in the remaining time I intend to focus on making SymPy work on alternative Python 3 compilers, such as PyPy, Jython, IronPython. Of the three, PyPy has the most rapid pace of development and will be my first goal. This will eliminate the reliance on some implementation details of the official compiler, which leads to improved cross-platform compatibility and makes the code more robust. 

In essence, my project is focused solely on infrastructure. None of the above-mentioned goals introduce any features at all, and might even make development harder in the short-term (as developers must write code for a dual code base). However, it is my belief that a strong infrastructure is essential for a project, especially a library, and that it will in the long-term help with implementing major features in a safe and, most-importantly, stable manner.

Post-GSoC, I would like to extend the test system to fulfill a benchmarking role, perhaps similar to the [PyPy Speed Center](http://speed.pypy.org/). I will also be available to help with further problems related to Python 3 support (for example, porting the works of other students to have them merged faster) and continue working on alternative compilers, as circumstances permit.

## Deliverables

 * Establish an automated building/testing system. 
 * Port to Python 3, using a dual code base.
 * (time permitting) Work on PyPy compatibility. 


## Schedule

Unfortunately, the beginning of my coding period coincides with start of all of my exams, so during the first two weeks I will not be able work a full 40 hour week. To compensate, I plan on spending more time coding during the community bonding period. As the first part of my work, making a build system, might rely considerably on other people (who will need time to respond), I think this is an acceptable compromise.

**April 25 – May 23 (Community Bonding Period):**

 * Research the buildbot framework, including how it was implemented in the past in SymPy, and get in contact with people who were responsible for it then. Once it gets implemented, I will campaign amongst the community, to increase the range of platforms covered by the buildbot system. 
 * Work on fixing all the warnings that "Python -3" produces, which is the first step towards porting. During this work, I will try to familiarize myself with the code in different parts of SymPy. If required, I will write additional tests to improve code coverage, as this will insure a less-painful transition to Python 3. It will be important to identify the most critical parts of SymPy, as these should be ported first.
 * Further research Python 3 porting; contact various projects for advice or ideas. Notably, I wish to contact the developer of [mpmath](http://code.google.com/p/mpmath/), which was recently ported to Python 3 and might have faced similar problems. Investigate the specific problems related to supporting both Python 2 and 3 in the same code base.
 * Bond with the community: get to know the developers responsible for the major parts of SymPy, so that I know who to turn to if problems arise; educate the current developers and new GSoC students on the good practices related to writing a dual-code base.

**May 23 – June 11 (Official coding period starts):**

 * Complete any leftover tasks, and start work on a Python 3 branch. My plan would be to aggressively push any changes I make upstream, as I expect rapid changes (due to all the students) which will make maintaining a completely separate branch prohibitively time-intensive. Instead of first porting to Python 3, and then trying to "backport" the changes to a Python 2-compatible state, I will constantly use the 2to3 and run from a Python 2 code base. This will make working closely to master easier.
 * Work will continue based on the order of important established earlier.

**MID TERM EVALUATION**

At this point, I expect to have a working Python 3 version of SymPy. If it turns out, this cannot be achieved, I hope to support at least the most critical parts. 

**July 15 – August 22:**

 * Port SymPy to Python 3 completely, if this wasn't previously accomplished. Iron out bugs and encourage extensive testing. If the circumstances allow it, I would work on making an "alpha" release of SymPy, to get testing beyond the developers (which ought to reveal further bugs). 
 * Once the core developers and myself are satisfied that Python 3 support is "rock-solid", I would turn my attention to supporting PyPy. PyPy is my first choice, as it's goals coincide with the design goals of SymPy (just Python), and it's rapid pace of development should make my work easier. Importantly, fast development means that I can submit patches directly upstream, rather than implementing work-arounds. 
 * If it turns out supporting PyPy is easy, I will continue work on further compilers, such as Jython and IronPython. 

## About Me

Name: Vladimir Perić
Student of [Open Informatics](http://informatika.fel.cvut.cz/en/for-students/bachelor-program) at the Faculty of Electrical Engineering, Czech Technical University in Prague.

Email: vlada.peric@gmail.com  / pericvla@fel.cvut.cz
IRC: vperic
Skype: vpericcze

Coding platform: 64bit Linux

I have experience with several programming languages (notably Java, C, Prolog), but I prefer using Python in most projects. Last semester I had a class which focused on solving problems and games, which included implementing the A* algorithm to solve a labyrinth, implementing Alpha-beta pruning for a game of Reversi and similar tasks. We had the opportunity to choose between Java and Python for each project, and this is what finally convinced me that Python is an excellent language: compared to Java, I was able to develop much faster and produced much cleaner code. The performance advantage offered by Java was nullified by me being able to implement a more efficient algorithm. After this course, I began taking a greater interest in Python, particularly the problematic of porting to Python 3.

I have made some minor contributions to open-source software, notably several patches in the Python-based genealogy application [GRAMPS](http://gramps-project.org/). I have experience with git (having contributed a couple of minor patches to the Linux kernel as well) and other useful unix tools. This would be my first major contribution to an open-source project.

My obligatory patch to SymPy was a trivial contribution in eliminating the deprecated dict.has_key(k) construct; it has been merged already and the pull request can be found [here](https://github.com/sympy/sympy/pull/164).