<pre>
 In [1]: %time a = pi.evalf(10**6)
 CPU times: user 7.44 s, sys: 0.06 s, total: 7.50 s
 Wall time: 7.51 s

 In [2]: len(str(a))
 Out[2]: 1000001
</pre>

In SymPy 0.6.0 you would use:

<pre>
 In [1]: from sympy.mpmath import mpf, mp, pi

 In [2]: mp.dps = 10**6

 In [3]: %time a = mpf(pi)
 CPU times: user 7.48 s, sys: 0.05 s, total: 7.53 s
 Wall time: 7.54 s

 In [4]: len(str(a))
 Out[4]: 1000001
</pre>

You need to have gmpy installed for this to work. Otherwise mpmath will use python integers instead and it will take much, much longer.

First 50 digits:

<pre>
 In [5]: str(a)[:50]
 Out[5]: 3.141592653589793238462643383279502884197169399375
</pre>

Last 50 digits:

<pre>
 In [6]: str(a)[-50:]
 Out[6]: 95678796130331164628399634646042209010610577945815
</pre>
