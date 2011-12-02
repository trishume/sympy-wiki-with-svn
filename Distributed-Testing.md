

# Introduction

Create a file `conftest.py` in the sympy root directory:
```
dist_hosts = [
        "localhost",
        "localhost",
        "localhost",
        "pc232",
        "pc232",
        ]
```
with addresses of computers you would like to use for testing. You don't need to install anything on them (except python). Now run:
```
py.test -d
```
That's it. 

# Result

And the result will look like this for a successful run:
```
ondra@fuji:~/sympy$ py.test -d
  Test started, hosts: localhost[0], localhost[1], localhost[2], pc232[0], pc232[1]  
local top directory: /home/ondra/sympy
local RSync root [1/1]: /home/ondra/sympy
   localhost[0]: gateway initialised (remote topdir: None)
   localhost[1]: gateway initialised (remote topdir: None)
   localhost[2]: gateway initialised (remote topdir: None)
       pc232[0]: gateway initialised (remote topdir: /home/ondra/pytestcache-pc232/sympy)
       pc232[1]: gateway initialised (remote topdir: /home/ondra/pytestcache-pc232/sympy)
   localhost[0]: skipping inplace rsync of '/home/ondra/sympy'
   localhost[0]: READY (still 4 to go)
   localhost[1]: skipping inplace rsync of '/home/ondra/sympy'
   localhost[1]: READY (still 3 to go)
   localhost[2]: skipping inplace rsync of '/home/ondra/sympy'
   localhost[2]: READY (still 2 to go)
       pc232[0]: rsync 'sympy' to remote '/home/ondra/pytestcache-pc232/sympy'
       pc232[1]: skip duplicate rsync to '/home/ondra/pytestcache-pc232/sympy'
       pc232[1]: READY (still 1 to go)
       pc232[0]: READY
   localhost[1]: PASSED  sympy.core.tests.test_arit.py testdiv
   localhost[0]: PASSED  sympy.core.tests.test_arit.py test_Symbol
   localhost[0]: PASSED  sympy.core.tests.test_arit.py test_ncpow
   localhost[0]: PASSED  sympy.core.tests.test_arit.py test_Pow_is_negative_positive
   localhost[1]: PASSED  sympy.core.tests.test_arit.py test_powerbug
   localhost[1]: PASSED  ...e.tests.test_arit.py test_Pow_is_nonpositive_nonnegative
   localhost[0]: PASSED  sympy.core.tests.test_assumptions.py test_negativeone
   localhost[1]: PASSED  sympy.core.tests.test_assumptions.py test_pos_rational
       pc232[0]: PASSED  sympy.core.tests.test_arit.py test_power_expand
       pc232[1]: PASSED  sympy.core.tests.test_arit.py test_ncmul
   localhost[2]: PASSED  sympy.core.tests.test_arit.py test_expand
   localhost[1]: PASSED  sympy.core.tests.test_assumptions.py test_symbol_positive
   localhost[2]: PASSED  sympy.core.tests.test_arit.py test_Add_Mul_is_integer
       pc232[0]: PASSED  sympy.core.tests.test_arit.py test_Mul_is_even_odd
   localhost[0]: PASSED  sympy.core.tests.test_assumptions.py test_I
   localhost[2]: PASSED  sympy.core.tests.test_assumptions.py test_symbol_unset
   localhost[2]: PASSED  sympy.core.tests.test_assumptions.py test_neg_rational
       pc232[0]: PASSED  sympy.core.tests.test_assumptions.py test_zero
   localhost[2]: PASSED  ....core.tests.test_assumptions.py test_neg_symbol_positive
       pc232[1]: PASSED  sympy.core.tests.test_arit.py test_Add_is_even_odd
       pc232[1]: PASSED  sympy.core.tests.test_assumptions.py test_one
       pc232[1]: PASSED  sympy.core.tests.test_assumptions.py test_E
       pc232[1]: PASSED  ...re.tests.test_assumptions.py test_neg_symbol_nonpositive
       pc232[0]: PASSED  sympy.core.tests.test_assumptions.py test_pi
       pc232[0]: PASSED  sympy.core.tests.test_assumptions.py test_symbol_nonpositive
   localhost[1]: PASSED  sympy.core.tests.test_basic.py test_ibasic
       pc232[1]: PASSED  sympy.core.tests.test_basic.py test_atoms
   localhost[1]: PASSED  sympy.core.tests.test_complex.py test_complex
   localhost[2]: PASSED  sympy.core.tests.test_basic.py test_ldegree
       pc232[1]: PASSED  sympy.core.tests.test_complex.py    localhost[2]: PASSED  sympy.core.tests.test_complex.py test_abs1
test_pythoncomplex
       pc232[1]: PASSED  sympy.core.tests.test_eval.py test_add_eval
       pc232[0]: PASSED  sympy.core.tests.test_basic.py test_leadterm
       pc232[0]: PASSED  sympy.core.tests.test_complex.py test_abs2
       pc232[0]: PASSED  sympy.core.tests.test_equal.py test_expevalbug
   localhost[1]: PASSED  sympy.core.tests.test_diff.py testdiff2
   localhost[1]: PASSED  sympy.core.tests.test_eval.py test_pow_eval
   localhost[2]: PASSED  sympy.core.tests.test_equal.py testequal
   localhost[2]: PASSED  sympy.core.tests.test_eval.py test_mulpow_eval
       pc232[1]: PASSED  sympy.core.tests.test_eval.py test_expbug
       pc232[0]: PASSED  sympy.core.tests.test_eval.py test_evalpow_bug
   localhost[1]: PASSED  sympy.core.tests.test_eval_power.py test_rational
       pc232[0]: PASSED  sympy.core.tests.test_evalf.py test_bug2
   localhost[2]: PASSED  sympy.core.tests.test_evalf.py test_bug1
       pc232[1]: PASSED  sympy.core.tests.test_functions.py test_func
   localhost[1]: PASSED  sympy.core.tests.test_functions.py test_exp_log
       pc232[0]: PASSED  sympy.core.tests.test_functions.py test_sign
       pc232[1]: PASSED  sympy.core.tests.test_functions.py test_exp_bug
   localhost[2]: PASSED  sympy.core.tests.test_functions.py test_log_hashing_bug
       pc232[1]: PASSED  sympy.core.tests.test_match.py test_interface
       pc232[0]: PASSED  sympy.core.tests.test_match.py test_complex
   localhost[2]: PASSED  sympy.core.tests.test_match.py test_add
   localhost[1]: PASSED  sympy.core.tests.test_match.py test_symbol
   localhost[2]: PASSED  sympy.core.tests.test_match.py test_bug2
       pc232[0]: PASSED  sympy.core.tests.test_numbers.py test_Rational
   localhost[2]: PASSED  sympy.core.tests.test_numbers.py test_Infinity
   localhost[1]: PASSED  sympy.core.tests.test_match.py test_behavior2
   localhost[0]: PASSED  sympy.core.tests.test_basic.py test_basic
   localhost[0]: PASSED  sympy.core.tests.test_basic.py test_is_polynomial
       pc232[0]: PASSED  sympy.core.tests.test_numbers.py test_powers
   localhost[1]: PASSED  sympy.core.tests.test_numbers.py test_Real_eval
       pc232[1]: PASSED  sympy.core.tests.test_numbers.py test_Rational_cmp
       pc232[1]: PASSED  sympy.core.tests.test_numbers.py test_abs1
   localhost[2]: PASSED  sympy.core.tests.test_numbers.py test_int
   localhost[0]: PASSED  sympy.core.tests.test_diff.py testdiff
   localhost[0]: PASSED  sympy.core.tests.test_eval.py test_addmul_eval
   localhost[1]: PASSED  sympy.core.tests.test_numbers.py test_accept_str
       pc232[1]: PASSED  sympy.core.tests.test_numbers.py test_bug_sqrt
   localhost[0]: PASSED  sympy.core.tests.test_eval.py test_symbol_expand
       pc232[0]: PASSED  sympy.core.tests.test_numbers.py test_real_bug
       pc232[1]: PASSED  sympy.core.tests.test_str.py test_bug3
       pc232[0]: PASSED  sympy.core.tests.test_str.py test_bug2
       pc232[1]: PASSED  sympy.core.tests.test_subs.py test_bug
   localhost[1]: PASSED  sympy.core.tests.test_str.py test_poly_str
       pc232[0]: PASSED  sympy.core.tests.test_subs.py test_logexppow
   localhost[2]: PASSED  sympy.core.tests.test_str.py test_bug1
   localhost[1]: PASSED  sympy.core.tests.test_str.py test_x_div_y
   localhost[2]: PASSED  sympy.core.tests.test_subs.py test_subs
   localhost[0]: PASSED  sympy.core.tests.test_functions.py test_log
   localhost[2]: PASSED  sympy.core.tests.test_symbol.py test_Symbol
       pc232[0]: PASSED  sympy.core.tests.test_symbol.py test_lt_gt
   localhost[0]: PASSED  sympy.core.tests.test_functions.py test_Derivative
   localhost[1]: PASSED  sympy.core.tests.test_subs.py test_dict
   localhost[0]: PASSED  sympy.core.tests.test_match.py test_behavior1
       pc232[0]: PASSED  sympy.modules.geometry.tests.test_geometry.py test_util
       pc232[1]: PASSED  sympy.modules.geometry.tests.test_geometry.py test_point
       pc232[1]: PASSED  ...dules.integrals.tests.test_integrals.py test_integration
       pc232[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_creation
       pc232[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_applyfunc
       pc232[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_util
       pc232[1]: PASSED  ...dules.matrices.tests.test_matrices.py test_sparse_matrix
   localhost[1]: PASSED  sympy.modules.geometry.tests.test_geometry.py test_ellipse
   localhost[1]: PASSED  ...integrals.tests.test_integrals.py test_integration_table
   localhost[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_submatrix
   localhost[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_LUdecomp
   localhost[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_QR
   localhost[0]: PASSED  sympy.core.tests.test_numbers.py test_Real
   localhost[0]: PASSED  sympy.core.tests.test_numbers.py test_accept_int
   localhost[0]: PASSED  sympy.core.tests.test_str.py test_pow
   localhost[0]: PASSED  sympy.core.tests.test_str.py test_bug4
       pc232[0]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_power
       pc232[0]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_reshape
       pc232[0]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_inverse
       pc232[0]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_eigen
   localhost[0]: PASSED  sympy.core.tests.test_subs.py test_subbug1
       pc232[0]: PASSED  ...ting.tests.test_plotting.py.TestPlotting.() test_plot_3d
       pc232[1]: PASSED  ...t_plotting.py.TestPlotting.() test_plot_3d_discontinuous
   localhost[2]: PASSED  sympy.modules.geometry.tests.test_geometry.py test_polygon
   localhost[2]: PASSED  ...ules.matrices.tests.test_matrices.py test_multiplication
   localhost[2]: PASSED  ...atrices.tests.test_matrices.py test_submatrix_assignment
   localhost[2]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_LUsolve
   localhost[2]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_nullspace
   localhost[0]: PASSED  sympy.modules.geometry.tests.test_geometry.py test_line
   localhost[0]: PASSED  ...egrals.tests.test_integrals.py test_multiple_integration
   localhost[1]: PASSED  ...ting.tests.test_plotting.py.TestPlotting.() test_plot_2d
   localhost[0]: PASSED  ...modules.matrices.tests.test_matrices.py test_determinant
   localhost[0]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_random
       pc232[0]: PASSED  ...test_plotting.py.TestPlotting.() test_plot_2d_parametric
   localhost[0]: PASSED  ...es.matrices.tests.test_matrices.py test_jacobian_hessian
       pc232[0]: PASSED  ...modules.polynomials.tests.test_polynomials.py test_coeff
       pc232[0]: PASSED  sympy.modules.polynomials.tests.test_polynomials.py test_lcm
       pc232[0]: PASSED  sympy.modules.polynomials.tests.test_polynomials.py test_sqf
       pc232[0]: PASSED  ...les.series.tests.test_demidovich.py test_Limits_simple_0
       pc232[1]: PASSED  ...test_plotting.py.TestPlotting.() test_plot_3d_parametric
   localhost[2]: PASSED  ...t_plotting.py.TestPlotting.() test_plot_2d_discontinuous
       pc232[1]: PASSED  sympy.modules.polynomials.tests.test_polynomials.py test_div
       pc232[1]: PASSED  ...es.polynomials.tests.test_polynomials.py test_real_roots
       pc232[0]: PASSED  ...les.series.tests.test_demidovich.py test_Limits_simple_4
       pc232[1]: PASSED  ...ules.polynomials.tests.test_polynomials.py test_sqf_part
       pc232[0]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_simple_x
       pc232[0]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_1
       pc232[0]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_5
       pc232[0]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page43_ex3_15
       pc232[0]: PASSED  ...ies.tests.test_limit.py test_MrvTestCase_page60_sec3_5_1
       pc232[0]: PASSED  ....series.tests.test_limit.py test_MrvLimitTestCase_simple
       pc232[0]: PASSED  ...series.tests.test_limit.py test_MrvLimitTestCase_page4_1
       pc232[1]: PASSED  ...les.series.tests.test_demidovich.py test_Limits_simple_1
       pc232[0]: PASSED  ...s.tests.test_limit.py test_MrvLimitTestCase_page13_ex2_7
       pc232[0]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page15_ex2_11
   localhost[1]: PASSED  ...s.test_plotting.py.TestPlotting.() test_plot_3d_cylinder
   localhost[0]: PASSED  ...tting.tests.test_plotting.py.TestPlotting.() test_import
   localhost[1]: PASSED  ...es.polynomials.tests.test_polynomials.py test_Polynomial
       pc232[0]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page51_ex3_25
       pc232[0]: PASSED  ...s.tests.test_limit.py test_MrvLimitTestCase_page77_ex5_2
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_simple_2
   localhost[2]: PASSED  ....test_plotting.py.TestPlotting.() test_plot_3d_spherical
   localhost[1]: PASSED  sympy.modules.polynomials.tests.test_polynomials.py test_gcd
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_simple_3
   localhost[2]: PASSED  ...es.polynomials.tests.test_polynomials.py test_coeff_ring
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_simple_4
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_contains_1
   localhost[1]: PASSED  ...modules.polynomials.tests.test_polynomials.py test_roots
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_contains_3
       pc232[1]: PASSED  sympy.modules.series.tests.test_demidovich.py test_f1
       pc232[1]: PASSED  ....series.tests.test_limit.py test_MrvTestCase_simple_poly
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_multivar_0
   localhost[1]: PASSED  ...modules.polynomials.tests.test_polynomials.py test_sturm
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_multivar_1
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_multivar_2
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_multivar_3
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_w
       pc232[1]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_2
       pc232[1]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_6
       pc232[1]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page44_ex3_17
       pc232[1]: PASSED  ...ies.tests.test_limit.py test_MrvTestCase_page60_sec3_5_2
       pc232[1]: PASSED  ...ies.tests.test_limit.py test_MrvLimitTestCase_simple_inf
       pc232[1]: PASSED  ...series.tests.test_limit.py test_MrvLimitTestCase_page4_2
       pc232[1]: PASSED  ...s.tests.test_limit.py test_MrvLimitTestCase_page14_ex2_9
       pc232[1]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page16_ex2_13
       pc232[1]: PASSED  sympy.modules.series.tests.test_order.py test_simple_5
       pc232[1]: PASSED  sympy.modules.series.tests.test_order.py test_contains_0
       pc232[1]: PASSED  sympy.modules.series.tests.test_order.py test_contains_2
   localhost[2]: PASSED  ...ules.polynomials.tests.test_polynomials.py test_groebner
       pc232[1]: PASSED  sympy.modules.series.tests.test_order.py test_add_1
       pc232[1]: PASSED  sympy.modules.series.tests.test_order.py test_multivar_mul_1
       pc232[0]: PASSED  sympy.modules.series.tests.test_oseries.py test_mul_1
       pc232[1]: PASSED  ...modules.series.tests.test_series.py test_generalexponent
       pc232[0]: PASSED  sympy.modules.series.tests.test_oseries.py test_pow_0
       pc232[1]: PASSED  sympy.modules.series.tests.test_series.py test_order_bug
   localhost[2]: PASSED  ....polynomials.tests.test_polynomials.py test_solve_system
   localhost[0]: PASSED  ...ests.test_plotting.py.TestPlotting.() test_plot_2d_polar
   localhost[1]: PASSED  ...les.series.tests.test_demidovich.py test_Limits_simple_2
   localhost[1]: PASSED  ...ies.tests.test_limit.py test_MrvCompareLeadTerm_simple_1
   localhost[1]: PASSED  ...s.series.tests.test_limit.py test_MrvTestCase_simple_exp
       pc232[0]: PASSED  sympy.modules.series.tests.test_oseries.py test_geometric_1
   localhost[0]: PASSED  ...ng.tests.test_plotting.py.TestPlotting.() test_plot_grid
       pc232[0]: PASSED  sympy.modules.series.tests.test_oseries.py test_sqrt_1
   localhost[1]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page41_ex3_13
   localhost[1]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_8
   localhost[1]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page51_ex3_25
   localhost[1]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page60_sec3_5
   localhost[2]: PASSED  sympy.modules.series.tests.test_demidovich.py test_leadterm
       pc232[1]: PASSED  sympy.modules.series.tests.test_series.py test_sinsinbug
       pc232[1]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_simplify
   localhost[1]: PASSED  ...s.series.tests.test_limit.py test_MrvLimitTestCase_page2
       pc232[1]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_separate
       pc232[1]: PASSED  sympy.modules.solvers.tests.test_solvers.py test_solve
       pc232[1]: PASSED  ...modules.specfun.tests.test_factorials.py test_factorial1
       pc232[1]: PASSED  sympy.modules.specfun.tests.test_factorials.py test_gamma
       pc232[1]: PASSED  sympy.modules.specfun.tests.test_specfun.py test_import
       pc232[0]: PASSED  sympy.modules.series.tests.test_oseries.py test_exp_1
   localhost[0]: PASSED  ...odules.polynomials.tests.test_polynomials.py test_factor
   localhost[2]: PASSED  ...les.series.tests.test_demidovich.py test_Limits_simple_3
   localhost[0]: PASSED  ...les.polynomials.tests.test_polynomials.py test_resultant
   localhost[0]: PASSED  sympy.modules.series.tests.test_demidovich.py test_f2
   localhost[2]: PASSED  ...ies.tests.test_limit.py    localhost[0]: PASSED  ...s.series.tests.test_limit.py test_MrvTestCase_simple_log
test_MrvCompareLeadTerm_simple_2
   localhost[0]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_3
   localhost[0]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_7
   localhost[2]: PASSED  ....series.tests.test_limit.py test_MrvTestCase_simple_exp2
   localhost[0]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page47_ex3_21
   localhost[1]: PASSED  ...s.tests.test_limit.py test_MrvLimitTestCase_page12_ex2_5
   localhost[0]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page43_ex3_15
   localhost[2]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_4
   localhost[1]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page47_ex3_21
   localhost[2]: PASSED  ...s.series.tests.test_limit.py test_MrvLimitTestCase_page4
   localhost[0]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page44_ex3_17
   localhost[1]: PASSED  sympy.modules.series.tests.test_oseries.py test_mul_0
   localhost[0]: PASSED  ...ests.test_limit.py test_MrvLimitTestCase_page47_ex3_21_1
   localhost[0]: PASSED  ...s.series.tests.test_limit.py test_MrvLimitTestCase_bug_0
   localhost[1]: PASSED  sympy.modules.series.tests.test_oseries.py test_pow_1
   localhost[2]: PASSED  ...s.tests.test_limit.py test_MrvLimitTestCase_page12_ex2_6
   localhost[1]: PASSED  sympy.modules.series.tests.test_series.py testseries1
   localhost[0]: PASSED  sympy.modules.series.tests.test_order.py test_simple_1
   localhost[1]: PASSED  sympy.modules.series.tests.test_series.py test_exp
   localhost[0]: PASSED  sympy.modules.series.tests.test_oseries.py test_simple_1
   localhost[2]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page15_ex2_10
   localhost[2]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page18_ex2_15
       pc232[0]: PASSED  sympy.modules.series.tests.test_oseries.py test_power_x_x
       pc232[0]: PASSED  sympy.modules.series.tests.test_series.py testseriesbug1
   localhost[1]: PASSED  sympy.modules.series.tests.test_series.py test_seriesbug2
   localhost[2]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page27_ex2_17
   localhost[2]: PASSED  sympy.modules.series.tests.test_order.py test_simple_6
   localhost[2]: PASSED  sympy.modules.series.tests.test_oseries.py test_exp_sqrt_1
   localhost[2]: PASSED  sympy.modules.series.tests.test_series.py testseries2
   localhost[2]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_fraction
   localhost[2]: PASSED  ...ecfun.tests.test_orthogonal_polynomials.py test_legendre
       pc232[0]: PASSED  sympy.modules.series.tests.test_series.py test_bug2
       pc232[0]: PASSED  sympy.modules.series.tests.test_series.py test_bug3
       pc232[0]: PASSED  sympy.modules.series.tests.test_series.py test_order
       pc232[0]: PASSED  ...odules.series.tests.test_series.py test_order_expand_bug
       pc232[0]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_ratsimp
       pc232[0]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_together
       pc232[0]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_collect
       pc232[0]: PASSED  ...dules.solvers.tests.test_solvers.py test_linear_systemLU
       pc232[0]: PASSED  ...modules.specfun.tests.test_factorials.py test_factorial2
       pc232[0]: PASSED  ...cfun.tests.test_orthogonal_polynomials.py test_chebyshev

====================  247 test run in 16.25s (rsync: 1.66) =====================
```
and like this for a failure:
```
ondra@fuji:~/sympy$ py.test -d
  Test started, hosts: localhost[0], localhost[1], localhost[2], pc232[0], pc232[1]  
local top directory: /home/ondra/sympy
local RSync root [1/1]: /home/ondra/sympy
   localhost[0]: gateway initialised (remote topdir: None)
   localhost[1]: gateway initialised (remote topdir: None)
   localhost[2]: gateway initialised (remote topdir: None)
       pc232[0]: gateway initialised (remote topdir: /home/ondra/pytestcache-pc232/sympy)
       pc232[1]: gateway initialised (remote topdir: /home/ondra/pytestcache-pc232/sympy)
   localhost[0]: skipping inplace rsync of '/home/ondra/sympy'
   localhost[0]: READY (still 4 to go)
   localhost[1]: skipping inplace rsync of '/home/ondra/sympy'
   localhost[1]: READY (still 3 to go)
   localhost[2]: skipping inplace rsync of '/home/ondra/sympy'
   localhost[2]: READY (still 2 to go)
       pc232[0]: rsync 'sympy' to remote '/home/ondra/pytestcache-pc232/sympy'
       pc232[1]: skip duplicate rsync to '/home/ondra/pytestcache-pc232/sympy'
       pc232[1]: READY (still 1 to go)
       pc232[0]: READY
   localhost[0]: PASSED  sympy.core.tests.test_arit.py test_Symbol
   localhost[0]: PASSED  sympy.core.tests.test_arit.py test_ncpow
   localhost[0]: PASSED  sympy.core.tests.test_arit.py test_Pow_is_negative_positive
   localhost[1]: PASSED  sympy.core.tests.test_arit.py testdiv
   localhost[1]: PASSED  sympy.core.tests.test_arit.py test_powerbug
   localhost[1]: PASSED  ...e.tests.test_arit.py test_Pow_is_nonpositive_nonnegative
   localhost[0]: PASSED  sympy.core.tests.test_assumptions.py test_negativeone
   localhost[1]: PASSED  sympy.core.tests.test_assumptions.py test_pos_rational
   localhost[2]: PASSED  sympy.core.tests.test_arit.py test_expand
   localhost[2]: PASSED  sympy.core.tests.test_arit.py test_Add_Mul_is_integer
   localhost[2]: PASSED  sympy.core.tests.test_assumptions.py test_symbol_unset
   localhost[2]: PASSED  sympy.core.tests.test_assumptions.py test_neg_rational
   localhost[0]: PASSED  sympy.core.tests.test_assumptions.py test_I
   localhost[2]: PASSED  ....core.tests.test_assumptions.py test_neg_symbol_positive
   localhost[1]: PASSED  sympy.core.tests.test_assumptions.py test_symbol_positive
       pc232[0]: PASSED  sympy.core.tests.test_arit.py test_power_expand
       pc232[0]: PASSED  sympy.core.tests.test_arit.py test_Mul_is_even_odd
       pc232[0]: PASSED  sympy.core.tests.test_assumptions.py test_zero
       pc232[1]: PASSED  sympy.core.tests.test_arit.py test_ncmul
       pc232[0]: PASSED  sympy.core.tests.test_assumptions.py        pc232[1]: PASSED  sympy.core.tests.test_arit.pytest_pi
       pc232[0]: PASSED  sympy.core.tests.test_assumptions.py  test_symbol_nonpositive
test_Add_is_even_odd
       pc232[1]: PASSED  sympy.core.tests.test_assumptions.py test_one
   localhost[2]: PASSED  sympy.core.tests.test_basic.py test_ldegree
       pc232[1]: PASSED  sympy.core.tests.test_assumptions.py test_E
       pc232[1]: PASSED  ...re.tests.test_assumptions.py test_neg_symbol_nonpositive
       pc232[1]: PASSED  sympy.core.tests.test_basic.py test_atoms
       pc232[1]: PASSED  sympy.core.tests.test_complex.py test_pythoncomplex
   localhost[1]: PASSED  sympy.core.tests.test_basic.py test_ibasic
   localhost[2]: PASSED  sympy.core.tests.test_complex.py test_abs1
   localhost[1]: PASSED  sympy.core.tests.test_complex.py test_complex
   localhost[2]: PASSED  sympy.core.tests.test_equal.py testequal
   localhost[1]: PASSED  sympy.core.tests.test_diff.py testdiff2
   localhost[1]: PASSED  sympy.core.tests.test_eval.py test_pow_eval
   localhost[2]: PASSED  sympy.core.tests.test_eval.py test_mulpow_eval
       pc232[0]: PASSED  sympy.core.tests.test_basic.py test_leadterm
       pc232[0]: PASSED  sympy.core.tests.test_complex.py test_abs2
       pc232[0]: PASSED  sympy.core.tests.test_equal.py test_expevalbug
       pc232[0]: PASSED  sympy.core.tests.test_eval.py test_evalpow_bug
       pc232[1]: PASSED  sympy.core.tests.test_eval.py test_add_eval
       pc232[1]: PASSED  sympy.core.tests.test_eval.py test_expbug
   localhost[2]: PASSED  sympy.core.tests.test_evalf.py test_bug1
       pc232[0]: PASSED  sympy.core.tests.test_evalf.py test_bug2
   localhost[1]: PASSED  sympy.core.tests.test_eval_power.py test_rational
       pc232[1]: PASSED  sympy.core.tests.test_functions.py test_func
   localhost[1]: PASSED  sympy.core.tests.test_functions.py test_exp_log
   localhost[2]: PASSED  sympy.core.tests.test_functions.py test_log_hashing_bug
       pc232[1]: PASSED  sympy.core.tests.test_functions.py test_exp_bug
       pc232[0]: PASSED  sympy.core.tests.test_functions.py test_sign
   localhost[1]: PASSED  sympy.core.tests.test_match.py test_symbol
       pc232[1]: PASSED  sympy.core.tests.test_match.py test_interface
   localhost[2]: PASSED  sympy.core.tests.test_match.py test_add
       pc232[0]: PASSED  sympy.core.tests.test_match.py test_complex
   localhost[2]: PASSED  sympy.core.tests.test_match.py test_bug2
   localhost[1]: PASSED  sympy.core.tests.test_match.py test_behavior2
   localhost[1]: PASSED  sympy.core.tests.test_numbers.py test_Real_eval
       pc232[0]: PASSED  sympy.core.tests.test_numbers.py test_Rational
   localhost[2]: PASSED  sympy.core.tests.test_numbers.py test_Infinity
       pc232[0]: PASSED  sympy.core.tests.test_numbers.py test_powers
   localhost[2]: PASSED  sympy.core.tests.test_numbers.py test_int
   localhost[1]: PASSED  sympy.core.tests.test_numbers.py test_accept_str
       pc232[0]: PASSED  sympy.core.tests.test_numbers.py test_real_bug
       pc232[1]: PASSED  sympy.core.tests.test_numbers.py test_Rational_cmp
       pc232[1]: PASSED  sympy.core.tests.test_numbers.py test_abs1
       pc232[1]: PASSED  sympy.core.tests.test_numbers.py test_bug_sqrt
   localhost[0]: PASSED  sympy.core.tests.test_basic.py test_basic
   localhost[2]: PASSED  sympy.core.tests.test_str.py test_bug1
   localhost[0]: PASSED  sympy.core.tests.test_basic.py test_is_polynomial
       pc232[1]: PASSED  sympy.core.tests.test_str.py test_bug3
   localhost[1]: PASSED  sympy.core.tests.test_str.py test_poly_str
   localhost[0]: PASSED  sympy.core.tests.test_diff.py testdiff
       pc232[0]: PASSED  sympy.core.tests.test_str.py test_bug2
   localhost[0]: PASSED  sympy.core.tests.test_eval.py test_addmul_eval
   localhost[1]: PASSED  sympy.core.tests.test_str.py test_x_div_y
   localhost[2]: PASSED  sympy.core.tests.test_subs.py test_subs
   localhost[0]: PASSED  sympy.core.tests.test_eval.py test_symbol_expand
       pc232[0]: PASSED  sympy.core.tests.test_subs.py test_logexppow
       pc232[1]: PASSED  sympy.core.tests.test_subs.py test_bug
   localhost[2]: PASSED  sympy.core.tests.test_symbol.py test_Symbol
   localhost[1]: PASSED  sympy.core.tests.test_subs.py test_dict
   localhost[0]: PASSED  sympy.core.tests.test_functions.py test_log
       pc232[0]: PASSED  sympy.core.tests.test_symbol.py test_lt_gt
   localhost[0]: PASSED  sympy.core.tests.test_functions.py test_Derivative
   localhost[0]: PASSED  sympy.core.tests.test_match.py test_behavior1
       pc232[0]: PASSED  sympy.modules.geometry.tests.test_geometry.py test_util
       pc232[0]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_power
   localhost[0]: PASSED  sympy.core.tests.test_numbers.py test_Real
       pc232[0]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_reshape
       pc232[0]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_inverse
   localhost[1]: PASSED  sympy.modules.geometry.tests.test_geometry.py test_ellipse
       pc232[1]: PASSED  sympy.modules.geometry.tests.test_geometry.py test_point
       pc232[1]: PASSED  ...dules.integrals.tests.test_integrals.py test_integration
       pc232[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_creation
       pc232[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_applyfunc
       pc232[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_util
       pc232[1]: PASSED  ...dules.matrices.tests.test_matrices.py test_sparse_matrix
   localhost[1]: PASSED  ...integrals.tests.test_integrals.py test_integration_table
       pc232[0]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_eigen
   localhost[0]: PASSED  sympy.core.tests.test_numbers.py test_accept_int
   localhost[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_submatrix
   localhost[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_LUdecomp
   localhost[1]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_QR
   localhost[2]: PASSED  sympy.modules.geometry.tests.test_geometry.py test_polygon
   localhost[0]: PASSED  sympy.core.tests.test_str.py test_pow
   localhost[0]: PASSED  sympy.core.tests.test_str.py test_bug4
   localhost[0]: PASSED  sympy.core.tests.test_subs.py test_subbug1
       pc232[0]: PASSED  ...ting.tests.test_plotting.py.TestPlotting.() test_plot_3d
   localhost[2]: PASSED  ...ules.matrices.tests.test_matrices.py test_multiplication
   localhost[2]: PASSED  ...atrices.tests.test_matrices.py test_submatrix_assignment
   localhost[2]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_LUsolve
   localhost[2]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_nullspace
       pc232[1]: PASSED  ...t_plotting.py.TestPlotting.() test_plot_3d_discontinuous
   localhost[1]: PASSED  ...ting.tests.test_plotting.py.TestPlotting.() test_plot_2d
   localhost[0]: PASSED  sympy.modules.geometry.tests.test_geometry.py test_line
   localhost[0]: PASSED  ...egrals.tests.test_integrals.py test_multiple_integration
   localhost[0]: PASSED  ...modules.matrices.tests.test_matrices.py test_determinant
   localhost[0]: PASSED  sympy.modules.matrices.tests.test_matrices.py test_random
   localhost[0]: PASSED  ...es.matrices.tests.test_matrices.py test_jacobian_hessian
   localhost[2]: PASSED  ...t_plotting.py.TestPlotting.() test_plot_2d_discontinuous
       pc232[0]: PASSED  ...test_plotting.py.TestPlotting.() test_plot_2d_parametric
       pc232[0]: PASSED  ...modules.polynomials.tests.test_polynomials.py test_coeff
       pc232[0]: PASSED  sympy.modules.polynomials.tests.test_polynomials.py test_lcm
       pc232[0]: PASSED  sympy.modules.polynomials.tests.test_polynomials.py test_sqf
       pc232[0]: PASSED  ...les.series.tests.test_demidovich.py test_Limits_simple_1
       pc232[0]: PASSED  sympy.modules.series.tests.test_demidovich.py test_f2
       pc232[1]: PASSED  ...test_plotting.py.TestPlotting.() test_plot_3d_parametric
       pc232[0]: PASSED  ....series.tests.test_limit.py test_MrvTestCase_simple_poly
       pc232[0]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_1
       pc232[0]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_4
       pc232[0]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_7
       pc232[1]: PASSED  sympy.modules.polynomials.tests.test_polynomials.py test_div
       pc232[0]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page44_ex3_17
       pc232[1]: PASSED  ...es.polynomials.tests.test_polynomials.py test_real_roots
       pc232[0]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page60_sec3_5
       pc232[0]: PASSED  ...series.tests.test_limit.py test_MrvLimitTestCase_page4_1
       pc232[0]: PASSED  ...s.tests.test_limit.py test_MrvLimitTestCase_page14_ex2_9
       pc232[1]: PASSED  ...ules.polynomials.tests.test_polynomials.py test_sqf_part
       pc232[0]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page16_ex2_13
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_simple_1
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_simple_2
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_simple_3
   localhost[1]: PASSED         pc232[1]: PASSED  ...les.series.tests.test_demidovich.py ...s.test_plotting.py.TestPlotting.() test_Limits_simple_2
test_plot_3d_cylinder
       pc232[1]: PASSED  ...ies.tests.test_limit.py test_MrvCompareLeadTerm_simple_1
       pc232[1]: PASSED  ...s.series.tests.test_limit.py test_MrvTestCase_simple_log
   localhost[1]: PASSED  ...es.polynomials.tests.test_polynomials.py test_Polynomial
       pc232[1]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_2
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_simple_4
   localhost[0]: PASSED  ...tting.tests.test_plotting.py.TestPlotting.() test_import
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_simple_5
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_contains_0
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py        pc232[1]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_5
test_contains_2
       pc232[1]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_8
       pc232[1]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page47_ex3_21
       pc232[1]: PASSED  ....series.tests.test_limit.py test_MrvLimitTestCase_simple
       pc232[1]: PASSED  ...series.tests.test_limit.py test_MrvLimitTestCase_page4_2
   localhost[2]: PASSED  ....test_plotting.py.TestPlotting.() test_plot_3d_spherical
   localhost[1]: PASSED  sympy.modules.polynomials.tests.test_polynomials.py test_gcd
       pc232[1]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page15_ex2_10
   localhost[2]: PASSED  ...es.polynomials.tests.test_polynomials.py test_coeff_ring
       pc232[1]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page18_ex2_15
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_add_1
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_multivar_1
       pc232[1]: FAILED  sympy.modules.series.tests.test_order.py test_simple_6
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_multivar_2
       pc232[1]: PASSED  sympy.modules.series.tests.test_order.py test_contains_1
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_multivar_mul_1
       pc232[1]: PASSED  sympy.modules.series.tests.test_order.py test_contains_3
   localhost[1]: PASSED  ...modules.polynomials.tests.test_polynomials.py test_roots
       pc232[0]: PASSED  sympy.modules.series.tests.test_order.py test_multivar_3
       pc232[0]: PASSED  sympy.modules.series.tests.test_oseries.py test_simple_1
       pc232[1]: PASSED  sympy.modules.series.tests.test_order.py test_multivar_0
   localhost[2]: PASSED  ...ules.polynomials.tests.test_polynomials.py test_groebner
       pc232[1]: PASSED  sympy.modules.series.tests.test_oseries.py test_mul_0
       pc232[1]: PASSED  sympy.modules.series.tests.test_oseries.py test_pow_1
   localhost[1]: PASSED  sympy.modules.series.tests.test_demidovich.py test_leadterm
   localhost[2]: PASSED  ....polynomials.tests.test_polynomials.py test_solve_system
       pc232[0]: PASSED  sympy.modules.series.tests.test_oseries.py test_pow_0
   localhost[2]: PASSED  ...les.series.tests.test_demidovich.py test_Limits_simple_0
       pc232[1]: PASSED  sympy.modules.series.tests.test_oseries.py test_exp_1
       pc232[1]: PASSED  sympy.modules.series.tests.test_series.py testseriesbug1
       pc232[0]: PASSED  sympy.modules.series.tests.test_oseries.py test_sqrt_1
       pc232[0]: PASSED  sympy.modules.series.tests.test_series.py testseries1
   localhost[0]: PASSED  ...ests.test_plotting.py.TestPlotting.() test_plot_2d_polar
   localhost[0]: PASSED  ...ng.tests.test_plotting.py.TestPlotting.() test_plot_grid
       pc232[0]: PASSED  sympy.modules.series.tests.test_series.py testseries2
       pc232[0]: PASSED  sympy.modules.series.tests.test_series.py test_bug3
       pc232[0]: PASSED  sympy.modules.series.tests.test_series.py test_order
       pc232[0]: PASSED  ...odules.series.tests.test_series.py test_order_expand_bug
       pc232[0]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_simplify
       pc232[0]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_together
       pc232[0]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_collect
   localhost[1]: PASSED  ...les.series.tests.test_demidovich.py test_Limits_simple_4
       pc232[0]: PASSED  ...modules.specfun.tests.test_factorials.py test_factorial1
   localhost[1]: PASSED  ...ies.tests.test_limit.py test_MrvCompareLeadTerm_simple_2
       pc232[0]: PASSED  ...ecfun.tests.test_orthogonal_polynomials.py test_legendre
   localhost[1]: PASSED  ...s.series.tests.test_limit.py test_MrvTestCase_simple_exp
   localhost[1]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_3
   localhost[1]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_page41_6
   localhost[2]: PASSED  sympy.modules.series.tests.test_demidovich.py test_f1
   localhost[2]: PASSED  ...les.series.tests.test_limit.py test_MrvTestCase_simple_x
   localhost[2]: PASSED  ....series.tests.test_limit.py test_MrvTestCase_simple_exp2
   localhost[0]: PASSED  ...odules.polynomials.tests.test_polynomials.py test_factor
   localhost[2]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page41_ex3_13
   localhost[1]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page43_ex3_15
   localhost[2]: PASSED  ...ies.tests.test_limit.py test_MrvTestCase_page60_sec3_5_2
   localhost[2]: PASSED  ...s.series.tests.test_limit.py test_MrvLimitTestCase_page4
   localhost[1]: PASSED  ...ies.tests.test_limit.py test_MrvTestCase_page60_sec3_5_1
   localhost[1]: PASSED  ...s.series.tests.test_limit.py test_MrvLimitTestCase_page2
   localhost[0]: PASSED  ...les.polynomials.tests.test_polynomials.py test_resultant
   localhost[1]: PASSED  ...s.tests.test_limit.py test_MrvLimitTestCase_page12_ex2_6
   localhost[0]: PASSED  ...modules.polynomials.tests.test_polynomials.py test_sturm
   localhost[2]: PASSED  ...s.tests.test_limit.py test_MrvLimitTestCase_page13_ex2_7
   localhost[2]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page15_ex2_11
   localhost[1]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page44_ex3_17
   localhost[1]: PASSED  sympy.modules.series.tests.test_order.py test_w
   localhost[2]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page27_ex2_17
   localhost[2]: PASSED  ...s.tests.test_limit.py test_MrvLimitTestCase_page77_ex5_2
   localhost[0]: PASSED  ...les.series.tests.test_demidovich.py test_Limits_simple_3
   localhost[0]: PASSED  ...eries.tests.test_limit.py test_MrvTestCase_page51_ex3_25
   localhost[0]: PASSED  ...ies.tests.test_limit.py test_MrvLimitTestCase_simple_inf
   localhost[1]: PASSED  sympy.modules.series.tests.test_oseries.py test_mul_1
       pc232[1]: PASSED  sympy.modules.series.tests.test_series.py test_bug2
   localhost[2]: PASSED  sympy.modules.series.tests.test_oseries.py test_power_x_x
       pc232[1]: PASSED  ...modules.series.tests.test_series.py test_generalexponent
       pc232[1]: PASSED  sympy.modules.series.tests.test_series.py test_order_bug
   localhost[2]: PASSED  sympy.modules.series.tests.test_series.py test_exp
   localhost[0]: PASSED  ...s.tests.test_limit.py test_MrvLimitTestCase_page12_ex2_5
   localhost[1]: PASSED  sympy.modules.series.tests.test_oseries.py test_exp_sqrt_1
   localhost[0]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page43_ex3_15
   localhost[0]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page47_ex3_21
   localhost[0]: PASSED  ...ests.test_limit.py test_MrvLimitTestCase_page47_ex3_21_1
       pc232[1]: PASSED  sympy.modules.series.tests.test_series.py test_sinsinbug
       pc232[1]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_fraction
       pc232[1]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_separate
       pc232[1]: PASSED  sympy.modules.solvers.tests.test_solvers.py test_solve
   localhost[2]: PASSED  sympy.modules.simplify.tests.test_simplify.py test_ratsimp
       pc232[1]: PASSED  ...modules.specfun.tests.test_factorials.py test_factorial2
       pc232[1]: PASSED  ...cfun.tests.test_orthogonal_polynomials.py test_chebyshev
   localhost[2]: PASSED  sympy.modules.specfun.tests.test_factorials.py test_gamma
   localhost[2]: PASSED  sympy.modules.specfun.tests.test_specfun.py test_import
   localhost[0]: PASSED  ....tests.test_limit.py test_MrvLimitTestCase_page51_ex3_25
   localhost[1]: PASSED  sympy.modules.series.tests.test_series.py test_seriesbug2
   localhost[0]: PASSED  ...s.series.tests.test_limit.py test_MrvLimitTestCase_bug_0
   localhost[1]: PASSED  ...dules.solvers.tests.test_solvers.py test_linear_systemLU
   localhost[0]: PASSED  sympy.modules.series.tests.test_oseries.py test_geometric_1

==================================  FAILURES  ==================================
____ sympy sympy modules series tests test_order.py test_simple_6 on pc232 _____
__________________________ entrypoint: test_simple_6 ___________________________

    def test_simple_6():
        assert Order(x)-Order(x) == Order(x)
E       assert Order(x)+Order(1) == Order(1)
>       AssertionError: assert (O(x) + O(1)) == O(1)
         +  where O(x) = Order(x)
         +  and   O(1) = Order(1)
         +  and   O(1) = Order(1)

[/home/ondra/pytestcache-pc232/sympy/sympy/modules/series/tests/test_order.py:46]
________________________________________________________________________________
===============  247 test run, 1 failed in 14.58s (rsync: 1.62) ================
```