
.. sectnum::

.. |date| date::
.. |time| date:: %H:%M

smichr/2084 IPython console for SymPy 0.6.7-git (Python 2.6.6)

|date| |time|.

.. contents:: Table of Contents

===============
Tests
===============

>>> from sympy import *
>>> x, y, z, t = symbols('x y z t')
>>> k, m, n = symbols('k m n', integer=True)
>>> f, g, h = map(Function, 'fgh')


Sources of examples for test work-flow
========================================
    * simple functions
    * http://www.maplesoft.com/support/help/Maple/view.aspx?path=series
    * http://reference.wolfram.com/mathematica/ref/Series.html



Types of remarks
================

_`The Big-O is not present at point==0`.
--------------------------------------------

    The Big-O was expected, but there is no one. And also series are not truncated.
    (This type of remark must be distinguished from `The Big-O is not present at point != 0`_ case, where there is not present one because of some reasons.)
    The typical examples are:
    
    >>> ((1+x)**7).series(x, n=3)
    1 + 7*x + 21*x**2 + 35*x**3 + 35*x**4 + 21*x**5 + 7*x**6 + x**7
    
    but expected:
    1 + 10*x + 45*x**2 + O(x**3)
    
    >>> abs(x + x**2).series(n=1)
    x + x**2
    
    but expected:
    O(x)
    
    Note that in some cases Big-O is not present correctly:
    
    >>> ((1+x)**2).series(x, n=6)
    1 + 2*x + x**2
    >>> (1 + 1/x).series()
    1 + 1/x
    
    Ok
    
    But even in this case this collaborate with the next one: `Method "lseries" yield many terms`_.

_`Method "lseries" yield many terms`
-------------------------------------

    This type of errors possibly arise because of `The Big-O is not present at point==0`_ error.
    
    The typical examples are:
    
    >>> (x+1/x).lseries().next()
    x + 1/x
    
    expected: 1/x
    
    >>> (x+x**2).lseries().next()
    x + x**2
    
    expected: x
    
    >>> ((1+x)**7).lseries(x).next()
    1 + 7*x + 21*x**2 + 35*x**3 + 35*x**4 + 21*x**5 + 7*x**6 + x**7
    
    expected: 1
    
_`Incorrect power in Big-O expression`
--------------------------------------------

    Typical examples are:

    >>> (exp(x)/x**2).series()
    1/2 + x/6 + 1/x + x**(-2) + x**2/24 + x**3/120 + O(x**4)
    >>> (exp(x)*x**2).series()
    x**2 + x**3 + x**4/2 + x**5/6 + x**6/24 + x**7/120 + O(x**8)
    >>> (exp(x)/x**4).series()
    1/24 + x/120 + 1/(6*x) + x**(-4) + x**(-3) + 1/(2*x**2) + O(x**2)
    >>> (sin(x)/x**4).series()
    x/120 - 1/(6*x) + x**(-3) + O(x**2)
    
    compare 
    
    >>> (exp(x)*x**2).series()
    x**2 + x**3 + x**4/2 + x**5/6 + x**6/24 + x**7/120 + O(x**8)
    
    with 
    
    >>> ((exp(x)).series() * x**2).expand()
    x**2 + x**3 + x**4/2 + x**5/6 + x**6/24 + x**7/120 + O(x**8)

    
_`The Big-O is not present at point != 0`.
--------------------------------------------

    It was discussed.
    It is not implemented because of some reasons: it was deviation from the main issues and there is no understanding what to implement exactly and how.

_`"lseries" with two-variable function`
----------------------------------------
    
    Typical examples are:
    
    >>> sin(x+y).series(x, n=3)
    x*cos(y) - x**2*sin(y)/2 + sin(y) + O(x**3)
    >>> (sin(x+y)).series(x, n=3).series(y, n=3)
    x + y - x*y**2/2 - y*x**2/2 + O(x**3) + O(y**3)
    
    Ok, but

    >>> g = (sin(x+y)).series(x, n=3).lseries(y)
    >>> g.next()
    O(x**3)
    
    is incorrect, and
    
    >>> # g.next()
    >>> # StopIteration:
    
    rise exception 


_`Sort order of the terms is not canonical`
---------------------------------------------
    
    This is because of automatic "sympy idiosyncracies".
    It is not a really big error. But it confuse the result.
    
    >>> exp(x).series(x,1,n=3)
    E - E*(1 - x) + E*(1 - x)**2/2
    
    Ok

    >>> (x**2 + x+1/x).series()
    x + 1/x + x**2
    >>> 1/x + x + x**2
    x + 1/x + x**2
    
    Expected: 1/x + x + x**2
    
    >>> cos(x).series(x,1,n=2)
    (1 - x)*sin(1) + cos(1)
    >>> cos(1) - sin(1)*(x-1)
    (1 - x)*sin(1) + cos(1)
    
    Expected: cos(1) - sin(1)*(x-1) + O((x-1)**2)
    
    At the same time the 'lseries' method work more better:
    
    >>> g = cos(x).lseries(x,1)
    >>> g.next()
    cos(1)
    >>> g.next()
    (1 - x)*sin(1)
    
    Though more canonical result for series term could be "-(x - 1)*sin(1)"
    

_`Bases functions are not the powers of natural`
------------------------------------------------

    It is not a  error.
    
    >>> (exp(x)*log(x)).series(n=3)
    x*log(x) + x**2*log(x)/2 + log(x) + O(x**3*log(x))
    
    >>> (sqrt(x)*exp(x)).series(n=3)
    x**(1/2) + x**(3/2) + x**(5/2)/2 + O(x**(7/2))
    
    >>> (sqrt(sin(x))).series()
    x**(1/2) - x**(5/2)/12 + x**(9/2)/1440 + O(x**6)
    
    >>> (sin(sqrt(x))).series()
    x**(1/2) - x**(3/2)/6 + x**(5/2)/120 - x**(7/2)/5040 + O(x**6)
    
    >>> (log(sin(x))).series()
    log(x) - x**2/6 - x**4/180 + O(x**6)

    
    But we must note that those cases are not real "natural power series".
    

_`Insufficient of operations with series`
------------------------------------------

    It is for a future.
    Some operation are work fine due to the fine "Order" class realization:
    
    #) multiplication "series" by "expr"
    
        >>> exp(x).series()
        1 + x + x**2/2 + x**3/6 + x**4/24 + x**5/120 + O(x**6)
        >>> (exp(x).series() * x).expand()
        x + x**2 + x**3/2 + x**4/6 + x**5/24 + x**6/120 + O(x**7)
        
        Ok. We assume that x ==> 0. So multiplication x by O(x**6) yield O(x**7).
        
        >>> (exp(x).series()*y).expand()
        y + x*y + y*x**2/2 + y*x**3/6 + y*x**4/24 + y*x**5/120 + O(x**6)
        
        Ok, y is not present in series arguments, so it is considered as constant for O(x**6) 
        
        >>> (exp(x).series() * (x +1)).expand()
        1 + 2*x + 3*x**2/2 + 2*x**3/3 + 5*x**4/24 + x**5/20 + O(x**6)

        Ok. O(x**6) "eat" O(x**7) correctly.
        
        
    #) Multiplication series by series.
        
        >>> (exp(x).series() * exp(-x).series()).expand()
        1 + O(x**6)

        Ok. O(x**6) "eat" higher powers.
        
        >>> (exp(x).series(n=3) * exp(-x).series()).expand()
        1 + O(x**3)
        
        Ok. O(x**3) "eat" higher powers and O(x**6) too.
    
        But Operations at point != 0 are not work fine: 
        
        >>> (exp(x).series(x, 1, n=4) * exp(-x).series(x, 1, n=4)).expand()
        8/9 + x/2 - 11*x**2/12 + 8*x**3/9 - x**4/2 + x**5/6 - x**6/36
        
        Expected "1 + O((x-1)**4)"
        
        Compare with:
        
        >>> (exp(x).series(x, 1, n=4) * exp(-x).series(x, 1, n=4)).subs(x, x+1).expand()
        1 - x**4/12 - x**6/36
        
        This is because of `The Big-O is not present at point != 0`_ .
        
        My notes: the realization of summation and multiplication of 'series' with each other could be connected with `Sort order of the terms is not canonical`_ . It is clear that if I know terms then I know how to produce the result. (Though I don't clear understand what to do with multiplication "series" by "expr" )
    
    #) generator of terms.
    
        In core there are three methods "series" - main, "nseries", "lseries"

        "lseries" used for yielding in some core spheres. (Though I donn't clear understand the name-token.)
        
        As I understand, "nseries" is a master for "lseries" by default for base Expr class, so that is not effectively. It is mentioned in code comments.
        It is became historically. But also mentioned that subclasses must be implement "lseries" as needed in a better way.
        
        In my opinion "lseries" must be a master for "nseries" in future. At least for "natural power series". Though in some cases (when series are not "natural power series") it can be out of sense and in any case it is a deal for the internal realization after examination all of risks.
        
    #) generator for coefficients.
    
        It differ from "lseries" so that only coefficients yields, without "x**i" multiplicators.
        
        It is concerned only the pure "natural powers series" (or other formalized series, may by for "log(x)*x**i" terms and even for Laurent "1/x + 1 + x" too)
        
        In some cases the method for coefficients could be needed. For the internal realization it could be convenient too.
        
        Do generators must skip 0 terms on some orders it is another question for mind.
        sin(x) ==> [0, 1, 0, -1/6, 0, ...]
        
    #) Suggested operations:
        
        InverseSeries - does series reversion to find the series for the inverse function of a series:
        (From wolfram mathematica)
        
        
        some function can work with series:
        
        >>> exp(x + O(x**3))
        exp(x + O(x**3))
        
        I expected the proceeding "exp" as series : "1 + (x + O(x**3)) + (x + O(x**3))**2/2 + (x + O(x**3))**3/6 + ..."
        so it resulting to "1 + x + x**2/2 + O(x**3)"
        
        Though it lucky produced by this way "manually":
        
        >>> exp(x + O(x**3)).expand()
        exp(x)*exp(O(x**3))
        >>> ( exp(x).series() * exp(O(x**3)).series()  ).expand()
        1 + x + x**2/2 + O(x**3)
        
        But will be better to implement it in automatic mode.


_`Realization for abstract analytic function`
----------------------------------------------

    Series of derivations
    
    >>> D = Derivative
    >>> assert D(x**2 + x**3*y**2, x, 2, y, 1).series(x).doit() == 12*x*y
    >>> assert D(cos(x), x).lseries().next() == D(1, x)
    >>> assert D(exp(x), x).series(n=3) == D(1, x) + D(x, x) + O(x**2)
    >>> assert Integral(x, (x, 1, 3),(y, 1, x)).series(x) == -4 + 4*x
    
    Ok
    
    Chris successfully have done those realizations, I took them from the latest smichr/2084 branch.
    
    For abstract analytic function I mean that we do "series" on it.
    Take some Function "f" and imply series method for it:
    
    >>> # series(f(x), x)
    >>> # rises RuntimeError: maximum recursion depth exceeded while calling a Python object
    
    Expected something like: f(0) + D(f(0), x).subs(x, 0)*x + ...
    
    BTW, I donn't know how does the substitution for derivatives work.
    
    >>> D(f(x), x).subs(x, 0)
    f(0)
    
    I expected something like "f_x(0)"
    
    Now play with derivation of series of exp(x):
    
    >>> D(exp(x), x).series()
    D(1, x) + D(x, x) + D(x**2/2, x) + D(x**3/6, x) + D(x**4/24, x) + O(x**5)
    >>> D(exp(x).series(), x).doit()
    1 + x + D(O(x**6), x) + x**2/2 + x**3/6 + x**4/24
    
    It work, but "D.doit()" do not work with Big-O.
    
_`Multiple cases results must to be more better`
------------------------------------------------

    (Piecewise functions ?)

    In some cases abstract series can produce a set of the results.
    For example transpose "abs(x)" to the right by "c" and look what is in the zero point.
    
    >>> c = var("c")
    >>> abs(x-c).series(x)
    -(x - c)*sign(c)
    
    Expected something like: "[-(x - c)*sign(c); when x!=0], [-x; when c==0]"
    
    It is difficult, in some cases solution of equations is needed.
    
    
_`Series with assumption x limit to oo`
----------------------------------------

    (raw issue)
    
    >>> # (sin(1/x)).series(x, oo, n=5)
    >>> # or
    >>> # (sin(1/x)).series(x, oo, n=-5)
    # rise Exception
    
    Expected: 1/x + (1/x)**3)/6 + O((1/x)**5)

_`Series with matrices`
------------------------

    >>> m = Matrix(2, 2, [0,1,1,0])
    >>> # exp(m)
    >>> # SympifyError: SympifyError: 'Matrix cannot be sympified'
    >>> # exp(m*x)
    >>> # SympifyError: SympifyError: 'Matrix cannot be sympified'
    
    Unfortunately exponent of matrices is not present in sympy.

    It would be good to realize this. May be with the aim of series.


_`Exception "NotImplemented" rises`
------------------------------------
    >>> # (1/(1-x**m)).series(x)
    
    >>> # ((sin(x)/cos(x))**(sin(2*x)/cos(2*x))).series()
    >>> # NotImplementedError: Don't know how to calculate the mrv of 'O(log(_p)/_p**6)'

_`Other`
------------------------

    >>> # (sin(1/x)).series()
    >>> # PoleError: Cannot expand 1/x around 0
    
    Exception
    
    >>> # (sin(x)* sin(1/x)).series()
    >>> # PoleError: Cannot expand 1/x around 0
    
    Exception
    



