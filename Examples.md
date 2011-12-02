


*Note*: This document was superseded by [http://code.google.com/p/sympy/wiki/Tutorial Tutorial], that contains everything here plus much more.

# Introduction

This document contains examples of most of the features of sympy.

You can find all the following examples in the `examples` directory as regular python scripts. More examples can be found in the tests directory in form of the testing suite.

*Note*: the code in `examples` directory is uptodate. We want to generate this page automatically, but until then, if the code on this page doesn't work, try the corresponding example in the svn repository.

## Basic manipulation

```
>>> import sympy
>>> a=sympy.Symbol('a')
>>> b=sympy.Symbol('b')
>>> c=sympy.Symbol('c')
>>> e=( a*b*b+2*b*a*b )**c
>>> print e
b^(2*c)*a^c*3^c
```

## Expansion

```
>>> import sympy
>>> a=sympy.Symbol('a')
>>> b=sympy.Symbol('b')
>>> e=(a+b)**5
>>> print e
(b+a)^5
>>> print e.expand()
10*a^3*b^2+5*b^4*a+a^5+b^5+5*a^4*b+10*a^2*b^3
```

## Functions

```
>>> import sympy
>>> a=sympy.Symbol('a')
>>> b=sympy.Symbol('b')
>>> e=sympy.log((a+b)**5)
>>> print e
5*log(b+a)
>>> e=sympy.exp(e)
>>> print e
exp(5*log(b+a))
>>> e=sym.log(sympy.exp((a+b)**5))
>>> print e
(b+a)^5
```

## Differentiation

```
>>> import sympy
>>> a=sympy.Symbol('a')
>>> b=sympy.Symbol('b')
>>> e=(a+2*b)**5
>>> print e
(2*b+a)^5
>>> print e.diff(a)
5*(2*b+a)^4
>>> print e.diff(b)
10*(2*b+a)^4
>>> print e.diff(b).diffn(a,3)
240*(2*b+a)
>>> print e.expand().diff(b).diffn(a,3)
240*a+480*b
```

## Series expansion

```
>>> import sympy
>>> x=sympy.Symbol('x')
>>> e=1/sympy.cos(x)
>>> print e.series(x,10)
1+50521/3628800*x^10+61/720*x^6+1/2*x^2+5/24*x^4+277/8064*x^8
>>> e=1/sympy.sin(x)
>>> print e.series(x,4)
x^(-1)+1/36*x^3+1/216*x^5+1/6*x
```

## Substitution

```
>>> import sympy
>>> x=sympy.Symbol('x')
>>> y=sympy.Symbol('y')
>>> e=1/sympy.cos(x)
>>> print e
cos(x)^(-1)
>>> print e.subs(sympy.cos(x),y)
y^(-1)
>>> print e.subs(sympy.cos(x),y).subs(y,x**2)
x^(-2)
>>> e=1/sympy.log(x)
>>> e=e.subs(x,sympy.Real(2.71828))
>>> print e
log(2.71828)^(-1)
>>> print e.evalf()
1.00000067265
```

## Arbitrary precision integers and rationals

```
>>> import sympy
>>> e=sympy.Rational(2)**50/sympy.Rational(10)**50
>>> print e
1/88817841970012523233890533447265625
```

## Limits

```
>>> from sympy import exp,log,Symbol,Rational,sin,limit,limitinf
>>>
>>> x=Symbol("x")
>>> a=Symbol("a")
>>> h=Symbol("h")
>>>
>>> def sqrt(x):
...     return x**Rational(1,2)
...
>>> def sqrt3(x):
...     return x**Rational(1,3)
...
>>> def limitminf(f,x):
...     return limitinf(f.subs(x,-x),x)
...
>>> def show(computed, correct):
...     print "computed:",computed,"correct:",correct
...
>>> show( limitinf(sqrt(x**2-5*x+6)-x,x) , -Rational(5)/2 )
computed: (-5/2) correct: (-5/2)
>>> show( limitinf(x*(sqrt(x**2+1)-x),x) , Rational(1)/2 )
computed: 1/2 correct: 1/2
>>> show( limitinf(x-sqrt3(x**3-1),x) , Rational(0) )
computed: 0 correct: 0
>>> show( limitminf(log(1+exp(x))/x,x) , Rational(0) )
computed: 0 correct: 0
>>> show( limitinf(log(1+exp(x))/x,x) , Rational(1) )
computed: 1 correct: 1
>>> show( limit(sin(3*x)/x,x,0) , Rational(3) )
computed: 3 correct: 3
>>> show( limit(sin(5*x)/sin(2*x),x,0) , Rational(5)/2 )
computed: 5/2 correct: 5/2
>>> show( limitinf(((x-1)/(x+1))**x,x) , exp(-2))
computed: exp((-2)) correct: exp((-2))
```