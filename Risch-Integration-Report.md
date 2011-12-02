


*Note, this report is not complete yet (it is still a work in progress).* 
# About Me

My name is Aaron Meurer.  I am an undergraduate student at New Mexico Tech double majoring in Mathematics and Computer Science.  This is my second year participating in Google Summer of Code.  Last year (2009), I also worked with !SymPy on improving the ODEs module (see the report for that project [http://code.google.com/p/sympy/wiki/ODEsModuleReport here].  
# Introduction

My project was to implement the full Risch Algorithm for Symbolic Integration in !SymPy.  In particular, I worked on implementing the transcendental part of the algorithm.  My work consisted mostly of implementing the algorithms from _[http://books.google.com/books?id=8SAaSd89sSkC&printsec=frontcover&dq=manuel+bronstein&hl=en&ei=Osp6TJK_IJPCsAPJ9oHuCg&sa=X&oi=book_result&ct=result&resnum=1&ved=0CCoQ6AEwAA#v=onepage&q&f=false Symbolic Integration I: Transcendental Functions]_ by Manuel Bronstein.  

Note that this is just an overview of my work this summer.  For more details, see the posts to my [http://asmeurersympy.wordpress.com/ blog], which also include more information on the theory behind the Risch Algorithm.  

You can see a copy of my full application for the project on the !SymPy !MediaWiki [http://wiki.sympy.org/wiki/User:Asmeurer/GSoC2010_Application here].

# GSoC Review

## Beginning

If you are interested in how I originally became involved with !SymPy and Google Summer of Code, you should read my [http://code.google.com/p/sympy/wiki/ODEsModuleReport report] for last year's project. This year, I was already an active developer of !SymPy and already knew the procedures for Google Summer of Code, which helped me to focus on my project itself. 

## The GSoC Period

### Preliminary Work

The Risch Symbolic Integration Algorithm is essentially a bunch of polynomial manipulation algorithms.  Therefore, all of these algorithms that I implemented are based on top of !SymPy's Polys module.  Prior to working on this project, I had only played with the Polys module a little, because I did not use it in my previous project, and because the module was new (it was merged into the !SymPy trunk in March of this same year).  Therefore, the first thing that I decided to do for my project was to familiarize myself with the Polys module in !SymPy.  The Polys module at that point had almost no doctests in the method/function docstrings, So the way that I chose to do this was to write doctests for all the major functions/methods in the Polys module.  This took me about two weeks to fully complete, after which I wrote almost 1000 doctests for the module.  Doing this forced me to understand what each function or method did, and in a way that required enough understanding to write a good doctest for it. In going through the functions and methods in the module, I also stumbled upon several bugs and efficiency problems, and I also added fixes for these in my development branch.  

I also had another good reason for doing this first instead of jumping straight into coding the Risch Algorithm algorithms, which is that I had to get through two chapters of theory in Bronstein's book first before I got to the part that started elaborating and proving the correctness of the algorithm.  

After documenting the Polys module, I still had a little bit to go in Bronstein's book before I got to some things that I could code, so I decided to go through the issues in the issue tracker that were related to integration.  For each of these, I labeled each of them, looked at what needed to be done to fix them, and I created a file of XFAILing tests in my branch for each failing integral, so that the progress for each could be tracked in the future. For a few, I was able to fix a bug or two to make them work.  

One thing that I did also after documenting the Polys module was attempt to rewrite the already existing heuristic Risch integration routine to use the new Polys module.  Now, I was able to successfully recode the function to use the new Polys, but I found that this actually made it _slower_, not faster.  The reason is that that function uses highly multivariate polynomials (hundreds of variables is not uncommon), and the current internal implementation  of polynomials in Poly is inefficient for these (it is a dense representation, rather than a sparse one).  Thus, this implementation was not useful directly, but it did help me to understand how that algorithm works, and also what are the bottlenecks in it that make it so slow (there are two, first, it uses what is currently a slow function is !SymPy, which is expand(), and second, it solves a massive system of linear equations, and solve_linear_system() is not as fast as it could be). 

## Coding the Algorithm

After I did these things, I had made my way in Bronstein's book to the point where there were algorithms that I could implement.  Bronstein's book gives pseudocode for almost all of the algorithms, so that implementing most of them was just a simple matter of translating the code given into !SymPy Python.  

This is how the Transcendental Risch Algorithm works.  

   1. Convert the input expression into a tower of transcendental differential extensions over `Q(x)`.  For example, the expression `exp(exp(1/x)) + log(x)` would first be converted into `exp(t0) + log(x)` over `Q(x, t0)`, where `t0 = exp(1/x)`, then `t1 + log(x)` over `Q(x, t0, t1)`, where `t1 = exp(t0)`, and finally `t1 + t2` over `Q(x, t0, t1, t2)`, where `t2 = log(x)` (see the "Risch Integration Algorithm" series of posts on my [http://asmeurersympy.wordpress.com/ blog] for more information about this).  There is a stipulation that each extension must be transcendental over the previous extensions, and that the derivative of each extension term must be a polynomial in that term and a rational function in the terms already extended (for example `D(t1) = -t1*t0/x**2)`.  
   1. After this step, we recursively perform the following steps on each extension, starting at the top:
     1. Perform some reduction algorithms to the input expression.  Each of these takes in a function and returns two parts.  The first part will be part of the integral of the function, and the second part will need to be integrated (symbolically, it reduces `Integral(f(x), x)` into `g(x) + Integral(h(x), x))`.  In each case, the remaining integral h(x) will be "simpler" in some sense to integrate.  The reduction methods are the Hermite Reduction, the Polynomial Reduction (when it is applicable), and the Residue Criterion/Reduction.  The last of these is also called a criterion because the reduction step might fail, in which case it will have proven that the function does not have an elementary integral.  
     1. Integrating the function that remains after these steps is the most difficult part of the algorithm.  There are three main types of transcendental functions that can be integrated, exponential, primitive, and tangent.  An exponential (or hyperexponential) is a function that satisfies `D(f) = Da*f`, i.e., `f = exp(a)`.  A primitive is a function whose derivative does not contain itself.  The most common example of this is `log()`, because `diff(log(x), x) = 1/x`, which does not have log in it.  `arctan()` also fits in this category.  A tangent (or hypertangent) is a function that satisfies `D(f) = Da*(f**2 + 1)`, i.e., `f = tan(a)`.  

These three types of functions all have specialized algorithms required to integrate them.  Bronstein dedicates a whole chapter of his book to each.  The first is the exponential.  Integrating exponential functions is equivalent to solving what is known as the Risch Differential Equation, which is `Dy + f*y = g`, where `f` and `g` are given.  The primitive case requires solving a similar equation called the Parametric Risch Differential Equation, and the tangent case requires solving what is known as the Coupled DE System, which turns out to also be very similar to the Risch Differential Equation in solving.

### Reduction Algorithms
The reduction algorithms were the first thing that Bronstein covered from the full algorithm, so these are the first things that I coded.  They were not difficult to code, and they provided a good start for the project.   Unfortunately, since they are only reduction algorithms, not full integration routines, they were only able to solve part of integration problems.  Furthermore, I had not yet coded the preparsing step (step 1), so all input to the algorithms had to be parsed by hand, which was a little meticulous, and not very good for showing them off.  

After doing this, I began to realize that I had made a few design mistakes in the API.  I still had only a rudimentary understanding of the recursive nature of the algorithm, so I originally coded the algorithms to only accept on extension, instead of arbitrarily many.  I soon realized this, and after figuring out how it should work in the general case, I made it accept a list of elements instead of just one.  This required going through and changing all the algorithms that I had written up to that point, which was a bit time consuming, but it was the correct way.  A little later in my work, I also realized that I made an additional mistake by treating x (the integration variable) separately from the other extensions, so I had to go through again at that point and change everything again.  

### Reduced Integral Algorithms
After doing the reduction algorithms, I started to work on the next thing in Bronstein's book, which was the Risch Differential Equation problem (recall that this is required to integrate exponential functions).  This algorithm is very long and meticulous, and requires breaking the problem down bit by bit until it finally reaches a form that can be easily solved.  At many points along the way, the algorithm may reach a mathematical inconsistency, which means that it will have proven that the integral is non-elementary.  Fortunately, every algorithm was given in pseudocode, so implementing this was again only a matter of translation in most cases (of course, I still needed to understand how each algorithm worked, so I had to read the proofs preceding each algorithm).  

Many parts of this problem requires further subproblem algorithms to solve, so when I finally finished and got a working version, many cases did not work (raised !NotImplementedError).  

The Parametric Risch Differential Equation algorithm (primitive case) was much more difficult to implement.  As the name suggests, the equation is very similar to the Risch Differential Equation, except the right hand side is parameterized, i.e., it is given as a linear combination of a finite number of terms with unknown constant coefficients.  This means that solving the problem requires first determining what constants in the linear combination could produce a solution, and then solving it (which is then just solving the Risch Differential Equation again).  Unfortunately, the constants themselves might have parametrized solutions, i.e., there might be an infinite number of solutions.  This is all workable because of linear algebra, but for whatever reason, at this point in the book, Bronstein started breaking down and not providing pseudocode for all the algorithms.  I reached a couple of points where I could not figure out how some matrix/linear algebra related step was supposed to work.  Also, the subalgorithms for this section were given out of order.  In the end, I never completely put together all the subalgorithms, so that only a subset of the problem is implemented (when there is a one-dimensional nullspace for the constants).  So all the subalgorithms are just sitting there in the file, waiting for me to get back to them to figure out how they go together properly.  

The tangent case I did not get to at all.  However, I should note that I plan on completing everything even though the program has finished.

### Building the Tower of Extensions

The main reason that I settled for only partially complete implementations in the reduced integral algorithms is that I wanted to have a function that would work from the user's point of view, like the current `integrate()` does. Doing this required implementing step 1, which is actually covered last in Bronstein's book.  Of all the algorithms given in the book, this one was the least explicitly given.  Rather, he spent a log time on the theory behind the algorithm, which is very interesting, but the algorithm is only stated as following directly from an important theorem called Risch's Structure Theorems.  

Basically, the transcendental risch algorithm is very picky.  Every extension has to be transcendental over all the previous extensions.  This excludes algebraic functions from the algorithm, but it also presents difficulties due to exponential and logarithmic identities.  For example, `exp(x + x**2) == exp(x)*exp(x**2)`, so we add `exp(x)` and `exp(x**2)`, we have to then rewrite `exp(x + x**2)` in terms of them using the above formula.  It can get more complicated when you use both logarithms and exponential.  For example, we cannot integrate `exp(log(x)/2)` using the transcendental algorithm, because even though it appears to be transcendental, it is equal to `sqrt(x)`.   The Risch Structure Theorems give explicit formulations for when a new exponential of logarithm is algebraic over the previous ones.  The theorem involves determining if an equation has solutions in rational numbers.  

The algorithms were a little more tricky to implement than any of the ones I had done since, because they were not explicitly given.  I also had to figure out a way to pull out constant factors, which was not difficult, but something that I didn't realize that I needed to do at first.  

After doing this, there was basically one more step, which was to write the function that parsed an expression and tried to build an extension from it, using the structure theorems to ensure that each extension is transcendental.  This was by far the most difficult thing I did the summer, and the function that I ended up with is quite complex.  The reason is that, if we have a function like `exp(x) + exp(x/2)` and start with `exp(x)`, we will find by the structure theorems that `exp(x/2) == sqrt(exp(x))`, which is algebraic.  But the algorithm actually shouldn't give up, because if it had started with `exp(x/2)` instead, it would have gotten `exp(x) == exp(x/2)**2`, which is just fine because it is a rational function.  Therefore, I had to handle everything in such a way that it only gives up on algebraic radical exponentials if they really cannot be dealt with by the transcendental algorithm (such as `exp(log(x)/2)`).  

### The `ricsh_integrate()` Prototype Function
So after I got this, I was able to put everything together into a function called `risch_integrate()`, which works at a user level.  The user simply has to enter something like `risch_integrate(exp(x)*log(x) + exp(x)/x, x)` to get a result (in this case `exp(x)*log(x)`). Now this was great, because people could play around with the function and give me feedback on any bugs that they find.  For example, Christian Muise, who did the [SuperchargingAssumptionsReport SAT Solving/Assumptions] GSoC project this year, wrote a simple random function generator to pass to it that found half a dozen bugs.  It also helped me myself to find many bugs, since it made entering functions much easier.  

As of this writing, this is where things stand.  The `risch_integration()` function still sits in my [http://github.com/asmeurer/sympy/tree/integration3 integration3] branch at !GitHub.  None of the changes have been merged in with the official repository, as I have not actually finished the algorithm yet.  Feel free to pull the branch and play around with it.

## Examples
In my [http://wiki.sympy.org/wiki/User:Asmeurer/GSoC2010_Application application to Google], I cited two problems with the existing integrator in !SymPy, which is based on Bronstein's Poor Man's Integrator, and is also knowns as the parallel or heuristic Risch Algorithm.  I shall refer to it hereafter by its internal name `heurisch()`, but understand that this is what you get by calling `integrate()` in `SymPy` at the present time.  

The first factor was speed.  For non-trivial integrals, the heurisch algorithm could easily take as much as ten minutes to complete, and for more complicated ones, it would never terminate.  When I worked on the heurisch function at the beginning of the summer (see the Preliminary Work section above), I soon discovered why this was.  First, it was using the built in arithmetic for polynomial manipulation instead of the new Polys module, which is much faster.  But more importantly, the algorithm works by setting up a candidate integral and solving for coefficients.  For these non-trivial integrals, this might involve solving a system of 400 linear equations in 1000 variables, which is way too much for !SymPy's sobers to handle in any kind of reasonable amount of time.  This is simply the nature of the heuristic algorithm.  

The second factor was the ability to compute anti-derivatives.  For many integrals, some not even very complicated, the heurisch would simply fail.  This again was due to the nature of the algorithm--because it is only a heuristic and not a complete algorithm.

Well, with the `risch_integrate()`, I was able to see directly how the new algorithm compared in these two aspects.  Now, for the second, it is clearly a winner.  Except for the cases I have not implemented yet, it can *always* find an anti-derivative.  In fact, if the function does not have an elementary anti-derivative, it can prove this.  Whenever `risch_integrate()` returns an unevaluated `Integral()`, it means that it has proven this to be so.  

The second one, I was not so sure about.  The Risch Algorithm is very complicated, and I was half expecting it to be very slow in the general case.  But in fact, it is actually very fast.  For example, Bronstein suggests using the Heuristic Risch Algorithm as a fast preparser to the full algorithm, but it is clear to me that the full algorithm is *always* faster than the heuristic, and in many cases, *much* faster.

Here are some examples that demonstrate this.  Remember that `integrate()` is the old integrator and `risch_integrate()` is the new one:

*An example of a simple integral that the old engine could not handle but the new one can.*

``` 
In [1]: integrate(2*log(x)/x, x)
Out[1]: 
⌠            
⎮ 2⋅log(x)   
⎮ ──────── dx
⎮    x       
⌡            

In [2]: risch_integrate(2*log(x)/x, x)
Out[2]: 
   2   
log (x) 
```

*An example of a more complex integral that causes the old engine to hang but that the new one handles fine.*
(Taken from _Algorithms for Computer Algebra_ by Keith O. Geddes, Stephen R. Czapor, and George Labahn, pg. 534.)

```

In [3]: f = (x*(x + 1)*((x**2*exp(2*x**2) - log(x + 1)**2)**2 +
   ...:     2*x*exp(3*x**2)*(x - (2*x**3 + 2*x**2 + x + 1)*log(x + 1))))/((x +
   ...:     1)*log(x + 1)**2 - (x**3 + x**2)*exp(2*x**2))**2

In [4]: f
Out[4]: 
          ⎛                          2                                                   ⎞
          ⎜⎛                       2⎞                                                   2⎟
          ⎜⎜     2           2  2⋅x ⎟        ⎛    ⎛           2      3⎞           ⎞  3⋅x ⎟
x⋅(1 + x)⋅⎝⎝- log (1 + x) + x ⋅ℯ    ⎠  + 2⋅x⋅⎝x - ⎝1 + x + 2⋅x  + 2⋅x ⎠⋅log(1 + x)⎠⋅ℯ    ⎠
──────────────────────────────────────────────────────────────────────────────────────────
                                                                2                         
                         ⎛                                    2⎞                          
                         ⎜   2                  ⎛ 2    3⎞  2⋅x ⎟                          
                         ⎝log (1 + x)⋅(1 + x) - ⎝x  + x ⎠⋅ℯ    ⎠                          

In [5]: risch_integrate(f, x)
Out[5]: 
       ⎛              ⎛ 2⎞⎞                   ⎛                ⎛ 2⎞⎞                             
       ⎜log(1 + x)    ⎝x ⎠⎟                   ⎜  log(1 + x)    ⎝x ⎠⎟          ⎛ 2⎞               
    log⎜────────── + ℯ    ⎟                log⎜- ────────── + ℯ    ⎟       2  ⎝x ⎠               
       ⎝    x             ⎠                   ⎝      x             ⎠      x ⋅ℯ    ⋅log(1 + x)    
x + ─────────────────────── - log(1 + x) - ───────────────────────── + ──────────────────────────
               2                                       2                                        2
                                                                              2           3  2⋅x 
                                                                       - x⋅log (1 + x) + x ⋅ℯ    

In [6]: %timeit risch_integrate(f, x)
1 loops, best of 3: 2.21 s per loop

In [7] integrate(f, x)
<hangs>
```

So we can see that not only can `risch_integrate()` handle this rather complicated integrand in a reasonable amount of time, but the old engine has no chance of doing it.  Even if you let `[7]` run for several hours, it will not complete.  

* Some examples of some integrals that `risch_integrate()` can prove to be non-elementary.*

These are some of the most famous non-elemetary integrals.

```
In [8]: risch_integrate(exp(-x**2), x)
Out[8]: 
⌠        
⎮    2   
⎮  -x    
⎮ ℯ    dx
⌡        

In [9]: risch_integrate(exp(exp(x)), x)
Out[9]: 
⌠         
⎮  ⎛ x⎞   
⎮  ⎝ℯ ⎠   
⎮ ℯ     dx
⌡         

In [10]: risch_integrate(1/log(x), x)
Out[10]: 
⌠          
⎮   1      
⎮ ────── dx
⎮ log(x)   
⌡          

In [11]: risch_integrate(exp(x)/x, x)
Out[11]: 
⌠      
⎮  x   
⎮ ℯ    
⎮ ── dx
⎮ x    
⌡      

In [12]: risch_integrate(exp(x*log(x)), x)
Out[12]: 
⌠             
⎮  x⋅log(x)   
⎮ ℯ         dx
⌡             
```

The last function is `x**x`.  Whenever `risch_integrate()` returns an unevaluated `Integral`, it means that it has proven that the function does not have an elementary integral (it will raise `NotImplementedError` if it fails).  This is quite different from the old `heurisch()` in `integrate()`, for which an unevaluated Integral could mean that the integrand does not have an elementary anti-derivative, or it could just mean that the routine failed.  

But this is not the most amazing part, because the engine can also split an integral into elementary and non-elementary parts in many cases.  Thus, it will return a partially integrated result.  For example:

```

In [13]: (1 + 2*x**2 + x**4 + 2*x**3*exp(2*x**2))/(x**4*exp(x**2) + 2*x**2*exp(x**2) + exp(x**2))
Out[13]: 
                           2 
         2    4      3  2⋅x  
  1 + 2⋅x  + x  + 2⋅x ⋅ℯ     
─────────────────────────────
    ⎛ 2⎞         ⎛ 2⎞    ⎛ 2⎞
 4  ⎝x ⎠      2  ⎝x ⎠    ⎝x ⎠
x ⋅ℯ     + 2⋅x ⋅ℯ     + ℯ    


In [14]: risch_integrate((1 + 2*x**2 + x**4 + 2*x**3*exp(2*x**2))/(x**4*exp(x**2) + 2*x**2*exp(x**2) + exp(x**2)), x)
Out[14]: 
⌠            ⎛ 2⎞ 
⎮    2       ⎝x ⎠ 
⎮  -x       ℯ     
⎮ ℯ    dx + ──────
⌡                2
            1 + x 
```

As you can see, `risch_integrate()` was able to split the integral into `exp(x**2)/(x**2 + 1)` and the integral of `exp(-x**2)` (which it has proven to be non-elementary).  Actually, the old `integrate()` hangs on this integral, but if it didn't, it would just return an unevaluated `Integral` for the whole thing, since the `Integral(exp(-x**2), x)` makes the whole integral non-elementary.

* Some examples of the time differences between the old `integrate()` and `risch_integrate()`*