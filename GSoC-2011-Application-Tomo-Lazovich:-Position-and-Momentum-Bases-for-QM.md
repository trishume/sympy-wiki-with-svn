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

Your Project
------------

Start a wiki page to work on your proposal at
https://github.com/sympy/sympy/wiki/. If add your proposal there, we
will help you edit it (though understand that we will not help you write
it).

Answer the following questions in your proposal:


* What do you want to achieve?
* If you have chosen an idea from our list, why did you choose this specific
  idea?
* If you are proposing a project of your own, what is unique about it?
* What qualifications do you have to implement your idea.  For example, if you
  are implementing solvers for partial differential equations, what courses
  have you taken or books have you read on PDEs?
* What makes you suited to do the project?
* How much time do you plan to invest in the project before, during, and after
  the Summer of Code? (we expect full time 40h/week during GSoC, but better
  make this explicit)
* Please provide a schedule of how this time will be spent on subtasks
  of the project over the period of the summer. While this is only
  preliminary, we will use it to help monitor your progress throughout
  the program.  Also understand that during the project you will issue
  weekly progress reports against that plan on your blog.

You do not need to format your application as a question/answer format
for the above questions, but we expect to see all of the above questions
answered in your application somewhere.
