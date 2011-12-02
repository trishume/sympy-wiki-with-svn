

# Introduction

We are looking for new developers - so far there were more than 40 people who contributed patches, some of them are long term !SymPy developers. Are you using !SymPy? We are interested to hear from you - join our mailinglist and if you have some nice code, we would like to include it in !SymPy. See WhyToJoin for some reasons why you should join us. :)

!SymPy development discussion takes place on
[http://groups.google.com/group/sympy sympy] and [http://groups.google.com/group/sympy-patches sympy-patches] mailing lists, and also in the !SymPy [http://code.google.com/p/sympy/issues/list issues tracker]. You can send your patch to either of them. Live discussions and coordination is done over IRC at #sympy on irc.freenode.net (but everything important is then also put into Issues/list, so that all decisions are documented). Also, all mercurial and svn commits (code, issues, wiki changes) are sent live to the #sympy channel, so when working on sympy, it's a nice idea to log in, to see what other people are doing on the project.

Then there is a [http://planet.sympy.org/ Planet SymPy], that aggregates blogs of all developers of !SymPy, so you can read what they are doing at one place.

When writing some code for !SymPy, please follow the guidelines in the [http://docs.sympy.org/sympy-patches-tutorial.html SymPy patches tutorial]

So please subscribe to both the mailinglists and issues, to be in touch with the other developers. Submit enough patches and you will be given hg push access (but all code is reviewed anyway, see below). Start by going into the Issues and try to fix/implement something, or create a new issue for something you want to implement and then do it and send your patch to [http://groups.google.com/group/sympy-patches sympy-patches], or append it to the issue. We'll review it and commit it.


# Rules

We have just two rules:

 * All code that goes to !SymPy needs to be reviewed by at least one other developer.
 * All the tests need to pass.

This means, that _all_ the functionality that the user expects from a symbolic system need to have a test case. If you implement a new feature, write a test case for it (and as long as this test case passes, the feature is considered to work). If you think there is a bug, write a test case which fails and then fix the bug. 
If you think some other test case should be modified, please discuss it on the mailing list first. It's very important, so let's repeat it once more: if you don't write a test case for all your features that you implement/fix, it will be like you contributed nothing and just wasted your time, because those features will stop working the next time we refactor the library (and conversely, if you write tests for the new features, they will be guaranteed to work forever).

This also means, that any refactoring is easy to do, just make sure all the tests run. And because refactoring is easy, we are not afraid of making huge changes if we think the code will be more readable or simpler. If you want to find more about this kind of attitude, google the phrase "extreme programming".

To execute tests before a commit, use:
```
python setup.py test
```
The result should look like the ExampleTestRun.

Optionally, when debugging, you may want to only execute some particular tests using `py.test`, or only the doctests using `python setup.py test_doc`. But before each commit, test the whole package including docstrings. You may also use DistributedTesting, it's much faster.

# How to work with git in !SymPy

  * `git clone git://github.com/sympy/sympy.git` to get the !SymPy repository
  * do some modifications in your local copy (implement a new feature, fix a bug, add some new files using `git add` etc.)
  * `./setup test` to make sure all the tests pass
  * `git status` (optional) prints a list of files that you modified
  * `git diff` (optional) shows a "diff", so that you can see what exact changes you are going to commit
  * `git commit` will fire up an editor and you write a comment about what you changed (the `git diff` output from above will help you). This command can also be run non-interactively using `git commit -m "comment"`.  It you want to commit everything, do `git commit -a`.  You can commit only chunks by doing `git commit --interactive`.
  * do some more commits if you want
  * `git format-patch HEAD^ ; git send-email 0001-Add-whitespace.patch sympy-patches@googlegroups.com` to send your changes the mailinglist, and we will review it and either commit it, or help you improve it.

See GitTutorials for more information on working with git.

# Lists

Besides the mailing list, there is a list where all issue changes are sent:

http://groups.google.com/group/sympy-issues

So if you want to be notified of any change, subscribe to the list. Then there is a list which receives all subversion commits:

http://groups.google.com/group/sympy-commits

And also, we review each-other's patches here:

http://groups.google.com/group/sympy-patches