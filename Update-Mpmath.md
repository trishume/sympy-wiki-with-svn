

*Follow this guide to update the mpmath install in !SymPy whenever mpmath is updated.  If you discover any other things that belong here when updating, please edit the wiki and add them. *

An announcement will be sent to the sympy mailing list whenever mpmath is updated.  When this happens, the mpmath that is included with !SymPy needs to be updated.  

  * You can obtain the new mpmath from http://code.google.com/p/mpmath/.  
  
  * You need to copy the new mpmath into sympy/mpmath. *Note: When you copy stuff over, delete the old directory first, then copy the new one, so that we don't end up keeping files that were deleted in mpmath.*
  
  * At this point, it might be a good idea to run `./setup.py clean` (or `py.cleanup`) from the command line to remove all the `.pyc` files that might be left over from any deleted mpmath files.  This is especially a good idea if you get an `ImportError` when trying to use !SymPy after updating.

  * Use:

```
python bin/adapt_paths.py > /tmp/x
patch -p0 < /tmp/x
```
to fix the import statements in the mpmath tests.  Remove any .orig files that `patch` creates (`find sympy/mpmath | grep orig`). Read the docstring of `adapt_paths.py` for more info.

  * Run `./bin/strip_whitespace sympy/mpmath/ --recursive` to fix carriage returns in the mpmath source files.  ```./bin/test sympy/utilities/tests/test_code_quality.py``` will verify that everything is fixed here.

  * Copy the Sphinx docs ~~from the `doc/source` directory of mpmath~~ _as of mpmath 0.16, the docs are a separate download_ to the `doc/src/modules/mpmath` directory of sympy.  Again, remember to delete the old docs first so that you don't end up keeping any deleted files.  Then do `cd doc; make html` and verify that the docs build correctly.  It might also be a good idea to run `make clean` here first to clear out any docs that might have already been built.  Open the built docs (in `_build`) in a web browser and make sure it looks correct.  Pay close attention to any Sphinx warnings or errors relating to mpmath when it builds.  As of mpmath 0.16, you will need to update the paths to some plots in the function docstrings, which are mostly in mpmath/function_docs.py, from `/plots` to `/modules/mpmath/plots`.  You should also fix any whitespace problems in the doc files.  The code quality test currently doesn't test those, but git will warn you about them when you try to commit.  

  * Run tests and see if everything works, usually then one has to fix some little bugs.  Be sure to run both regular tests and doctests, and also to test all supported versions of Python (2.4 - 2.7 right now).  If you have any problems, ask on the mailing list or IRC.  Frederick Johansson is the author of mpmath, so he will be able to help solve any mpmath bugs you find.

  * If everything works, submit a patch.  When you commit, be sure to add any new untracked files in the mpmath directory .  `git status` will show you all untracked files, and `git add` will add them, or, if you use `git commit --interactive`, choose "add untracked", and add everything in the mpmath and mpmath docs directory.  