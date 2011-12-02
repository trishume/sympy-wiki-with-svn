

# Introduction

This wiki describes how to work with setup.py. Help:
```
./setup.py --help-commands
```
This will print a summary of all commands that `setup.py` understands.

# Cleaning

To clean the sources (so that `svn st` returns nothing), do 
```
./setup.py clean
```

# Man page

The man page is in `doc/man/isympy.1`, and it is generated from the file `doc/man/isympy.xml`. To edit it, edit just the file `doc/man/isympy.xml` and then rebuild the man page with

```
  docbook2x-man doc/man/isympy.xml
  mv isympy.1 doc/man/isympy.1
```

# Testing dependencies

Use the `bin/test_pure` file (see the documentation in it).

# Generating the (html) documentation for the api

## pydoctor

In the sympy root directory (where the setup.py is):

```
$ pydoctor --make-html --add-package sympy
adding directory sympy
findImportStars
210 / 210 modules parsed 
extractDocstrings
210 / 210 modules parsed 737 warnings 
finalStateComputations
writing html to apidocs using pydoctor.html.SystemWriter
```

a new directory `apidoc` is created with the documentation. Copy `apidoc/*` to `http://sympy.googlecode.com/svn/sympy/api/`

Don't forget to:
```
svn propset svn:mime-type text/css apidocs.css
svn propset svn:mime-type text/html *.html
```

## epydoc

Unfortunately, this doesn't work for sympy anymore.

You'll need epydoc (wajig install python-epydoc). (The output is written to ../api/ (you can change this editing the variable gen_doc.target_dir ))

```
svn checkout https://sympy.googlecode.com/svn/ sympy --username ondrej.certik
cd sympy/trunk
./setup.py gen_doc
cd ../api
svn propset svn:mime-type text/html *.html
svn ci
```

# How to make a new release

See NewRelease.