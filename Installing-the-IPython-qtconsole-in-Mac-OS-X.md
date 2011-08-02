I had a hell of a time getting the qtconsole for the new [IPython 0.11](http://ipython.org/) to work in Mac OS X, so I'm noting everything I did here.  I did this all in Lion, but it should also work in Snow Leopard.

1. First, make sure that you do everything with the latest version of the system Python.  This should be `/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7`.  

    Make sure that this is 64-bit.  You can check this by running

    ```python
    print '32-bit' if isinstance(int(2**42), long) else '64-bit'
    ```

    in Python.  You can also just run `python -c "print '32-bit' if isinstance(int(2**42), long) else '64-bit'"`. If it isn't 64-bit, download the 10.6/10.7 installer at http://www.python.org/download/.

2. Now, you need to install IPython.  A simple `pip install ipython` or `easy_install ipython` should do it.  Alternately, you can download the source, or clone the [git repo](https://github.com/ipython/ipython) and install from that.

    Now, you have the new IPython.  It will work with the terminal out of the box.  You may want to play around with the new configuration (it should tell you about this the first time you start IPython).  

    To get the qtconsole, you need to install some dependencies.  

3. First, you will need Xcode to compile some stuff.  In Lion, just install it from the App store (note, this installs an installer, which you then need to run).  I used Xcode 4, but this might also work with Xcode 3.

4. Next, you need to install QT.  Install the QT **Library** (not the SDK) for Mac OS X from http://qt.nokia.com/downloads.  If you installed the right one, there should now be a QT folder in `/Developer/Applications`.  

5. Here is the hard part: pyqt.  Don't even try compiling this yourself; it won't work (or at least that's what I've been told; I haven't tried it since a few months ago when I was using Mac OS X 10.6, when it didn't work).  You want to rather use [homebrew](https://github.com/mxcl/homebrew) to compile it for you (alternately, you can try manually applying the [homebrew formula](https://github.com/mxcl/homebrew/blob/master/Library/Formula/pyqt.rb) for it; I haven't tried this myself).  

    Install homebrew by running

    ```bash
    /usr/bin/ruby -e "$(curl -fsSL https://raw.github.com/gist/323731)"
    ```

    (see https://github.com/mxcl/homebrew/wiki/installation).  This will guide you to do some stuff.  If you have fink or macports installed, it will warn you.  I have fink installed, and this all worked.  

6. Now, install pyqt by running `brew install pyqt`.  Make sure you extend your `PATH` as it tells you, or else Python won't be able to find it.

    Test that you have done this right so far by running

    ```bash
    $ ipython qtconsole
    ```

    If you did it right, it should tell you you need pyzmq.  If it tells you you need pyside or pyqt, you didn't install pyqt correctly.

    Now, to get pyzmq.

7. First, install zeromq.  I compiled this from the master of [the git repository](github.com/zeromq/zeromq2-1).  The tarball from http://www.zeromq.org/intro:get-the-software should work too.  I think you need version 2, not 3.

    Compile this using

    ```
    ./autogen.sh # you may not need this one if you use the tarball
    ./configure
    make
    make check
    sudo make install
    ```

    Note that I had some errors when I did `make check`, but it doesn't seem to be a problem.

8. Now, get pyzmq.  Again, you can go [tarball](http://www.zeromq.org/bindings:python) or [git](https://github.com/zeromq/pyzmq).  `easy_install`/`pip` won't work because you need to specify the zmq path when you build.  

    8a. Note, if you use git, you will first need to install cython (you might as well use [git](https://github.com/cython/cython) for this too).  

    To build pyzmq, do `sudo python setup.py install --zmq="/usr/local"`.  

9. If you did this all right, you should now be able to use the qtconsole.  Try

    ```bash
    $ ipython qtconsole
    ```

    If it works, the Python rocketship application should open, and a GUI window with a IPython shell should open up.  This is the qtconsole!

# Notes

- `./setup.py clean` doesn't work very well in most repositories (such as IPython).  If you are using git, you can clean everything better using `git clean -Xdn` first (this is a dry run), and then `git clean -Xdf` if you are OK with what it will delete.

- If you use fink, or for whatever reason have some other version of Python from the system one in your `PATH`, make sure you always explicitly call `/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7` in all the `setup.py install` steps.  If you installed something but it still can't find it, this is likely the culprit.  Do a hard clean (see above) and try again.

- To use the qtconsole with SymPy, run `ipython qtconsole --profile=sympy`.  This makes the qtconsole run similar to isympy.  It's also supposed to use LaTeX for the math, though this hasn't been the case for me.

- This is all just how I did it.  Hopefully I didn't forget anything.  Your milage may vary.

