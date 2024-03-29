# GCI 2011 Landing

This is our landing page for students wishing to participate in Google Code-In 2011 with SymPy.

## SymPy

![logo](https://github.com/sympy/sympy.github.com/raw/master/media/logo-200x200.png)

SymPy is an open source python library for symbolic computing. In the SymPy community we all believe in the merits and greatness of the open source approach but for the moment let us focus on the "symbolic computing" part.

Symbolic computing systems, also called computer algebra systems (CASs) are used in research and engineering for solving a variety of mathematical problems symbolically. In modern labs you will rarely see a researcher solving mundane equations by hand. They usually give them to a computer algebra system to solve so they can spend their time on more interesting and intricate work.

What does it mean to solve problems symbolically?  It means that instead of giving a numerical solution, as many systems do, a CAS will derive the solution using symbolic algebra, the same way that you would do it if you were to do it by hand on paper.  So if you tell SymPy to solve the equation *x<sup>2</sup> = 2* for *x*, it will give you *&radic;2* and *-&radic;2*, *exactly*.

You can see some [[Quick examples]] to start to get an idea of the rich set of abstract operations that a CAS supports. Some of the math may be unknown to you but do not be afraid: there is much that you can do for the project that does not involve hard math. You can look also at [Wolfram Alpha](www.wolframalpha.com) to see another example of a CAS. This one is more feature complete than SymPy, but proprietary, so the source code is not available to the public. Actually Wolfram Alpha is just one service based on the Mathematica CAS, a popular proprietary CAS.

## How to get started

### Using SymPy

First [install SymPy](http://code.google.com/p/sympy/wiki/DownloadInstallation). If you are on Windows, you will first need to install Python (http://python.org/).  Python should already come installed on Linux and Mac OS X.  If you want to just get a feel of it you can use the latest package available for your operating system, but if you want to contribute to the code (or some parts of the documentation) you will need the development version from GitHub. More about this later.

Now that you have SymPy there are a number of ways to use it. Some people use SymPy as a library for building other software, but we will focus on interactive use: the Python interpreter permits interactive use of all of SymPy's functionality. From your command prompt, cd into the sympy directory, and run the `bin/isympy` script.  This will start a Python (or IPython, if you have it installed) interpreter, and will automatically import all the sympy functions and create some symbols for you.


```py
$ ./bin/isympy
Python console for SymPy 0.7.1 (Python 2.7.2-64-bit) (ground types: gmpy)

These commands were executed:
>>> from __future__ import division
>>> from sympy import *
>>> x, y, z, t = symbols('x y z t')
>>> k, m, n = symbols('k m n', integer=True)
>>> f, g, h = symbols('f g h', cls=Function)

Documentation can be found at http://www.sympy.org

>>> a = 1/x + (x*sin(x) - 1)/x
>>> simplify(a)
-sin(x)
```

Look at our [[Quick examples]] for more examples of the things you can do with SymPy.

Most of the advanced users use a more powerful interface to the python interactive interpreter called [IPython](http://ipython.org/). You do not need to have it to use or contribute to SymPy, but it is highly recommended.

Both of these (python or IPython) support the help command. Typing `help(object_of_interest)` will give you the documentation string for `object_of_interest`.  This is a good way to learn about the various functions in SymPy.

### Development Workflow

If your task does not include editing code or documentation, then you probably don't need the information here. It explains how to set up the system that we use for tracking changes to our code.

As many people are working on sympy at the same time we need some way to collaborate. We are using the [git](http://git-scm.com/) system together with the [GitHub](https://www.github.com) website. Those permit us to keep track of all changes to the project and review each other's work.

The git software is installed on every developer's computer and tracks his own copy of all the code (that is your _repository_). When the developer finishes adding a feature, fixing a bug, or even just adding a sentence to a documentation string, he registers that change (he makes a _commit_). Then he communicates this change to the central repository (which is no different than the rest of the repositories - it's just the place we agreed to keep the current version of sympy). This is called a _pull request_. Now the people that have access to the central repository can discuss and eventually accept the change (i.e., _merge_ the change).

We use github.com for the central repository, for keeping a copy of our own repository, and for making, discussing, and merging the pull requests.

Here are the basic steps for making a patch. The list was adapted from [[Development-workflow]].  That page contains more detailed instructions for each of the below steps, with screenshots, so please look there if anything below is confusing.

1. Setup your environment on your computer (you only need to do this once):

    a) **Create a [GitHub](https://github.com/) account, if you don't already have one.**

    b) **Fork SymPy to your GitHub account,** Click on the `Fork` button at the top right of this page.

    c) **Install [git](http://git-scm.com/download) on your computer.** When creating your GitHub profile and forking our repository, the GitHub site will explain how to connect your git installation to your GitHub profile.  This is also explained at [[Development-workflow]]. Don't forget to add your name and email to git, so you can be properly credited for your work:

        $ git config --global user.name "Firstname Lastname"
        $ git config --global user.email "your_email@youremail.com"


    If you are on Windows, you may want to install https://github.com/downloads/github/GitPad/Gitpad.zip, which will make it easier to edit your commit messages (unless you know how to use Vim).

    d) **Create a clone of the [SymPy repository](https://github.com/sympy/sympy) on your computer.** First, cd to the directory where you want to download the code.  Then type


        git clone git://github.com/sympy/sympy.git
        cd sympy

    in your shell prompt.  This will download the development version of SymPy, as well as all of the development history.


    e) **Assign your read-and-write repo to a remote called `github`.** That means that your GitHub clone of SymPy to your local repository that you have created with the clone command. You will use your local repository to make changes to the code. Then you will communicate those changes to your remote repository (that is, you will _push_ the commits), so we can see them.

        git remote add github git@github.com:YOUR-USERNAME/sympy.git

2. Create a git branch for your task and make it the current working branch. Creating a branch is the way to isolate your changes from the main stable state of the code (also called _master_).

        git branch your_task_branch_name
        git checkout your_task_branch_name

3. Do with the code whatever is needed to complete the task.

4. Be sure that all tests pass. If you are fixing a bug or implementing a feature you should write new tests to ensure that the problem does not occur again. Test are written in the appropriate `test` folders. Copy the style of the tests there, i.e., functions starting with `test_` with assert statements inside them.  To run all tests use:

        ./bin/test
        ./bin/doctest

    Be aware that there is also a code style test that warns you if your code is badly structured (trailing whitespace, etc).

5. If all tests pass, commit the changes to your branch and push the branch to your fork:

        git commit -a
        git push github your_task_branch

    Another way is to use the `git gui` command that gives you a graphical interface.

6. Create the pull request: navigate to https://github.com/YOUR-USERNAME/sympy, select the branch for for your task from the "current branch" popup, and press the *Pull Request* button at the top.  Then, fill out the form, and click "Send Pull Request".

See the [github's documentation for pull requests](http://help.github.com/pull-requests/) for more information.

Everyone is welcome to join and to implement new feature, fix some bug, give
general advice, etc. Also, we try to discuss everything and to review each
other's work so that many eyes can see more thus raising the quality.

### Contact us

General discussion, both for developers and for users, takes place on the mailing list ([sympy@googlegroups.com](http://groups.google.com/group/sympy)) and in the [issue tracker](http://code.google.com/p/sympy/issues/list). Some discussion also takes place on IRC (our channel is #sympy at freenode: irc://irc.freenode.net/sympy). Do not hesitate to contact us for any help you might need.

## Development Guidelines

### Code style

Please follow the standard code style, as recommended by Style Guide for Python Code ([PEP-0008](http://www.python.org/dev/peps/pep-0008), [PEP-0257](http://www.python.org/dev/peps/pep-0257)). In particular:

- use four spaces instead of tabs for indentation levels.
- the name of the functions should be lowercase with words separated by underscores: `def set_some_value():`. Note, however, that some functions do have uppercase letters where it makes sense. For example, for matrices they are LUdecomposition or T (transposition) methods.
- the name of classes should be CamelCase: `class PolynomialRing(object):`
- Put spaces around assignment operators (`=`, `+=`, `-=`, etc.), comparison operators (`==`, `<`, `<=`, `>`, `>=`, `!=`), and addition and subtraction operators (`+`, `-`).
- Do not put spaces around parentheses (`(`, `)`, `[`, `]`, `{`, `}`), multiplication or exponentiation operators (`*`, `**`), or `=` when used as a default for keyword arguments (e.g., `function(x=True)`.
- Put a space after, but not before, commas (`,`) and colons in dictionaries (`:`) (e.g., `{'a': 1, 'b': 2}`).
- If in doubt, use the same coding style as the code around the code you are modifying, or ask on the list. And you can't go wrong with PEP 8. Note that we do not have many restrictions on coding style beyond this: just use your own coding style and use your best judgement on what looks best.


### Tests and docstrings:

All new features should be documented and have tests.

If you implement a new feature, write a test case for it (and as long as this test case passes, the feature is considered to work). If you fix a bug, write a test case that would fail without the bug fix but now passes. If you think some other test case should be modified, please discuss it on the mailing list first. It's very important, so let's repeat it once more: if you don't write a test case for all your features that you implement/fix, it will be like you contributed nothing and just wasted your time, because those features will stop working the next time we refactor the library (and conversely, if you write tests for the new features, they will be guaranteed to work forever).  Patches will not be accepted without tests.

This also means that any refactoring is easy to do:  just make sure that all the tests run. And because refactoring is easy, we are not afraid of making huge changes if we think the code will be more readable or simpler. If you want to find more about this kind of attitude, google the phrase "extreme programming".

There are two kinds of tests in SymPy: tests and doctests.

#### Tests

Every module has a suite of accompanying tests. In general, if module's code is stored in `sympy/modulename`, then the tests are stored in `sympy/modulename/tests` folder. Furthermore, the corresponding tests are in files `sympy/path/module_name/tests/test_something.py`, `sympy/path/module_name/tests/test_otherthings.py`,  and so on.

Here is an example of what a test looks like (taken from the `sympy/solvers/tests/test_solvers.py` file):

```python
def test_solve_linear():
    x, y = symbols('x y')
    w = Wild('w')
    assert solve_linear(x, x) == (0, 1)
    assert solve_linear(x, y - 2*x) in [(x, y/3), (y, 3*x)]
    assert solve_linear(x, y - 2*x, exclude=[x]) ==(y, 3*x)
    assert solve_linear(3*x - y, 0) in [(x, y/3), (y, 3*x)]
    assert solve_linear(3*x - y, 0, [x]) == (x, y/3)
    assert solve_linear(3*x - y, 0, [y]) == (y, 3*x)
    assert solve_linear(x**2/y, 1) == (y, x**2)
    assert solve_linear(w, x) in [(w, x), (x, w)]
    assert solve_linear(cos(x)**2 + sin(x)**2 + 2 + y) == \
           (y, -2 - cos(x)**2 - sin(x)**2)
    assert solve_linear(cos(x)**2 + sin(x)**2 + 2 + y, symbols=[x]) == (0, 1)
    assert solve_linear(Eq(x, 3)) == (x, 3)
    assert solve_linear(1/(1/x - 2)) == (0, 0)
    raises(ValueError, 'solve_linear(Eq(x, 3), 3)')
```

Notice some things:

- The test function starts with the word `test_`.  This is important.  The test runner will not run the tests unless this is true.
- Symbols used in the test are defined at the top.  This is important.  Since SymPy is just Python, we have to define all variables, including symbols (this is a little different from some other computer algebra systems, where variables are auto-defined).
- The test consists of `assert` statements, which assert the equality of a function and its output.  The test runner will run each of these statements, and if one of them is False, it will raise `AssertionError` and the test will fail.
- The `raises()` function can be used to test if a function should raise an exception, e.g., on bad input.  In this case, it tests that you cannot solve for a number (only solving for a Symbol is allowed).

Tests should throughly test the output of the function, so that we can know right away just from running the tests that everything works correctly.

#### Doctests

In addition to tests, examples for the main functionality of classes and functions must be present in the appropriate docstrings:

```
def center(self):
    """The center of the ellipse.

    Returns
    -------
    center : number

    Examples
    --------
    >>> from sympy import Point, Ellipse
    >>> p1 = Point(0, 0)
    >>> e1 = Ellipse(p1, 3, 1)
    >>> e1.center
    Point(0, 0)

    """
    ...
```

Unlike tests, the purpose of these examples, or _doctests_ as they are called, is to show the user how to use the function.  They should be instructive.

To make sure that the doctests are correct, we test them (hence the name doctests).  This ensures that the output in the docstring is exactly the same as the output the user would see if he pasted it into a Python session, and prevents the documentation from becoming out-of-date.  Note that because of this, all doctests must import every function and class that is used, and also, as before, all Symbols must be defined.  Note that we do not allow the use of `import *` anywhere, and if you use this, the code quality tests will fail.

#### Running the tests.

You can run the tests by running these commands in the shell:

```
./bin/test
./bin/doctest
```

You can run the tests for one specific module by adding its path as an argument to the test runner command, for example

```
./bin/test sympy/solvers
```

will just run the tests in the solvers.  Note that you can do this to save some time when developing, but you must make sure that **all** tests pass, or else your patch will not be accepted.

How to create and run tests is written in more detail at [[Running-tests]].

## Code-In Guidelines

We have some requirements for all Code-In tasks:

- When relevant (i.e., there is some kind of a patch), the task is not considered complete until the code is merged with the official repository.  This means that you need to completely finish the review of the task to the point where it has passed review and someone with push access has pushed it in.  If you feel that your task is not being reviewed, please contact one of the mentors.  Please note that if you are waiting on a response from a *specific* mentor, that you should take into consideration things like timezone difference, and the fact that all mentors are volunteers who have other things to do beyond Code-In.

- Any task that involves submitting a patch must go through a pull request, unless otherwise specified.  It is much easier for us to review a pull request than a patch uploaded on the task page, and so this will make the review process go much quicker for us.

- If you are running out of time for a task *and you can demonstrate that you are doing work on the task*, we will extend the time period. This is in case we underestimated the time required to complete a task.  Please contact us and be prepared to demonstrate this. If you are not doing work on the task, however, you need to let it go and let someone else give it a try.  Do not claim a task until you are prepared to work on it.

## Mentors

See [[GCI-2011-Mentors]] for a list of the people who will be mentoring for Google Code-In. In the list you can see which areas the respective mentors work on, as well as contact information for each individual mentor. However, the preferred method of communication is through our mailing list or IRC channel (see "Contact Us", above). Specific mentors may be busy at various time throughout the program, so the best way is to contact the entire community. This is also more aligned with the way open-source development works.

## Links:
- [[GCI-2011 Mentors]]
- [CGI-2011 Task list (spreadsheet)](https://docs.google.com/spreadsheet/ccc?key=0AiMKW-ZM-_fedFpSWm51VFBFZkdTRnh3WkhYRndSVXc)
- [GCI-2011 Task list (wiki)](https://github.com/sympy/sympy/wiki/GCI-2011-Task-list)
- [[GCI-2011 Organization Application]]
