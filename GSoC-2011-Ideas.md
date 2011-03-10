# Google Summer of Code 2010

This is the list of ideas for students wishing to apply for Google Summer of Code 2011.  

## Ideas

Please add new ideas here. And remember, that you can apply with something completely different if you like (if you are a student interested in applying, please get in touch with us on our [mailing list](http://groups.google.com/group/sympy), so that we can help you with the application). This is for inspiration. The ideas are in no particular order.  Ideas in bold are ones that we would really like to have implemented.  However, it is best for you to apply to do something that you are interested in, and also something that you are knowledgeable about.  That way, you will be the most successful in your project, and will have the most fun doing it.  Some of these things are already partially implemented.  Checkout the current source or asking on the mailing list to see where things presently stand.

* anything from our [http://wiki.sympy.org/wiki/Plan_for_SymPy_1.0 roadmap]
* '''integrate our experimental [http://groups.google.com/group/sympy/browse_thread/thread/aa3f4263bc3f7e23 Cython core] into SymPy'''
* asymptotic series
* port to Python 3.0 ({{issue|1262}})
* improve the integration algorithm, so that SymPy can integrate anything that can be integrated.
  * implement recursive Risch algorithm (compare with heuristic version)
  * improve integration of rational functions (via subresultants)
  * integration of functions on domains of maximum extent, etc.
* definite integration & integration on complex plane using residues
* Groebner bases and their applications in geometry, simplification and integration
  * improve Buchberger's algorithm and implement Faugere F4 (compare their speed)
* improve polynomial algorithms (gcd, factorization) by allowing coefficients in algebraic extensions of the ground domain
* implement efficient multivariate polynomials (arithmetics, gcd, factorization)
  * choose a polynomial representation (e.g. recursive dense) or use task dependent representations
  * implement efficient arithmetics (e.g. using geobuckets (Yan) or heaps (Monagan & Pearce))
  * implement factorization algorithm (Musser's or Wang's EEZ (better)) and gcd (e.g. EEZ-GCD)
  * provide high-level OO abstraction over polynomial tools you've developed
* '''Add support for solving inequalities, and support for assumptions like Assume(x>y) (I think these two will require each other).'''
* improve SymPy's pattern matching abilities (efficiency and generality)
  * experiment with regular expressions over SymPy's algebraic expressions
  * implement similarity measure between expression trees
  * expression complexity measures (e.g. Kolmogorov's complexity)
  * implement expressions signatures and heuristic equivalence testing
  * implement semantic matching (e.g. expression: cos(x), pattern: sin(a*x) + b)
    * e.g by using power series for this purpose (improve series speed)
  * matching of Python's objects (lists, sets, tuples etc.)
  * use pure Python syntax for all this (no preparsing)
* improve simplification and term rewriting algorithms
  * add (improve) verbatim and semi-verbatim modes (more control on expression rewriting)
  * fix annoying minus sign rewriting problem (separate internal representation and printing)
  * extend simplify() function to support something more than rational functions (see trim())
  * implement more expression rewrite functions (to an exact form that user specifies)
  * maybe put transformation rules in an external database (e.g. prolog), what about speed?
  * improve context (e.g. input) depended simplification steps in different algorithms
    * e.g. the integrator needs different sets of rules to return "better" output for different input
    * but there are more: recurrences, summations, solvers, polynomials with arbitrary coefficients
  * what about information carried by expressions?
    * what is simpler: chebyshevt(1, x) or x ?
    * what is simpler: chebyshevt(1000, x) or (...) ?
* implement symbolic (formal) logics and set theory ''I think some of this might already be implemented with the new assumptions.  Check the source. -Aaron'''
  * implement predicate (e.g. first-order), modal, temporal, description logics
  * implement multivalued logics; fuzzy and uncertain logics and variables
  * implement rewriting, minimization, normalization (e.g. Skolem) of expressions
  * implement set theory, cardinal numbers, relations etc.
  * add nice unicode, latex and mathml pretty printing  ''Don't we already have this?  -Aaron''
    * maybe use user dependent sets of symbols e.g. for implication (=>), (->)
  * add drawing of Venn diagrams (e.g. for educational purpose)
  * improve SymPy's logic facilities to boost assumptions engine
* implement symbolic global optimization (value, argument) with/without constraints, use assumptions
* '''improve the series expansion ([http://code.google.com/p/sympy/issues/list?q=label:Series relevant issues])'''
  * formal power series (FPS)
  * improve limits - make sure all basic limits work
* objects with indices (tensors)
* improve the plotting module:
  * better matplotlib integration
  * extract the math TeX typesetting engine from matplotlib (it has some external dependencies on freetype and Agg that will need to be resolved), and integrate it in our plotting lib (maybe create a new project for this engine)
* generalized functions -- Dirac delta, P(1/x), etc... Convolution, Fourier and Laplace transforms
* vector calculus, differential fields, maybe Lie algebras & groups
* parametric integrals asymptotic expansion (integral series)
* ordinary differential equations. Currently, SymPy only supports many basic types of differential equations, but there are plenty of methods that are not implemented. Maybe support for using Lie groups to help solve ODEs.  See [http://docs.sympy.org/modules/solvers/ode.html the ODE docs] and the current source (sympy/solvers/ode.py) for information on what methods are currently implemented.  Also, there is no support currently for solving systems of ODEs.  You also might want to look at [http://www-sop.inria.fr/cafe/Manuel.Bronstein/sumit/index.html Manuel Bronstein's sumit]
* partial differential equations.  Currencly, SymPy can solve only very simple case of separable PDEs.  
* increase image processing of PIL+SymPy functionality to match that of octave or matlab
* improve SymPy's interoperatibility with other CAS software
  * implement general code parsing (Mathematica, Maxima, Axiom etc.) using e.g. pyparsing
  * implement Python + SymPy (structure + semantics) translation to your favorite CAS (other than SymPy :)
* '''Symbolic quantum mechanics in SymPy.'''  The follow would each probably be a solid summer's work (or more).
  * Abstract Dirac notation, including Hilbert spaces, Operators, States, Basis sets, density matrices, measurement, etc.
  * Spin states and operators for arbitrary spin.  This would include things like angular momentum coupling, Clebsch-Gordon coefficient, Wigner 3j and 6j, etc.
  * Position and momentum basis functions on arbitrary intervals and sets in 1D, 2D and 3D.  Use to implement basis quantum systems like particle in a box, H atom, simple harmonic oscillator, scattering, etc.
  * Symbolic quantum computing:  qubits, gates, algorithms, measurement, noise, error-correction. 
  * Second quantization capabilities:  Wick's theorem for Bosons, port to new assumption system, port to new general quantum module.

==Detailed Ideas==

'''Note:  Some of this material was just copied from [[GSoC2009Ideas|Last Year's List]], but we have started to update it.'''

===Symbolic quantum mechanics (sympy.physics)===

'''Abstract Dirac notation'''

* Status:

We would like to have a framework for general, abstract, symbolics quantum mechanics in SymPy.  This would include
Hilbert spaces, Operators, States, Basis sets, density matrices, measurement, Tensor products, approximations, time evolution, etc.  We have started to
sketch out the design of this in this branch:

http://github.com/ellisonbg/sympy/tree/quantum

* Idea:

Take the sketch and turn it into a general framework for symbolic quantum mechanics.  The goal would be that this
could be the base layer for all quantum modules in SymPy, including spin, position/momentum wavefunctions, quantum
computer, etc.  Thus, whoever works on this would need to work with the developers working on these other aspects of SymPy. 
Critical parts of this layer will be handling tensor products of Hilbert spaces, operators and states and general representations (including basis transformations) of
operators and states.

* Rating: 3 (moderate)

'''Spin states and operators for arbitrary spin'''

* Status:

Spin is a critical part of quantum mechanics.  The spin algebra in quantum mechanics is rich and complex, even for spin 1/2.
We would like to have a reasonably complete implementation of various spin states and operators for arbitrary spin s.
So far, nothing has been done on this.

* Idea:

Using the base layer of quantum states and operators in SymPy (see previous topic), implement symbolic spin states and operators for
arbitrary spin s.  This would include the angular momentum coupling using Clebsch-Gordon coefficients, Wiger 3j/6j symbols, etc.
While SymPy already has spherical harmonics, it would be nice to integrate those into the treatment of orbital angular momentum.

* Rating: 3-4 (moderate-hard)

'''Position and momentum basis functions'''

* Status:

The position and momentum basis functions in quantum mechanics are somewhat pathological because the basis functions are not square integrable. In spite of
this, these representations are immensely useful and are introduced to students early on.  We would like to be able to handle position and momentum wavefunctions
on arbitrary domains in 1D, 2D and 3D.  

* Idea:

Implement full machinery for position and momentum wavefunctions, including modified Hilbert spaces, Dirac delta functions, basis transformations in 1D, 2D and 3D.
This should use the base layer of quantum states and operators in SymPy (see first topic).  The test suite should include classic examples from quantum mechanics, 
such as particle in box, H atom, simple harmonic oscillator, scattering, etc.

* Rating: 3-4 (moderate-hard)

'''Symbolic quantum computing'''

* Status:

Quantum computing refers to the usage of quantum states, operators, time-devolution and measurement to perform non-trivial computations.  In SymPy, we would like
to extend our base layer to include the states and operators used in quantum computing.  The main goal is to create a general symbolic quantum computing framework
that integrates with the rest of SymPy's quantum modules.  No work as been done on this topic in SymPy.

* Idea:

Using the base layer of quantum states and operators in SymPy (see first topic) implement qubits, gates, algorithms, measurement, noise, error-correction, etc.

* Rating: 3-5 (hard)

'''Second quantization capabilities'''

Status:

SymPy currently has a good bit of second quantization implemented here:

http://github.com/ellisonbg/sympy/blob/master/sympy/physics/secondquant.py

However, there are many things we could do to improve this and add more sophisticated capabilities.

* Idea:

Work on sympy.physics.secondquant in the following areas:

1. Refactor to use the new assumptions system.
2. Refactor to use the new base quantum layer we are developing (see above).
3. Implement Wick's theorem for Bosons, including the macroscopic population of the ground states.
4. Density matrices.
5. Time evolution.
6. Various approximations, such as perturbation theory, Hartree-Fock, time-dependent Hartree-Fock, Hartree-Fock-Bogoliubov, etc.
7. Implement new functions for simplifying products of second quantized operators in different ways (such as moving an annihilation operator R).

* Rating: 5 (hard)

===Polynomials module===

'''Efficient Groebner bases and their applications'''

* Status:

Groebner bases computation is one of the most important tools in computer algebra, which can be used for computing multivariate polynomial LCM and GCD, solving systems of polynomial equations, symbolic integration, simplification of rational expressions, etc. Currently there is an efficient version of Buchberger algorithm implemented, along with naive multivariate polynomial arithmetics in monomial form.

* Idea:

Improve efficiency of Groebner basis algorithm by using better selection strategy (e.g. sugar method) and implement Faugere F4 or F5 algorithm and analyze which approach is better in what contexts. Apply Groebner bases in integration of rational and transcendental functions and simplification of rational expressions modulo a polynomial ideal (e.g. trigonometric functions).

* Rating: 5 (very hard)

'''Multivariate polynomials and factorization'''

* Status:

Factorization of multivariate polynomials is an important tool in algebra systems, very useful by its own, also used in symbolic integration algorithms, simplification of expressions, partial fractions, etc. Currently multivariate factorization algorithm is based on Kronecker's method, which is impractical for real life problems. Undergo there is implementation of Wang's algorithm, the most widely used method for the task.

* Idea:

Start with implementing efficient multivariate polynomial arithmetics and GCD algorithm. You do this by improving existing code, which is based on recursive dense representation or implement new methods based on your research in the field. There are many interesting methods, like Yan's geobuckets or heap based algorithms (Monagan & Pearce). Having this, implement efficient GCD algorithm over integers, which is not a heuristic, e.g. Zippel's SPMOD, Musser's EZ-GCD, Wang's EEZ-GCD. Help with implementing Wang's EEZ factorization algorithm or implement your favourite method, e.g. Gao's partial differential equations approach. You can go further and extend all this to polynomials with coefficients in algebraic domains or implement efficient multivariate factorization over finite fields.

* Rating: 4-5 (quite hard)

'''Univariate polynomials over algebraic domains'''

* Status:

Currently SymPy features efficient univariate polynomial arithmetics, GCD and factorization over Galois fields and integers (rationals). This is, however, insufficient in solving real life problems, and isn't very useful symbolic integration and simplification algorithms.

* Idea:

Choose a univariate polynomial representation in which elements of algebraic domains will be efficiently encoded. By algebraic domains we mean algebraic numbers and algebraic function fields. Having a good representation, implement efficient arithmetics and GCD algorithm. You should refer to work due to Monagan, Pearce, van Hoeij et. al. Having this, implement your favourite algorithm for factorization over discussed domains. This will require algorithms for computing minimal polynomials (this can be done by using LLL or Groebner bases). You can also go ahead and do all this in multivariate case.

* Rating: 4-5 (quite hard)

===Integration module===

'''Implement Risch algorithm, a decision procedure for symbolic integration'''

* Status:

The main symbolic integration algorithm in SymPy is the heuristic Risch algorithm, which is based on Manuel Bronstein's Poor Man Integrator. Although, this heuristic algorithms is quite simple and fast, and handle sever classes of special functions, it is not a decision procedure so it may fail to find an antiderivative, even if one exists (and it happens quite often with very simple integrals). It also have very weak support for algebraic functions.

* Idea:

A symbolic manipulation package must be equipped with a decision procedure for integration problem. The task is to implement Risch algorithm (also known as the recursive Risch algorithm) for integrating elementary transcendental functions. You should implement as much as possible of the algorithm, especially special cases. The algorithm is described in detail in Bronstein's book but you will need to put some effort to handle algebraic functions in your implementation.

* Rating: 3-5 (quite hard)

'''Implement symbolic integration via Marichev-Adamchik Mellin transform'''

* Status:

SymPy's integrator supports several classes of special function. This is, however, insufficient in solving advanced physics and engineering problems.

* Idea:

Extend the integrator by implementing methods for integration of elementary and special functions via Meijer G-functions (also known as Marichev-Adamchik Mellin transform). This approach is useful in both indefinite and definite integration. The problems are how to convert arbitrary input expression to a G-function and how to rewrite the resulting expression in terms of more familiar functions (elementary, special, hypergeometric).

* Rating: 3-5 (quite hard)

'''Implement definite integration algorithm using residues'''

* Status:

Currently the integrator handles definite integration problem by applying Newton-Liebnitz theorem. This is, however, only useful when there are no poles on the path of integration.

* Idea:

Improve the integrator by expressing the initial integral as an integral on the complex plane and applying Cauchy integral theorem.

Rating: 3-4 (hard)

===Concrete module===

'''Implement Karr algorithm, a decision procedure for symbolic summation'''

* Status:

SymPy currently features Gosper algorithm and some heuristics for computing sums of expressions. Special preference is for summations of hypergeometric type. It would be very convenient to support more classes of expressions, like (generalized) harmonic numbers etc.

* Idea:

Algorithm due to Karr is the most powerful tool in the field of symbolic summation, which you will implement in SymPy. There are strong similarities between this method and Risch algorithm for the integration problem. You will start with implementing the indefinite case and later can extend it to support definite summation (see work due to Schneider). Possibly you will also need to work on solving difference equations.

* Rating: 3-5 (quite hard)

==Potential Mentors==

If you are willing to mentor, please add yourself here:
* Aaron Meurer - If I don't decide to apply as a student, I would love to be a mentor.
* Ondrej Certik <!-- Ondrej, I am assuming you are willing -Aaron -->
* Brian E. Granger: I am willing to mentor any of the physics related projects.
* Andy R. Terrel
[[Category:Development]]
