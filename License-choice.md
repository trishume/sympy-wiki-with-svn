## Introduction

We try to use rational arguments and open discussion for all decisions in SymPy, the license is no exception.
 
We started with a GPL, but switched to a new BSD after a consenus in the [[issue 138|http://code.google.com/p/sympy/issues/detail?id=138]].

Here we try to present a lot of general arguments about licensing, so that we all have a good knowledge about this problematic.

## Open source

The idea of defining which license is and which is not opensource started probably in Debian in the [[Debian Free Software Guidelines (DFSG)|http://www.debian.org/social_contract#guidelines]] part of the Debian Social Contract, initially designed as a set of commitments that Debian Developers agree to abide by,
that has later been adopted by the free software community as the basis of the [[Open Source Definition|http://www.opensource.org/docs/osd]].

It's important to keep in mind, that even though these are quite definite terms, the final decision which license is open source and which is not
involves a judgement (in the case of Debian, it needs to be generally accepted by Debian Developers). No one disputes BSD and GPL. But for example
GNU FDL is on the border of free/non-free - if it has the so called invariant subsections, it is considered non-free by Debian, if it hasn't,
it is free.  

## Options

One should use a well-known license, so that people know what rights they have just from the name of it. 
Also when choosing a license, it's important so choose a license that clearly belongs among opensource licenses, and does not balance in the shady
area between free and nonfree, like GNU FDL. 

Basically the options are just BSD, LGPL 2 or 3, GPL 2 or 3, all of them definitely open source licenses.

## Views of people

It's important to know what well-known people think about this. For example Linus Torvalds, Richard Stallman. And also why some well known
projects chose the license they chose.

http://paraview.org/Wiki/ParaView_III_and_Qt_licensing

http://www.scipy.org/License_Compatibility

###  Ondrej

My view:

```
For stuff that I want other people to use and include in their programs, I use BSD. for end user programs, GPL can be a good idea too. also it depends on the atmosphere around the particular area - there are good reasons to use GPL for libraries too, like GMP (that Mathematica and other's use without giving nothing back). In python I just use BSD, like scipy, numpy, etc., because the atmosphere allows that.
```