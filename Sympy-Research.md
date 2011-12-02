


# Introduction

This page collects documentation notes for the new trunk, which merged new core developed by Pearu with !SymPy. More information can be found in 
[http://code.google.com/p/sympy/issues/detail?id=144 Issue 144]

Usage:

simply checkout the trunk, most things should be working the same way as before.

# Mathematical constants

The following mathematical constants are defined in `sympy`:

 * I --- imaginary unit `sqrt(-1)`
 * oo --- positive infinity
 * nan --- undefined value
 * pi --- pi = 3.14..
 * E, exp(1)  --- Euler number E = 2.718.., exp(1)

Use `.evalf()` method to get floating point approximation with the current precision `Basic.set_precision()`.

## Examples

```
>>> Basic.set_precision()
28
>>> pi.evalf(), E.evalf()
(3.141592653589793238462643383, 2.718281828459045235360287471)
>>> Basic.set_precision(40)
28
>>> pi.evalf(), E.evalf()
(3.141592653589793238462643383279502884197,
 2.718281828459045235360287471352662497757)
>>> I,I**2,oo,nan
(I, -1, oo, nan)
```

# Assigning properties to symbols and expressions

## Construction call

  <symbolic class>(<constructor arguments>, property1=value1, property2, ..)

## Method call

  `<expr>.assume(property1=value1, property2=value2, ..)`

## Parameters

  * `property1, ...` --- names of mathematical properties
  * `value1, ...` --- `True` or `False` or `None`

## Details

  * The following predefined mathematical propeties are supported (opposite properties are given in parenthesis):

     1. `positive` (`nonpositive`), `negative` (`nonnegative`) --- `expr` can have only positive or negative real values, respectively
     1. `complex` (`noncomplex`) --- `expr` has values from the set of complex numbers
     1. `real` (`nonreal`) --- `expr` has values from the set of real numbers
     1. `rational` (`irrational`) --- `expr` has values from the set of rational numbers
     1. `integer` (`noninteger`) --- `expr` has values from the set of integers
     1. `odd` (`even`) --- `expr` value is an odd integer
     1. `prime` (`composite`) --- `expr` value is a prime
     1. `zero` (`nonzero`) --- `expr` value is zero
     1. `bounded` (`unbounded`) --- `expr` absolute value is bounded
     1. `finite` (`infinitesimal`) --- `expr` value is nonzero and finite
     1. `commutative` (`noncimmutative`) --- `expr` value commutes with other values with respect to multiplication
     1. `homogeneous` (`inhomogeneous`) --- `expr` value is a homogeneous function with respect to its arguments
     1. `comparable` --- `expr` value can be compared with numbers (`expr.evalf()` returns `Number` object).
     1. `pi` is alias to `integer`, `positive` properties
     1. `nni` is alias to `integer`, 'nonnegative' properties

  * If property value is `False`, the opposite property is set. For example, setting `positive=False` is equivalent to `nonpositive=True`.
  * Assigned properties can be unset using property value `None`.
  * Unsetting a property will unset related properties. For example, unsetting `real` will also unset `positive` property, for instance.
  * `expr` properties can be requested via `.is_property` attributes. If no information is known for a given property then `.is_property` attribute is `None`.
  * `expr` properties can be set using `property=value` keyword arguments in the corresponding class constructor.

## Rules

From a set of properties on can derive more properties. For example, if
an expression has property `positive` then it follows that the expression
has also a property being `real` (as the set of positive numbers is a subset of
real numbers) as well as being `complex` (as the set of real numbers
is a subset of complex numbers), etc. In general, a property, say _P_,
may be a union of subproperties, say _P_^1^, _P_^2^, etc. For example, if
_P_ is `real` then _P_^1^ and _P_^2^ can be `positive` and `nonpositive`, respectively.
Each property has opposite property, e.g. the opposite property of `odd` is `even`.

The following rules apply for derived properties:

  * if `x` sets _P_^i^ to `True` or `False`, then _P_ is `True`
  * if `x` sets _P_^i^ to `None`, then _P_ keeps its value.
  * if `x` sets _P_ to `True`, _P_^i^ is not modified (it's probably `None`)
  * if `x` sets _P_ to `False` or `None`, then _P_^i^ is set to `None`. 
  * if `x` sets _P_^1^ to `False` or `True` or `None`, then its opposite property `_P_^2^` is set to  `True` or `False` or `None`, respectively.


## Examples

```
>>> x = Symbol('x')
>>> x.is_real
>>> x.assume(positive=True)
>>> x.is_real
True
>>> x.is_negative
False
>>> exp(x).is_positive
True
>>> log(x).is_negative
>>> x.assume(infinitesimal=True)
>>> log(x).is_negative
True
>>> y = Symbol('y', even=True)
>>> y.is_integer
True
>>> y.is_odd
False
```

# O – the domain of order terms (Landau symbols)

  `O(f, x)` represents the Landau symbol _O(f, x -> 0)_.

## Call

  `O(f, x, y, ..)`

## Parameters

  * `f` --- an arithmetical expression representing a function in x, y, etc.
  * `x, y` --- variables, assumed to be infinitesimal and positive symbols

## Return value

  an `O` or `Zero` instance.

## Details

 * According to the mathematical definition, for a function f with variables x,y, .., the  Landau symbol _g = O(f, x, y, ..)_ is a representative of a class of functions having the following property: there exists a constant M and a neighborhood of the limit point _(0, 0, ..)_ such that _|g| <= M|f|_ for all values _(x,y,..)_ in that neighborhood. Note that in general `O(f(x,y),x,y) + O(g(x,y),x,y)` is not the same as `O(f(x,y)+g(x,y), x,y)`.

 * If variables `x, y, ..` are not specified then all symbols in `f` are considered as order variables. Otherwise all other symbols in `f` except `x, y, ..` are considered as parameters.

 * The symbols in `O` instance can be accessed via `.symbols` attribute.

 * The expression in `O` instance can be accessed via `.expr` attribute.

 * The inclusion relation between _O(f, x)_ and _O(g, x)_ is determined by the result of `limit(f/g, x, 0)`. If the result is unbounded (e.g. `oo`) then _O(g, x)_ is a subset of _O(f, x)_ and `O(f,x)+O(g,x)` results `O(f,x)`.

 * Automatic simplification is applied to `O` expression. See examples.

 * Assumptions `infinitesimal=True, positive=True` are set to `O` symbols.

 * Using `O` in the argument expression of a function leads to either Add or Order instance after applying the rule: _f(g(x) + O(h(x),x)) -> f(g(x)) + O(h(x) f'(g(x)), x)_ provided that _f'(g(x))_ is not zero.

## Examples

```
>>> from sympy.core import *
>>> x,y=Symbol('x'), Symbol('y')
>>> O(x,x),O(3*x,x),O(x+x**2),O(x+1/x),O(x+1/x+exp(2/x))
(O(x, x), O(x, x), O(x, x), O(1 / x, x), O(exp(2 / x), x))
>>> O(x+3*y), O(x+x*y), O(3*x*y**2-x**2*y+x**2*y**2), O(y**2*x**2+x*y**3,y)
(O(x + y, x, y), O(x, x), O(x * y ** 2 + y * x ** 2, x, y), O(y ** 2, y))
>>> O(x*y).expr, O(x*y).symbols
(x * y, (x, y))
>>> O(0,x), O(2,x)
(0, O(1))
>>> O(x) + O(y), O(x+y)
(O(x, x) + O(y, y), O(x + y, x, y))
>>> exp(1+x+O(x**3))
exp(1 + x) + O(x ** 3, x)
>>> cos(O(x))
1 + O(x ** 2, x)
```

# Functions

To define a new function in !SymPy, a three step process is needed. First of all we need to create _the_ function with its name, the number of arguments, default properties, series handling and, especially, evaluation procedure. As an example consider the following code:

```
class Im(DefinedFunction):
    nofargs = 1

    is_real = True

    def _eval_apply(self, arg):
        arg = Basic.sympify(arg)

        if isinstance(arg, Basic.NaN):
            return S.NaN
        elif arg.is_real:
            return S.Zero
```

This way new function called _Im_ has been defined (which stands here for the simplified version of an imaginary part function, which is implemented in `sympy/functions/elementary/complexes.py`). Later this function will be identified via this name in lower case form.

The number of obligatory arguments is specified by setting `nofargs` class member. Additional arguments do not account here, but they will be visible in `_eval_apply` method. For example logarithm has `fnoargs=1` for primary expression but you can also pass its base as an additional parameter. However logarithm function will rewrite itself to form with exactly one parameter (using the base change formula).

If function has properties which are valid for all arguments, you can set these using assumptions mechanism. In case of imaginary part, I've set `is_real=True` as this is what always holds.

Now the most important part of our function is evaluation procedure, `_eval_apply`, which will have exactly `nofargs` arguments without default value, plus additional with default value set to `None`. It's recommended, as the first step in this procedure, to check if all arguments are !SymPy compatible using `Basic.sympify()`. This step is a cheap if those arguments are already derived from the Basic class.

Next step is to analyze the arguments. First we needed to get rid of the optional ones. We must check for them and then rewrite the function so that only obligatory arguments will be present. If this is done, the next step is to put function into a normal form. What this term means depends on a concrete function and its implementation. However, the general rule is to perform *non-expensive* rewriting to function's arguments, which means you must avoid using complex procedures like polynomial algorithms, `expand()`, `combine()` functions and any general simplification procedures like `simplify()`. What you should use are all representation functions (those which begin with `as_`, also functions like `has()`, `atoms()` and eventually `match()`.

If any reasonable rewrite is possible, then the function should return new value if function invocation is no more needed or self with new arguments otherwise. If no rewrite is possible for some classes of arguments then `_eval_apply` should return nothing ie. no return at all, or stand alone return statement or return None. In all three cases the super class, which is `DefinedFunction`, will fall back to the original function with arguments left untouched, for efficiency reasons.

If you follow the above steps you will get a !SymPy compatible function. However its capabilities are quite limited. What you can improve is to define its derivative and inverse, add floating point evaluation, power series expansion, non-default handling of value substitution etc.

It is important to notice that thte function defined is just an ordinary Python object so it is created with following syntax: `function_name()` with no arguments eg. `Im()`. One must not mix this with application of arguments to a function, which is done with calling an instance of defined function class ie. `Im()(x)` where `x` is a symbol. This way instance of `Apply` class is created which will handle 'runtime' properties of this function. Try in _isympy_ shell the following:

```
>>> type(Basic.Log())
<class 'sympy.core.defined_function.Log'>

>>> type(Basic.Log()(x))
<class 'sympy.core.defined_function.ApplyLog'>
```

For usage simplicity `Basic` class provides `singleton` attribute, which is a mapping of simple names to instances of defined functions. For example you can write just `log` for the logarithm function rather than `Log()`. However notice that this is available only on run time and in library code you are obliged to use the _full_ form.

When you issue log(x) in _isympy_ shell or `Log()(x)` in library code, new instance of Apply class is created with first argument being the logarithm function and obligatory and also additional parameters.

Having only an instance of defined function class we are able to work with the function itself eg. we can compute function derivative. However the result might be interesting:

```
>>> log.fdiff()
lambda _x: 1 / _x
```

or 

```
>>> sin.fdiff()
cos
```

In the first example we got anonymous function (or just lambda for functional programmers). In the other we got another defined function. In both cases the result is unevaluated function (notice the `f` in front of `diff`). To compute the well known derivative we need function application rather than definition, eg.

```
>>> log.fdiff()(x)
1 / x

>>> log(y).diff(y)
1 / y
```

or 

```
>>> sin(2*x).diff(x)
2*cos(x)
```

By default instance of `Apply` is created. You can change this behavior by overriding this class and implementing new specific one. Going back to the very first example, we can define the following:

```
class ApplyIm(Apply):

    def _eval_is_real(self):
        return True

    def _eval_complex_expand(self):
        return self.func(self.args[0].as_real_imag()[1])
```

When implementing such class we care about the _runtime_ behavior of our defined function. Previously we stated that `is_real=True`. However now we have to restate the same in `_eval` form.

Notice also `_eval_complex_expand` method. Finally we have access to function's arguments and its name, which will be `im` in this case. What can be implemented more here are all functions with names beginning with `_eval_*` (with exceptions like `_eval_apply` and `_eval_apply_evalf`). You can also implement representations functions here (those with begin with `as_`) and `tostr()` method.

When you are finished with implementation, remember to add both new classes to `ordering_of_classes` list in `core/basic_methods.py` in appropriate places. This will help !SymPy properly display new functions in combination with all other objects.

The last step is to write tests for all functionalities you have implemented. Especially great care must be taken in testing evaluation procedure. For this there is separate test suit in `core/tests/test_eval_apply.py`. One general rule applies, all cases must be covered with at least one test. This way when we modify this function's logic or we change something very different we will be sure that with those modifications functions are evaluated properly. Of course the same applies to other code too.

Currently, there are all elementary functions implemented (exponential, trigonometric, hyperbolic and their inverses), complex components (real and imaginary parts, conjugate, argument and absolute value) and integer functions like floor and ceiling. All of these are located in `core/defined_functions.py`. There is also a preliminary support for some special functions ie. complete and incomplete gamma and zeta, and combinatorial functions, in _specfun_ module. In most cases symbolic evaluation is done, however improvements are needed to power series expansions (especially handling of singularities) and assumptions. 

# Developers notes

Below some design decisions in the `sympy.core` are explained.

`sympy.core` uses a symbolic model where all symbolic objects are immutable,
they are constructed from classes that are derived from `Basic` class.
For example, sympy.core defines the following classes for elementary symbolic manipulations: `Symbol`, `Number`, `Add`, `Mul`, `Pow`, `Function`, `Apply`.
There is a number of other classes derived from Basic or classes listed above
for adding more features to the used symbolic model. For example, `Symbol` is
a base class to `Wild`, `Temporary` and `Number` is a base class to `Real`, 
`Rational`, and `Integer` classes.

The implementation of the symbolic model uses many advanced features from the
Python language such as newstyle classes, metaclasses, properties, decorators, etc. The goal is to keep code minimal, readable, and to get maximum performance using
pure Python code while keeping in mind that in future some computationally 
intensive code should be implemented in a C/C++ extension module.

For efficiency, the following is taken into account:

  * In pure Python constructing an object _is_ an expensive operations. This is especially true for symbolic objects that may need to evaluate their arguments to some normal form. For example, constructing a rational number involves finding gcd of its numerator and denominator. In constructing `Add` and `Mul` instances some elementary simplifications (evaluations) are carried out. Therefore, many frequently used symbolic notions like numbers are created only once (via singleton or caching technique) and computed results that might be needed in further operations are cached.

  * Also, the result of an evaluation may be different from the original constructor. For example, `Add(x, x)` will result in `Mul(2,x)`. In this situation, `sympy.core` will never create an intermediate object representing `x+x` but carries out evaluation and then creates a final object representing `2*x`.

  * Comparing symbolic objects for an equality can be very expensive as one may need to walk through large trees of symbolic objects. Therefore, the code must be optimized for elementary comparisons such as if a symbolic object is an instance of some special number, etc. So, a codelet like `obj == 1` should be replaced with `obj is S.One` or `isinstance(obj, Basic.One)` or `obj.is_one`, that involve only single operations, for efficency. Note that executing `obj==1` involves a number of operations, it is equivalent to the following code: `Equality(obj, Basic.sympify(1)).__nonzero__()` where the `__nonzero__` code contains comparison code for symbolic objects.

  * In `sympy.core` the comparison of symbolic objects takes advantage of the fact that all symbolic objects are strictly ordered (not always in mathematical sense, of course). This is achived by sorting the content of otherwise commutative operations such as `Add` and `Mul`. The order of symbolic objects is first defined by the class name in the `ordering_of_classes` list in `basic_methods.py` file, and then by the order of tuple representation of symbolic objects returned by the `._hashable_content()` methods. See the implementation of `Basic.compare` for more details.

For extending the symbolic model, the following is taken into account:

  * Different symbolic classes may need to have access to each other features while the classes are implemented in different modules or even in different packages. Therefore one must be careful with importing modules as in the given situation cyclic imports are introduced. `sympy.core` resolves this issue by making all `Basic` subclasses to be attributes of the `Basic` class at the moment of defining the subclasses. As a result, one only needs to import `Basic` from `sympy.core.basic` module to get access to _all_ classes that are derived from the `Basic` class.