



# About Me
  My name is Christian Muise, and I am currently starting my fourth year of graduate school at the University of Toronto in the PhD program for Computer Science. My research focuses on Automated Planning and Satisfiability. I have a strong interest in various forms of logic, supported by a number of graduate courses and specific research projects.


# Introduction
  For my GSoC project, I was tasked with speeding up the new assumption system in !SymPy to a workable state. This could (roughly) be put into three categories:

  * Removal of the old assumption system.
  * Improving the SAT Solver
  * Adding Knowledge Compilation

  While the first point was primary geared towards learning the !SymPy system, it hasn't made it to the main part of !SymPy yet. The other two points have recently been pushed into the !SymPy code-base, and will be part of the next release of the system.


# The GSoC Project

## Removal of Old Assumptions
  By a decent margin, this was the most time consuming task, and likely the one that will see the least contribution to !SymPy's code-base. The conversation as to how best strip out !SymPy's old assumptions continues, and my foray into the mess can be found in [http://github.com/haz/sympy/tree/disconnect-assumptions [these]] [http://github.com/haz/sympy/tree/disconnect-assumptions-2 [two]] branches (the latter being the most recent and promising).

  Despite the possibility of this code not making it into the trunk, this task served as a vital in-depth introduction to the !SymPy system as a whole, and gave me a far greater understanding of !SymPy in general than I could have hoped by simply browsing the code-base. It also brought some of the issues with the assumption system to the forefront for discussion, which will hopefully continue beyond the bounds of the SoC timeline.

## SAT Solver
  Probably the most effective use of my skills, I implemented a new SAT Solver from the ground up for !SymPy. It has an [http://haz-tech.blogspot.com/2010/07/clause-learning-and-heuristics.html effective heuristic], the [http://haz-tech.blogspot.com/2010/07/clause-learning-flunk.html ground work] for clause learning, and advanced SAT solver [http://haz-tech.blogspot.com/2010/08/whos-watching-watch-literals.html data structures]. [http://github.com/haz/sympy/tree/sat-solver This] is the branch, and here's how it stacks up against the old DPLL solver (note that the y-axis is log scale):

http://4.bp.blogspot.com/_DvrW_QLstcQ/TF3S_KdyDJI/AAAAAAAACLU/9qhiJV4q0CM/s1600/dpll.png

## Knowledge Compilation
  This here is a fuzzy term used to describe pre-computation that helps in online queries. There's a large body of research when considering queries in boolean logic, and I've had some experience dealing with such things. In fact, [http://github.com/sympy/sympy/blob/master/sympy/assumptions/ask.py#L214 [this line]] in !SymPy could be considered something along the lines of knowledge compilation for the assumption system -- it pre-computes the CNF of the known rules so that queries to the ask function don't need to compile them every time for the logical inference.

  Well we can take this a step further. And that's precisely what [http://github.com/haz/sympy/tree/atms [this]] branch does. One thing it does is [http://github.com/haz/sympy/blob/atms/sympy/assumptions/ask.py#L253 [explicitly store]] the CNF so it's not computed at import time. This is accomplished by copying the output of [http://github.com/haz/sympy/blob/atms/sympy/assumptions/ask.py#L180 [this function]] to the ask.py file. So now we have a simple CNF ready to go whenever the SAT solver is invoked to answer an ask query.

  Beyond this simple compilation, there is more we can do to completely avoid calling the SAT solver -- if we can answer the query quickly, there's no sense in calling the full DPLL algorithm. This is accomplished by pre-computing all of the implications from single assumptions -- see [http://github.com/haz/sympy/blob/atms/sympy/assumptions/ask.py#L280 [this dictionary]]. An entry such as `Q.imaginary: set([Q.complex, Q.imaginary])` should be read as, "If we know it's imaginary, then we know it must be complex and it must be imaginary".

  Simple, I know, but it saves us from calling a sat solver simply to find out that a variable is imaginary if we assume it's imaginary ;). Well maybe that would be captured by [http://github.com/haz/sympy/blob/atms/sympy/assumptions/ask.py#L101 [this line]], but successive implications are all compiled down, so this does save you a fair bit. How much? Well running 'bin/test sympy/assumptions' on the trunk calls the SAT Solver 811 times while this branch cuts it down to a mere 258. Granted we now have a faster SAT solver, but why use such a big hammer when the query is simple?

  The method also captures things like `ask(x, Q.imaginary, Assume(x, Q.complex, False))` -- if Q.imaginary was true, then Q.complex must be true (because of the lookup we pre-compiled), and since we know this isn't the case, we can conclude that x is not imaginary as well. How are these facts compiled? Well we do the exhaustive checks with the SAT solver ([http://github.com/haz/sympy/blob/atms/sympy/assumptions/ask.py#L195 [this line]]), and dump the results just like the pre-computed CNF.

# Working with !SymPy
## Communication
  The !SymPy organization communicates primarily through their Google Groups lists (one for patches and one for other discussion), on their IRC channel, and on the specific issues found in the Google Code project. Over the course of the summer, the different mediums served specific purposes for me:

  * The Google Groups list are a great place to engage with the general !SymPy developer community. If you have changes to be committed, or high level questions that impact the entire project (e.g. dropping support for Python 2.4), then this is the place to go.
  * The IRC channel served as a great resource for getting over small roadblocks when developing for !SymPy. Small questions about how the system works are best placed here.
  * Issue discussion is great for bringing up flaws with !SymPy, even if you aren't going to push forward in fixing them. They represent a fairly extensive view of what is currently being worked on and discussed. A lot of the detailed problem solving discussion happens here.

## Version Control
  Learning Git was a bit of an undertaking, but fun and rewarding. Unfortunately, early on I (for some unknown reason) pulled in a commit on another branch into the master I forked for everything. This caused some headaches on the merger of my GSoC work into the !SymPy trunk. As such, I'd suggest this as a more reasonable workflow:
  * Fork the sympy/sympy project on !GitHub (found [http://github.com/sympy/sympy here]).
  * Add sympy/sympy as a remote so you can continuously pull in new changes to the trunk.
  * When it comes time to send a pull request, create a branch from sympy/sympy:master, and cherry-pick all of the commits you want to submit.

  This would keep things very clean and avoid any nasty merge stuff in the pull request. It may be a bit more tedious, but it definitely would have saved me on my GSoC work.

# Conclusions and Future Work

My experience with !SymPy was a great one for a number of reasons. The community is great, the project directly coincides with my interests, and my contributions have already made it into the project's core.

Moving forward, I hope to implement a number of suggestions that came out of reviews on my summer's work. First and foremost I hope to address the removal of the old assumption system so my work will actually be used by default when assumptions are invoked in the !SymPy system. With any luck, I'll have my !SymPy skills up to snuff by next summer to apply as a mentor for the next round of students coming by.