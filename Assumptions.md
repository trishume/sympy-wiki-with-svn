## Introduction
The assumptions in SymPy need to be rewritten. This page is dedicated to discussing the best way to go about this.

## Approaches
Here we discuss the merits of each approach to replacing the old assumption system.


### Algebra Objects

#### Introduction and Goals
As for all proposals on this page, the main aim is to figure out a way to disconnect assumptions from the core, within the time frame before the next release.

A closely related aim is to sort out the entanglement of assumptions, core and caching.

Thirdly, this proposal also aims to resolve some conceptual tensions and practical shortcomings I see with the current object model in Sympy. Obviously this last part has a good chance of being mis-guided since I don't know sympy very well. So I will try to concentrate on the first two aims.

For an example of a practical shortcoming I see, consider the treatment of order terms. Since we want to be general the dominance problem has to be solved by computing limits. But this is slow if we are actually working with power series, where the dominance problem is a simple comparison of exponents. We could special-case this (which is what I essentially did in one of my commits), but it remains delicate. The underlying problem is that a *simple* object (a power series + order term) gets a *complicated* representation (indeed the most general representation of objects we allow).

This brings me to the conceptual tension: in the one case in sympy where we really want to "crunch simple objects", namely polys, the principal objects of interest become sort of "second-class citizens". By this I mean that (as far as I can see) the polys functions that are exposed to the user take an arbitrary sympy expression, convert it into the private (efficient) representation and then proceed. Finally the private representation is converted back to an ordinary sympy expression. This works (obviously) but it is cumbersome and hence not done a lot in other parts of the code. But I think whenever there are time-intensive computations, the sympy object model should naturally encourage using the most efficient representation of data.

What follows will be an amalgamation of the ideas of Frederik and Pearu (i.e. sympycore). All cleverness is theirs and all stupidity of the presentation is mine :-).

#### The Element/Algebra Model

The basic idea is that to every expression that is to be manipulated (sin(x), `x**2 + 7`, ...) we associate an explicit *algebra* object. This algebra object defines how elements can be operated on. For example if A and B are two expressions, then A+B will cause `Basic.__add__` to check if A and B belong to the same algebra, and if so call A.algebra.do_add(B). The result will be a new element of the same algebra.

The "core" algebra, i.e. the one which most closely resembles the current objects of sympy, will be called "calculus" in what follows.

##### Verbatim: the most general algebra there is

Since algebras are allowed to represent their elements in any way they like, it is important to introduce a uniform way of converting them. The verbatim algebra can store and manipulate arbitrary elements, without making any assumption about their meaning. To do this it stores what is usually called S-expressions: much like in the current design, every element is stored as a pair (head, args) where head is any kind of identifier (not necessarily a callable) and args represents the parameters for head. Args is a tuple of S-expressions. So for example (ADD, (x, y, 5)) represents x+y+5.

In order to allow conversion between algebras, every algebra needs to be able to convert its elements into elements of Verbatim, and it needs to provide a general method to construct its own representations of a given S-expr. For this to make sense the possible heads have to be standardised somewhat, but not completely: while (probably) every algebra needs to represent addition and should use ADD for that, not every algebra knows about the sine function. In general if compatibility with other algebras is not important, private identifiers can be used for the heads. If an algebra encounters an unrecognised head, it can simply throw an exception.

Note that e.g. the pretty printing can usefully operate on the verbatim algebra.

##### Extension, Specialisation and Unification of Algebras

*Extension* refers to the process of creating a new algebra from a given one, where the new one provides additional functionality. For example there could be a CachingAlgebra which extends any given algebra and caches all operations. Note that I use the term extension here only for thin wrappers like this. For example the calculus algebra can represent any object of a polynomial algbra, but the representation is totally different so it should not be seen as an extension for the purpose of this writing.

*Specialisation* refers to the process of using a more efficient representation for a subset of the elements of a given algebra, while retaining extensions. For example computing limits could be done in a cached version of the calculus algebra. However one crucial part is series expansions, and this could usefully be done in a "truncated generalised power series" algebra. We would, however, like to keep all the extensions of the original algebra (in particular the caching).

A third operation is *unification*: what to do if the user requests an operation on two elements of differing algebras? Throwing an exception would be one possibility, but in particular for transition purposes, and also for convenience, it would be helpful to just pick an algebra that can represent both objects, convert them, and continue operating there.

#### Use Case 1: Caching
As mentioned above, caching would be an obvious candidate for specialisation. An algorithm that relies on caching for reasons of performance would create a cached version of whatever algebra it is supposed to operate in and convert all objects to there as the first step. Note that 1) the caching algebra constructor can be intelligent so as not to add several layers of caching, 2) the cache is cleared automatically after the algorithm is finished, since the caching algebra object was constructed specially for this purpose (except if the ground algebra already had caching...), and 3) the algorithm now has to ensure that all requirements for caching are fulfilled, e.g. no assumptions are changed in interim.

The CachingAlgebra presumably would not necessarily cache *all* operations, but only those marked @cachethis. Normally @cachethis would be a no-op.

#### Use Case 2: Assumptions
This is a bit more complicated, especially if we want to be able to use both caching and assumptions at the same time. There has been a sentiment of removing all assumptions from objects, but I think this is wrong (or mis-represented). If assumptions are tied to objects (implicitely using global assumptions or explicitely by making them part of the objects), then the cache *has* to know this.

But notice that the original goal (as far as I know) was not principally to remove assumptions from objects, but to simplify the core. So it would be enough if objects of the calculus algebra simply don't have assumptions. So here is how I could imagine assumptions being implemented:

1. Basic retains all the standard is_... properties, but they always return None. In the calculus algebra, Add etc don't overwrite any of the is_... properties.
2. There is an AssumptionsAlgebra extension algebra which adds assumptions to symbols. Also all of the objects that can do assumption inference (e.g. Add) overwrite the appropriate is_... methods again.

Finally with things separated out like this, it would also be easy to instead of using the old implementations of is_... in step two to refer to the ask interface. The ask function then would have to be changed to ignore all is_... properties except those on symbols.

Passing around explicit assumptions in addition would also be possible, but this needs some thinking on how it can play along nicely with extension/specialisation of algebras etc.

#### Implementation Strategy
As far as I can see the following steps would be necessary to solve the caching and assumptions issues in the new framework.

1. Add an Algebra base class.
2. Add the verbatim algebra.
3. Make most of the current core part of a new calculus algebra.
4. Separate assumptions inference from calculus algebra objects, and move them to an AssumptionsAlgebra extension algebra.
5. Make the "Symbol" constructor alias calculus.Symbol if no assumptions are passed, and the assumptions version otherwise.
6. Add CachingAlgebra extension algebra.
7. Add the necessary unification code.
8. Extend non-core code that relies on caching to create CachingAlgebras.

The following steps would be desirable in the long term, but are not essential initially:
9. Make the pretty printers operate on Verbatim.
10. Separate out non-commutative code from the core, create a NonCommutativeCalculus algebra.
11. Make polys part of the algebras framework.
12. Add a TruncatedGeneralisedPowerSeries algebra for series expansions.


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

*Vinzent:* 
The idea is the following: In the old system assumptions were tied to symbols. We decided to decouple assumptions from symbols, so the new assumptions system was born. Tying assumptions to symbols had the advantage that they were also tied automatically to the local scope. The idea is to reproduce this behavior in the new system, by using "local assumptions" which are stored as a hidden variable in the local scope where the symbol was defined. This way, we can conserve the advantage of the old system.

I think this approach in not as intrusive as other approaches, because it allows to use both assumption systems in parallel. This would allow to replace the old system gradually with the new one, without changing the interface. (If we decide to, we can still deprecate and remove the old syntax.)
Also it does not require a lot of work, because basically we let Python do the scoping.
(I think global assumptions are completely broken by design, they work only in interactive sessions, not in a library, so they should be removed.)
The `x.is_assumption` syntax would be equivalent to `ask(x, Q.assumption)` and could be kept. The same applies for `Symbol('x', assumption=True)`.

*Ondrej:*
Even though the hack is simple, it is still a hack, so my gut
feeling is telling me, that this will bite us quite substantially in
the future. (E.g. if you want to rewrite the core in C/C++, will this
design still work?)

*Tom:*
I think this should not be a problem, if it is made clear that "core library" code should not use the positive=True etc syntax, just like it should not use var.

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
