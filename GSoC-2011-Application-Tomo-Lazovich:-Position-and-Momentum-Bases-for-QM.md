GSoC 2011 Application Tomo Lazovich: Position and Momentum Bases for QM
==============================

## My information

* Name: Tomo Lazovich
* University / current enrollment: Harvard University (graduating May 2011)
* Bio/background: I am a physics major with a CS minor at Harvard and am about to graduate this May. My main research has been in particle physics. I spent one summer working at Fermilab on the CDF experiment and two summers on the ATLAS experiment at CERN. My experience is in writing software for data analysis at these experiments. As a physics major, I also have much experience with quantum mechanics, having taken all of the undergraduate courses on QM offered as well as courses with applications of QM, such as solid state physics. I also have experience in C++, C, Python, Java, and many web programming technologies. I believe that I am qualified to write the necessary code for sympy and to understand the quantum mechanics of the systems that will be represented. 
* Email: lazovich [at] NOSPAM gmail [dot] com
    
    
## My coding platform

My current setup is an Ubuntu system. I have been programming in Python for two years now. I am familiar with both SVN and git so I will be able to work in the open source setting. 

## Getting to know the community/codebase

I forked the git repository and began to tackle this issue: [[http://code.google.com/p/sympy/issues/detail?id=2186&q=label%3Aquantum]]

to become familiar with the code base, particularly in sympy.physics.quantum. After introducing myself to the list and privately to Brian Granger, the physics project mentor, as well as asking some questions about how to handle operators that are both Hermitian and Unitary. After changing HermitianOperator to handle the special case where the operator is also Hermitian, I submitted my first pull request here: [[https://github.com/sympy/sympy/pull/160]]

That request is still under review!

## My Project
------------

### Goal

Currently in sympy, there is support for discrete Hilbert spaces, which are quite useful for spin calculations or symbolic quantum computing. However, there is no support for continuous Hilbert spaces
