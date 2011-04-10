## Download python and msysgit

Install Python from:

[[http://python.org/download/]]

by downloading the "Python 2.7 Windows installer" (or Python 2.6 or 2.5) and running it.

Install msysgit:

[[http://code.google.com/p/msysgit/]]

by downloading and running the .exe in "Featured Downloads". Select to only install "Git Bash". Select "Checkout as-is, commit as-is" option. There should be a "Git Bash" executable on your Desktop. 

## Clone SymPy repository

Run "Git Bash" terminal window, then:

```bash
$ git clone git://github.com/sympy/sympy.git
$ cd sympy
$ bin/isympy
```

Enjoy!

You can also run python just like on linux. In sympy directory type:
```bash
$ python
>>> import sympy
>>>
```

If you want to make patches for SymPy see also: [Development workflow](https://github.com/sympy/sympy/wiki/Development-workflow)