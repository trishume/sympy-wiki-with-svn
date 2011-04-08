# UD - Function expansions and series - current situation and applications

# Usage and applications

## Series
- In some cases it is easier to work with series, while processing with original function is difficult or impossible symbolically.
- One can use formal power series to prove several relations familiar from analysis in a purely algebraic setting.
- Some ODE can be solved by consideration of the desired result as formal series. Some recurrence formula for series coefficients can be obtained.
- limits
        
## Asymptotic expansion

- Asymptotic expansions through series is used for approximation of functions. In some cases it is easier to work with truncated series, while processing with original function is difficult or impossible.
- Some ODE, Integral equations can be solved by consideration of the desired result as asymptotic expansions.
        
## Generating function

- Find a closed formula for a sequence given in a recurrence relation.
- Find recurrence relations for sequences — the form of a generating function may suggest a recurrence formula.
- Define function through sequence.
- Discrete representation of function.

## Common tasks
- Calculate items of sequences by recurrent formula

# Current situation

- According to its docstring, ``f(x).series(x, x0, n)`` is supposed to return the (n-1)th order generalized Taylor expansion of \(f(x)\) for \(x \rightarrow x_0\).
Actually, it works only for \(x_0 = 0\) and when f doesn't have a generalized Taylor expansion, it returns some arbitrarily chosen asymptotic expansion of \(f(x)\).

- But the present method "series" which returns various kinds of series is convenient and used for the task of limits processing: limits use necessary amount of first terms of series whatever it be.
The work with processing of many various cases of series and limits was executed recently, also many tests have been collected and passed for series and limits.

- Class *Function* , *exp* *sin* and others contain method **taylor_term**.

- general algorithm for series() and nseries() consist in that the operations with asymptotic expansion  used through recursion:  F.e: ((sin(x))^1000 ).series() = \( (1 + \frac{x^3}{6} + O(x^4))^1000 = \cdots \).

- There is an object **Sum** defined in sympy, which represent unevaluated summation \( \sum_{k=a}^b a(n) \).

- sympy/solvers/recurr.py contains some methods for solving recurrences, main function on this module is **rsolve()**.

- The implementation of some series methods for solving IDEs is processing now in Saptarshi's branch (https://github.com/saptman/sympy/tree/dev_ide
).


## problems and remarks which we encounter

- Problems with big O representation and behaviour at non zero point or oo.
- representation of Derivative of function at some (no zero) point ([issue 1620](http://code.google.com/p/sympy/issues/detail?id=1620 "issue 1620")).
- representation of composition of functions while differentiation ([issue 1660](http://code.google.com/p/sympy/issues/detail?id=1660 "issue 1660")).
- Not effective algorithm in some cases: now is used that: (cos(x)*(sin(x)).series() = sin(x).series() * cos(x).series(), lseries.next() calculate the nseries(n)  every time  (f.e. fifth next() calculate nseries(5) and after this yield fifth term)
- How to deal with `acosh`, `acoth` - branches ([issue 564](http://code.google.com/p/sympy/issues/detail?id=564 "issue 564"))
- Singularities ([issue 2200](http://code.google.com/p/sympy/issues/detail?id=2200 "issue 2200"))



# Open questions and future topics
- what is exp(1/x).series(x, oo) - classical Laurent or power series at point oo?
- multivariable extension.
- complex numbers, non commutative formal variables.
- split-complex numbers, may be sometimes more convinient to expand in this plane e.g. hyperbolic inverse functions.
- convergence
- singularity and branches


# Links

- [rmpoly](http://code.google.com/p/rmpoly/wiki/Tutorial) - nice Python project, by Mario Pernici. Handling polynomials and series.

# Part-2
At this page we will be concentrated to the end-user's aims of series usage in sympy:

[Function expansions and series-2](https://github.com/sympy/sympy/wiki/Function-expansions-and-series-2 "Function expansions and series-2")
