

# Download & setup Sage

```
wget http://sagemath.org/SAGEbin/linux/32bit/sage-2.11-debian32-intel-i686-Linux.tar.gz
cd ~/ext
tar xzf sage-2.11-debian32-intel-i686-Linux.tar.gz
ln -s sage-2.11-debian32-intel-i686-Linux sage
```

Now you can always call it using `~/ext/sage/sage`. Now put this:
```
~/ext/sage/sage $@
```
into `~/bin/` and put `~/bin/` into your search path. Then you start Sage just by typing `sage`.

# Steps

```
$ hg clone http://hg.sympy.org/sympy-spkg/
$ cd sympy-spkg
```
Edit get-hg
```
$ ./get-hg
$ cd ..
$ cp -a sympy-spkg sympy-0.5.13
$ sage -pkg sympy-0.5.13
```
And a fresh package sympy-0.5.13.spkg is created. Install it:
```
$ sage -f sympy-0.5.13.spkg
```
Test it
```
$ sage -t ~/ext/sage/devel/sage/sage/calculus/test_sympy.py
```

## how to install the original sympy version

```
cd spkg/standard
rm sympy-0.5.7.spkg
wget http://sagemath.org/packages/standard/sympy-0.5.7.spkg
sage -f sympy-0.5.7.spkg
```

## How to develop with Sage

Change some files in Sage and do:
```
sage -b
```