Hello.

I know this page is kinda drafty and sketchy, but it'll have to do for now.
I'm mainly uploading it in hope of getting some feedback (via any of the means below) before I finalize my application during the submit period.

# Personal details
**Name**: Shai Wyborski, though friends often call me 'Deshe'.

**Current Institute**: The Hebrew University of Jerusalem institute, Edmund Safra campus for mathematics and exact science.

**Enrollment**: Advanced undergrad in both mathematics and computer science.

## A little bit about myself and my relevant experience

Ever since I was a child I was inclined towards mathematics. Life circumstances made me part with this passion during my youth years, but as I started gaining higher education it came back with a vengeance!
As I got to the Hebrew university I already had some head start on account of some classes I took in the open university. I applied this advantage taking second year classes and overburdening myself with CS classes as well.

I managed to end my first year with honors and decided to attempt jumping ahead again.
Two notable classes I'm taking this semester are the grad level course "topics in complex analysis" given by prof. Genady Levin, and guided reading of Cromwell's "Knot and Links" under the guidance of prof. [Ruth Lawrence](http://en.wikipedia.org/wiki/Ruth_Lawrence).

My current day job and project is at the [continuous symmetry measure](http://www.csm.huji.ac.il/new/) laboratory, where, under the supervision of prof. [David Avnir](http://chem.ch.huji.ac.il/avnir/), I develop (from existing, yet quite obsolete, C code) a tool for performing calculations on models of molecules. The proposed design is a set of C++ calculations which are bound together by python scriptology, and it is both mine and my employer's ambition to release it into the world as an open source project.

I've also been playing guitar for about 13 years now, and I can play some mean blues.

## Relevant classes and personal experience

### Classes:

 - Object Oriented Programming, Spring 2010

 - Data Strucutres, Spring 2010

 - Complex functions and their applications, Spring 2010

 - Computer System workshop from NAND to Tetris, Spring 2010

 - Workshops in C and C++, summer 2010

 - Set Theory, fall 2011

 - Advanced Calculus, fall 2011

 - Algebraic Structures, fall 2011

 - Operating Systems, currently

 - Topics in Complex Analysis, currently

 - Introduction to topology, currently

 - Advanced Calculus II, currently

 - Knot theory (guided reading), currently


### Personal experience:

 - I've been a local Bash goto-guy for a while now, which (in my mind) means that, unlike most "university programmers", I've got some broad base in scripting and working with live consoles. This came in handy when I taught myself Python and I'm positive it would prove itself worthwhile if I'll have the chance to work on this project.

 - I've been monkeying around (to varying extents) with various languages and environments including (but not limited to) Ruby, Haskell, Pascal (back when it was relevant and I didn't hit puberty yet) and Lua.

 - I can type with the keyboard behind my head.

**Please do note** however, that the GSoC timeline isn't very congruent with the local academic schedule, so, if you choose to accept me, my work output will be on the slow side for the first couple of weeks (which coincide with my finals). I hope this application will show that I'm dedicated enough you could trust me repay the debt during the rest of the GSoC period (and in the month after, during which I'll have nothing to do, as the lack of congruence I mentioned before leaves a month long gap to be filled.

# Project proposals

I have no idea if the "appropriate" thing to do is to write a different page for each proposal. My spider senses always encourage me to avoid copypasta, so I'll stick to this line with a dual proposal page.
I'm also open for combining the two, or partner up, or whatever works for you guys.

If I'll be put in a position where I need to choose one of the two, I'd go with the second one.

## Complex integration

It's well established that the real line is a special case of the complex plane. It's also known that when you limit yourself to that subset things get awkward.

Moving beyond the real line to the extended complex field allows us to better understand what was once narrowed to "discontinuity points" as singularities, their classifications to poles and essentialities, and their deep connection they have to vanish points via the argument principle.

The classical research (which I'm sure you're all familiar with) has led to the development of many powerful tools. One of which is Cauchy's integral formula and it's resulting residue calculus, and another is the generalized power series expansion (or Laurent series).

Integrating both these tools in a symbolic manner into SymPy will not only extend it's integration capacities by a whole dimension, but also add new tools to calculating definite integrals on the real line (especially proper integrals, where there are no singularities on the integration curve.)

I don't have the experience to portray any detailed work plan which I'd feel isn't too Hard (or Hard enough!), but I guess the work process will be along these lines:

 - Learning phase, where I inquire the structure and style of SymPy and structure the following in a more specialized manner.
 - Develop a tool to reduce the value of curve integrals on the complex plane to definite integral (should be quite easy and straightforward).
 - Incorporate Cauchy's formula (at least in a symbolic manner) into SymPy
 - Develop a tool to find (easy) and classify (not so easy) singularities of a given function
 - Write a solver for calculating the argument integral (f' over f) over a closed line given the singularities of a function within the bound region (which will be calculated with the previous tool).
 - Write a tool, that, given a definite real integral, tries to find an optimal closed curved along the complex plane to apply Cuachy's theorem on. The trick is to find one whose total integration value is easy to calculate using the argument principle, and it's integral over the part which doesn't coincide with the given segment can be calculated as easy as possible. This is probably the hardest battle in the conquest.
 - Optimize, add usage of the approximation theorem, maybe some other techniques.
 - As long as we're on the complex plane we might as well start working on a tool for analytic continuations (hopefully this could be my project for GSoC 2012 ;) ).


## Set theoretical entities

It's needless to explain how meaningful set theory is to contemporary mathematics. This is why I believe (and it's prevalent in my current project, see above) that intuitive support for set theoretic notions is very lacking in todays current applications.

From what I've seen in the [set theoretic code](https://github.com/sympy/sympy/blob/master/sympy/core/sets.py), not only that hardly any properties are defined, but those who are defined are mostly properties of intervals! Above this are some properties of ordered set, and then one or two properties of measurable sets.

According to my philosophy these should not be a part of the property of a set at all.
Of course, it makes perfect sense to build on sets, to create hierarchies such as set -> ordered set -> interval, or set -> measurable set -> border of an integrable set in R and so on.

But the set notion itself has so many useful and interesting features that could and should be taken into consideration.

I suggest the following work oredr:

 - First, snoop around, get acquainted.
 - Having done that, clean up the notion of a set from any implementation specific properties (keeping them on the side for steps to come, of course).
 - Implement basic operations that aren't already there. Such as simplification of a set theoretic expression/equation.
 - Define and implement a relation on a set, obviously with special emphasis on functions, equivalence relations and partial order.
 - Implement actions on relations: Completing a relation to a minimal equivalence relation, combining two equivalence relations into a minimal equivalence relation, etc. etc. etc. (this list is quite endless).
 - Implement cardinalities, alephs and so on, and cardinal arithmetics.
 - Implement more advanced set operations (power set, for example).
 - Define a notion of operations, implement some basic operations.
 - Define and implement some more complicated set operation, such as infinite (and uncountable) unions and intersections.
 - This is where it gets wild. Given that the previous steps were thoroughly accomplished, it's possible to define just about anything in a set theoretic manner. We could start with groups, fields, rings and so on. From the other way around it would be easy to define topologies, and I guess this could go even further into homotopies, homologies and so on. Essentially everything can be formalized now.
 - On the other hand, it's always possible to implement some more advanced properties. Such as finding a maximal chain, Writing a tool that checks if some set satisfies Zorn's lemma (I doubt that's even possible), implementing ordinals and order arithmetics, transfinite recursion and so on.

This is really an endless climb and I'm sure only a portion of it is enough to fill an entire GSoC project.

### Contact information

Name: Shai 'Deshe' Wyborski

Gmail/G-chat: Shai.Wyborski@mail.huji.ac.il

Cell phone: (972) +50 699-4080

IRC handle: StrangeLoop on Freenode
