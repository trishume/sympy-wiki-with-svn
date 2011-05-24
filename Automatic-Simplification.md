These are my thoughts on automatic simplification of expressions.  This is adapted from [this message to the mailing list](http://groups.google.com/group/sympy/msg/76e8d488d3c32736?pli=1).  

-- Aaron Meurer

When creating a new object, or modifying an already existing one, there is often a temptation to make some evaluation and simplification rules happen automatically.  However, this is often a bad idea.  I will elaborate on why in a bit.  There are four conditions that should be met for any evaluation or simplification rule to be done automatically (i.e., at object instantiation time):

1. The rule is correct.
2. The rule will always make the object simpler. 
3. The rule is very cheap in every case. 
4. The rule is so trivial that no one will ever not want it done. 

**1.** is probably the most obvious of the rules, but it often does not hold.  For example, in SymPy 0.6.5 and earlier, `sqrt(x*y)` was automatically reduced to `sqrt(x)*sqrt(y)`.  But this does not hold for general `x` and `y`, for the same reason that `sqrt(x**2)` does not equal `x` in general.  For example, if `x == y == -1`, then `sqrt(x*y) == sqrt(-1*-1) == sqrt(1) == 1`, but `sqrt(-1)*sqrt(-1) == I*I == -1`. This simplification is only true in general if `x, y >= 0`.  If `x` and `y` are given these assumptions (`x, y = symbols('x y', nonnegative=True)`), then SymPy will automatically convert `sqrt(x*y)` to `sqrt(x)*sqrt(y)`.

It usually happens that the simplification that you want to apply do hold for a subset of possible inputs, like above, but fail to be correct in the general case.  In SymPy, 99% of the time this is related to assumptions.

**2.** also seems obvious, but it too is often violated.  The problem is often that the automatically evaluated form may seem simpler for certain input values, like small input values.  But becomes clear that the rule makes things far more complicated with more carefully chosen input values.  Since less simple expressions are by their nature larger, a violation of this rule will invariably mean a violation of rule **3.**.

For example, suppose that you wanted to apply the rules `log(a**p) == p*log(a)` and `log(a*b) == log(a) + log(b)` automatically, where `a` and `b` are positive integers and `p` is real (apologies to Chris Smith, who wanted to do this; if you can think of a better example, I will use it instead).  This rule is correct, because of the assumptions on `a`, `b`, and `p`.  If you look at small values, it looks like it might be something worth doing.  For example, `log(18) == log(2*3**2) == log(2) + 2*log(3)`.  And it would allow things like `log(6) - log(2)` to automatically simplify to `log(3)`, because the `log(6)` would automatically be expanded to `log(2) + log(3)`, and the `log(2)`s would cancel.  

But if you consider large inputs values, you will soon see that this makes things much less simple.  `log(factorial(10))` would become `2*log(5) + 4*log(3) + 8*log(2) + log(7)` instead of just `log(3628800)`.  You can imagine what `log(factorial(100))` would look like.  

*More to come…*