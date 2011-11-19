# GCI 2011 Landing

This will be our landing page for students wishing to participated in Google Code-In 2011 with SymPy.

## SymPy

![logo](https://github.com/sympy/sympy.github.com/raw/master/media/logo-200x200.png)

SymPy is an open source python library for symbolic computing. In the SymPy community we all believe in the merits and greatness of the open source approach but for the moment let us focus on the "symbolic computing" part.

Symbolic computing systems, also called computer algebra systems (CASs) are used in research and engineering for solving a variety of mathematical problems symbolically. In modern labs you will rarely see a researcher solving mundane equations by hand. They usually give them to a computer algebra system to solve so they can spend their time on more interesting and intricate work.

What does it mean to solve problems symbolically?  It means that instead of giving a numerical solution, as many systems do, a CAS will derive the solution using symbolic algebra, the same way that you would do it if you were to do it by hand on paper.  So if you tell SymPy to solve the equation *x<sup>2</sup> = 2* for *x*, it will give you *&radic;2* and *-&radic;2*, *exactly*.

You can see for examples [[Quick examples]] to start to get an idea of the rich set of abstract operations that a CAS supports. Some of the math may be unknown to you but do not be afraid: there is much that you can do for the project that does not involve hard math. You can look also at [Wolfram Alpha](www.wolframalpha.com) to see another example of a CAS. This one is more feature complete than SymPy, but proprietary, so the source code is not available to the public. Actually Wolfram Alpha is just one service based on the Mathematica CAS, a popular proprietary CAS. 

## How to get started

### Using SymPy

First install SymPy (you need to install python before that). If you want to just get a feel of it you can use the latest package available for you operating system, but if you want to contribute to the code (or some parts of the documentation) you will need the development version from github. More about this later.

Now that you have SymPy there are a number of different ways to use it. Some people use SymPy just as a library for building another software, but we will focus on the interactive use: the python interpreter permits interactive use of all of sympy's functionality. Just start the interpreter with the `python` command from your shell or command prompt and look at our [[Quick examples]]. 

### Development Workflow

See [[Development-workflow]] for detailed instructions. And here a brief list of basic steps how to make a patch:

1. Setup your environment:

    a) Create your [github](https://github.com/) account, if it was not created earlier, and
    create your fork of the [SymPy repository](https://github.com/sympy/sympy) (click `Fork` button on this page).
    Install [git](http://git-scm.com/download).

    b) Get a clone of [SymPy repository](https://github.com/sympy/sympy) with the shell commands:

        $ git clone git://github.com/sympy/sympy.git
        $ cd sympy

    c) assign your read-and-write repo to a remote called "github"

        $ git remote add github git@github.com:mynick/sympy.git

2. Choose the task from a [list](https://docs.google.com/spreadsheet/ccc?key=0AiMKW-ZM-_fedFpSWm51VFBFZkdTRnh3WkhYRndSVXc), create git branch for it, and enter to it:

        $ git branch your_task_branch
        $ git checkout your_task_branch

3. Modify code to solve it.

4. Be sure that all tests are passed

        $ ./bin/test
        $ ./bin/doctest

5. Commit changes in your branch and push branch to your fork:

        $ git commit
        $ git push github your_task_branch

6. Create pull request: navigate to https://github.com/mynick/sympy, select your task's branch, and press the *Pull Request* button.


Everyone is welcome to join and to implement new feature, fix some bug, give
general advice, etc. Also, we try to discuss everything and to review each
other's work so that many eyes can see more thus raising the quality.

General discussion takes place on [sympy@googlegroups.com](http://groups.google.com/group/sympy) mailing list and in
the [issues list](http://code.google.com/p/sympy/issues/list), and the code is discussed in [sympy-patches@googlegroups.com](http://groups.google.com/group/sympy-patches)
mailing list. Some discussion also takes place on IRC (our channel is [#sympy at freenode](irc://irc.freenode.net/sympy)).

_Adapt [[Development Workflow]] to something aimed for GCI students.  Also, include information on how to contact the mailing list/IRC, how to use SymPy, etc._

## Development Guidelines

_Talk about running tests, code style, doctests, docstrings, etc. Don't forget the importance of adding tests for every fixed bug or new functionality._

## Mentors

See [[GCI-2011-Mentors]] for a list of the people who will be mentoring for Google Code-In.