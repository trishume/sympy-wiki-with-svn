


My name is Fredrik Johansson, and I participated in Google Summer of Code 2008 as a !SymPy developer. The project consisted of implementing "robust high-precision numerical evaluation" for !SymPy (you can read the [http://code.google.com/soc/2008/psf/appinfo.html?csaid=523E75373CEC7F39 abstract of my application]).

I had an advantage of already having worked on !SymPy for a while when the project started. In fact, I was a !SymPy developer long before I started writing my application. Being familiar with the codebase early on was very useful. I would therefore recommend future students to try to get involved as early as possible. (A good entry point is to try to write patches for some of the simpler-looking open issues, or just to try out some computations in !SymPy and discuss your impressions of how they worked out on the mailing list.) Discussing your project idea with other !SymPy developers before writing the application is very strongly recommended. In any case, !SymPy is a great project to work on, and the other developers (hopefully also myself) are very friendly and helpful.

One problem I had to face (and this is probably true of many other projects), was that there was more than one way to approach the problem, and I knew that not all possible solutions would be equally good. I therefore spent roughly the first half of the summer just working out the basics of the significance arithmetic implementation. It was only during the latter half that I got to work on more fun features, like numerical summation, that required all the basic code in the background to work. At this point, my work became much more fun (and I was able to work more efficiently).

Fortunately, my project application was written with the potentially slow initial progress in mind. Having realistic expectations from the start certainly helped; it is way too easy to overestimate the amount of work that can be accomplished in a limited amount of time. My advice to future students (for !SymPy or elsewhere) is to choose a relatively small problem to solve, such that there is a good chance of being able to solve it well.

Much more detail about how my project progressed can be found in my blog updates (listed here in reverse chronological order):

 * [http://fredrik-j.blogspot.com/2008/08/wrapping-it-up.html Wrapping it up]
 * [http://fredrik-j.blogspot.com/2008/07/division-sequel-with-bonus-material.html Division: the sequel (with bonus material)]
 * [http://fredrik-j.blogspot.com/2008/07/making-division-in-python-faster.html Making division in Python faster]
 * [http://fredrik-j.blogspot.com/2008/07/hypergeometric-series-with-sympy.html Hypergeometric series with SymPy]
 * [http://fredrik-j.blogspot.com/2008/07/faster-pi-more-integrals-and-complex.html Faster pi, more integrals and complex numbers]
 * [http://fredrik-j.blogspot.com/2008/06/gmpy-makes-mpmath-more-speedy.html GMPY makes mpmath more speedy]
 * [http://fredrik-j.blogspot.com/2008/06/taking-n-to-limit.html Taking N to the limit]
 * [http://fredrik-j.blogspot.com/2008/06/how-many-digits-would-you-like.html How many digits would you like?]
 * [http://fredrik-j.blogspot.com/2008/06/basic-implementation-of-significance.html Basic implementation of significance arithmetic]
 * [http://fredrik-j.blogspot.com/2008/06/significance-of-arithmetic.html The significance of arithmetic]
 * [http://fredrik-j.blogspot.com/2008/05/first-post.html First post]