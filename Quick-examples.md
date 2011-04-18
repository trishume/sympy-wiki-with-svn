This page gives quick examples of common symbolic calculations in SymPy. Print it and keep it under your pillow!
<!-- wikitest release -->

## Elementary operations
```py
 >>> from sympy import *
 >>> x, y, z, t = symbols('x y z t')
 >>> k, m, n = symbols('k m n', integer=True)
 >>> f, g, h = map(Function, 'fgh')
```

### Construct a symbolic expression
Construct the formula \( \frac{3 \pi}{2} + \frac{e^{ix}}{x^2 + y}\) :
```py
 >>> Rational(3,2)*pi + exp(I*x) / (x**2 + y)
 3*pi/2 + exp(I*x)/(y + x**2)
```

### Evaluate a symbolic expression

Calculate the value of \( e^{ix}\)  for \( x=\pi\) :
```py
 >>> x = Symbol('x')
 >>> exp(I*x).subs(x,pi).evalf()    #doctest: +SKIP
 -1.00000000000000
```

### Deconstruct an expression
```py
 >>> expr = x + 2*y
 >>> expr.__class__
 <class 'sympy.core.add.Add'>
 >>> expr.args
 (2*y, x)
```

### Calculate a numerical value
Calculate 50 digits of \( e^{\pi \sqrt{163}}\) :
```py
 >>> exp(pi * sqrt(163)).evalf(50)
 262537412640768743.99999999999925007259719818568888
```

## Algebra
### Expand products and powers
Expand \( (x+y)^2 (x+1)\) :
```py
 >>> ((x+y)**2 * (x+1)).expand()
 2*x*y + x**2 + y**2 + x*y**2 + 2*y*x**2 + x**3
```

### Simplify a formula
Simplify \( \frac{1}{x} + \frac{x \sin x - 1}{x}\) :
```py
 >>> a = 1/x + (x*sin(x) - 1)/x
 >>> simplify(a)
 sin(x)
```

### Solve a polynomial equation
Find the roots of \( x^3 + 2x^2 + 4x + 8\) :
```py
 >>> solve(Eq(x**3 + 2*x**2 + 4*x + 8, 0), x)
 [-2*I, 2*I, -2]
```
or more easily:
```py
>>> solve(x**3 + 2*x**2 + 4*x + 8, x)
 [-2*I, 2*I, -2]
```

For details, see: [[Finding roots of polynomials]].

### Solve an equation system
Solve the equation system \( \left(x+5y=2, -3x+6y=15\right)\) :
```py
 >>> solve([Eq(x + 5*y, 2), Eq(-3*x + 6*y, 15)], [x, y])
 {x: -3, y: 1}
```
or
```py
 >>> solve([x + 5*y - 2, -3*x + 6*y - 15], [x, y])
 {x: -3, y: 1}
```

### Calculate a sum
Evaluate \( \sum_{n=a}^b 6 n^2 + 2^n\) :
```py
 >>> a, b = symbols('a b')
 >>> sum(6*n**2 + 2**n, (n, a, b))
 b - a + 3*a**2 + 3*b**2 - 2*a**3 + 2*b**3 - 2**a + 2**(1 + b)
```

### Calculate a product
Evaluate \( \prod_{n=1}^b n (n+1)\) :
```py
 >>> product(n*(n+1), (n, 1, b))
 RisingFactorial(2, b)*gamma(1 + b)
```

## Calculus
### Calculate a limit
Evaluate \( \lim_{x\to 0} \frac{\sin x - x}{x^3}\) :
```py
 >>> limit((sin(x)-x)/x**3, x, 0)
 -1/6
```

### Calculate a Taylor series
Find the Maclaurin series of \( \frac{1}{\cos x}\)  up to the \( O(x^6)\)  term:
```py
 >>> (1/cos(x)).series(x, 0, 6)
 1 + x**2/2 + 5*x**4/24 + O(x**6)
```

### Calculate a derivative
Differentiate \( \frac{\cos(x^2)^2}{1+x}\) :
```py
 >>> diff(cos(x**2)**2 / (1+x), x)
 -4*x*cos(x**2)*sin(x**2)/(1 + x) - cos(x**2)**2/(1 + x)**2
```

### Calculate an integral
Calculate the indefinite integral \( \int x^2 \cos x \, dx\)
```py
 >>> integrate(x**2 * cos(x), x)
 -2*sin(x) + x**2*sin(x) + 2*x*cos(x)
```

Calculate the definite integral \( \int_0^{\pi/2} x^2 \cos x \, dx\) :
```py
 >>> integrate(x**2 * cos(x), (x, 0, pi/2))
 -2 + pi**2/4
```

### Solve an ordinary differential equation
Solve \( f''(x) + 9 f(x) = 1\,\!\) :

```py
 >>> f = Function('f')
 >>> dsolve(Eq(Derivative(f(x),x,x) + 9*f(x), 1), f(x))
 f(x) == 1/9 + C1*sin(3*x) + C2*cos(3*x)
```

You can also use `.diff()`, like here (an example in `isympy`)

```py
 >>> f = Function("f")
 >>> Eq(f(x).diff(x, x) + 9*f(x), 1)
 9*f(x) + D(f(x), x, x) == 1
 >>> dsolve(_, f(x))
 f(x) == 1/9 + C1*sin(3*x) + C2*cos(3*x)
```