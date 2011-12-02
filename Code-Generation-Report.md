


# About Me

I am a Ph.D. candidate at the University of Bergen, Norway.  My research
is within theoretical nuclear physics with an emphasis on the
Coupled-Cluster method.  Before the GSOC I had contributed a fermionic second
quantization framework to Sympy as well as some sporadic patches.

# Introduction

The project was to improve the code generation features of Sympy, making it
possible to generate complex code that can be compiled without manual
intervention.  In particular I wanted to have this functionality available for
quantum mechanical calculations.  The project proposal is available [http://socghop.appspot.com/gsoc/student_project/show/google/gsoc2010/python/t127230762991 here].  More details about this project are available in the
[http://ojensen.wordpress.com blog] that I updated regularly during the
Summer.

# The Summer

In the original project description I was very ambitious about what I wanted
to achieve, but I also think that I have delivered on the most important
parts.  When writing the project proposal I saw a need to spend about half my
time on improving the quantum physics module.  But when it turned out that
there were other GSOC-projects adressing quantum mechanics, my mentor and I
quickly decided that we should focus on the code generation and try to link it
with the physics efforts later on.

## Fortran free-form and a Fortran Code Generator

I started by studying the existing code generation functionality, i.e. the
Fortran and C printers and the codegen utility.  The printers provide the
literal translation of a mathematical expression to a programming language,
while the codegen utility takes care of technical infrastructure, such as
variable declearations.  To get productive early on, and to learn more about
the exisiting framework, I implemented a free-form option to the Fortran
printer as well as a Fortran code generator to complement the exisiting C
generator.  It was inspiring to be able to create new functionality even
though I was still in an early learning phase.

## A new tensor module

Another thing I did early on was to create a page on the Sympy wiki where I
sketched my ideas for better code generation.  This turned out to be a very
good investment of time. In addition to the useful feedback I got from
several people, it is always a good exercise to express thoughts as clearly as
possible in writing.

It soon became clear to me that I had to create new Sympy classes in order to
generate code with array calculations.  I created a new tensor module that
would play a special role for code generation as the way to represent arrays
in the mathematical expressions.  The tensor module ended up providing all the
functionality I originally planned to build into the quantum physics
framework.  In retrospect, having a specialized module for this a much better
solution than building the functionality into the physics framework.  The
tensor module makes array based code generation available to a wide range of
applications.

## Automatic coding, compilation and wrapping

Another tangible product of my project was a utility to automate the process
of generating code, compile it and wrap it as a python callable.   Putting together this module at the end of the summer was particularily rewarding, as it is a small
component that provides easy access to the heavy functionality that I spent
the whole summer implementing.  The autowrap module also includes `ufuncify`, a function that can turn Sympy expressions into fast universal functions for use with numpy arrays.  Here is a plot showing the scaling of execution time of a "ufuncified" sympy expression with the same expression computed as a sequence of native numpy ufuncs:

http://ojensen.files.wordpress.com/2010/08/time_numpy_sympy.png?w=450

As _n_ increases, the complexity of the expression increases, leading to the slowdown. The values of each curve are normalized against the corresponding _n_=1 calculation.  More details about the plot is available in [http://ojensen.wordpress.com/2010/08/10/fast-ufunc-ish-hydrogen-solutions/ this blog post].


# Conclusion and Outlook

I really wish that I could have spent more time developing tests of the framework I built.  There are plenty of tests implemented for the regular test framework in Sympy, but it would be very nice to also have an extensive test case that could verify the complete framework with one single number.  There was not enough time for this, because at the end of the summer I was still in the learning phase with respect the new functionality I had created;  Despite being the author of the framework, I was still experimenting to find out what the autowrapper could do, and what it couldn't.

What became clear at the very end of the Summer, as I was experimenting with 
the outcome, was that the implementation have some limitations.  It is difficult to do array calculations involving composite index expressions, such as a divided difference: `(f[i+1] - f[i])/h`.  Issues like this are expected to show up once a fresh code meets the demands of real life, and confirm only that the work I did should be considered a first version, so there is more to do, and I do plan to continue working on it.

# Acknowledgments

It was very rewarding to work with the Sympy community.  The atmosphere is
friendly and knowledgeable, so it was an excellent opportunity to learn
both math and programming.  Thanks to all who have shared their thoughts by
commenting on mailing lists, blog posts, the wiki and during the code reviews.
In particular I'd like to thank my mentor Andy R. Terrel for useful
discussions and good guidance throughout the Summer.  Thanks also to
Toon Verstraelen for reviewing a sizable portion of my code, and James
Bergstra at the Theano project for an inspiring mail exchange.
Lastly, I wish to express my gratitude towards Google for organizing the Summer
of Code.  I would not have been able to work full time on Sympy this summer
without Google's commitment to sponsor open source software.