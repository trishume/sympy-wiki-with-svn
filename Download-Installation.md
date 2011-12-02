

([ All downloads])

# Download

!SymPy is packaged for the following systems below, so if you use one of them, simply follow the instructions. Otherwise (or if you prefer), you can install the sources directly.

# Sources

The only prerequisite is python 2.5 or newer. !SymPy optionally uses some other modules or packages, but they are optional. If you have problems using it on a pure Python installation, please report the problems into the Issues and we'll fix that.

* latest release *

Download the latest tar.gz (something like `sympy-0.6.7.tar.gz`) from the [ Featured Downloads] on the front page.

On unix systems (linux, BSD, Mac OS X, cygwin, etc.): extract it with the command `"tar xzf sympy-0.4.0.tar.gz"` and follow the README located in the sympy directory.

You can also download it from the Python Package Index: 

* previous releases *

You can access all the previous (and other) downloads
from [ Downloads].

This is useful if the latest release doesn't work for you for some reason.

* git version *

To get the git repository, use:
```
git clone 
```

And you can also access it on the web:



# Packages

[ ] * Debian * 

!SymPy is in Debian Lenny and later. The exact !SymPy versions in Debian can be seen  here: 

So just add the unstable (or testing) among your sources and
```
apt-get install python-sympy
```

[ ] * Ubuntu *

!SymPy is in all version starting from Gutsy. The exact !SymPy versions in Ubuntu can be seen here:  

[ ] *Gentoo*

!SymPy is available in the portage tree. To install !SymPy issue:
```
emerge -av dev-python/sympy
```
You can also install !SymPy from `sunrise` overlay.

To setup this overlay, issue:
```
emerge -va layman
echo "source /usr/portage/local/layman/make.conf" >> /etc/make.conf
layman -f -a sunrise
```
You can then regularly update to the latest reviewed revision:
```
layman -s sunrise
```

All packages in the `sunrise` overlay are considered unstable, so:
```
echo "sci-libs/sympy ~x86" >> /etc/portage/package.keywords
```

Then you can install !SymPy as any other package:
```
emerge -av sci-libs/sympy
```

[ ]
* openSUSE *

You can get it using the Build Service: 
or using zypper:
```
zypper ar 
zypper in python-sympy
```

[ ] * SAGE *

!SymPy is in SAGE 2.7 and later. The exact version of !SymPy in SAGE can be seen here:


[ ] * Windows *

Download the windows installer from the frontpage ([ Featured Downloads]) and execute it. There is one known [ issue] with missing MSVCR71.dll, but !SymPy works fine.


*Mac OS X*

An alternative for Mac OS X users is to use the [ Fink] package manager system. You can install sympy by typing `fink install sympy-py26`.  Replace `py26` with whatever version of Python you want to use.  The most recent version available is recommended.  Do `fink list sympy` to see all available options.  

# Installation

Either use the usual:
```
python setup.py install
```
or just go to the unpacked directory and use it directly (without installation):
```
$ python
Python 2.4.4 (#2, Aug 16 2007, 02:03:40) 
[GCC 4.1.3 20070812 (prerelease) (Debian 4.1.2-15)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import sympy
>>> 
```

If it is possible for you, we suggest you use `isympy`:
```
$ bin/isympy 
Python 2.4.4 console for SymPy 0.5.8-hg. These commands were executed:
>>> from __future__ import division
>>> from sympy import *
>>> x, y, z = symbols('xyz')
>>> k, m, n = symbols('kmn', integer=True)
>>> f = Function("f")
>>> Basic.set_repr_level(2)     # pretty print output; Use "1" for python output
>>> pprint_try_use_unicode()    # use unicode pretty print when available


In [1]: integrate(x*sin(x), x)
Out[1]: -x*cos(x) + sin(x)

In [2]: Integral(x**2 * sin(x), x)
Out[2]: 
⌠             
⎮  2          
⎮ x *sin(x) dx
⌡             
```

## Test it

Test that !SymPy works:
```
>>> from sympy import Symbol, cos
>>> x = Symbol('x')
>>> e = 1/cos(x)
>>> print e.series(x, 0, 10)
1 + (1/2)*x**2 + (5/24)*x**4 + (61/720)*x**6 + (277/8064)*x**8 + O(x**10)
```

To test the whole !SymPy package, run `./setup.py test` in the `sympy` directory. Note: you only need the standard Python 2.4 (or newer) to run all tests. If it doesn't work, please report the problem into the [ Issues].
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 