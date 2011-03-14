At this page we will be concentrated to the end-user's aims of series usage.

# Introduction

Now we determine in [Function expansions and series](https://github.com/sympy/sympy/wiki/Function-expansions-and-series "Function expansions and series")
  that there exists many kind of series in mathematics. And that we must distinguish them from asymptotic expansions. (This situation was raised due to the historical development way of various CAS'es and remains f.e. in Sage and Wolfram Mathematica)

To be more extendable CAS in future the problems and use-cases will be considered for ideal CAS. Even when some of the problems will be not easy for realization or deserving for separated mathematical research. (The example of those problems is to find symbolic function knowing only coefficients of series.)

There is no doubts now that for efficient processing some object and classes will be needed and considered. End-user must know about them in minimal mode, only necessary for concrete task. But if task is complex then knowledge of them for user will be necessary extended too.

But we will not be concentrated to concrete algorithms or precise realizations, however we will take into consideration their basic shapes.

After discussion about this material we will be able to turn to the concrete plan of implementations: which issues can be isolated or how related, priority of them, how they are related with current situation, and so on.

Remark:

All of the name-tokens below are rough, also all code examples below are imaginary as desired or as variants offered.
They must be discussed further.


# Basical usage


## Main task

Main task for user is to obtain series.

Example:

    >>> sin(x).series(x)
    x + x**3/6 + x**5/120 + ...

Sometime more convenient to obtain asymptotic expansion for some expression or function:

    >>> sin(x).expansion(x)
    x + x**3/6 + x**5/120 + O(x**6)
    
Both .series(x) and .expansion(x) methods tells to user about terms and both methods cope with the main task.

## Operations

Then he can try to manipulate with them thinking that they are some expressions.
But it is unreasonably to operate for series only with a few first terms "x + x\*\*3/6 + x\*\*5/120" as ordinary polynomial (except on case of user want to do indeed and understand it) - series is infinite, so final result may be incorrect.

More sense to operate with expansion with Big-O notation:

    >>> sin(x).expansion(x)
    x + x**3/6 + x**5/120 + O(x**6)
    >>> sin(x).expansion(x) + cos(x).expansion(x)
    1 + x - x**2/2 - x**3/6 + x**4/24 + x**5/120 + O(x**6)
    >>> cos(x).expansion(x)**2 
    1 - x**2 + x**4/3 + O(x**6)
    
Big-O signals to user what precision is and to do not forget terms of orders. Also it help for operations: eats high order terms which is not needed for user:

    >>> cos(x).expansion(x)**2 + 1 + x + x**6 + 777*x**7 + x**8
    2 + x - x**2 + x**4/3 + O(x**6)

This is the main historical motive why .series() method yield in many CAS'es expansion indeed: it is more convenient for user, prevalent task, and it was enough to implement O() behaviour to begin manipulate with them as ordinary expressions.


But we will be distinguish these objects, especially if there exists operations with series too if we consider them as the formal series:

    >>> sin(x).series(x) + cos(x).series(x)
    1 + x - x**2/2 - x**3/6 + x**4/24 + x**5/120 + ...
    
    >>> cos(x).series(x)**2 + 1 + x + x**6 + 777*x**7 + x**8
    2 + x - x**2 + x**4/3 + ...

## Difference of series and expansion.

It seems that there is no difference between the last result and the above analog result for .expansion(x) except the trailers "..." and "O()".

But the difference is that the last result continue remembering about "x\*\*6 + 777*x\*\*7 + x\*\*8" terms.

    >>> _.show(n=8)
    2 + x - x**2 + x**4/3 + 43*x**6/45 + 777*x**7 + ...
 
One can wonder that it seems that sympy expression must secretly keep in mind the infinite number of terms. Is it really possible? Yes, it is possible in many cases.

## Internal and screen representations

User in above examples can do not suspect of internal representation of series. But really .series() method yield the expression of special type.

    >>> s = sin(x).series(x)
    >>> type(s)
    <class 'sympy.series.PowerSeries'>
    
    >>> a = sin(x).expansion(x)
    >>> type(a)
    sin(x).series(x)
    <class 'sympy.series.PowerSeriesExpansion'>

Examples of operations for summation, multiplications which was described in previous section also are maintained by this classes.

These classes track some info about:

    >>> s.expression
    sin(x)
    >>> s.variable
    x
    >>> s.coefficients(n=3)
    [0, 1, 0, 1/6]
    
    >>> a.precision
    6
    
Have some methods for transformations.

Transformation of series to asymptotic expansion:

    >>> s.to_expansion(n=6)
    x - x**3/6 + x**5/120 + O(x**6)

Transformation of series to polynomial:
    >>> s.to_polynomial(n=6)
    Poly(x - x**3/6 + x**5/120, x, domain='ZZ')
   
Transformation of asymptotic expansion to polynomial:   
    >>> a.truncate() | a.removeO() | a.to_polynomial()
    Poly(x - x**3/6 + x**5/120, x, domain='ZZ')

Transformation of asymptotic expansion object to ordinary sympy expression (but with Big-O):

    >>> a.to_normal()
    x - x**3/6 + x**5/120 + O(x**6)
    >>> type(_)
    <class 'sympy.core.add.Add'>

   
Representation variants:

    >>> s.as_sum()
    Sum(x**(n)/n! - x**(n+2)/(n+2)!, (n=1, 5, 9 ...))

Some analytic:

    >>> s.is_periodical()
    False
    >>> s.is_finite()
    False
    >>> s.to_teylor().coefficients(n=8)
    [0, 1, 0, -1, 0, 1, 0, -1]
    >>> s.to_teylor().is_periodical()
    True
    >>> s.to_teylor().period()
    4
   
## Various kinds of series

Image:

![class-view-1.png](https://github.com/goodok/series-texts/raw/master/class-view-1.png)

# (Draft) Full variants.

1. Along with others specific methods to obtain specific series (Taylor, Laurent) a method to obtain series as a single procedure needs too - user may do not know what kind of series he have to obtain. This method plays a role of distribution job and is related with analyze job (isAnalytical, hasLaurentSeries and so on). Also this method can be used for limits processing implementation. 

2. Constructors

Sequences

- by formula (finite or infinite sequence)
- periodical (by list) (finite or infinite sequence)
- as list (only finite sequence)

Series

- throw sequences (or like sequences constructor)
- from source function

# Algorithms

1. Determine what is the kind of series of expression will be

2. Checker methods:

- .isAnalytic()
- hasLaurentSeries() and so on...

3. Determine if LaurentSeries has principal part or not. If not then it is a Taylor. This can be used internally and must be fast.

4. Isolated tasks: are the operations over the fields NAME_Series (NAME_Polynomials, NAME_Expansion).
   

# Relation with current situation

It is necessary first
- representation of Derivative of function at some (no zero) point (issue 1620).
- representation of composition of functions while differentiation (issue 1660).

- The class TaylorExpansion can be used even now (replaced little by little in core), with present algorithm of recursive expansion of complexes functions - for effective multiplication it will be easy fix (issue 1038).