<!-- wikitest skip -->
# UD Under Development
This page written to estimate the current situation and some fundamental problems.

## Assumptions

The problems with Assumptions have a few types:
 
1. Entangled current assumption system.
 It is not well described what `is_something` means exactly. Especially in the case
 when `is_something` have not boolean value but a None.
 Also it turned out that `S.One.is_complex` means that integer field *can be* extends to complex plane.
 
2. Existence of another variant of assumption system.
 This "ask" system is not well tested.
 Additionally the situation is raised: the more we use the old system (for development of new code), the less new system tested.
 And the less new system tested, the less it is used in coding.
 
3. It turned out that that some assumptions are inflexibly and globally stitched into in Sympy, and it is impossible to regulate it.

Links:

- New assumption system creation [issue 1047](http://code.google.com/p/sympy/issues/detail?id=1047)
- New assumption system `sympy/sympy/assumptions/ask.py`, `sympy/assumptions/assume.py`
- Stitched global assumption [issue 2260](http://code.google.com/p/sympy/issues/detail?id=2260#c16)

See also: [[Assumptions]]


## Series

For series this section are dedicated:
    [[UD-series]]
    
The main problem that they have many entangled problems, and it is became impossible to operate
with them as ordinary SymPy expressions.
For effective and clear operation with them we must use special types of series and apply appropriated algorithms.

Now the series mostly used for limits calculation, and they slave for this aim (so they are turned out to be transseries)

They might use some missed in SymPy topics too:

 - sequences (to describe internal structure)

Algorithms:

- (*zelous* and  *lazy* algorithms, [*relax* algorithm](http://www.texmacs.org/joris/relax/relax-abs.html))
for multiplication, division, resolution of differential equations, composition and reversion.


## limits

...

## The operation with intervals

Introduction: http://en.wikipedia.org/wiki/Interval_arithmetic

Only some things are present now in SymPy:

-`Interval`, `Union` (set of Intervals), with operation of intersection and union.
And only real intervals are supported. (sympy/core/sets.py)

- `Peace-wises`
- `Fields` (with no operations)

Desired behaviour is to have arithmetic operations upon Intervals:

Real axes:

    >>> Interval(-1, 1)
    [-1, 1]
    >>> Interval(-1, 1])**2
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

Can be use Sequences to describe infinite number of points in (or out of) intervals.


## Singularities

(Yuri GSoC-2011 concern this topic too)

    >>> singularities(1/x)
    [0]  # Infinite singularity

Needed for:

- to analyse the continuous of functions 
    
Might use other topics:

- Solve (for finding the roots in denominator)
- Resolve question is_equal_zero (mixing python == and relative operation with expressions, `zero-test` problem)

Related with:
- sympy/polys/algebratools.py: Field

References:

- http://www.texmacs.org/www.texmacs.org/joris/unif/unif.html
-  [vdH97] J. van der Hoeven. Automatic asymptotics. PhD thesis, École polytechnique, Palaiseau, France, 1997. 
- [vdH06] J. van der Hoeven. Transseries and real differential algebra, volume 1888 of Lecture Notes in Mathematics. Springer-Verlag, 2006. 

Also for curves and surfaces (the separated problematic)

- http://en.wikipedia.org/wiki/Resolution_of_singularities

## Analytic function

References:

- www.texmacs.org/joris/effan/effan.html

## Sequences 

[[UD-series-user-interface]]

Required for:

- series constructor
- may be for interval (domains) description
- may be for infinite structures.

Related with:

- sympy/solvers/recurr.py: rsolve() (recurrences solving for sequences)
- Set class.


## Abstract Function

- Current issue for realization of "Undefined functions" [issue 2205](http://code.google.com/p/sympy/issues/detail?id=2205)
- representation of Derivative of function at some (no zero) point [issue 1620](http://code.google.com/p/sympy/issues/detail?id=1620).
- representation of composition of functions while differentiation [issue 1660](http://code.google.com/p/sympy/issues/detail?id=1660).
