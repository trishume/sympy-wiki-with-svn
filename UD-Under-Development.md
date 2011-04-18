# UD Under Development
This page written to estimate the current situation and some fundamental problems.

1.  Series
2.  limits
2.1.  Problematic
3.  The operation with intervals
4.  Singularities
5.  Sequences
6.  Assumptions
6.  Abstract Function


## Assumptions
[[Assumptions]]

- [issue 1047](http://code.google.com/p/sympy/issues/detail?id=1047)
- sympy/sympy/assumptions/ask.py
- sympy/assumptions/assume.py

## Series

- [[UD-series]]

- (*zelous* and  *lazy* algorithms, [*relax* algorithm](http://www.texmacs.org/joris/relax/relax-abs.html))
for multiplication, division, resolution of differential equations, composition and reversion.

## limits

## The operation with intervals
Real axes:

    >>> Interval([-1, 1])
    [-1, 1]
    >>> Interval([-1, 1])**2
    [0, 1]
    
    >>> Interval(RR - S.Zero)
    [-oo, 0)U(0, oo]

Complex plane:

    >>> Domain(ZZ - S.Zero)
    Domain(ZZ - S.Zero)

Required for:

- singularity description (`sin(x)--> oo`)
- to analyse the continuous of functions (recursive method for suspicious points which can be)
- also with procedure to find singularities

Related with:

 - sympy/function s/elementary/piecewise.py
( http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.70.4127&rep=rep1&type=pdf)

- http://en.wikipedia.org/wiki/Interval_arithmetic
- http://www.dmitry-kazakov.de/ada/intervals.htm


## Singularities
    

    >>> singularities(1/x)
    [0]  # Infinite singularity

- (Yuri GSoC-2011 involved)
    
- to analyse the continuous of functions 
    
Using:
- Solve (for finding the roots in denominator)
Needs:
- Resolve question is_equal_zero (mixing python == and relative operation with expressions, `zero-problem`)

Related with:

- sympy/polys/algebratools.py: Field

References:

- http://www.texmacs.org/www.texmacs.org/joris/unif/unif.html
-  [vdH97] J. van der Hoeven. Automatic asymptotics. PhD thesis, École polytechnique, Palaiseau, France, 1997. 
- [vdH06] J. van der Hoeven. Transseries and real differential algebra, volume 1888 of Lecture Notes in Mathematics. Springer-Verlag, 2006. 

Also for curves and surfaces

- http://en.wikipedia.org/wiki/Resolution_of_singularities

## Analytic function

References:

- www.texmacs.org/joris/effan/effan.html

## Sequences 

[[UD-series-user-interface]]

Required for:

- series constructor (and internal)
- may be for powerful interval (domains) description

Related with:

- sympy/solvers/recurr.py: rsolve()

## Abstract Function

- Current issue for realization of "Undefined functions" [issue 2205](http://code.google.com/p/sympy/issues/detail?id=2205)
- representation of Derivative of function at some (no zero) point [issue 1620](http://code.google.com/p/sympy/issues/detail?id=1620).
- representation of composition of functions while differentiation [issue 1660](http://code.google.com/p/sympy/issues/detail?id=1660).
