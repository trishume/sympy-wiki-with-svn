This is a step by step to make a new release of SymPy.  If you are following it to make a new release, please update it with any corrections or problems that you come across.  This guide was written with 0.7.0 as the sample release.  Replace "0.7.0" in the commands with the version that you are releasing, and "0.6.7" with the previous version.

# How to make a new release 

Proposed workflow (for the 0.7.0 release, for example)

1. Fix all blockers (i.e., issues marked with the label Milestone-Release0.7.0).
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
$ for i in `find * -name __init__.py | rev | cut -f 2- -d '/' | rev | egrep -v "^sympy$ | thirdparty" `; do echo "'${i//\//.}',"; done | sort
```

## Does it depend on python2.4 only?

Do this on the git version:

``` bash
$ cd bin
$ sudo pbuilder --execute test_pure
```

All tests need to run here.  Note that this request debian to work.  It's actually much better to run the tests sandboxed using tox.  See [[Using-Tox]] and the tox.ini.sample file in the git repo.

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
$ examples/all.py
```

Make sure no traceback is generated and this is printed at the end:

```
NO FAILED EXAMPLES
```


## Does pyglet work?

Do this on the git version:

``` bash
$ cd bin
$ sudo pbuilder --execute test_pure_plotting
[...]
running install_egg_info
Writing /usr/lib/python2.4/site-packages/sympy-0.5.10_hg.egg-info
[0]: cos(x)*sin(y), sin(x)*sin(y), 0.2000000000000000111022302463*x + cos(y) + log(tan((1/2)*y)), 'mode=parametric'
Window initialization failed: Cannot connect to ""
/run: line 36: 14889 Segmentation fault      python plotting.py
Was the plot successful? If not, fix it and do 'python plotting.py'.
root@fuji:/# 
```

Note that like the test_pure test above, this requires Debian.  

Important is the `[0]: cos(x)*sin(y), ...` line, that shows that plotting was ok
and pyglet started. It cannot plot in the chroot, so the segmentation fault happens. That's ok. If it says "cannot import pyglet", that's bad and needs to be fixed.

I did this with tox on Mac OS X by creating a file `plotting.py` with

```python
from sympy import Symbol, cos, sin, Plot, log, tan
from sympy.abc import x, y
print Plot(cos(x)*sin(y), sin(x)*sin(y), cos(y)+log(tan(y/2))+0.2*x, [x, -0.00,
    12.4, 40], [y, 0.1, 2, 40])
```

(this is what the `test_pure_plotting.py` file creates).  Then I created a file `tox.ini.plotting` with

```
[tox]
envlist = py24,py25,py26,py27

[testenv:py24]
basepython = /Library/Frameworks/Python.framework/Versions/2.4/bin/python2.4
deps=ctypes
commands = pythonw plotting.py

[testenv:py25]
basepython = /Library/Frameworks/Python.framework/Versions/2.5/bin/python2.5
deps=ctypes
commands = pythonw plotting.py

[testenv:py26]
basepython = /Library/Frameworks/Python.framework/Versions/2.6/bin/python2.6
commands = pythonw plotting.py

[testenv:py27]
basepython = /Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7
commands = pythonw plotting.py
```

(Python 2.4 and 2.5 require ctypes, see <http://docs.sympy.org/dev/modules/plotting.html>). You can make this work in non-Mac OS X by modifying the basepython lines, or just removing them.

Then, I ran

```bash
$tox -c tox.ini.plotting 
```

And verified that the plots opened correctly all four times.  
## check all tests in sympy/test_external

Currently numpy, scipy, sage, and some fortran compilers.  Open the test files to see what libraries you need to install for them to run.  To run the sage tests, you have to run `sage -python bin/test sympy/test_external/test_sage.py` (see the docstring of the `sympy/test_external/test_sage.py` file).

## check docs

```bash
$ cd doc
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

## does the tarball contain all the needed files?

The previous paragraph tests, that all tests pass in the tarball,
but still check by inspection, that the tarball includes all necessary files. Files in the bin directory are potentially installed to /usr/bin, so be careful.

You may have a look an at MANIFEST.in which defines the files to be included in the tarball.

## Do the actual release

Change version in `sympy/__init__.py` and `doc/src/conf.py`, e.g.

``` bash
vim doc/src/conf.py  # Or your preferred text editor
vim sympy/__init__.py
git ci -a -m v0.5.9
```

Change the copyright year in README if needed.  Note that this should be done at the beginning of each year.

Tag it, e.g.

```bash
git tag sympy-0.7.0
```

Prepare the release tarball and win32 installer (should work ok even on Linux)

```bash 
./setup.py sdist
./setup.py bdist_wininst
```

Compile the html documentation

```bash
cd doc
make html
cd _build
mv html sympy-0.5.9-docs-html
zip -9lr sympy-0.5.9-docs-html.zip sympy-0.5.9-docs-html
```

And put dist/sympy-0.7.0.tar.gz, dist/sympy-0.7.0.win32.exe and sympy-0.7.0-docs-html.zip on the website.

Change version to 0.7.0-git, and start new development cycle

```bash
vim sympy/__init__.py
git ci -a -m 'Start of 0.7.1 development cycle'
```


Don't forget to finally push you changes back to the main repository:

```bash
git push git@github.com:sympy/sympy.git master
```

## Sites to update

  * http://code.google.com/p/sympy/ (FrontPage)
  * http://wiki.sympy.org
  * http://code.google.com/p/sympy/wiki/Changes  (use `git shortlog -n sympy-0.6.7.. | sort` to get the list of contributors)
  * http://en.wikipedia.org/wiki/SymPy
  * http://en.wikipedia.org/wiki/Comparison_of_computer_algebra_systems
  * http://freshmeat.net/projects/sympy/
  * http://pypi.python.org/pypi/sympy/
  * http://live.sympy.org/
  * http://docs.sympy.org/

=== pypi ===

```bash
$ git co sympy-0.7.0
$ python setup.py register
$ python setup.py sdist upload
```
You may have to fix the uploaded file by hand over the web, so that it has the
same md5sum as the one on googlecode.

Make sure it is installable using easy_install


## Other things

  * Create a Debian package
  * Create a [SymPyspkg SymPy spkg] Sage package
  * Send an email to the list.