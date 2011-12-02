

This page is obsolete and not accurate anymore. We do patch reviews now and all code that goes in needs to be reviewed by at least one other developer and it needs to be maintainable. That's how we work now.


Below is some old info:

# Introduction

This page contains arguments for and against some decisions made in sympy.

The driving idea is this: *Don't think about the design decisions too much. Write a testcase for every functionality we want from sympy. We don't care how the functionality is achieved as far as it works.*

Write tests, so that they are written from the users point of view. i.e.,
write them, as we would like to use the library. Particularly, tests should
be independent on the way we print results using str(), because this can be
changed (check this only in 1 test regarding str()). They should also be
independent on when we call eval(). The user just wants sympy to work, he's
not interested in such a low level stuff.


# eval()

We used to call .eval() manually, but we switched to an automatic evaluation implemented using a metaclass, see the Documentation. This is much more elegant, it cleaned the source  code of the whole SymPy, so now not only the user doesn't need to know about the eval() at all, but even the developers don't have to think about it most of the time.

What about exp(a+b) and `ln(a*b)`? Right now, we are doing `ln(a*b)` in eval(), but sometimes, we *don't* want to expand `exp(a+b)` - e.g. in limits.py. maybe move to `expand()`? Look at mathematica,
maple, what they are doing. the same in series expansion. needs to be
specified. I am rather skeptical, I don't want eval() to do any magic.
my conclusion now i that `ln(a*b)` and exp(a+b) should be rewritten on
expand(), but not on eval().

# Series

need to create a special class for series (probably a child of mul, which
would only accept polynoms of one variable), which would implement
multiplication, adding etc. copy from ginac. can neglect higher terms, so
it should be pretty fast. otherwise it's going to be slow.
but try first without it, if it works.

It seems to work somehow. Let's forget about it now. Let's thing it through when we really need it.


# Caching

objects could remember a pointer to evaluated self. so that next time they
just return the pointer. maybe also there could be a huge database (dict) of
hashes and evaluated objs. (memory intensive probably)

The same with some methods in `limits.py` - they should cache results.

# New features

  * factorisation
  * integration according to issac98.pdf
  * symbolic matrices (linear algebra)
  * asymptotic expansion
  * equations solving
  * objects with indices (tensors)
  * noncommutative objects
  * complex numbers


# References

See the issue tracker, where most of the discussions take part.

http://www.inf.ethz.ch/personal/gonnet/CAII/HeuristicAlgorithms/

http://www.ucw.cz/~fox/work/factoring/index.en.html

http://www.amazon.com/Fundamental-Problems-Algorithmic-Algebra-Chee/dp/0195125169/ref=sr_1_1/002-4937825-8471200?ie=UTF8&s=books&qid=1174572166&sr=8-1