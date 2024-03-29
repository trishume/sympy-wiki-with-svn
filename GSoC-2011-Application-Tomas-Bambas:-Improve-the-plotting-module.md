GSoC 2011 Application Tomas Bambas: Improve the plotting module
===============================================================
[[http://www.google-melange.com/gsoc/proposal/review/google/gsoc2011/conyx/1]] Sent 2011-04-02

Name and Contact Info
---------------------

Name: Tomas Bambas

Residence: Czech Republic

E-mail: tomas.bambas{at}gmail.com

JID: conyx@jabber.cz

IRC: Conyx on freenode

Biographical Information
------------------------

### Study

I'm studying 3rd year at The Faculty of Information Technology at Brno University of Technology in the Czech Republic. My faculty focuses on software design, programming and team projects (less theory, more practice). I have passed through many programming courses like Java, C/C++, AI Basics, Information Systems, OOP, Scripting Languages, GUI, Computer Graphics and many more. My bachelor work is called "Taroky network multiplayer game". It's the computer implementation of classic European card game (written in Python).

This is just the great school for making software developers. See [1].

### Coding Skills

   * Python (both 2.x and 3.x): my primary language, experiences with PIL [2], PyQt and PyGame [3] toolkits
   * C/C++: also good knowledges (language core, unix networking, OpenGL)
   * Java: good
   * PHP, Perl, JavaScript, Prolog, Lisp: basics
   * Platform: My working platform is Linux (openSUSE) and Windows Vista.

### Past Projects

I have never participated in any OSS project (except translations to czech lang, but not coding). This is my first try to get in. Anyway I have finished many small commercial projects, bespoke software (all in Python). I can send references by mail. In most cases it was some data manipulating software, like data harvesters, image manipulating scripts, import scripts, etc.

Project Proposal
----------------

### Overview

Plotting is an important component of every math software. SymPy has a basic plotting support by pyglet [4] toolkit, which must be actually shipped with SymPy (some older version comatible with SymPy plotting module). This is not a perspective situation. I would like to implement a new general Plot() interface which should support multiple backends. The goal is connect a new Plot() interface with matplotlib and pyglet library, also implement an independent Google chart API [5] backend (exactly URL generator) and finally get rid of a shipping an old pyglet library with new SymPy releases.

### Midterm Goals

   * First I should design and implement a new Plot interface. My vision is a simple user interface with many chart options. I can consult a plot user interface with Maple [6], great commercial CAS software. Plot object should accept every expression/function (one variable and surfaces) and also every geometric object (like Point). The back side of the interface should be easy connected to new backends. Every backend should have a way how the user/interface can find out which options of charts are supported and which objects can be plotted. Another thing is letting know if the backend is ready for use (for example matplotlib backend can't be used if matplotlib library isn't installed).
   * The second midterm goal is an implementation of Google Chart API [5] backend module, which should be URL generator of Google charts. Of course backend could download graph image and save it, but it makes itself dependent on an internet connection. Anyway this will be consulted with the community. Google chart API module will not use any external library.

### Project Goals

   * The next task is a transformation the old pyglet plotting code to the new pyglet backend. The new module will work with the last pyglet release. The module should support all Plot possibilities and user options.
   * Final and for me the most important goal is the implementation of matplotlib [7] backend module. matplotlib is the best plotting library for python. I would like to use all its possibilities and also reflect them in the Plot interface design. Like the pyglet backend module, the matplotlib backend will be dependent on external libraries (matplotlib and its dependency list), which user has to install for using this module.

### My Motivation

This is my only GSoC application. There are more mentoring organisations which I would like to help, but SymPy is the one for what I can use my Python skills. "Improve the plotting module" is the item from Ideas list. I choose that one because I have experiences with image manipulating scripts and a plotting too and I really think SymPy needs this work. I have no summer plans and I need a job. Of course GSoC job would be a perfect item in my CV.

Schedule
--------

Week 1-3: Design and coding the new Plot interface (the new plotting module)

Week 4: Implementation of Google chart API backend module

Week 5-6: Implementation of pyglet backend module

Week 7-8: Implementation of matplotlib backend module

Anyway I would like to start coding/design before the first coding week.

Future
------

This shouldn't be an one-off job. I would like to stay in the SymPy community and solve issues regarding a new plotting module. There is also another one backend I would like to implement. Everyone who is involved in the charts world knows Gnuplot software. In my opinion this is the best software for making graphs. I would like to implement an independent backend for generating gnuplot code. I mean this backend shouldn't be dependent on any external library like pygnuplot. It will be just a text/code generator (like Google chart API backend). This will be a backend for sophisticated users, because they can edit gnuplot code in detail and then use it in Gnuplot software.

References
----------

[1] The Faculty of Information Technology at Brno University of Technology [[http://www.fit.vutbr.cz/FIT/.en]]

[2] PIL [[http://www.pythonware.com/products/pil]]

[3] PyGame [[http://www.pygame.org]]

[4] pyglet [[http://www.pyglet.org]]

[5] Google Chart API [[http://code.google.com/apis/chart/]]

[6] Maple [[http://www.maplesoft.com/products/maple/]]

[7] matplotlib [[http://matplotlib.sourceforge.net/]]