If you have been around for some time and actively participating in
SymPy's development, you will be granted push access to the main
repository.  Then you can push in patches that passed review.


You need to add a remote repository for the main sympy repo if you don't
already have one (``git remote`` will show you all your remote
repositories).  If you don't, add one by doing ``git remote add sympy
git@github.com:sympy/sympy.git``.  You need to use this url because it
is the ssh url, which gives you push access (the others are read only).
When you have a branch ready to push in, say, the branch is named
"test", you do::

    git push --dry-run sympy test:master

and see what it tells you.  This will test the push.  The command
basically says "push to the remote repository "sympy", fast-forwarding
the remote branch "master" to the position of the local branch "test".
If it says everything is ok, and it looks right, then you can remove the
--dry-run and do the actual push.

"test" should be fast-forward from master.  **NEVER** do a -f push to
master.  If it tells you that a branch is non-fastforward, it is
probably because someone else updated the official master since you
created test.  So in that case you need to pull in the latest master and
update test using "git rebase test master" or "git merge test master"
(rebase is better for small branches, merge is better for large
branches).

Once a patch is pushed in to master, it is there.  There is no modifying the
history using ``git rebase`` or some similar. The reason is that if you change
the history to master, it will screw up the history of everyone who pulls from
it.  If you want to change what has been pushed in, you need to do it using
additional patches, like with ``git revert``.

Once you have pushed the test branch in, if test is the same as the
commit from a pull request at GitHub, or if you merged with master,
GitHub will close the pull request on its own.  Otherwise, i.e., if you
did a rebase, you will have to close it manually.  In either case, you
need to manually close the issue on the Google Code issue tracker.  Just
mark the status as Fixed.

So you can avoid breaking anything if you just do the --dry-run push
first, never do a -f push to master, and always make sure that you only
push stuff in that has been reviewed and passes tests.

And finally, don't be afraid to push something in if it has passed
review (including review by yourself) and the tests pass.  We tend to
have a backlog of patches that have passed review but have not been
pushed in for whatever reason. If you are not sure, consider whether the
patch is an improvement over the current situation.  If the answer is
yes, just push it in, it can be improved later.

For non-trivial patches it makes sense to wait until the patch has been
under review for at least 24 hours before pushing, so others have a
chance to state their objections.

## Checklist

There are basically four things that you need to do before pushing anything in:

1. Make sure all tests pass (if it is part of the main repo; for the webpage, make sure everything looks good and also that the pages are built).  Do this for the merged/rebased version to make sure that that didn't introduce any errors.

2. Make sure that all content has been reviewed (for example, make sure that the person didn't push in a new commit to the branch for review that you didn't notice).

3. Make sure that no one else has any objections to the branch.  Everything is based on consensus, so until one is reached, the branch cannot be pushed in.

4. All new functionality should be tested, and all new methods/functions/classes should have some doctests showing how to use them (the `./bin/coverage_doctest.py` script will show you what methods have doctests). 

