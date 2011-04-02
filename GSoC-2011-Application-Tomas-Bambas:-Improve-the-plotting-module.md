GSoC 2011 Application Tomas Bambas: Improve the plotting module
===============================================================

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

This is just the great school for making software developers. See [[http://www.fit.vutbr.cz/FIT/.en]].

### Coding Skills

   * Python (both 2.x and 3.x): my primary language, experiences with PIL, PyQt and PyGame toolkits
   * C/C++: also good knowledges (language core, unix networking, OpenGL)
   * Java: good
   * PHP, Perl, JavaScript, Prolog, Lisp: basics
   * Platform: My working platform is Linux (openSUSE) and Windows Vista.

### Past Projects

I have never participated in any OSS project (except translations to czech lang, but not coding). This is my first try to get in. Anyway I have finished many small commercial projects, bespoke software (all in Python). I can send references by mail. In most cases it was some data manipulating software, like data harvesters, image manipulating scripts, import scripts, etc.

Project Proposal
----------------

### Overview

Plotting is an important component of every math software. SymPy has a basic plotting support by pyglet toolkit, which must be actually shipped with SymPy (some older version comatible with SymPy plotting module). This is not a perspective situation. I would like to implement a new general Plot() interface which should support multiple backends. The goal is connect a new Plot() interface with matplotlib and pyglet library, also implement an independent Google chart API backend (exactly URL generator) and get rid of a shipping an old pyglet library with new SymPy releases.

### Midterm Goals

   * First I should design and implement a new Plot interface. My vision is a simple user interface with many chart options. I can consult a plot user interface with Maple, great commercial CAS software. Plot object should accept every expression/function (one variable and surfaces) and also every geometric object (like Point). The back side of the interface should be easy connected to new backends. Every backend should have a way how the user/interface can find out which options of charts are supported and which objects can be plotted. Another thing is letting know if the backend is ready for use (for example matplotlib backend can't be used if matplotlib library isn't installed).
   * The second midterm goal is an implementation of Google Chart API backend, which should be URL generator of Google charts. Of course backend could download graph image and save it, but it makes itself dependent on internet connection. Anyway this will be consulted with the community. Google chart API module will not use any external library.

### Project Goals

   * ---pyglet: use old plotting code in pyglet backend---
   * ---matplotlib---

### My Motivation

This is my only GSoC application. There are more mentoring organisations which I would like to help, but SymPy is the one for what I can use my Python skills. "Improve the plotting module" is the item from Ideas list. I choose that one because I have experiences with image manipulating scripts and a plotting too and I really think SymPy needs this work. I have no summer plans and I need a job. Of course GSoC job would be a perfect item in my CV.

Schedule
--------

---summer plan in detail---

Future
------

This shouldn't be an one-off job. I would like to stay in the SymPy community and solve issues regarding a new plotting module. There is also another one backend I would like to implement. Everyone who is involved in the charts world knows Gnuplot software. In my opinion this is the best software for making graphs. I would like to implement an independent backend for generating gnuplot code. I mean this backend shouldn't be dependent on any external library like pygnuplot. It will be just a text/code generator (like Google chart API backend). This will be a backend for sophisticated users, because they can edit gnuplot code in detail and then use it in Gnuplot software.