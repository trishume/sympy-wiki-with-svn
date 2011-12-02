


# All tests pass - ok to commit

```
$ ./setup.py test
running test
============================= test process starts ==============================
executable:   /usr/bin/python  (2.4.4-final-0)
using py lib: /usr/lib/python2.4/site-packages/py <rev unknown>

sympy/concrete/tests/test_gosper.py[2] ..
sympy/concrete/tests/test_products.py[3] ...
sympy/concrete/tests/test_sums_products.py[9] ......fff
sympy/core/tests/test_arit.py[35] .................................ff
sympy/core/tests/test_assumptions.py[18] ................ff
sympy/core/tests/test_basic.py[21] .....................
sympy/core/tests/test_complex.py[10] ..........
sympy/core/tests/test_count_ops.py[1] .
sympy/core/tests/test_diff.py[3] ...
sympy/core/tests/test_equal.py[4] ....
sympy/core/tests/test_eval.py[8] .......f
sympy/core/tests/test_eval_power.py[6] ......
sympy/core/tests/test_functions.py[20] ................fff.
sympy/core/tests/test_match.py[24] .......................f
sympy/core/tests/test_numbers.py[20] ....................
sympy/core/tests/test_str.py[8] ........
sympy/core/tests/test_subs.py[11] ...........
sympy/core/tests/test_symbol.py[3] ...
sympy/core/tests/test_sympify.py[12] ............
sympy/core/tests/test_truediv.py[3] ...
sympy/core/tests/test_var.py[2] ..
sympy/functions/combinatorial/tests/test_factorials.py[4] ....
sympy/functions/combinatorial/tests/test_numbers.py[20] ....................
sympy/functions/elementary/tests/test_complexes.py[5] .....
sympy/functions/elementary/tests/test_exponential.py[5] ...ff
sympy/functions/elementary/tests/test_hyperbolic.py[5] .....
sympy/functions/elementary/tests/test_integers.py[2] ..
sympy/functions/elementary/tests/test_interface.py[3] ...
sympy/functions/elementary/tests/test_trigonometric.py[10] ..........
sympy/functions/special/tests/test_error_functions.py[3] ...
sympy/functions/special/tests/test_gamma_functions.py[6] ......
sympy/functions/special/tests/test_polynomials.py[4] ....
sympy/functions/special/tests/test_spherical_harmonics.py[5] .....
sympy/functions/special/tests/test_zeta_functions.py[2] ..
sympy/geometry/tests/test_geometry.py[6] ......
sympy/integrals/tests/test_integrals.py[19] .................ff
sympy/integrals/tests/test_risch.py[17] .............ssss
sympy/integrals/tests/test_trigonometry.py[2] ..
sympy/matrices/tests/test_matrices.py[26] ..........................
sympy/ntheory/tests/test_ntheory.py[9] .........
sympy/numerics/tests/test_constants.py[2] ..
sympy/numerics/tests/test_evalf_.py[2] .f
sympy/numerics/tests/test_float_.py[15] ...........ffff
sympy/numerics/tests/test_functions.py[20] ................fff.
sympy/numerics/tests/test_functions2.py[3] ...
sympy/numerics/tests/test_numerics.py[1] .
sympy/numerics/tests/test_optimize.py[3] ..f
sympy/numerics/tests/test_quad.py[3] ...
sympy/parsing/tests/test_mathematica.py[1] .
sympy/parsing/tests/test_maxima.py[3] ...
sympy/physics/tests/test_matrices.py[26] ..........................
sympy/physics/tests/test_paulialgebra.py[1] .
sympy/physics/tests/test_units.py[1] .
sympy/plotting/tests/test_plotting.py[10] ..........
sympy/polynomials/tests/test_polynomials.py[4] ....
sympy/polynomials/tests/test_polynomials_fast.py[3] ...
sympy/printing/tests/test_gtk.py[1] X
sympy/printing/tests/test_latex.py[8] .......f
sympy/printing/tests/test_mathml.py[6] .....f
sympy/printing/tests/test_pretty.py[10] .........f
sympy/printing/tests/test_pretty_unicode.py[9] .........
sympy/printing/tests/test_python.py[6] ......
sympy/series/tests/test_demidovich.py[14] .........fffff
sympy/series/tests/test_limit.py[20] ...................f
sympy/series/tests/test_limit_series.py[39] .......................................
sympy/series/tests/test_order.py[20] ..................ff
sympy/series/tests/test_oseries.py[10] ..........
sympy/series/tests/test_series.py[38] ..........................XfffffffffXf
sympy/simplify/tests/test_rewrite.py[6] .....f
sympy/simplify/tests/test_rootof.py[1] .
sympy/simplify/tests/test_simplify.py[15] ..........fffff
sympy/simplify/tests/test_sqrtdenest.py[2] ..
sympy/solvers/tests/test_ode.py[7] .......
sympy/solvers/tests/test_recurr.py[3] ...
sympy/solvers/tests/test_solvers.py[6] ......
sympy/specfun/tests/test_factorials.py[4] ....
sympy/statistics/tests/test_statistics.py[3] ...
sympy/test_external/test_numpy.py[11] ...........
sympy/utilities/tests/test_lambdify.py[9] .........


__________________________ reasons for skipped tests ___________________________
Skipped in /home/ondra/sympy/sympy/integrals/tests/test_risch.py:158
Skipped in /home/ondra/sympy/sympy/integrals/tests/test_risch.py:131
Skipped in /home/ondra/sympy/sympy/integrals/tests/test_risch.py:149
Skipped in /home/ondra/sympy/sympy/integrals/tests/test_risch.py:140
reason: Skipped: takes too much time


________________________________ *** XPASS *** _________________________________
XPASS: test_bug2

XPASS: test1

XPASS: test_issue364

== tests finished: 663 passed, 3 xpass, 52 xfail, 4 skipped in 97.97 seconds ===
```

Explanation:
 
 * "f" ... the test was XFAILed and failed
 * "X" ... the test was XFAILed and passed
 * "F" ... the test failed

Both "f" and "X" are fine (ok to commit), "F" is bad (do not commit). The "f" and "X" are generated using the @XFAIL decorator, that means that the test is ok to both pass or fail,
we use it when we know some test sometimes fail (instead of commenting out the test completely).

# Failing tests

This is how it looks like when some tests fail.

```
ondra@dakol:~/sympy$ python setup.py test
running test
============================= test process starts ==============================
testing-mode: inprocess
executable:   /usr/bin/python  (2.4.4-final-0)
using py lib: /home/ondra/py-dist/py <rev 25083>

tests/test_arit.py[8] ........
tests/test_basic.py[6] ......
tests/test_complex.py[4] .F..
tests/test_demidovich.py[2] ..
tests/test_diff.py[2] ..
tests/test_equal.py[2] ..
tests/test_eval.py[3] ...
tests/test_evalf.py[3] ...
tests/test_functions.py[13] .............
tests/test_hashing.py[9] .........
tests/test_integrals.py[4] ....
tests/test_limits.py[16] ................
tests/test_match.py[7] .......
tests/test_mathml.py[2] F.
tests/test_matrices.py[5] .....
tests/test_numbers.py[13] ........F....
tests/test_paulialgebra.py[1] .
tests/test_polynomials.py[8] ........
tests/test_series.py[11] ...........
tests/test_solvers.py[4] ....
tests/test_str.py[7] .......
tests/test_subs.py[5] .....
tests/test_symbol.py[1] .
tests/test_trigonometric.py[2] ..

________________________________________________________________________________
____________________________ entrypoint: test_abs1 _____________________________
    def test_abs1():
        a=Symbol("a", is_real=True)
        b=Symbol("b", is_real=True)
        assert abs(a) == a
        assert abs(-a) == a
        assert abs(-a) != -a
E       assert abs(a+I*b) == (a*a+b*b).sqrt()
>       assert abs(b*I+a) == (a**2+b**2)**(1/2)
         +  where abs(b*I+a) = abs((a + (I * b)))
         +  and   (a**2+b**2)**(1/2) = ((a * a) + (b * b)).sqrt()

[/home/ondra/sympy/tests/test_complex.py:24]
________________________________________________________________________________
__________________________ entrypoint: test_mathml_1 ___________________________
    def test_mathml_1():
        assert f.mathml == '<apply><int/><bvar><ci> x </ci></bvar><lowlimit><cn> 1 </cn></lowlimit><uplimit><cn> 2 </cn></uplimit><apply><log/> <ci> x </ci> </apply></apply>'
E       assert (x**2 + x +1/x).mathml == '<apply><plus/><apply><power/><ci> x </ci><cn> 2 </cn></apply><apply><power/><ci> x </ci><cn> -1 </cn></apply><ci> x </ci></apply>'
>       assert (((x ** 2) + x) + (1 / x)).mathml == '<apply><plus/><apply><power/><ci> x </ci><cn> 2 </cn></apply><apply><power/><ci> x </ci><cn> -1 </cn></apply><ci> x </ci></apply>'

[/home/ondra/sympy/tests/test_mathml.py:12]
________________________________________________________________________________
____________________________ entrypoint: test_abs1 _____________________________
    def test_abs1():
        a=Symbol("a", is_real=True)
        b=Symbol("b", is_real=True)
        assert abs(a) == a
        assert abs(-a) == a
        assert abs(-a) != -a
E       assert abs(a+g.I*b) == (a*a+b*b).sqrt()
>       assert abs(b*I+a) == (a**2+b**2)**(1/2)
         +  where abs(b*I+a) = abs((a + (I * b)))
         +    where I = g.I
         +  and   (a**2+b**2)**(1/2) = ((a * a) + (b * b)).sqrt()

[/home/ondra/sympy/tests/test_numbers.py:108]
============ tests finished: 135 passed, 3 failed in 11.39 seconds =============
ondra@dakol:~/sympy$

```