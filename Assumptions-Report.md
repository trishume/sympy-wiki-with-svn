


# About me

I'm an math undergraduate student from Granada's University (Spain). I am fascinated with math, open source and music, so this project matches most of my main interests.

# Introduction

The main goals in my project are to build a new assumption system. By an assumption system I mean a module that can extract conclusions from assumptions and known facts. My module should have the following qualities:

  - It should be out of the core, and the core should not have any dependencies on this.

  - It should be easily extensible.

  - It should have a nice user interface.

  - It should be fast.


# First steps

In the month of march I had some initial code for a new assumption system. It depended heavily on sympy.core.facts and was rather slow, but that served as a model for future work. It already had some nice ideas: all computations where done in modules that got imported at runtime and thus there was no overhead at load time (as opposed to the old system).


# Facing some problems

In the initial implementation of the module is that it made extensive use of sympy.core.facts, and that module was extremely difficult to extend. It is necessary to implement a new logic and facts module. At that point I discussed the problem with Ondrej Certik and he suggested that it would be a nice Summer of Code Project.

# GSoC

The first thing to do was to implement a new logic module. I adapted source code from project aima-python, so initially that went really fast, but it revealed to have some hidden bugs that were very hard to debug. I finally solved those bugs and committed module sympy.logic. We decided then to make sympy release before committing source code of the query module. That was mid June, and I had still some exams. In Spain, academic year ends really late (July).

# Query module

While preparing sympy 0.6.5 relase, I coded the query module. This module is responsible for asking questions about expressions, e.g. Is 2*x even given that x is integer ?. Having a logic module that was solid and clean made this process really fast, although it is quite a big module (+2200 lines).

When the query module was ready to be merged into trunk, I had to opportunity to meat some sympy developers attending EuroSciPy in Leipzip. I had some very interesting conversations regarding user interface, and I decided to change most of the user interface.

Back home, I made the changes we discussed in Leipzig and [http://fseoane.net/blog/?p=161 merged in the query module]. 

# Refine module

Shortly after that, [http://fseoane.net/blog/?p=162 I began working on the refine module]. This module makes simplifications on expressions based on assumptions. It is the last step that we need to finally remove the old assumption system.

After this was committed, we had implemented all that the old system was able to do (and some more things). However, there were some problems. Some of the goals listed in my introduction were not met: It was horribly slow!!

# Speed improvements

The logic module proved to be the real bottleneck for the query and refine module. Making logic work internally with instances of sympy.Symbol was making the whole system horribly slow.

Solution is simple, the logic module and concretely the DPLL algorithm should not use symbols internally, but some lighter structures. Integers where perfect for my purposes.

The following week, I managed to recode the DPLL algorithm to use integer representation and avoid the conversion to integer representation in ask(). The speed gains where far beyond what [http://fseoane.net/blog/?p=164 I had expected].

# Future work and removing the old assumption system

All of what was proposed in my application was done, with one notable exception: removing the old assumption system. Despite some progress, I could not remove the old assumption system without breaking lots of things, so I am still working on that in my [http://fseoane.net/cgi-bin/gitweb.cgi?p=sympy.git;a=shortlog;h=refs/heads/remove_assumptions git branch]. This is a major work that still remains to be done and that affects to all sympy's community.

There is also some work to be done in performance: the logic module can still be improved, some ideas are listed in doc/src/modules/logic.txt

# Conclusions

I had a great time working on this project. The whole community was great responding to questions and patches both in IRC and mailing list. Also, knowing them in person was one of the best experiences in this summer.

There were also some difficult moments. For a number of reasons, some weeks I could not concentrate on this project 100% and I wish I would have had more time to work on this. So my advice to new students is: don't overbook yourself!.