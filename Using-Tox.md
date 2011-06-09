Tox as is a generic virtualenv management and test command line tool, see the [web page](http://tox.testrun.org/en/0.9/index.html) or [this PyCon 2011 talk](http://python.mirocommunity.org/video/4240/pycon-2011-supporting-all-vers) for more information. The idea is to set it up and run tests locally in different environments (different Python versions, different ground types etc). 

The first step is installing it:

    pip install tox

Then, create a tox.ini file in the root directory (where setup.py is located). (perhaps there should be a "canonical" tox.ini file that will be tracked by git; for now, just create it) The following is an example:

    [tox]
    envlist = py25, py26, py27, docs
    [testenv]
    commands=python bin/test []
    [testenv:docs]
    commands=python bin/doctest [] 

The first specifies the environments to be tested; py24-py32 are builtin environments (as are jython and pypy) while docs is a (simple) custom one defined later. Following [testenv] we have some basic commands to be executed (in our case, we simply call our test script, but it can be anything). The last part defines a custom "environment", which is just a way of running doctests separately. The brackets [] allow us to pass arguments to the script we are calling (see next part).

NOTE: The appropriate Python interpreters have to be installed for tox to work.

Finally, run tox with:

    tox

or

    tox -e py25  (builds just the given environments, can be a comma-seprated list (no spaces!))

Tox will automatically create the necessary virtualenv, reusing them if they already exist (in case of some errors, you can force a rebuild with "tox --recreate") Everything else functions the same like normally.

It is also possible to call just specific tests, with the same syntax we currently support (that is the reason for [] in the tox.ini file). For example, the following command will recreate the Python 2.5 and 2.7 environments and run the hydrogen tests in them.

    tox --recreate -e py25,py27 hydrogen

## Installing multiple Python versions
In case your distribution doesn't provide multiple Python versions easily, you could try installing them from source. The trick is to use the following command:

    sudo make altinstall

which will append the number version to the executable (ie. Python2.4, Python2.5 ..). This will assure that the system remains functioning; Tox will find the correct executables, if they are in your PATH. Otherwise, you may use the `basepython` variable inside the desired environment, as demonstrated in the sample tox.ini file.