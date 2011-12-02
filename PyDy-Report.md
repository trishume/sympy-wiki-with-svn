


# About Me
My name is Dale Lukas Peterson ('Luke') and I am a Ph.D candidate in the Mechanical and Aerospace Engineering department at the University of California Davis.  My research emphasis is dynamical systems and control, with a special interest in bicycle dynamics and control.  

# Introduction
This page summarizes the events of my Google Summer of code project "!PyDy: Newtonian Mechanics with Python".  The main goals of my project are:

   1. Provide a convenient and easy to use framework for performing kinematic and dynamic analysis of mechanical systems.
   1. Symbolic derivation of equations of motion of systems of rigid bodies and particles with applied forces or torques, and nonholonomic or holonomic constraints.
   1. Automatic generation of first order ODE's which allow for numerical integration using existing packages such as [http://www.scipy.org/ !SciPy] and [http://numpy.scipy.org/ !NumPy]. 
   1. Automatic generation of functions which make animation of the system very easy.
   1. Customized LaTeX output of equations of motion and symbolic vector expressions.


# First Contact
I first contacted the Sympy mailing list in January with a [http://groups.google.com/group/sympy/browse_thread/thread/e5a92f7b766bcf51# question] about how hard it might be to implement some code that deals with rotations in a convenient fashion for classical mechanics.  I had been using a closed source program [http://www.autolev.com Autolev] to do some of my research, and while it was quite mature and well tested, it lacked many modern features and I found my workflow in using it to be quite cumbersome and frustrating.  I had a solid understanding of the mathematics behind what it did, but I didn't have much of an idea how I would go about implementing my own code that provided many of the same features.

Ondrej responded to me and suggested I come visit him in Reno and we could start hacking.  So I did, and few days later we had a lot of the basic functionality for working with Symbolic vector expressions.  In that short period of time, the power of Python as a high level language really sunk in -- to implement what we did in 4 days of heavy coding would have taken weeks or months in other languages.

From there, I began working on the project on my own and began writing the GSoC application.  I also began learning git and started to study up on the Python language by reading [http://oreilly.com/catalog/9780596513986/ Learning Python] and also [http://www.qtrac.eu/py3book.html Programming in Python 3].  While Python 3 isn't quite mainstream yet, I figured it would be at some point so it was worth my time to start learning it as well.

By the time my Google Summer of Code application was submitted, I had somewhere around 800-1000 lines of Python code written, and many tests written for the functionality I had implemented.

# The Summer
Classes got out June 16th and at that point I dedicated myself full time to !PyDy.  My approach was to start working on deriving the equations of motion for several examples and in doing so see what sort of functionality would be needed and what would make the derivation as straight forward and clear as possible.  A couple of examples that I worked on were the rolling disc, the rolling torus, a rigid body, and a pendulum.  

I started a website for my project and a Google group.  This made discussion of the project with others much easier.  The details of my project are fairly technical so I won't go into them here, but all of the source is available on my [http://github.com/hazelnusse/pydy/tree/master github] and there are lots of examples of use there.

Throughout the summer, I was on the #sympy channel on irc.freenode.net and tried to be as active as possible on the mailing list (it can be hard to keep up -- there are lots of people doing lots of very different things with Sympy).  I carried with me my dynamics text book and would constantly refer to it as I was implementing code.  I also [http://www.dlpeterson.com/blog blogged] about the various issues I ran across and the progress that I made.

I organized a documentation day for Sympy, which was a great way to learn about Sphinx and to improve the Sympy documentation so that others can more easily find the help they need to get their work done.

Near the end of the summer I visited Ondrej at his house in Los Alamos along with Aaron, and we spent the weekend coding, fixing bugs, and also went on a hike to a hot spring in [http://www.vallescaldera.gov/ Calles Valdera].  A week or so later, Ondrej and I attended the [http://conference.scipy.org Scipy conference] at Caltech.  There were two days of tutorials and two days of talks, during which time I got to meet the developers of iPython, Cython, Mayavi, and lots of other people using python in their own scientific work.  I gave a [http://www.archive.org/details/scipy09_day1_17-Lightning_talks_5-8 lightning talk] on my GSoC work, and at that point things were working well enough for me to have complete examples of use (symbolic derivation, numerical integration, animation) for systems such as the rolling disc and a rigidbody.

# Acknowledgements
Throughout the summer, Ondrej was always responsive via email/phone/chat.  He was extremely patient with me as I started learning and using git, and also as I became more familiar with the Sympy code base.  It was great working with him and I am extremely thankful for the oppurtunity.

My office mate, Thomas Johnston, and I had numerous discussions about dynamics and how to implement algorithms in a generic setting.  We spent many lunches and afternoons discussion the general procedure one takes when deriving equations of motion using Kane's method, and many of his suggestions were implemented in !PyDy.  It was great having somebody else who is familiar with Kane's method (and who also knows Python) to talk with.  The discussion with him have definitely improved !PyDy.

I am thankful that Google is such a strong sponsor of open source software.  This project wouldn't have happened at the speed it did if it hadn't been for there Summer of Code program, so I am indebted to them for this.  Thanks Google!

# Conclusions and Future Work
There are few things that I would recommend to anybody doing a GSoC project:
   1. Get in touch with the people who work on and develop the project that you are interested in getting involved with.  This means follow the mailing list, join their IRC channel, and email/call/meet the developers and discuss your ideas.
   1. Spend a lot of time and thought on your proposal.  Be specific about what you want to achieve -- if you can't clearly explain the goal, it is going to be harder to get started in the right direction.  Make sure goals are specific and written down in your proposal, and be sure to explain *why* they are important.
   1. Learn a version control program -- preferably git.
   1. Study the language in which you will be programming so that you are familiar with the tools in the language and this won't be a hurdling block.
   1. Study the existing code base for the project you wish to be involved with.  This will help you understand how your project will integrate with what has already been completed.
   1. Be consistent about working your 40 hours -- don't slack off or you will get impossibly behind.
   1. Don't be afraid to ask questions -- but make sure you have at least looked in the obvious places (i.e., searched google or read/skimmed the documentation) before you ask your question.

I am still working actively on !PyDy and will continue to do so as much as possible.  It is my hope that other people who study dynamical systems will be interested in collaborative efforts to improve and extend !PyDy in order to give it much more functionality.  These sorts of applications will also really help improve Sympy -- the more users there are to test things out, the faster new changes get implemented and bugs get fixed.  

An important issue to me in the sciences is that of verifiability and reproducibility.  If others cannot verify your work or reproduce it, it hurts everybody because:
   1. Nobody will be able to double check to make sure you didn't make a mistake and people may carry on assuming your conclusions are correct when they may in fact be incorrect.
   1. People will waste a lot of time on duplicating efforts of others if they can't work with a common tool that is peer reviewed (Open Source) and available to everybody.

With a tool like Sympy and !PyDy, people in the field of dynamical systems now have a the beginnings of a tool which is cross-platform, free, open-source and collaborative in nature -- this is how science should be!  For more information on this line of thinking, check out [http://www.openscience.org/blog/ The Open Science Project].   

My most pressing goal at the moment is to use !PyDy to derive the equations of motion for a bicycle model that I use in my research.  This is a notoriously difficult system to model without making lots of simplifying assumptions, so if !PyDy can do it, I am confident that it can do nearly any system that is thrown its way.

Integrating !PyDy into a !MayaVi / Traits application is on my list of things to do as well.  This would be an amazing way to interact and study a dynamical system -- visualize it, perform stability analysis, and perform symbolic manipulations to the equations all within one place.