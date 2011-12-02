

The internals of !SymPy has changed many times. The current state in the trunk is described in SymPySvn.

We try to make the sources easily understandable, so you can look into the sources and read the doctests, it should be well documented and if you don't understand something, ask on the mailinglist. 

  * For !SymPy <= 0.4.3 the documentation is on this page
  * For !SymPy == 0.5.0 the documentation is in SympyResearch
  * For !SymPy > 0.5.0 and svn, read SymPySvn and/or read the sources

You can find all the decisions archived in the Issues, to see rationale for doing this and that. If you want to have the full picture, read all 3 documentations (<=0.4.3, ==0.5.0, >0.5.0), this will give you the historical background and you'll see what we tried, what ideas were behind the decisions made and how we arrived at the current state.

Documentation to !SymPy <= 0.4.3 is below.

# Basics

All symbolic things are implemented using subclasses of the `Basic` class.
First, you need to create symbols using `Symbol("x")` or numbers using
`Rational(5)` or `Real(34.3)`. Then you construct the expression using any class
from !SymPy.  For example `Add(Symbol("a"),Symbol("b"))` gives an
instance of the `Add` class.  You can call all methods, which the particular
class supports.

For easier use, there is a syntactic sugar for expressions like:

`cos(x)+1` is equal to `cos(x).__add__(1)` is equal to `Add(cos(x),Rational(1))` 

or

`2/cos(x)` is equal to `cos(x).__rdiv__(2)` is equal to `Mul(Rational(2),Pow(cos(x),Rational(-1)))`.

So, you can write normal expressions using python arithmetics like this:
```
a=Symbol("a")
b=Symbol("b")
e=(a+b)**2
print e
```
but from the sympy
point of view, we just need the classes `Add`, `Mul`, `Pow`, `Rational`.

# Automatic evaluation to canonical form: eval()

For computation, all expressions need to be in a
canonical form, this is achieved using the method `eval()`, which  only performs
unexpensive operations necessary to put the expression in the canonical form.
So the canonical form doesn't mean the simplest possible expresion. The exact
list of operations performed by `eval()` depends on the implementation.
Obviously, the definition of the canonical form is arbitrary, the only
requirement is that all equivalent expressions must have the same canonical
form.  We tried the conversion to a canonical (standard) form to be as fast as possible and
also in a way so that the result is what you would write by hand - so for example `b*a + -4 + b + a*b + 4 + (a+b)^2` becomes `2*a*b + b + (a+b)^2`.  The order of terms in the
sum is sorted according to their hash values, so they don't have to be in the
alphabetical order (depends on the hash implementation).

Whenever you construct an expression, for example `Add(x,x)`, the instance of the class `Add` is constructed, in this case it represents `x+x`, and then it's eval() method is called automatically and the result of eval() is actually returned. In this case:
```
e=Add(x,x)
```
`e` actually is an instance of `Mul(2,x)`, because `Add.eval()` retuned `Mul`. This magic is done using the `AutomaticEvaluationType` metaclass, which is implemented in `basic.py` and the class `Basic`. This metaclass just constructs a given instance and returns the result of it's `eval()` method. All the other classes in sympy just don't have to care about it. All that is needed when you create a new sympy class is to optionally implement it's eval() method to simplify things like `cos(0)` to `1`. It's not mandatory, if you don't want any simplifications to happen, but then `cos(0)==1` would return `False`.

There is no place in the code, which needs to think about evaluation and
`eval()`, with two exceptions:

  * the `eval()` itself, whose responsibility is to return a canonical form of `self`. Whatever the canonical form is - this is completely optional and depends only what we implement inside of `eval()`.
  * There are very rare cases, where you actually don't want the automatic evaluation to happen, currently only 3:
     1. in `Pow.expand()`, we call `Mul(a+b,a+b).expand()`, but we don't want that to be evaluated, because it would change to `Pow(a+b,2).expand()` resulting in infinite recursion.
     1. `Add.eval()` and `Mul.eval()` after converting itself to canonical form, we have n arguments and we need to construct `Add` or `Mul` using these arguments and we set `evaluate=False`, otherwise we again would get infinite recursion.

This is handled by the metaclass `AutomaticEvaluationType` in `basic.py`.
It simulates another keyword parameter to all `__init__`s: `evaluate`,
default is `True`, which means that after construction of any instance,
the `AutomaticEvaluationType` will call it's `eval()` method. If you set
`evaluate=False`, the `eval()` method is not called. Example:
```
Mul(a+b,a+b,evaluate=False)
```
is just `(a+b)*(a+b)` and
```
`Mul(a+b,a+b)`
```
is the same as `Mul(a+b,a+b, evaluate=True)`, which is `(a+b)**2`.

# Comparisons

Expressions can be compared using a regular python syntax:
```
a+b==b+a
```
This is equivalent to `(a+b).__eq__(b+a)` and the `Basic.__eq__()` method just calls `eval()` to both `self` and the argument and then compare the hashes.

Which means that if the expansion operation is not performed upon evaluation (which is
reasonable), then `(a+b)^2 != (a^2+2ab+b^2)`, on the other hand
`((a+b)^2).expand() == (a^2+2ab+b^2)`. As we said, what exactly is performed in `eval()` depends on the implementation, for example the expansion would be in `pow.eval()`. In the current implementation of sympy, we do not perform expansion in `pow.eval()`.

We made the following decision in sympy: `a=Symbol("x")` and another `b=Symbol("x")` (with the same string "x") is the same thing, i.e `a==b` is `True`. Note that this is different from Ginac. We chose `a==b`, because it is more
natural - `exp(x)==exp(x)` is also `True` for the same intance of `x` but different instances of `exp`, so we chose to have `exp(x)==exp(x)` even for different instances of `x`. 

Sometimes, you need to have a unique symbol, for example as a temporary one in some calculation, which is going to be substituted for something else at the end anyway. This is achieved using `Symbol("x",dummy=True)` or simply as `Symbol("x",True)`. So, to sum it up: `Symbol("x")==Symbol("x")`, but `Symbol("x",True)!=Symbol("x",True)`.

# Functionality

There are no given requiremens on classes in the library. For example, if they
don't implement the `diff()` method and you construct an expression using such a
class, then trying to use the `Basic.series()` method will raise an exception of not
founding the `diff()` method in your class. This "duck typing" has an advantage
that you just implement the functionality which you need. You can define the
function `cos` like this
```
class cos(Basic):
    def __init__(self,arg):
        basic.__init__(self)
        self.arg=arg
```
and use it like `1+cos(x)`, but if you don't implement the `diff()` method, you
will not be able to call `(1+cos(x)).series()`.
the symbolic object is characterized (defined) by the things which it can do.
so implementing more methods like `diff`, `subs` etc., you are creating a "shape" of the symbolic object. Useful things to implement in new classes are: `hash` (to use the class in comparisons), `eval` (to do some easy rewritings automatically, like `a+a -> 2a`), `diff` (to use it in series expansion), `subs` (to use it in expressions, where some parts are being substituted), `series` (if the series cannot be computed using the general `basic.series()` method). When you create a new class, don't worry about this too much - just try to use it in your code, and you will realize immediately, which methods need to be implemented in each situation.

All objects in the sympy are immutable - in the sense, that any
operation (like `eval()` for example) just returns a new instance (it can
return the same instance only if it didn't change). This is a common mistake
to change the current instance, like `self.arg=self.arg +1` (wrong!). Use
`arg=self.arg + 1;return arg` instead. The object in immutable in the
sense of the symbolic expression it represents. It can modify itself to keep
track of for example its hash. Or it can precalculate
anything regarding the expression it contains. But the expression cannot be
changed. So you can pass any instance to other objects, because you don't have
to worry that it will change, or that this would break anything.

# Conclusion

So, those are the main ideas behind sympy, which we try to obey. The rest depends on the current implementation and can possibly change in the future. The point of all of this is that the inter dependecies inside sympy should be kept to a minimum. If one wants to add new functionality to sympy, all that is necessary is to create a subclass of `Basic` and implement what you want.

# Other systems

very interesting link describing the algorithms used by mathematica: 
[http://documents.wolfram.com/v5/TheMathematicaBook/MathematicaReferenceGuide/SomeNotesOnInternalImplementation/A.9.5.html here]
 
 
 
 
 