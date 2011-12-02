

*Update January 3, 2008*: Current state is written in the blogpost:

http://ondrejcertik.blogspot.com/2008/01/sympysympycore-pure-python-up-to-5x.html

*Update December 22, 2007*: The motivation is slightly changing over the time - Sage has currently the biggest potential to compete with Mathematica and Maple. Sage's notebook is just awesome. Sage uses Maxima for Sage.calculus now, because Maxima is well tested and works most of the time (also it's quite fast, etc.), but it has issues - it's in LISP and it's difficult (impossible) to extend using Python. So !SymPy's approach is the way to go in the long term. But until we reach similar features as maxima (not that far away), comparable speed (still quite a lot of work to do) and make !SymPy as a drop in replacement for Maxima in Sage, it cannot and it will not be made default in Sage.

*Older text*

Why not use CAS with its own language (like Maple/Mathematica/Maxima)
is best described by: http://www.ginac.de/FAQ.html#whynotmaple

We want to use CAS from a 'classic' language like C, C++, Python (maybe
Java, Ruby, and C# as well). There are many symbolic manipulation programs (see the links), but currently, there are only three libraries, GiNaC, Giac
(both for C++) and Sage (Python, see below) that satisfy this need. Even GiNaC and Giac are too
complicated (thousands lines of code) and difficult to extend, unfortunately. !SymPy
tries to be as simple as possible while remaining a full
featured CAS. This means that we prefer the algorithm that is
implemented by the least amount of lines; also, we try to avoid
implementing one feature several times. It will not be as fast (it wouldn't be anyway,
it's written in Python) as it could if we used C++, but it will be easy to extend with your own new algorithms or symbolic functions. And your code is just a regular Python program, calling !SymPy as a regular module, so you are not stuck in a language of the CAS system, which is not well designed for real programming.

Later, we might implement special algorithms for special cases to
make it faster and also rewrite it in C++. It is not certain though, that
a general purpose CAS (which !SymPy is intended to be) can be as fast as a
specialised CAS (say, for polynomial computations). The aim is to play
with the problem in !SymPy, implement a working algorithm, and later,
if it works and is not fast enough, implement it in
a different language, more suitable for the task. 

To sum it up: It would be nice to have an opensource alternative to Maple/Mathematica, that is reasonably fast (maybe written in C++), could be easily extended with your own ideas, would be callable from python and could be used in real world problems (as Maple/Mathematica can). Sage is also trying to achieve this goal (see also their [http://modular.math.washington.edu/sage/doc/html/tut/node58.html Why Python?] explanation), but using a different approach - !SymPy aims to be a lightweight normal python module, whereas Sage aims
to glue together every useful open source mathematics software package
and provide a transparent interface to all of them. Thus it is quite huge, which brings other problems, like that it cannot be easily packaged in Debian at the moment. Also we think !SymPy classes are currently simpler than Sage.calculus (Sage is faster though, since it uses Maxima as its backend).

Another advantage of !SymPy is that since it is written in pure Python (and doesn't need anything else), it is perfectly multiplatform, it's small and easy to install and use.

!SymPy can be used from Sage as an optional module (it is in Sage version 2.7 and later by default). Sage is promising, because it will eventually allow to use all good opensource CAS systems from python, but our aim is a little different - !SymPy will remain as a simple (but powerful) Python module for symbolic manipulation and the stress is not on a speed, but on a simplicity and versatility.

The code is still in development, but it's already quite useful - for
example, we believe !SymPy has the shortest (around 300 lines) open source
code for computing symbolic limits.