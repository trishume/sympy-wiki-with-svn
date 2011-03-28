## About Me

My name is Tom Bachmann and I study mathematics (second year) at the
university of cambridge, england.

email: tb401@NOSPAMcam.ac.uk.
IRC: ness (authenticated with freenode)

Here is an overview of my computer
programming experience: I have previously worked on the Hurd project
(in C), I did a project that started the port of the kaXen/afterburner
pre-virtualisation environment to amd64 (in C++), and I have extended
the wikireader codebase to handle ebooks from project gutenberg
(mostly python). I can supply more details and/or references if you
wish. I have also created some "fun projects" on my own, the most
relevant here being probably what I call [[fz|https://bitbucket.org/ness/fz/overview]], a program to plot
various special functions in the complex plane and on riemann surfaces
(in C++). Finally here in cambridge there are so-called [["CATAM"|http://www.maths.cam.ac.uk/undergrad/catam/]]
(computer-aided teaching of all of mathematics) projects on which I
got excellent results; this may or may not be meaningful to you.

## Setup
My introduction to the list is [[here|http://groups.google.com/group/sympy/browse_thread/thread/fc67b5725d9d740e#]].

I have been investigating a few bugs, issues [[1321|http://code.google.com/p/sympy/issues/detail?id=1321]], [[341|http://code.google.com/p/sympy/issues/detail?id=341&q=label%3AEasyToFix&colspec=ID%20Type%20Status%20Priority%20Milestone%20Owner%20Summary%20Stars]], [[360|http://code.google.com/p/sympy/issues/detail?id=360]] and [[905|http://code.google.com/p/sympy/issues/detail?id=905]]. No code committed, yet.

## Project
I would like to work on improving the definite integration capabilities. In particular I would like to implement (a version of) the Meijer G transform algorithm [1], as suggested by Aaron Meurer. I study mathematics at an (advanced, I'd like to think :) ) undergraduate level, and I believe I understand the required mathematical background. I have taken courses on analysis, complex analysis, rings and modules, mathematical methods that will be helpful in carrying out this project.


## Deliverables
My past experience shows that I am very bad at estimating any schedules. In principle, the goal of this work is to replace huge tables of definite integrals, available e.g. in [2]. In practice, this will likely turn out to be an impossible task. Instead, the goal should be to provide the infrastructure necessary, and to develop the codebase to such an extent that a significant portion of such integrals can be evaluated. It should then be easy to add further code whenever use arises.

I have no significant plans for the summer, so I will be able to work on this project essentially full-time. I will keep in touch with my mentor in any way she/he prefers.

### Integrals of G functions that we can do
The G function is a very general function with many parameters. For the sake of this exposition I shall write \(G(z)\), for any such function suppressing all parameters. Moreover if \(G\) appears twice in a formula, it should not be expected to be the same function. I shall write \(E(z)\) for a combination of elementary functions such as \(z^a\).

\[ \int G(z) \mathrm{d}z = G(z) \]
\[ \int_0^\infty t^a G(tw) G(tz) \mathrm{d}t = E(w) G(z/w) \]

### G-function relations
The G function satisfies exceedingly many relations. The following are useful. Many formulas of this and the following sections only hold under certain restrictions which I shall omit here.

\[ z^a G(z) = G(z) \]
\[ G(z^{-1}) = G(z) \]
\[ G(wz) = \sum E(w) G(z) \]
\[ G(z^k) = E(k) G(az) \]

### Special functions in terms of G functions
Essentially all elementary functions (trigonometric, exponential etc) and special functions of mathematical physics (such as bessel functions) can be expressed in terms of G functions.

### Laplace and Fourier Transforms
Laplace and fourier transforms of \(G(z)\) can be computed, since \(e^{z} = G(z)\) [fourier transform integral has to be evaluated in two parts]. The relevant integral theorems do hold in these cases. Inverse laplace transforms can also be computed, see e.g. [3].

Hence we will get laplace and fourier transforms of all (implemented) special functions.

### Inner products
In mathematical physics there are many "inner product" relations of the form \(\int_0^\infty J_m(t) J_n(t) w(t) \mathrm{d}t = \dots \), these should also follow from the G-function relations.

### Integrals missing in SymPy
The following tickets should be fixed as a side effect:
[[841|http://code.google.com/p/sympy/issues/detail?id=841&q=label%3AIntegration&colspec=ID%20Type%20Status%20Priority%20Milestone%20Owner%20Summary%20Stars]],
[[1426|http://code.google.com/p/sympy/issues/detail?id=1426&q=label%3AIntegration%20definite&colspec=ID%20Type%20Status%20Priority%20Milestone%20Owner%20Summary%20Stars]] (at least for definite integrals), [[1893|http://code.google.com/p/sympy/issues/detail?id=1893&q=label%3AIntegration%20definite&colspec=ID%20Type%20Status%20Priority%20Milestone%20Owner%20Summary%20Stars]], probably a few more.

## Plan
In principle, definite integration using the G-transform consists of three steps:

1. Rewrite the integrand in terms of G functions (except for powers/polynomials)
2. Simplify the resulting expression using the algebraic relations of the G function; hope that we hit a form where one of the integration theorems applies.
3. Transform back the resulting expression in G functions into a recognisable form.

It seems like a good idea to select a representative subset of formulae from a reference table such as [2], investigate which sympy can currently solve, and then implement the G transform, focussing on making the selected formulae work. I can then evaluate the algorithm against more formulae from said reference works, and implement extensions if time permits.


So the plan would look roughly like this:

* Add classes for hypergeometric functions and G-functions.
  These classes are much more like a container for indices than anything else. In principle we don't need hypergeometric functions, but many books are phrased in terms of them so it is probably helpful to have them around, together with conversion to G functions.
* Implement pattern matching code to rewrite an integrand as a product of at most two G-functions.
  This is probably an incremential work, driven by given use cases. I cannot see a very general strategy here. Many detailed reference works available, e.g [3].
* Integration of G-functions in the described form is trivial.
* Compute G-functions in terms of named special functions.
  This is also hard, and definitely an incremential work. One strategy is described in [1].
* For this to make sense, there need to be many classes of special functions available. mpmath provides very many of these, but it is geared towards actually computing them.


## Tentative Schedule
The GSoC consists of three months. This is a *very* tentative schedule:

* Week 1: Add classes for bessel, hypergeometric and G functions; add basic conversions
  bessel->hypergeometric<->G
* Week 2 and 3: Implement shift and inverse shift operators for G functions;
  implement basic framework for Kelly's algorithm
* Week 4: Extend integration code to try a G function approach if everything else fails; implement
  basic pattern matching for G function expressions and basic G function integrals
* Week 5-6: Extend and refine the previous work to yield most of the formulas involving bessel
  functions from [2], sections 6.5 and 17.

The following weeks: on a case-by-case basis, iterate the following process:

* Add new class of special functions
* Improve pattern matching
* Extend Kelly's algorithm

so as to yield iteratively more and more formulas from [2].


## Sources
[1] - K. Roach. Meijer g function representations. In ISSAC ’97: Proceedings of the 1997 international symposium on Symbolic and algebraic computation, pages 205–211, New York, NY, USA, 1997. ACM.

[2] Ryzhik, I. M., Jeffrey, A., Zwillinger, D. (2007), Table of integrals, series and products, Translated from Russian by Scripta Technica, Inc.

[3] Luke, Y. L. (1969), The Special Functions and Their  Approximations, Volume 1, Academic Press, San Diego.