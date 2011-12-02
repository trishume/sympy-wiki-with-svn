

# Concrete mathematics

## Hypergeometric terms

The center stage, in recurrence solving and summations, play hypergeometric terms. Formally these are sequences annihilated by first order linear recurrence operators. In simple words if we are given term `a(n)` then it is hypergeometric if its consecutive term ratio is a rational function in `n`.

To check if a sequence is of this type you can use `is_hypergeometric` method which is  available in Basic class. Here is simple example involving a polynomial:

```
>>> (n**2 + 1).is_hypergeometric(n)
True
```

Of course polynomials are hypergeometric but are there any more complicated sequences of this type? Here are some trivial examples:

```
>>> factorial(n).is_hypergeometric(n)
True
>>> binomial(n, k).is_hypergeometric(n)
True
>>> rf(n, k).is_hypergeometric(n)
True
>>> ff(n, k).is_hypergeometric(n)
True
>>> gamma(n).is_hypergeometric(n)
True
>>> (2**n).is_hypergeometric(n)
True
```

We see that all species used in summations and other parts of concrete mathematics are hypergeometric. Note also that binomial coefficients and both rising and falling factorials are hypergeometric in both their arguments:

```
>>> binomial(n, k).is_hypergeometric(k)
True
>>> rf(n, k).is_hypergeometric(k)
True
>>> ff(n, k).is_hypergeometric(k)
True
```

To say more, all previously shown examples are valid for integer linear arguments:

```
>>> factorial(2*n).is_hypergeometric(n)
True
>>> binomial(3*n+1, k).is_hypergeometric(n)
True
>>> rf(n+1, k-1).is_hypergeometric(n)
True
>>> ff(n-1, k+1).is_hypergeometric(n)
True
>>> gamma(5*n).is_hypergeometric(n)
True
>>> (2**(n-7)).is_hypergeometric(n)
True
```

However nonlinear arguments make those sequences fail to be hypergeometric:

```
>>> factorial(n**2).is_hypergeometric(n)
False
>>> (2**(n**3 + 1)).is_hypergeometric(n)
False
```

If not only the knowledge of being hypergeometric or not is needed, you can use `hypersimp()` function. It will try to simplify combinatorial expression and if the term given is hypergeometric it will return a quotient of polynomials of minimal degree. Otherwise is will return `None` to say that sequence is not hypergeometric:

```
>>> hypersimp(factorial(2*n), n)
(1 + 2*n)*(2 + 2*n)
>>> hypersimp(factorial(n**2), n)
```

## Difference equations

# Term rewriting

Term rewriting is a very general class of functionalities which are used to convert expressions of one type in terms of expressions of different kind. For example expanding, combining and converting expressions apply to term rewriting, and also simplification routines can be included here. Currently !SymPy has several functions and Basic built-in methods for performing various types of rewriting.

## Expanding

The simplest rewrite rule is expanding expressions into a _sparse_ form. Expanding has several flavors and include expanding complex valued expressions, arithmetic expand of products and powers but also expanding functions in terms of more general functions is possible. Below are listed all currently available expand rules.

Expanding of arithmetic expressions involving products and powers:
```
>>> ((x + y)*(x - y)).expand(basic=True)
x**2 - y**2

>>> ((x + y + z)**2).expand(basic=True)
x**2 + y**2 + z**2 + 2*x*y + 2*x*z + 2*y*z
```

Arithmetic expand is done by default in `expand()` so the keyword `basic` can be omitted. However you can set `basic=False` to avoid this type of expand if you use rules described below. This give complete control on what is done with the expression.

Another type of expand rule is expanding complex valued expressions and putting them into a normal form. For this `complex` keyword is used. Note that it will always perform arithmetic expand to obtain the desired normal form:

```
>>> (x + I*y).expand(complex=True)
-im(y) + I*re(y) + I*im(x) + re(x)

>>> sin(x + I*y).expand(complex=True)
sin(-im(y) + re(x))*cosh(re(y) + im(x)) + I*cos(-im(y) + re(x))*sinh(re(y) + im(x))
```

Note also that the same behavior can be obtained by using `as_real_imag()` method. However it will return a tuple containing the real part in the first place and the imaginary part in the other. This can be also done in a two step process by using `collect` function:

```
>>> (x + I*y).as_real_imag()
(-im(y) + re(x), re(y) + im(x))

>>> collect((x + I*y).expand(complex=True), I, evaluate=False)
{I: re(y) + im(x), 1: -im(y) + re(x)}
```

There is also possibility for expanding expressions in terms of expressions of different kind. This is very general type of expanding and usually you would use `rewrite()` to do specific type of rewrite:

```
GoldenRatio.expand(func=True)
1/2 + (1/2)*5**(1/2)
```

## Rewriting

## Combining

## Collecting