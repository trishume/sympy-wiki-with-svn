


# Introduction

This page summarizes the events of my Google Summer of code project
"!SymPy: Multivariate Polynomial Equations and Gröbner Bases". 

# About me

My name's Robert Schwarz and I'm a third year student of mathematics
and computer science at the University of Heidelberg, Germany. I like
abstract math, like algebra and topology, would like to know more
about discrete math and will probably specialize in computer algebra.

# Preparations

I knew of the Google Summer of Code since 2004, but thought that it
was limited to US citizens. On Planet Ubuntu, I learned that I was
wrong and began looking for interesting project suggestions. The
timeline fitted perfectly well for me, as I was still in Paris, at the
end of 2 semesters with the Erasmus exchange program, and had not much
to do from june on. The lectures in Heidelberg don't begin before
october. My roommate then pointed me to the !SymPy project, which I
haven't heard of since then. It was a perfect match, being written in
pure Python, which I had just begun to learn, and with a reasonable
small code base, which I could all read and understand.

At the time, I was about to review some basic algebraic geometry on my
own, with the help of books like "Ideals, Varieties and Algorithms",
which features a lot of examples and computations, besides the
theory. So I suggested some additions to the polynomial module, namely
an implementations of Groebner bases with common applications.

# Code work

My first task was to create a new representation for univariate and
multivariate polynomials. I chose a sparse list, where the entries
contain the coefficient and the exponents of the different
variables. To do that, I had to change the way .expand() works, so I
got quite some insight in the !SymPy core and how things work "under
the hood". Then followed all the items of the applications and some
other stuff I found out, while reading in my books (mainly "Modern
Computer Algebra", besides the one already mentioned).

Some features where quite easily implemented, like the multivariate
division algorithm, and Buchberger's algorithm to compute a Groebner
base. With this, one can also compute multivariate lcm and thus gcds.
This was quite disappointing with respect to efficiency and running
time, especially with the factorization, which is quite limited, as
for now.

All communication was done openly, in the issues and on the mailing
list. By that, all the developers (!SymPy was lucky to get quite some
SoC students) could interact with each other and discuss open
questions. I also enjoyed picking small problems that turned up on the
mailing list, mostly concerning automatic evaluation of products,
powers etc.

Then came the move to the new core. It is more complex, I have not yet
understood everything in the details, but the speed improvements is
really worth it, and I think nearly all features are ported now.

After I restructured the module and the Polynomial class and added
some documentation, at the end of the project timeline, I started with
some modular algorithms. For this, I played with some more lightweight
representation of univariate polynomials in Python dicts, using Python
integers directly. There already is (quite fast) factorization modular
a prime p and some integer polynomial arithmetic.

# Future

It was a lot of fun to work with the !SymPy project (my first free
software project I got really involved in) and am sure to hang around
in the next time. Luckily, there is a lecture about computer algebra
at my university next semester I am going to attend, so there will be
some algorithms to try and implement.

= Administration = 

I'm quite happy with Google's interaction, there wasn't too much
bureaucracy until now and the mailing list provided all necessary
information (mostly for people having problems with the payments). I'm
not sure if I'm going to apply for another project next year, because
most of the organizations focus more on web stuff or desktop
applications (not my area of expertise) but I heavily recommend it to
students wishing to get a nicely organized entry point to free
software development.

Thanks to all developers and thanks to Google!