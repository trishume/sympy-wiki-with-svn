Blabla.

# Definitions

A **formal power series** is an object of the form \(S = \sum_{n=0}^{+\infty} a_n X^n\) where \(X\) is a formal parameter. The set of formal power series over a field \(K\) is noted \(K[[X]]\) and has a ring structure.

A **generalized formal power series**, or **formal Laurent series**, in an object \(S\) such that \(X^n S\) is a formal power series for some integer \(n\). The set of formal Laurent series over a field \(K\) is noted \(K((X))\) and has a field structure.

The **Taylor series** at \(x_0\) of a smooth function \(f\) is the formal power series \(TS_{x_0}(f) = \sum_{n = 0}^\infty \frac{f^{(n)}(x_0)}{n!} X^n\). \(f\) is analytic iff there exists a neighbourhood \(V\) of \(x_0\) where \(f(x) = S(x-x_0), x \in V, S = TS_{x_0}(f)\).

f is **dominated** by g at \(x_0\), written \(f = O_{x_0}(g)\), iff \(f/g\) is bounded at \(x_0\). Similarly, \(f(x) = O_{x \rightarrow x_0}(g(x))\) iff \(f = O_{x_0}(g)\), i.e. iff \(f(x)/g(x)\) is bounded for \(x\) going to \(x_0\). Note that \(\cdot = O_\cdot(\cdot)\) is a purely notational device here, not an equality.

The set of functions dominated by a function \(g\) at \(x_0\), \(O_{x_0}(g)\) is defined by \(f \in O_{x_0}(g)\) iff \(f = O_{x_0}(g)\). \(h + O(g)\) is a set of functions defined in the usual way: \(h + O(g) = \{h+\alpha ; \alpha \in O(g)\}\). It is called an **asymptotic expansion** of f iff \(f \in h + O(g)\).

The n-th order **Taylor polynomial** of f at \(x_0\) is the degree-n polynomial \(TP_{n, x_0}(f) = \sum_{n = 0}^n \frac{f^{(k)}(x_0)}{k!} X^k\). If f is analytic, \(TP_{n, x_0}(f)\) is the degree-n truncation of \(TS_{x_0}(f)\). The n-th order **Taylor expansion** of f at \(x_0\) is \(TP_{n, x_0}(f)(x-x_0) + O_{x \rightarrow x_0}((x-x_0)^{n+1})\)

# Current situation

According to its docstring, ``f(x).series(x, x0, n)`` is supposed to return the (n-1)th order generalized Taylor expansion of f(x) for x -> x0.
Actually, it works only for x0 = 0 and when f doesn't have a generalized Taylor expansion, it returns some arbitrarily chosen asymptotic expansion of f(x).