# Integration

<pre>
In [1]: integrate(sin(x)*exp(x), x)
In [2]: integrate(sin(x)*exp(2*x), x)
In [3]: integrate(1/(x**2+1), x)
In [4]: integrate(1/(x**4+1), x)
...
>>> integrate(x/(x**2+1), x)
>>> integrate(x/(x**2+1), x).diff(x)
>>> simplify(integrate(x/(x**2+1), x).diff(x))


In [1]: integrate(LambertW(x), x)
In [2]: _.diff(x)
In [3]: trim(_)
In [4]: var('a b')
In [5]: integrate(a*LambertW(b*x), x)
In [6]: _.diff(x)
In [7]: trim(_)
In [8]: integrate(sin(2*sqrt(x)), x)
In [9]: f = (x-tan(x))/tan(x)**2 + tan(x)
In [10]: integrate(f, x)
</pre>



Linear Solving

<pre>
In [11]: var('a b c d e f g h i')
In [12]: f_1 = a*x + b*y + c*z - 1
In [13]: f_2 = d*x + e*y + f*z - 1
In [14]: f_3 = g*x + h*y + i*z - 1
In [15]: s = solve([f_1, f_2, f_3], x, y, z)
In [16]: s
In [17]: f_1.subs(s)
In [18]: simplify(f_1.subs(s))
In [19]: simplify(f_2.subs(s))
In [20]: simplify(f_3.subs(s))
</pre>

Nonlinear Solving

<pre>
In [21]: f_1 = x**2 + y + z - 1
In [22]: f_2 = x + y**2 + z - 1
In [23]: f_3 = x + y + z**2 - 1
In [24]: solve([f_1, f_2, f_3], x, y, z)
</pre>

Factorization

<pre>
In [1]: factor(x**56-1, x)
In [2]: f = x**16+4*x**15+14*x**14+32*x**13+47*x**12+92*x**11+66*x**10+120*x**9 \
	-50*x**8-24*x**7-132*x**6-40*x**5-52*x**4-64*x**3-64*x**2-32*x+16
 
In [3]: f
In [4]: factor(f, x)
</pre>

Term Rewriting

<pre>
In [29]: 36/(x**5-2*x**4-2*x**3+4*x**2+x-2)
In [30]: f = apart(36/(x**5-2*x**4-2*x**3+4*x**2+x-2), x)
In [31]: f
In [32]: f = apart(36/(x**5-2*x**4-2*x**3+4*x**2+x-2), x, evaluate=False)
In [33]: f
In [34]: Add(*[ g.doit() for g in f.args ])
</pre>

Matrices

<pre>
In [1]: M = Matrix(4, 4, lambda i,j: i*j+1)
In [2]: M.eigenvals()

In [3]: M = Matrix(4, 4, lambda i,j: i*j+2)
In [4]: M.eigenvals()

In [5]: M = Matrix(4, 4, lambda i,j: i*j+3)
In [6]: M.eigenvals()
In [7]: M

In [35]: M = Matrix(4, 4, lambda i,j: i*j+x)
In [36]: M
In [37]: M.eigenvals()
</pre>

General relativity example

<pre>
$ examples/advanced/relativity.py
</pre>

Integrals table

<pre>
from sympy import *
 
def derivative_table(functions, x):
    for f in functions:
        s = printing.latex(Eq(Derivative(f, x), diff(f, x)))
        print ":<math>" + s[1:-1] + "</math>", "\n"
 
def integral_table(functions, x):
    for f in functions:
        s = printing.latex(Eq(Integral(f, x), integrate(f, x)))
        print ":<math>" + s[1:-1] + "</math>", "\n"
 
var('x')
 
print "===Derivatives==="
derivative_table([cos(x)/(1 + sin(x)**i) for i in range(1, 5)], x)
 
print "===Integrals==="
integral_table([x**i * exp(i*x) for i in range(1, 5)], x)
</pre>


Million digits of pi

<pre>
In [1]: %time a = pi.evalf(10**6)
CPU times: user 7.44 s, sys: 0.06 s, total: 7.50 s
Wall time: 7.51 s
 
In [2]: len(str(a))
Out[2]: 1000001

In [5]: str(a)[:50]
Out[5]: 3.141592653589793238462643383279502884197169399375

In [6]: str(a)[-50:]
Out[6]: 95678796130331164628399634646042209010610577945815
</pre>


Numerical Integration

One-liner:

<pre>
In [1]: Integral(sin(1/x), (x, 0, 1)).transform(x, 1/x).evalf(quad="osc")
Out[1]: 0.504067061906928
</pre>

Detailed steps:

<pre>
In [1]: e = Integral(sin(1/x), (x, 0, 1))
In [2]: e
In [3]: e.transform(x, 1/x)
In [4]: e.transform(x, 1/x).evalf(quad="osc")
In [5]: e.transform(x, 1/x).evalf(40, quad="osc")
</pre>

Numerical Summation 

quickly convergent series:

<pre>
>>> Sum((2*n**3+1)/factorial(2*n+1), (n, 0, oo)).evalf(1000)
</pre>

slowly convergent (polynomial rate) series:

<pre>
>>> Sum(n/(n**3+9), (n, 1, oo)).evalf(1000)
</pre>


Numerical Simplification

<pre>
In [4]: float(1/7)
In [5]: nsimplify(_)
In [6]: float(1/81)
In [7]: nsimplify(_)
>>> nsimplify(pi, tolerance=0.01)
>>> nsimplify(pi, tolerance=0.001)
>>> nsimplify(0.33333, tolerance=1e-4)
>>> nsimplify(4.71, [pi], tolerance=0.01)
>>> nsimplify(2.0**(1/3.), tolerance=0.001)
>>> nsimplify(2.0**(1/3.), tolerance=0.001, full=True)
>>> nsimplify(4/(1+sqrt(5)), [GoldenRatio])
>>> nsimplify(2 + exp(2*atan('1/4')*I))
>>> nsimplify((1/(exp(3*pi*I/5)+1)))
>>> nsimplify(I**I, [pi])
>>> nsimplify(Sum(1/n**2, (n, 1, oo)), [pi])
>>> nsimplify(gamma('1/4')*gamma('3/4'), [pi])
</pre>


Ordinary differential equations

<pre>
In [1]: f = Function("f")
In [2]: Eq(f(x).diff(x, x) + 9*f(x) + 1, 1)
In [3]: dsolve(_, f(x))

In [11]: Eq(f(x).diff(x, x) + 8*f(x) + 1, 1)
In [12]: dsolve(_, f(x))
</pre>


Limits

<pre>
$ vim sympy/series/tests/test_demidovich.py
</pre>


Plotting:

<pre>
>>> Plot(x**2)
>>> Plot(x**2*y)
>>> Plot(x*y**3-y*x**3)
>>> Plot( cos(x)*sin(y), sin(x)*sin(y), cos(y)+log(tan(y/2))+0.2*x, [x, -0.00,
12.4, 40], [y, 0.1, 2, 40])
</pre>
[[Category:Documentation]]
