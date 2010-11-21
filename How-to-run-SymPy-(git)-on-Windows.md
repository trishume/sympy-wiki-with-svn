## Download python and msysgit

Install Python from:

[[http://python.org/download/]]

by downloading the "Python 2.7 Windows installer" (or Python 2.6 or 2.5) and running it.

Install msysgit:

[[http://code.google.com/p/msysgit/]]

by downloading and running the .exe in "Featured Downloads". Select to only install "Git Bash". There should be a "Git Bash" executable on your Desktop. Run it:
```bash
$ echo "export PATH=/c/Python26/:\$PATH" > .bashrc
```

## Clone SymPy repository

Close and open the bash terminal window again, then:

```bash
$ git clone git://git.sympy.org/sympy.git
$ cd sympy
$ bin/isympy
```

Enjoy!

You can also run python just like on linux:
```bash
$ python
>>> import sympy
>>>
```
