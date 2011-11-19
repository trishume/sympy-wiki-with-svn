# GCI 2011 Landing

This is our landing page for students wishing to participated in Google Code-In 2011 with SymPy.

## SymPy

![logo](https://github.com/sympy/sympy.github.com/raw/master/media/logo-200x200.png)

SymPy is an open source python library for symbolic computing. In the SymPy community we all believe in the merits and greatness of the open source approach but for the moment let us focus on the "symbolic computing" part.

Symbolic computing systems, also called computer algebra systems (CASs) are used in research and engineering for solving a variety of mathematical problems symbolically. In modern labs you will rarely see a researcher solving mundane equations by hand. They usually give them to a computer algebra system to solve so they can spend their time on more interesting and intricate work.

What does it mean to solve problems symbolically?  It means that instead of giving a numerical solution, as many systems do, a CAS will derive the solution using symbolic algebra, the same way that you would do it if you were to do it by hand on paper.  So if you tell SymPy to solve the equation *x<sup>2</sup> = 2* for *x*, it will give you *&radic;2* and *-&radic;2*, *exactly*.

You can see for examples [[Quick examples]] to start to get an idea of the rich set of abstract operations that a CAS supports. Some of the math may be unknown to you but do not be afraid: there is much that you can do for the project that does not involve hard math. You can look also at [Wolfram Alpha](www.wolframalpha.com) to see another example of a CAS. This one is more feature complete than SymPy, but proprietary, so the source code is not available to the public. Actually Wolfram Alpha is just one service based on the Mathematica CAS, a popular proprietary CAS. 

## How to get started

### Using SymPy

First install SymPy (you need to install python before that). If you want to just get a feel of it you can use the latest package available for your operating system, but if you want to contribute to the code (or some parts of the documentation) you will need the development version from github. More about this later.

Now that you have SymPy there is a number of different ways to use it. Some people use SymPy just as a library for building other software, but we will focus on the interactive use: the python interpreter permits interactive use of all of sympy's functionality. Just start the interpreter with the `python` command from your shell or command prompt and look at our [[Quick examples]]. Even in interactive mode you still need to import all of sympy's functionality. As you do not need any fine grain control for the moment just use `from sympy import *` which will give you access to most of the functionality.

Most of the advanced users use a more powerful interface to the python interactive interpreter called IPython. You do not need to have it to use or contribute to sympy.

Any one of those (python or IPython) supports the help command. Typing `help(object_of_interest)` will give you the documentation string.

### Development Workflow

As many people are working on sympy at the same time we need some way to collaborate. We are using the git system together with the github.com website. Those permit us to keep track of all changes to the project and review each-others work.

The git software is installed on every developers computer and tracks their own copy of all the code (that is your _repository_). When the developer finishes adding a feature, fixing a bug or even just adding a sentence to a documentation string he registers that change (he makes a _commit_). Then he communicates this change to the central repository (which is no different than the rest of the repositories - it's just the place we agreed to keep the current version of sympy). This is called a _pull request_. Now the people that have access to the central repository can discuss and eventually accept the change (ie _merge_ the change).

We use github.com for the central repository, for keeping a copy of our own repository and for making, discussing and merging the pull requests.

Here are the basic steps for making a patch. The list was adapted from [[Development-workflow]].

1. Setup your environment on your computer (only the first time, so you have a copy of our code):

    a) Create your [github](https://github.com/) account, if it was not created earlier, and create your personal copy (called a _fork_) of the [SymPy repository](https://github.com/sympy/sympy) (click on the `Fork` button on this page).
    Install [git](http://git-scm.com/download). When creating your github profile and forking our repository the github site will explain you how to connect your git installation to your github profile.

    b) Get a clone of [SymPy repository](https://github.com/sympy/sympy) with the following shell commands. This is just like the forking you have done in the previous step but instead on github the new repository is on your computer.

        $ git clone git://github.com/sympy/sympy.git
        $ cd sympy


    c) Assign your read-and-write repo to a remote called "github". That means that you connect the remote repository (that you have created on github) to your local repository (that you have created with the clone command). You will use your local repository to make changes to the code. Then you will communicate those changes to your remote repository (that is you will _push the commits_) so we can see them.

        $ git remote add github git@github.com:mynick/sympy.git

2. Choose your task from the [task list](https://docs.google.com/spreadsheet/ccc?key=0AiMKW-ZM-_fedFpSWm51VFBFZkdTRnh3WkhYRndSVXc), create git branch for it, and enter to it. Creating a branch is the way to isolate your changes from the main stable state of the code(also called _master_).

        $ git branch your_task_branch_name
        $ git checkout your_task_branch_name

3. Do with the code whatever is needed to complete the task.

4. Be sure that all tests pass. If you are fixing a bug or implementing a feature you should write new tests to ensure that the problem does not occur again. Test are written in the appropriate `test` folders. To run all tests use:

        $ ./bin/test
        $ ./bin/doctest

Be aware that there is also a code style tests that warns you if your code is badly structured (trailing whitespaces, etc).

5. Commit the changes to your branch and push the branch to your fork:

        $ git commit
        $ git push github your_task_branch
Another way is to use the `git gui` command that gives you a graphical interface.

6. Create the pull request: navigate to https://github.com/<YOUR-USERNAME>/sympy, select your task's branch, and press the *Pull Request* button.


Everyone is welcome to join and to implement new feature, fix some bug, give
general advice, etc. Also, we try to discuss everything and to review each
other's work so that many eyes can see more thus raising the quality.

### Contact us

General discussion takes place on [sympy@googlegroups.com](http://groups.google.com/group/sympy) mailing list and in the [issues list](http://code.google.com/p/sympy/issues/list), and the code is discussed in [sympy-patches@googlegroups.com](http://groups.google.com/group/sympy-patches)
mailing list. Some discussion also takes place on IRC (our channel is [#sympy at freenode](irc://irc.freenode.net/sympy)).

## Development Guidelines

_Talk about running tests, code style, doctests, docstrings, etc. Don't forget the importance of adding tests for every fixed bug or new functionality._

## Mentors

See [[GCI-2011-Mentors]] for a list of the people who will be mentoring for Google Code-In.

## Links:
- [[GCI-2011 Landing]]
- [[GCI-2011 Mentors]]
- [CGI-2011 Task list](https://docs.google.com/spreadsheet/ccc?key=0AiMKW-ZM-_fedFpSWm51VFBFZkdTRnh3WkhYRndSVXc)
- [[GCI-2011 Organization Application]]