## Introduction
The assumptions in SymPy need to be rewritten. This page is dedicated to discussing the best way to go about this.

## Approaches
Here we discuss the merits of each approach to replacing the old assumption system.


### Tom
DISCLAIMER: I have no knowledge of the inner workings of the assumption system, or of the rationale of the switch to the new system. I shall follow Haz in assuming that there is a general consensus that assumptions should be stored separately, not alongside the objects, and that the old assumptions system should be phased out.

The following issues have been brought up about the new assumptions system:

1. Slow for trivial queries.
2. Cleaning global assumptions.
3. The Symbol('x', positive=True) syntax.
4. Interaction of the cache with changing assumptions.

#### Slow for trivial queries
Haz has said that this should probably not be an issue.

Consider this trivial benchmark:

<pre>
In [1]: x = Symbol('x', positive=True)

In [2]: global_assumptions.add(Assume(x, Q.positive))

In [3]: %timeit x.is_positive
1000000 loops, best of 3: 418 ns per loop

In [4]: %timeit ask(x, Q.positive)
10000 loops, best of 3: 97.3 us per loop
</pre>

This is probably fast enough, even if it is about 200 times slower.


#### Cleaning global assumptions
The cleanest way to do this would seem to me to have assumptions store weak references to symbols they involve, and have assumptions be cleared out when their symbols die. It is clear that python does not make guarantees about when objects are garbage collected, but that would seem OK to me: we don't need assumptions to go away for correctness, we want to have them go away for speed.

In case I am not clear this is what I mean about weak references.

     def Assume(expr):
         """ Assume that expr is True """
         s = expr.free_symbols
         for x in s:
             expr = expr.subs(x, weakref,ref(x))
         # Now store expr somewhere

There are a couple of points to note:

* It is not (currently) possible to actually create weak references to symbols.
* Even if this were possible it is not clear if other parts of sympy would play along nicely with weakrefs.

But note that in any case weak referencing refers a concept, not an implementation. We could still roll our own implementation that does exactly what we want.

One objection is that this is not very much different from storing assumptions with objects in the first place. I'm not sure about this, but one essential difference is that assumptions can be removed and introduced manually, all the weakreferencing does is to make sure assumptions go away when the objects do.

#### Replacing global assumptions by local assumptions
As outlined by Vinzent in the discussion of issue [[1884|http://code.google.com/p/sympy/issues/detail?id=1884]], even if global assumptions can be cleaned automatically as symbols die, this still would hardly be the desired behaviour. A better approach would be to use local assumptions, and inject a local assumptions context in the stack frame of the symbol creation. This has the disadvantage of being somewhat hackish, but apart from that it would have all the benefits of the above solution, plus more desirable semantics.

*Vinzent:* I think this approach in not as intrusive as other approaches, because it allows to use both assumption systems in parallel. This would allow to replace the old system gradually with the new one, without changing the interface. (If we decide to, we can still deprecate and remove the old syntax.)
Also it does not require a lot of work, because basically we let Python do the scoping.
(I think global assumptions are completely broken by design, they work only in interactive sessions, not in a library, so they should be removed.)
The `x.is_assumption` syntax would be equivalent to `ask(x, Q.assumption)` and could be kept. The same applies for `Symbol('x', assumption=True)`.

#### Symbol('x', positive=True) syntax
If the weakreferencing can be done, this would just be sugar for convenience.

#### Interaction with the cache
Computations depend on the assumptions active about objects, and the cache needs to be aware of this. One way to do this would be to just make the assumptions part of the hash for caching. Currently the cache does something like this:

     key = tuple(*args)
     try:
         return func_cache[key]
     ...

Instead we could just do something like this:

     objs = [x for x in args if isinstance(x, Basic)]
     syms = reduce(list.join, [x.free_symbols for x in objs])
     key = tuple(*args) + get_assumptions_involving[syms]
     try:
         return func_cache[key]

I did something similar regarding argument types (namely for functions to automatically evalf() it is necessary for the cache to distinguish Integer(1) and Real(1)).

Actually the cache *itself* would have to be made to use weakrefs, because otherwise cached symbols can never go away.

## Assumption Examples
<pre>
M ... Mathematica
S0 ... SymPy, current approach
S1 .... SymPy, approach 1
S2 .... SymPy, approach 2

M: Simplify[1/Sqrt[x] - Sqrt[1/x], x > 0]
S1: x = Symbol('x', assumptions=IsPositive)
  simplify(1/sqrt(x) - sqrt(1/x))
S2: simplify(1/sqrt(x) - sqrt(1/x), Assumptions(x>0))

M: FunctionExpand[Log[x y], x > 0 && y > 0]
S1: x, y = Symbol('x', assumptions=IsPositive), Symbol('y', assumptions=IsPositive)
 log(x*y).expand()
S2: log(x*y).expand(Assumptions([x>0, y>0]))

M: Simplify[Sin[n Pi], n \[Element] Integers]
S1: n = Symbol('n', assumptions=IsInteger)
  simplify(sin(n*pi))
S2: simplify(sin(n*pi), Assumptions(Element(n, Integer)))

# we can talk about the syntax of Element(n, Integer)

M: FunctionExpand[EulerPhi[m n], {m, n} \[Element] Integers && GCD[m, n] == 1]
S1: n = Symbol('n', assumptions=IsInteger)
  m = Symbol('m', assumptions=IsInteger)
  n.assumptions.add(Eq(gcd(m, n) - 1))
  euler_phi(m, n)
S2: euler_phi(m, n).expand(Assumptions([Element(n, Integer), Element(m, Integer), Eq(gcd(m, n) - 1)]))

# again we can talk about the syntax of Element(n, Integer)

M: RealQ[x, x \[Element] Real]
S0: x = Symbol('x',real=True, integer=True)
  assert x.is_real == True
S1:
S2: assert IsElement(x, Real, assumptions=Element(x, Real))

M: Refine[Abs[x], x>0]
   Refine[Abs[x], x<0]
S0:
S1:
S2: e = abs(x)
  print e.refine(Assumptions(x>0))
  print e.refine(Assumptions(x<0))
</pre>
