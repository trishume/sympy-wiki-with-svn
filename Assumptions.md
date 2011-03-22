## Introduction
The assumptions in SymPy need to be rewritten. This page is dedicated to discussing the best way to go about this.

## Approaches
Here we discuss the merits of each approach to replacing the old assumption system.

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
