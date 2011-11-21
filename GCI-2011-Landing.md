# GCI 2011 Landing

This is our landing page for students wishing to participate in Google Code-In 2011 with SymPy.

## SymPy

![logo](https://github.com/sympy/sympy.github.com/raw/master/media/logo-200x200.png)

SymPy is an open source python library for symbolic computing. In the SymPy community we all believe in the merits and greatness of the open source approach but for the moment let us focus on the &quot;symbolic computing&quot; part.

Symbolic computing systems, also called computer algebra systems (CASs) are used in research and engineering for solving a variety of mathematical problems symbolically. In modern labs you will rarely see a researcher solving mundane equations by hand. They usually give them to a computer algebra system to solve so they can spend their time on more interesting and intricate work.

What does it mean to solve problems symbolically?  It means that instead of giving a numerical solution, as many systems do, a CAS will derive the solution using symbolic algebra, the same way that you would do it if you were to do it by hand on paper.  So if you tell SymPy to solve the equation *x&lt;sup&gt;2&lt;/sup&gt; = 2* for *x*, it will give you *&amp;radic;2* and *-&amp;radic;2*, *exactly*.

You can see some [[Quick examples]] to start to get an idea of the rich set of abstract operations that a CAS supports. Some of the math may be unknown to you but do not be afraid: there is much that you can do for the project that does not involve hard math. You can look also at [Wolfram Alpha](www.wolframalpha.com) to see another example of a CAS. This one is more feature complete than SymPy, but proprietary, so the source code is not available to the public. Actually Wolfram Alpha is just one service based on the Mathematica CAS, a popular proprietary CAS.

## How to get started

### Using SymPy

First [install SymPy](http://code.google.com/p/sympy/wiki/DownloadInstallation). If you are on Windows, you will first need to install Python (http://python.org/).  Python should already come installed on Linux and Mac OS X.  If you want to just get a feel of it you can use the latest package available for your operating system, but if you want to contribute to the code (or some parts of the documentation) you will need the development version from GitHub. More about this later.

Now that you have SymPy there are a number of ways to use it. Some people use SymPy as a library for building other software, but we will focus on interactive use: the Python interpreter permits interactive use of all of SymPy&#39;s functionality. From your command prompt, cd into the sympy directory, and run the `bin/isympy` script.  This will start a Python (or IPython, if you have it installed) interpreter, and will automatically import all the sympy functions and create some symbols for you.


```py
$ ./bin/isympy
Python console for SymPy 0.7.1 (Python 2.7.2-64-bit) (ground types: gmpy)

These commands were executed:
&gt;&gt;&gt; from __future__ import division
&gt;&gt;&gt; from sympy import *
&gt;&gt;&gt; x, y, z, t = symbols(&#39;x y z t&#39;)
&gt;&gt;&gt; k, m, n = symbols(&#39;k m n&#39;, integer=True)
&gt;&gt;&gt; f, g, h = symbols(&#39;f g h&#39;, cls=Function)

Documentation can be found at http://www.sympy.org

&gt;&gt;&gt; a = 1/x + (x*sin(x) - 1)/x
&gt;&gt;&gt; simplify(a)
-sin(x)
```

Look at our [[Quick examples]] for more examples of the things you can do with SymPy.

Most of the advanced users use a more powerful interface to the python interactive interpreter called [IPython](http://ipython.org/). You do not need to have it to use or contribute to SymPy, but it is highly recommended.

Both of these (python or IPython) support the help command. Typing `help(object_of_interest)` will give you the documentation string for `object_of_interest`.  This is a good way to learn about the various functions in SymPy.

### Development Workflow

If your task does not include editing code or documentation, then you probably don&#39;t need the information here. It explains how to set up the system that we use for tracking changes to our code.

As many people are working on sympy at the same time we need some way to collaborate. We are using the [git](http://git-scm.com/) system together with the [GitHub](https://www.github.com) website. Those permit us to keep track of all changes to the project and review each other&#39;s work.

The git software is installed on every developer&#39;s computer and tracks his own copy of all the code (that is your _repository_). When the developer finishes adding a feature, fixing a bug, or even just adding a sentence to a documentation string, he registers that change (he makes a _commit_). Then he communicates this change to the central repository (which is no different than the rest of the repositories - it&#39;s just the place we agreed to keep the current version of sympy). This is called a _pull request_. Now the people that have access to the central repository can discuss and eventually accept the change (i.e., _merge_ the change).

We use github.com for the central repository, for keeping a copy of our own repository, and for making, discussing, and merging the pull requests.

Here are the basic steps for making a patch. The list was adapted from [[Development-workflow]].  That page contains more detailed instructions for each of the below steps, with screenshots, so please look there if anything below is confusing.

1. Setup your environment on your computer (you only need to do this once):

    a) **Create a [GitHub](https://github.com/) account, if you don&#39;t already have one.**

    b) **Fork SymPy to your GitHub account,** Click on the `Fork` button at the top right of this page.

    c) **Install [git](http://git-scm.com/download) on your computer.** When creating your GitHub profile and forking our repository, the GitHub site will explain how to connect your git installation to your GitHub profile.  This is also explained at [[Development-workflow]].

    d) **Create a clone of the [SymPy repository](https://github.com/sympy/sympy) on your computer.** First, cd to the directory where you want to download the code.  Then type

        ```bash
        git clone git://github.com/sympy/sympy.git
        cd sympy
        ```
    in your shell prompt.  This will download the development version of SymPy, as well as all of the development history.


    e) **Assign your read-and-write repo to a remote called `github`.** That means that your GitHub clone of SymPy to your local repository that you have created with the clone command. You will use your local repository to make changes to the code. Then you will communicate those changes to your remote repository (that is, you will _push_ the commits), so we can see them.

        ```bash
        git remote add github git@github.com:YOUR-USERNAME/sympy.git
        ```

2. Create a git branch for your task and make it the current working branch. Creating a branch is the way to isolate your changes from the main stable state of the code (also called _master_).

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

6. Create the pull request: navigate to https://github.com/YOUR-USERNAME/sympy, select your task&#39;s branch, and press the *Pull Request* button.

See the [github's documentation for pull requests](http://help.github.com/pull-requests/) for more information.

Everyone is welcome to join and to implement new feature, fix some bug, give
general advice, etc. Also, we try to discuss everything and to review each
other&#39;s work so that many eyes can see more thus raising the quality.

### Contact us

General discussion takes place on [sympy@googlegroups.com](http://groups.google.com/group/sympy) mailing list and in the [issues list](http://code.google.com/p/sympy/issues/list), and the code is discussed in [sympy-patches@googlegroups.com](http://groups.google.com/group/sympy-patches)
mailing list. Some discussion also takes place on IRC (our channel is #sympy at freenode: irc://irc.freenode.net/sympy). Do not hesitate to contact us for any help you might need.

## Development Guidelines

### Code style

Please follow the standard code style, as recommended by Style Guide for Python Code ([PEP-0008](http://www.python.org/dev/peps/pep-0008), [PEP-0257](http://www.python.org/dev/peps/pep-0257)). In particular:

- use four spaces instead of tabs for indentation levels.
- the name of the functions should be lowercase with words separated by underscores: `def set_some_value():`
- the name of classes should be CamelCase: `class PolynomialRing(object):`

Note, however, that some functions do have uppercase letters where it makes sense. For example, for matrices they are LUdecomposition or T (transposition) methods.

### Tests and doc strings:

All new features should be documented and have tests.

If you implement a new feature, write a test case for it (and as long as this test case passes, the feature is considered to work). If you think there is a bug, write a test case which fails and then fix the bug. If you think some other test case should be modified, please discuss it on the mailing list first. It&#39;s very important, so let&#39;s repeat it once more: if you don&#39;t write a test case for all your features that you implement/fix, it will be like you contributed nothing and just wasted your time, because those features will stop working the next time we refactor the library (and conversely, if you write tests for the new features, they will be guaranteed to work forever).

This also means, that any refactoring is easy to do, just make sure all the tests run. And because refactoring is easy, we are not afraid of making huge changes if we think the code will be more readable or simpler. If you want to find more about this kind of attitude, google the phrase &quot;extreme programming&quot;.

Every module has a suite of accompanying tests. In general, if module&#39;s code is stored in `sympy/path/modulename`, then the tests are stored in `sympy/path/modulename/tests` folder. Furthermore, the corresponding tests are in files `sympy/path/module_name/tests/test_something.py`, `sympy/path/module_name/tests/test_otherthings.py`,  and so on.

In addition, tests for the main functionality of classes and functions must be present in the appropriate docstrings:


```
&quot;&quot;&quot;The center of the ellipse.

Returns
-------
center : number

Examples
--------
&gt;&gt;&gt; from sympy import Point, Ellipse
&gt;&gt;&gt; p1 = Point(0, 0)
&gt;&gt;&gt; e1 = Ellipse(p1, 3, 1)
&gt;&gt;&gt; e1.center
Point(0, 0)

&quot;&quot;&quot;
```

Tests verified by running the commands in shell:

```
    $ ./bin/test
    $ ./bin/doctest
```

How to create and run tests is written in more detail at [[Running-tests]].


_Talk about running tests, code style, doctests, docstrings, etc. Don&#39;t forget the importance of adding tests for every fixed bug or new functionality._

## Mentors

See [[GCI-2011-Mentors]] for a list of the people who will be mentoring for Google Code-In. In the list you can see which areas the respective mentors work on, as well as contact information for each individual mentor. However, he preferred method of communication is through our mailing list or IRC channel (see &quot;Contact Us&quot;, above). Specific mentors may be busy at various time throughout the program, so the best way is to contact the entire community. This is also more aligned with the way open-source development works.

## Links:
- [[GCI-2011 Mentors]]
- [CGI-2011 Task list (spreadsheet)](https://docs.google.com/spreadsheet/ccc?key=0AiMKW-ZM-_fedFpSWm51VFBFZkdTRnh3WkhYRndSVXc)
- [GCI-2011 Task list (wiki)](https://github.com/sympy/sympy/wiki/GCI-2011-Task-list)
- [[GCI-2011 Organization Application]]
