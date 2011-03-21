# Polynomials Module

## Introduction

This tutorial tries to give an overview of the functionality concerning polynomials within SymPy. All code examples assume:

    >>> from sympy import *
    >>> x, y, z = symbols('xyz')

## Basic functionality

These functions provide different algorithms dealing with polynomials in the form of SymPy expression, like symbols, sums etc.

## Division 

The function `div()` provides division of polynomials with remainder. That is, for polynomials `f` and `g`, it computes `q` and `r`, such that `f == g*q + r` and `degree(r) < q`. For polynomials in one variables with coefficients in a field, say, the rational numbers, q and r are uniquely defined this way.


    >>> f = 5*x**2 + 10*x + 3
    >>> g = 2*x + 2
    >>> q, r = div(f, g)
    >>> q
    5 + (5/2)*x
    >>> r
    3
    >>> (q*g + r).expand()
    13 + 5*x**2 + 15*x


As you can see, q has a non-integer coefficient. If you want to do division only in the ring of polynomials with integer coefficients you can specify an additional parameter.

    >>> q, r = div(f, g, coeff='int')
    >>> q
    0
    >>> r
    13 + 5*x**2 + 15*x

But be warned, that this ring is no longer euclidean and that the degree of the remainder doesn't need to be smaller than that of f. Since 2 doesn't divide 5, 2*x doesn't divide 5*x**2, even if the degree is smaller. But:

    >>> g = 5*x + 1
    >>> q, r = div(f, g, coeff='int')
    >>> q
    x
    >>> r
    13 + 14*x
    >>> (q*g + r).expand()
    13 + 5*x**2 + 15*x

This also works for polynomials with multiple variables.

    >>> f = x*y + y*z
    >>> g = 3*x + 3*z
    >>> q, r = div(f, g)
    >>> q
    (1/3)*y
    >>> r
    0

In the last examples, all of the three variables x, y and z are assumed to be variables of the polynomials. But if you have some unrelated constant as coefficient, you can specify the variables explicitly:

    >>> a, b, c = symbols('abc')
    >>> f = a*x**2 + b*x + c
    >>> g = 3*x + 2
    >>> q, r = div(f, g, var=[x])
    >>> q
    -2/9*a + (1/3)*b + (1/3)*a*x
    >>> r
    c - 2/3*b + (4/9)*a

Another option is division by multiple polynomials at the same time. In general, the output is not unique and depends on the order of the divisors and the given monomial order (if specified).

    >>> f = x*y + y*z + z*x
    >>> g1 = x + 1
    >>> g2 = 2*y + 1
    >>> q, r = div(f, [g1, g2])
    >>> q
    [y + z, (-1/2) + (1/2)*z]
    >>> r
    1/2 - 3/2*z
    >>> (q[0]*g1 + q[1]*g2 + r).expand()
    x*y + x*z + y*z

    >>> q, r = div(f, [g2, g1])
    >>> q
    [(1/2)*x + (1/2)*z, (-1/2) + z]
    >>> r
    1/2 - 3/2*z
    >>> (q[0]*g2 + q[1]*g1 + r).expand()
    x*y + x*z + y*z

## GCD and LCM

With division, there is also the computation of the greatest common divisor and the least common multiple.

When the polynomials have integer coefficients, the contents' `gcd` is also considered.

    >>> f = 12*(x + 1)*x
    >>> g = 16*x**2
    >>> gcd(f, g)
    4*x

It also works with multiple variables. In this case, the variables are ordered alphabetically, be default, which has influence on the leading coefficient.

    >>> f = x*y/2 + y**2
    >>> g = 3*x + 6*y
    >>> gcd(f, g)
    x + 2*y
    >>> gcd(f, g, var=[y, x])
    y + (1/2)*x

The `lcm` is connected with the `gcd` and one can be computed using the other.

    >>> f = x*y**2 + x**2*y
    >>> g = x**2*y**2
    >>> gcd(f, g)
    x*y
    >>> lcm(f, g)
    x**2*y**3 + x**3*y**2
    >>> (f*g).expand()
    x**3*y**4 + x**4*y**3
    >>> (gcd(f, g)*lcm(f, g)).expand()
    x**3*y**4 + x**4*y**3

## Square-free factorization

You can compute the square-free part of a univariate polynomial, which is the product of all the different irreducible divisors.

    >>> sqf_part(x**3*(x+1)**2)
    x + x**2

The square-free factorization of a univariate polynomial is the product of all factors (not irreducible) of degree 1, 2, ...

    >>> sqf((x + 2)*(x*(x + 1))**2)
    (x + x**2)**2*(2 + x)

# Factorization

This function provides factorization of univariate and multivariate polynomials with rational coefficients.

    >>> factor(Rational(1,2)*x**4 + Rational(5,12)*x**3 - Rational(1,3)*x**2)
    -1/12*x**2*(1 - 2*x)*(4 + 3*x)

    >>> factor(x**2 + 4*x*y + 4*y**2)
    (x + 2*y)**2

## Groebner bases

Buchberger's algorithm is implemented, supporting various monomial orders.

    >>> groebner([x**2 + 1, y**4*x + x**3], order='lex')
    [(-1) + y**4, 1 + x**2]

    >>> groebner([x**2 + 1, y**4*x + x**3, x*y*z**3], order='grevlex')
    [(-1) + y**4, z**3, 1 + x**2]

# Solving Equations

We have (incomplete) methods to find the complex or even symbolic roots of polynomials and to solve some systems of polynomial equations.

    >>> roots(x**3 + 2*x + 3)
    [-1, 1/2 + (1/2)*I*11**(1/2), 1/2 - 1/2*I*11**(1/2)]

    >>> roots(x**2 + p*x + q, var=[x])
    [(1/2)*(p**2 - 4*q)**(1/2) - 1/2*p, -1/2*p - 1/2*(p**2 - 4*q)**(1/2)]

    >>> solve_system([y - x, x - 5])
    [(5, 5)]

    >>> solve_system([y**2 - x**3 + 1, y*x])
    [(0, I), (0, -I), (1, 0), ((-1/2) + (1/2)*I*3**(1/2), 0), ((-1/2) - 1/2*I*3**(1/2), 0)]

## The Polynomial class

Coming soon...

