

# Introduction

This page serves as a reference for developers of !SymPy, how things are done internally and which idioms to use and which not. Please discuss new and current features in the [http://code.google.com/p/sympy/issues/detail?id=387 issue 387]. This page is a consensus, that we arrived at and thus if some code in !SymPy doesn't follow these recommendations, it's a bug. Note that we are still figuring things out and thus we may decide to change some recommendations on this page in the future. 

All changes to the trunk should be discussed in Issues and should follow this page. However, it's also necessary to try new ideas without asking others to agree with that and we do these things in other branches, like `sympy-sandbox`. When we discover, that something should be done differently, we'll arrive at a consensus and update this page.

# Functions

How to create a new function of a one variable:
```
class sign(Function):

    nargs = 1

    @classmethod
    def canonize(cls, arg):
        if isinstance(arg, Basic.NaN):
            return S.NaN
        if isinstance(arg, Basic.Zero): return S.One
        if arg.is_positive: return S.One
        if arg.is_negative: return S.NegativeOne
        if isinstance(arg, Basic.Mul):
            coeff, terms = arg.as_coeff_terms()
            if not isinstance(coeff, Basic.One):
                return cls(coeff) * cls(Basic.Mul(*terms))

    is_bounded = True

    def _eval_conjugate(self):
        return self

    def _eval_is_zero(self):
        return isinstance(self[0], Basic.Zero)
```

and that's it. The `_eval_*` functions are called when something is needed. The `canonize` is called when the class is about to be instantiated and it should return either some simplified instance of some other class or if the class should be unmodified, return `None` (see `core/function.py` in `Function.__new__` for implementation details). See also tests in [http://hg.sympy.org/sympy/file/tip/sympy/functions/elementary/tests/test_interface.py sympy/functions/elementary/tests/test_interface.py], that test this interface and you can use them to create your own new functions.

The applied function `sign(x)` is constructed using
```
sign(x)
```
both inside and outside of !SymPy. Unapplied functions `sign` is just the class:
```
sign
```
Both inside and outside of !SymPy. 
This is the current structure of classes in !SymPy:
```
class BasicType(type):
    pass
class MetaBasicMeths(BasicType):
    ...
class BasicMeths(AssumeMeths):
    __metaclass__ = MetaBasicMeths
    ...
class Basic(BasicMeths):
    ...
class FunctionClass(MetaBasicMeths):
    ...
class Function(Basic, RelMeths, ArithMeths):
    __metaclass__ = FunctionClass
    ...
```
The exact names of the classes and the names of the methods and how they work can be changed in the future.

This is how to create a function of two variables:
```
class chebyshevt_root(SingleValuedFunction):
    nofargs = 2

    @classmethod
    def _eval_apply(cls, n, k):
        if not 0 <= k < n:
            raise ValueError, "must have 0 <= k < n"
        return Basic.cos(S.Pi*(2*k+1)/(2*n))
```

Note 1: the `nofargs` is obsoleted and will be removed in a near future.

Note 2: the first argument of a @classmethod should be `cls` (not `self`).

## common tasks

Please use the same way as is show below all across !SymPy.

### accessing parameters
```
In [1]: e = sign(x**2)

In [2]: e[:]
Out[2]: (x**2,)

In [3]: e[0]
Out[3]: x**2

In [4]: (x+y*z)[:]
Out[4]: (x, y*z)

In [5]: (y*z)[:]
Out[5]: (y, z)

In [6]: sin(y*z)[:]
Out[6]: (y*z,)

```
Never use internal methods or variables, prefixed with "`_`" (example: don't use `_args`, use `[:]` instead).

=== testing the structure of a !SymPy expression == 

Applied functions:
``` 
In [1]: e = sign(x**2)

In [4]: isinstance(e, sign)
Out[4]: True

In [5]: isinstance(e, exp)
Out[5]: False

In [2]: isinstance(e, Function)
Out[2]: True
```
So `e` is a `sign(z)` function, but not `exp(z)` function. 

Unapplied functions:
```
In [1]: e = sign

In [2]: f = exp

In [3]: g = Add

In [4]: isinstance(e, FunctionClass)
Out[4]: True

In [5]: isinstance(f, FunctionClass)
Out[5]: True

In [6]: isinstance(g, FunctionClass)
Out[6]: False

In [10]: g is Add
Out[10]: True
```
So `e` and `f` are functions, `g` is not a function.