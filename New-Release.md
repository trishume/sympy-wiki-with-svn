This is a step by step guide on how to make a new release of SymPy.  If you are following it to make a new release, please update it with any corrections or problems that you come across.  This guide was written with 0.7.0 as the sample release.  Replace "0.7.0" in the commands with the version that you are releasing, and "0.6.7" with the previous version.

# How to make a new release 

Proposed workflow (for the 0.7.0 release, for example)

1. Fix all blockers (i.e., issues marked with the label Milestone-Release0.7.0), or postpone them if they aren't too important and will take too much work to fix.  While you're doing this, it's a good idea to start writing the release notes.  See "Release notes" below.
2. Create a new branch 0.7.0, do the release patches in it.
3. Continue in master just like if nothing was happening.
4. Create rc1 from the 0.7.0 branch, test it, push fixes to 0.7.0. do rc2 etc. do final release.
5. Wait for some time and see if all is ok, possibly do some release fixes (like wait for one week).
6. Merge 0.7.0 with master, delete the branch.
7. If more fixes are needed, simply fork from the latest 0.7.0 tag, and push more fixes, release and merge.

Note that some of the stuff below tests things in master (like the test_pure* scripts). If you choose this route, you may need to modify them to test the 0.7.0 branch). 

## Are all tests included?

As directed in `setup.py`, check the tests list using the command:
```bash
$ python bin/generate_test_list.py
```

# Are all modules included?

As directed in `setup.py`, check the module list using the command:

```bash
$ for i in `find sympy -name __init__.py | rev | cut -f 2- -d '/' | rev | egrep -v "^sympy$" `; do echo "'${i//\//.}',"; done | sort
```

## Does it depend on Python 2.5-2.7 only?

Run the tests sandboxed using tox.  See [[Using-Tox]] and the tox.ini.sample file in the git repo.

## speed of import

After several runs, this should be around:

``` python
$ ipython 

In [1]: time import sympy
CPU times: user 0.08 s, sys: 0.00 s, total: 0.09 s
Wall time: 0.09
```

You can also use the `test_import` utility like this:

``` bash
$ bin/test_import 
Note: the first run (warm up) was not included in the average + std dev
All runs (including warm up):
[0.112630844116, 0.112730026245, 0.13080096244799999, 0.11622381210299999, 0.113546848297, 0.13612699508699999, 0.115744113922, 0.112670898438, 0.11331987381, 0.13219594955399999, 0.113155126572]
Number of tests: 10
The speed of "import sympy" is: 0.119651 +- 0.008924
```

Run this in the last release and see it the tolerance intervals overlap. If they do, there is no statistically significant change in the import time.  If they do not, and the new time is slower, you should investigate.

You should not compare them with the timings pasted here, as they were probably run on a different machine, and are thus not comparable to yours. 

## Do all tests run in the isolated environment?

Do this on the git version:

``` bash
$ bin/test_isolated 
Generating py.test isolated testsuite...
Done. Run '/tmp/test_sympy.sh'.
$ /tmp/test_sympy.sh |less
```

And check manually, that no py.test run generated a stack trace. (search for "COMMIT" in the `less` environment, when all tests have finished)

## Do all examples work?

```bash
$ examples/all.py -w
```

Make sure no traceback is generated and this is printed at the end:

```
NO FAILED EXAMPLES
```

Note that the `-w` will make it also run windowed examples, which will require things like pyglet and matplotlib to be installed to work.  

Also, make sure that all the examples are included in `all.py` by comparing the included modules with the output of `ls -R examples`.

## Does pyglet work?

Create a file `plotting.py` with

```python
from sympy import Symbol, cos, sin, Plot, log, tan
from sympy.abc import x, y
print Plot(cos(x)*sin(y), sin(x)*sin(y), cos(y)+log(tan(y/2))+0.2*x, [x, -0.00,
    12.4, 40], [y, 0.1, 2, 40])
```

Then I create a file `tox.ini.plotting` with

```
[tox]
envlist = py25,py26,py27

[testenv:py25]
basepython = /Library/Frameworks/Python.framework/Versions/2.5/bin/python2.5
deps=ctypes 
    pyglet
commands = pythonw plotting.py

[testenv:py26]
deps=pyglet
basepython = /Library/Frameworks/Python.framework/Versions/2.6/bin/python2.6
commands = pythonw plotting.py

[testenv:py27]
deps=pyglet
basepython = /Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7
commands = pythonw plotting.py
```

(Python 2.5 requires ctypes, see <http://docs.sympy.org/dev/modules/plotting.html>). If you do not use Mac OS X, you will need to modify the basepython lines, or just remove them.

Then, run

```bash
$tox -c tox.ini.plotting 
```

And verify that the plots open correctly all three times.

Note, because of the `pythonw` calls, the above tox call does not actually run from the virtualenv.  Therefore, you will have to have Pyglet installed in each version of Python. You can get it at http://www.pyglet.org/.  We should support whatever the latest version is.

In Linux, it might work without the `pythonw`.  So if it says it can't find `pythonw`, try changing it to just `python`.
 
## check all tests in sympy/external

Currently numpy, scipy, sage, and some fortran compilers.  Open the test files to see what libraries you need to install for them to run.  To run the sage tests, you have to run `sage -python bin/test sympy/external/tests/test_sage.py` (see the docstring of the `sympy/external/tests/test_sage.py` file).

## check docs

```bash
$ cd doc
$ make clean
$ make html
$ epiphany _build/html/index.html # Or your preferred web browser
```

and update the version in `src/conf.py`, update the list of contributors both in docs and in AUTHORS, using (for example, for the 0.7.0 release):

```bash 
$ git shortlog -ns sympy-0.6.7..
```

(use the tag of the latest release) and then update the information what each contributor changed using 

``` bash
$ git shortlog -n sympy-0.6.7..
```

See also the bit about .mailmap below for another useful git command to use here.

## does the tarball contain all the needed files?

The previous paragraph tests, that all tests pass in the tarball,
but still check by inspection, that the tarball includes all necessary files. Files in the bin directory are potentially installed to /usr/bin, so be careful.

You may have a look an at MANIFEST.in which defines the files to be included in the tarball.

## Do the actual release

Change version in `sympy/__init__.py` and `doc/src/conf.py`, e.g.

``` bash
vim doc/src/conf.py  # Or your preferred text editor
vim sympy/__init__.py
git commit -a -m "SymPy 0.7.0 release"
```

Make sure you also change it everywhere else by doing `git grep 0\.6\.7` (replacing `0\.6\.7` with the last release version).

Change the copyright year in README if needed.  Note that this should be done at the beginning of each year.

Tag it, e.g.

```bash
git tag sympy-0.7.0
```

Prepare the release tarball and win32 installer (should work ok even on Linux)

```bash 
./setup.py clean
./setup.py sdist
./setup.py bdist_wininst
```

Note: It's possible to make a 64-bit Windows installer if you are on Windows.  See http://docs.python.org/distutils/builtdist.html#cross-compiling-on-windows and http://code.google.com/p/sympy/issues/detail?id=1235.

Compile the html documentation

```bash
cd doc
make clean
make html
cd _build
mv html sympy-0.7.0-docs-html
zip -9lr sympy-0.7.0-docs-html.zip sympy-0.7.0-docs-html
```

And put `dist/sympy-0.7.0.tar.gz`, `dist/sympy-0.7.0.win32.exe` and `sympy-0.7.0-docs-html.zip` on the website.  Note that depending on what operating system you run the above in, you may need to rename the Windows binary to `sympy-0.7.0.win32.exe` (as mentioned above, even if you compile it in Linux or Mac OS X, it should still work in Windows).

Upload these files to http://code.google.com/p/sympy/downloads/ Use the files from previous versions as a guide.  Be sure to remove the "Featured" tag from the files from the previous release.

Change version to 0.7.0-git, and start new development cycle

```bash
vim sympy/__init__.py
git ci -a -m 'Start of 0.7.1 development cycle'
```


Don't forget to finally push you changes back to the main repository:

```bash
git push git@github.com:sympy/sympy.git master
```

## Get list of authors who contributed to the release
Use `git log sympy-0.6.7.. --format="%aN" --reverse | sort -u` to get the list of contributors (see [this page](http://stackoverflow.com/questions/6482436/list-of-authors-in-git-since-a-given-commit)). 

This is a good time to update the `.mailmap` file, so that there are no duplicates.  You may need to email the people in question concerning the preferred spelling of their names/preferred email addresses, though you should generally prefer real email address to auto-generated addresses (like `devnull@localhost` or `john@example.(None)`), and names with accents to names without accents.  This should also be in sync with the AUTHORS file.  If you can't contact someone about the preferred email or name spelling, just use the version in the AUTHORS file. Note that when you update the `.mailmap` file, you should use the command `git log --format="%aN <%ae>" | sort -u`, which will show the whole log and include email addresses. 

Sort the authors everywhere by last name.  Note that we decided to do this, instead of sorting by number commits or number of lines changed for fairness purposes (for example, if someone updates mpmath, they will unfairly have a larger count of line's changed; this can also happen, e.g., if someone moves some files around).  You can change the above bash command to use `sort -u +1 -2` which sorts on the second "field" in the list, which should be the last name.

This list should be included at the bottom of the release notes.  Mark anyone who contributed for the first time for this release with a `*` (you can get this list by running `git diff sympy-0.6.7..sympy-0.7.0 -- AUTHORS`).

## Building a Mac OS X Installer package

_Note, this relies on https://github.com/sympy/sympy/pull/748_

A Mac OS X PackageMaker project file can be found under the `data/OS X Package` directory. It references the isympy shell, its man page, and the `sympy` subdirectory. To build a new Installer package, open the project file and hit 'Build'. The resulting file can be distributed for Macs running OS X version 10.5 "Leopard" and above.
#How to make new 64-bit release of SymPy for Windows 

The Windows SymPy binary("sympy-0.7.1.win32.exe") doesn't work, when the user using 64-bit Python release.

When try to install SymPy he get an error message: "No Python information found in the registry".

That's because "python-2.7.2.amd64.msi" installer put his regystry file in:
```bash
[HKEY_LOCAL_MACHINE\SOFTWARE\Python\PythonCore\2.6\InstallPath]
```
but "sympy-0.7.1.win32.exe" binary search it in:
```bash
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Python\PythonCore\2.6\InstallPath]
and
[HKEY_CURRENT_USER\Software\Python\PythonCore]
```

So the user need to install "sympy-0.7.1.win-amd64.exe" witch is the 64-bit version of SymPy

To make new 64-bit installer of SymPy we need to have Windows machine and then:
```bash
cd /path/to/SymPy
python setup.py build --plat-name=win-amd64 bdist_wininst
```

That will create "sympy-0.7.1.win-amd64.exe" in dist directory.

You can't create "sympy-0.7.1.win-amd64.exe" in other machine(linux,mac), because binary creator in them doesn't support "--plat-name" attribute.
More information:
http://docs.python.org/distutils/builtdist.html#cross-compiling-on-windows

## Sites to update

If you don't have privileges to write to any of these, ask Aaron, and he will either give you write access or do it himself.

  * http://code.google.com/p/sympy/ (FrontPage)
  * https://github.com/sympy/sympy/wiki/ (May not be much to do here)
  * http://code.google.com/p/sympy/wiki/Changes
  * http://en.wikipedia.org/wiki/SymPy (If you can, update the article for other languages too)
  * http://en.wikipedia.org/wiki/Comparison_of_computer_algebra_systems (Both version and features)
  * http://freshmeat.net/projects/sympy/
  * http://pypi.python.org/pypi/sympy/ (see below)
  * http://live.sympy.org/
  * http://docs.sympy.org/ (via https://github.com/sympy/sympy_doc)
  * http://sympy.org/ (via https://github.com/sympy/sympy.github.com)
  * http://sympy.blogspot.com/

### pypi

```bash
$ git co sympy-0.7.0
$ python setup.py register
$ python setup.py sdist upload
```
You may have to fix the uploaded file by hand over the web, so that it has the
same md5sum as the one on googlecode.  See also http://guide.python-distribute.org/contributing.html.

Make sure it is installable using easy_install and pip.  For the documentation to upload for http://packages.python.org/sympy, the zip file you created above won't work, because it is a zip of the directory, and it wants an index.html at the root level.  I was able to fix it by selecting everything in the `sympy-0.7.0-docs-html` directory in the Finder in Mac OS X and right clicking and choosing "Compress", and uploading the `Archive.zip` file that created.  No doubt this could also be done with the command line (if you know how, please update the zip command above to do it).

## Release notes

If you haven't done it already, write up the release notes at [[Release-Notes-for-0.7.0]], replacing "0.7.0" with this version.  Use the notes from pervious versions as a guide.  Go through the git log and include all important changes from the user perspective (there's no need to document changes that only affect internals).  There's no need to be exhaustive against every single change, as there always exists the git log.

It's generally a good idea to enlist the people who made the various changes to write that section of the release notes, especially if you aren't familiar with that code or change.

But the most important changes up front (at the top).  This includes major new functionality and any backwards compatibility breaks.

## Other things

  * Merge the 0.7.0 branch back with master.
  * Delete the 0.7.0 branch.
  * Create a Debian package
  * Create a SymPy spkg Sage package. See http://code.google.com/p/sympy/wiki/SymPyspkg, which is kind of outdated.  You can get a more up-to-date guide from the current Sage spkg.  See http://trac.sagemath.org/sage_trac/ticket/11560#comment:8
  * Send an email to the list.  Include a copy of the release notes and the list of people who contributed to the release.
  * Make sure that there are milestone labels in the issue tracker for at least two versions in the future.  So if 0.7.0 is the most recently released version, make sure there are Milestone-release0.7.1 and Milestone-release0.7.2 labels.
  * Make sure any issues in the issue tracker that were fixed by the release are closed (this should not be done until the 0.7.0 branch is merged with master).