## Preamble

While beginning to work with the codebase I have stumbled a couple of
times over the aforementioned problem. A situation occured in bug
1321; also bug 360 is directly related. The "official" ticket is 2200.
You can find there also a link to previous discussion, though under a
non-ideal heading. 

## Epistemology

There are three kinds of
objects involved: expressions, "limit directions" and "limit result
descriptions".

Expressions are the things we want to take limits of, like cos(x), 1/
x^2, exp(z), ...

Limit directions describe how the limit is to be taken.
In R (reals), this generally is a point and a side of approach, or +oo
or -oo.
In general topological spaces limit directions can be described by
filters.

Other common filters are: a point of C (complex plane), approached
from all sides. This is the definition of limit of normed spaces and
hence generalises. Also ComplexInfinity is a well-defined limit
direction.

Limit result descriptions are the answers of limits.
These can be very complicated, if a lot of information is to be
conveyed. For example:

* limits can exist as ordinary numbers, this is the base case
(limit(sin(x), x, 0) == 0 for example)
* limits taken in R can be +oo or -oo in a well-defined sense, e.g.
limit(x**2, x, oo)
* limits such as limit(sin(x), x, oo) have to be described in a more
complicated way. The result could say "point of accumulation for any x
in [-1, 1]".
* limits of meromorphic functions in C can be classified as a number,
a pole of order n (for some n > 0), or essential singularity
* in general, not much can be said. Even a rational function of two
variables can have limits that cannot usefully be interpreted as a
number or infinity.

## Discussion

Much confusion arises, I think, because objects of the three different
classes are often described by the same names:

* a number can be seen as an expression and as a limit description,
and also as a limit direction at least two different ways (over C and
over R)
* oo can be seen as both a singularity description and as a limit
direction
* ditto for zoo

Moreover +-oo can be seen as two points of an extended real line
(topologically its end-compactification). Similarly zoo can be seen as
a point on the riemann sphere.

Finally, we typically want to be able to do at least some arithmetic
with infinities, to write things such as oo+1 == oo. SympyCore calls
this extended number system.

## Operations with filters
We have (in principle) the following operations, for
f(z), g(z, y) any functions of complex variables, F, G any filters

* limit(f, F).
* f(F) =: filter generated by {f(U) | U \in F}
* g(F, G)  =: filter generated by {f(U, V) | (U, V) \in FxG}

The latter two allow many "arithmetic" operations to be performed on filters, and the result are often of the expected form.

## Limit directions as filters

So we have the following commonly used filters (I find it easier to
think in terms of filter bases):

for x in R:

    RB(x) = {filter generated by [x, x+1/n) for n in N}
    LB(x) = {filter generated by (x-1/n, x] for n in N}
    B(x)  = LB(x) + RB(x) = {filter generated by (x-1/n, x+1/n)}

For z in C:
    CB(z) = {filter generated by {y in C: |z-y| < 1/n}, n in N}
    P(z) = {filter generated by {z}} = {all subsets of C containing z}.

    oo = {filter generated by (x, oo) for x > 0}
    -oo = -1 * oo = {filter generated by (-oo, x) for x < 0}

    zoo = {filter generated by {y in C: |y| > n}, n in N}

## Why filters are not limit result descriptions
limit(f, F) does not return a filter: it usually returns a number. Indeed limit(f, F) = c iff for all U in CB(c), there exists V in f(F) with U \subset V.

Hence it would be desirable to find an equivalence relation on the set of all filters, such that

* Distinct principal ultrafilters are not equivalent.
* All filters converging to the same point are equivalent.
* A non-convergent filter is not equivaelent to a convergent filter.
* The equivalence class of f(F) can be computed in many interesting cases.
* Arithmetic on filters (as defined above) descends in a useful way to the equivalence classes.

Please do tell if you know such an equivalence relation :-).