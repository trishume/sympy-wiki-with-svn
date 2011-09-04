#About Me#
My name is Saptarshi Mandal. When GSOC 2011 started I had graduated from IIT Kharagpur with a degree in Maths and Computing. My project involved setting up a combinatorics branch for Sympy.

#Introduction#
The goal of the project was to mimic the various capabilities of Combinatorica. Most of the functionality involving elementary combinatorial objects such as Permutations, Partitions, Subsets, Gray codes and Prufer codes are complete. The project is has now evolved into an excursion in computational group theory. Using the Permutations infrastructure, various routines from computational group theory are to be implemented. Additional combinatorial objects will continue to be added as necessary.

#GSoC Project#
Most of the code resides in sympy/combinatorics with Residue groups having been implemented in sympy/ntheory and some generational algorithms that have been incorporated in sympy/utilities.

I will attempt to give a brief description of the functionality that has been implemented.
For references, you can refer to the doctests or the blog I maintained during the GSoC: http://saptman.wordpress.com/

##Permutation##
This was the first thing that I started working on for the project. Permutations was important to implement because it would form the base of the Group theory module to be implemented later on.
Standard functions such as ranking, unranking and various operations have been implemented. Various distances have also been implemented.

##Subsets and Gray code##
This module has undergone several revisions. Some of the code was buggy and the documentation not very good. I was able to fix these thanks to the community members. Again, the standard generational algorithms and operations have been implemented. This will later take advantage of the FiniteSet class.

##Partitions##
The only unimplemented portion is lexicographical generation. This will be implemented using the routines to generate restricted growth strings.

The reader should note that all the combinatorial objects inherit from Basic.

##Prufer codes##
This is to be used for generating trees. All the standard functionality has been implemented.

##Permutation groups##
Currently, algorithms to generate stabilizers, schreier trees and members of a group have been implemented. The Screier Sims algorithms is still a work in progress but should be complete in a few days.

#Status at Time of Writing#
There are 5 pull requests that are open. 4 are complete and are under revision while one is still incomplete. Another pull request is to be submitted that has algorithm for generating specialized combinatorial objects.

#Future Work & Recommendations#
The future work involves making the combinatorial objects completely symbolic and extending the computational group theory abilities of Sympy to match that of GAP. This could form the basis of a future GSoC project.

Tips for future Summer of Code students

**1:** Break up your project into small distinct pieces. Ideally you should have a mental picture in your head of what you are going to do. Commit early and commit fast. Realize that the review process is intended to help you become a better programmer.

**2:** Communicate often with your mentor and other members of the community. Stay in their good books. Most of these people have not met you and will not know you personally. Its important to keep a few interested folks in the loop. As a rule of thumb, the more the number of folks involved with reviewing your pull request, the more recognition you will get.

**3:** Make atomic commits. This way, its easier to tweak around and modify the commit history. A clean commit history is important for large open source projects, especially if a large number of separate modules are affected.