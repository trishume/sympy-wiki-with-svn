

# GCI-2011 Task list


The source if this page is based on the [google-malange](https://docs.google.com/spreadsheet/ccc?key=0AiMKW-ZM-_fedFpSWm51VFBFZkdTRnh3WkhYRndSVXc#gid=0) spreadsheet.

## Categories

<ul>
<li><a href="##Hard">Hard</a>
<ul>
<li><a href="##93">Square root denesting</a></li>
<li><a href="##2319">LaTeX input</a></li>
<li><a href="##2626">Piecewise should use a different syntax for "otherwise"</a></li>
<li><a href="##2773">Implement the trigsimp algorithm by fu et al</a></li>
<li><a href="##2789">minpoly should work with roots of unity in exponential form</a></li>
<li><a href="##1594">bin/test --random should also shuffle tests inside a file</a></li>
<li><a href="##2791">Allow to manage slow tests better with our test runner</a></li>
<li><a href="##2799">coverage testing should be part of the bot test</a></li>
<li><a href="##2812">Fix failures found by shuffling tests in test file</a></li>
<li><a href="##1941">Objects that know how to combine themselves</a></li>
<li><a href="##2765">Research ways to do the assumptions system, including removing the old system</a></li>
<li><a href="##2792">Investigate how to employ complexity measures in functions like trigsimp(), etc.</a></li>
<li><a href="##1817">SymPy Cheat Sheet</a></li>
<li><a href="##2771">Write a document showing the difference between SymPy and other mathematical systems: Maple</a></li>
<li><a href="##2521">live.sympy.org isn't so easy to use on a mobile device</a></li>
<li><a href="##2768">Add a feed of what people are doing at SymPy Live</a></li>
<li><a href="##2772">Some UI/GUI for the test runner</a></li>
</ul>
</li>
<li><a href="##Medium">Medium</a>
<ul>
<li><a href="##281">Infinity should not be a subclass of Rational</a></li>
<li><a href="##363">Add a split() method for sympy expressions</a></li>
<li><a href="##716">either tangent_line or is_tangent is wrong</a></li>
<li><a href="##754">Have re and im call expand(complex=True)</a></li>
<li><a href="##2513">Create a SymPyDeprecationWarning for deprecated SymPy behavior</a></li>
<li><a href="##2552">(1/(x*y)).subs(x*y, whatever) doesn't work</a></li>
<li><a href="##2632">Add isympy -c qtconsole</a></li>
<li><a href="##2793">The dsolve solver for 1st_exact should use integration</a></li>
<li><a href="##2794">Implement ode solvers from the Moses "Stormy Decade" paper: Almost Linear</a></li>
<li><a href="##2841">integrate() can not integrate the Abs() function, fix it</a></li>
<li><a href="##2849">Better heuristics and simplification for integral of cos(x)/sin(x)**n and similar</a></li>
<li><a href="##294">Pass coverage_doctest.py</a></li>
<li><a href="##707">move some wikis to github.com/sympy/sympy/wiki</a></li>
<li><a href="##2470">Fix all sphinx errors and warnings</a></li>
<li><a href="##2770">Update stuff that SymPy can do on the homepage</a></li>
<li><a href="##2779">``See Also`` feature in Geometry</a></li>
<li><a href="##2801">lambdify() is not mentioned anywhere</a></li>
<li><a href="##2528">Update SymPy's Wikipedia article</a></li>
<li><a href="##2764">Improve our webpage</a></li>
<li><a href="##2787">Create sticker for SymPy based on the logo</a></li>
<li><a href="##2796">Package the latest version of SymPy for the major distributions: Debian / Ubuntu</a></li>
<li><a href="##1456">use pyflakes to identify simple bugs in sympy and fix them</a></li>
<li><a href="##1752">setup.py test should run the doctests even when the regular tests fail</a></li>
<li><a href="##2786">Fill in missing tests for sympy.physics module in test_args.py</a></li>
<li><a href="##1235">Problem installing in Windows</a></li>
<li><a href="##2762">Investigate ways to improve substitution, pattern matching, etc.</a></li>
<li><a href="##2795">Investigate a robust way to have translated documentation</a></li>
<li><a href="##2798">Research ways to extract statistics from the issue tracker</a></li>
<li><a href="##2803">Investigate how to make the rewrite framework more flexible</a></li>
<li><a href="##2790">Create examples/short tutorials using IPython's notebook (IPython >= 0.12)</a></li>
<li><a href="##2766">Translate tutorial to German</a></li>
<li><a href="##2767">Improve the interface of SymPy Live</a></li>
<li><a href="##2857">sqrt(2).is_irrational is None (should be True)</a></li>
</ul>
</li>
<li><a href="##Easy">Easy</a>
<ul>
<li><a href="##615">Fix the occasions where functions are called with wrong name and write tests</a></li>
<li><a href="##654">Remove dead code from _eval_subs()</a></li>
<li><a href="##1058">Classifying formulas</a></li>
<li><a href="##2276">integrate() should use the ode module's undetermined coefficients solver when possible</a></li>
<li><a href="##2427">Check for incorrect usage of expr.atoms() and change it to free_symbols</a></li>
<li><a href="##2534">Use "with open" instead of "open … close"</a></li>
<li><a href="##2570">Remove bare except statements</a></li>
<li><a href="##2639">The Product() class should not evaluate by default</a></li>
<li><a href="##2683">det() is called when inverting matrix through GE</a></li>
<li><a href="##2760">latex(symbol_names) not working with ~x</a></li>
<li><a href="##2776">``See Also`` feature in integrals</a></li>
<li><a href="##2784">1/function() should be printed differently by latex printer</a></li>
<li><a href="##2785">Use \functionname instead of \operatorname{functionname} whenever possible</a></li>
<li><a href="##2815">Parts of the pyglet plotting module does not follow PEP 8, fix it</a></li>
<li><a href="##2817">Make sure all the built-in __methods__ are defined</a></li>
<li><a href="##2830">checkodesol() should use force=True</a></li>
<li><a href="##2838">Move the KroneckerDelta class to another module </a></li>
<li><a href="##2846">Integral.transform should allow a change to a different variable</a></li>
<li><a href="##16">Check and compare an old patch concerning object with indices against current sympy</a></li>
<li><a href="##1886">Documentation for the Expr class</a></li>
<li><a href="##2115">Move stuff from the Google Code SVN to git</a></li>
<li><a href="##2160">List of dependencies</a></li>
<li><a href="##2204">Document why unpickling a singleton doesn't return the singleton object with protocol 0 and 1</a></li>
<li><a href="##2367">SymPy's readthedocs documentation is broken</a></li>
<li><a href="##2597">Import all public functions and classes into Sphinx: polys</a></li>
<li><a href="##2599">Update isympy manpage</a></li>
<li><a href="##2679">Refactor GA* documentation to use doctests (or move it to examples/)</a></li>
<li><a href="##2774">``See Also`` feature in Number Theory</a></li>
<li><a href="##2775">``See Also`` feature in Combinotorics </a></li>
<li><a href="##2777">``See Also`` feature in functions</a></li>
<li><a href="##2778">``See Also`` feature in functions/special</a></li>
<li><a href="##2780">``See Also`` feature in Matrices</a></li>
<li><a href="##2763">Fix the SymPy Logo</a></li>
<li><a href="##2800">Flesh out the SymPy Papers wiki page</a></li>
<li><a href="##1616">Bug in subs</a></li>
<li><a href="##2493">Clean up test_lambdify.py</a></li>
<li><a href="##2788">Commented out tests should be XFAILed</a></li>
<li><a href="##2157">sympy development rules</a></li>
<li><a href="##2769">Make video tutorials for SymPy</a></li>
<li><a href="##2806">Add more tips to the tips page (10 tips)</a></li>
<li><a href="##2797">Translate our webpage to German</a></li>
<li><a href="##2797">Translate our webpage to French</a></li>
<li><a href="##2797">Translate our webpage to Czech</a></li>
<li><a href="##2797">Translate our webpage to Polish</a></li>
<li><a href="##2797">Translate our webpage to Bulgarian</a></li>
<li><a href="##2797">Translate our webpage to Serbian</a></li>
<li><a href="##2637">Unicode Sigma for pretty printed Sum</a></li>
<li><a href="##2636">Pretty print Product</a></li>
</ul>
</li>
</ul>

## <a name="#Hard">Hard</a>
<a name="#93"></a>
### [93](http://code.google.com/p/sympy/issues/detail?id=93&q=label%3ACodeInImportedIntoSpreadsheet) - Square root denesting

Just an idea: implement the "square root denesting" ideas of
<a href="http://www.almaden.ibm.com/cs/people/fagin/symb85.pdf" rel="nofollow">http://www.almaden.ibm.com/cs/people/fagin/symb85.pdf</a>
doesn't look to complicated.


 

- *Category:* Code
- *Time to complete:* 144 hours

<a name="#2319"></a>
### [2319](http://code.google.com/p/sympy/issues/detail?id=2319&q=label%3ACodeInImportedIntoSpreadsheet) - LaTeX input

So my friend pointed out to me that WolphramAlpha lets you enter any LaTeX formula, and it will parse it and evaluate it.  I think we should have a parser that lets us do the same thing. In his case, he takes notes in LaTeX and does all of his homework in it, and he was able to just paste an expression from his homework into WolphramAlpha and it did if for him. 

- *Category:* Code
- *Time to complete:* 144 hours

<a name="#2626"></a>
### [2626](http://code.google.com/p/sympy/issues/detail?id=2626&q=label%3ACodeInImportedIntoSpreadsheet) - Piecewise should use a different syntax for "otherwise"

This is something that's been bothering me for a while.  Piecewise has the following syntax (I quote the docstring):

```
Usage
=====
  Piecewise( (expr,cond), (expr,cond), ... )
    - Each argument is a 2-tuple defining a expression and condition
    - The conds are evaluated in turn returning the first that is True.
      If any of the evaluated conds are not determined explicitly False,
      e.g. x < 1, the function is returned in symbolic form.
    - If the function is evaluated at a place where all conditions are False,
      a ValueError exception will be raised.
    - Pairs where the cond is explicitly False, will be removed.

Examples
========
  >>> from sympy import Piecewise, log
  >>> from sympy.abc import x
  >>> f = x**2
  >>> g = log(x)
  >>> p = Piecewise( (0, x<-1), (f, x<=1), (g, True))
  >>> p.subs(x,1)
  1
  >>> p.subs(x,5)
  log(5)
```

The problem is the use of (g, True) for the "otherwise" condition.  The problem is that if a conditional reduces to True, then this will be interpreted as an "otherwise" condition rather than returning it.  

```py
>>> Piecewise((f(x), x < 0), (x, 1 > 0))
⎧f(x)  for x < 0
⎨               
⎩ x    otherwise
```


This is also inconsistant in that it treats it correctly if only one condition is given:

```py
>>> Piecewise((x, 1 > 0))
x

```
 

- *Category:* Code
- *Time to complete:* 144 hours

<a name="#2773"></a>
### [2773](http://code.google.com/p/sympy/issues/detail?id=2773&q=label%3ACodeInImportedIntoSpreadsheet) - Implement the trigsimp algorithm by fu et al

Implement the algorithm for trigonometric simplification from the paper "Automated and readable simplification of trigonometric expressions" by Fu, et. al. (you should be able to find the paper for free from Google Scholar, otherwise email me and I will send it to you).
 

- *Category:* Code
- *Time to complete:* 144 hours

<a name="#2789"></a>
### [2789](http://code.google.com/p/sympy/issues/detail?id=2789&q=label%3ACodeInImportedIntoSpreadsheet) - minpoly should work with roots of unity in exponential form


```py
>>> minpoly(exp(I*pi/8))
ERROR: An unexpected error occurred while tokenizing input
The following traceback may be corrupted or invalid
The error message is: ('EOF in multi-line statement', (16, 0))
---------------------------------------------------------------------------

/Users/aaronmeurer/Documents/python/sympy/sympy/sympy/polys/numberfields.pyc in bottom_up_scan(ex)
    117                 return symbols[ex.root]
    118 
--> 119         raise NotAlgebraic("%s doesn't seem to be an algebraic number" % ex)
    120 
    121     polys = args.get('polys', False)

NotAlgebraic: exp(I*pi/8) doesn't seem to be an algebraic number
```

But this is a root of `x**16 - 1`.  I don't know how minpoly works internally if this can be done in a general fashion for exponentials nested inside other expressions (like e.g., `sqrt(1 + exp(I*pi/8)))`.

Marking as Code-In difficulty hard because this is a nontrivial algorithm, especially for a high school student.
 

- *Category:* Code
- *Time to complete:* 144 hours

<a name="#1594"></a>
### [1594](http://code.google.com/p/sympy/issues/detail?id=1594&q=label%3ACodeInImportedIntoSpreadsheet) - bin/test --random should also shuffle tests inside a file
Also it is related with issue 1594: once we have the shuffling, we should fix all the failures caused by it. Marking this as a hard task for Code-In, per Aaron's comment on the other issue. 


Currently it only shuffles the test files, not the test functions. 

- *Category:* QA
- *Labels:* Priority-Medium, Testing, Type-Defect
- *Time to complete:* 144 hours

<a name="#2791"></a>
### [2791](http://code.google.com/p/sympy/issues/detail?id=2791&q=label%3ACodeInImportedIntoSpreadsheet) - Allow to manage slow tests better with our test runner
Currently slow tests are simply skipped, but this makes it hard to actually run them. There should be a decorator for this (e.g. @slow) that would all to to run such tests when give an extra option to bin/test or test() (--slow and slow=True, respectively). It should be also possible to specify a timeout for slow tests so that they do not hang test runner. It should be also possible to press Ctrl+C (KeyboardInterrupt) to kill a slow test without killing test runner. There should be statistics added at the end which would tell how many slow tests were run, how many timed out and maybe other. Also, almost all skipped tests (or maybe all) are currently skipped because they are slow, so after this is implemented, they should all be converted. 


Currently slow tests are simply skipped, but this makes it hard to actually run them. There should be a decorator for this (e.g. @slow) that would all to to run such tests when give an extra option to bin/test or test() (--slow and slow=True, respectively). It should be also possible to specify a timeout for slow tests so that they do not hang test runner. It should be also possible to press Ctrl+C (KeyboardInterrupt) to kill a slow test without killing test runner. There should be statistics added at the end which would tell how many slow tests were run, how many timed out and maybe other. 

- *Category:* QA
- *Labels:* Priority-Medium, Testing, Type-Enhancement
- *Time to complete:* 144 hours

<a name="#2799"></a>
### [2799](http://code.google.com/p/sympy/issues/detail?id=2799&q=label%3ACodeInImportedIntoSpreadsheet) - coverage testing should be part of the bot test

Two things on my wish list for testing;

1) a coverage fingerprint of master would be compared to a given branch's coverage profile to make sure that no line has become uncovered.

2) a report of lines added that are not covered would be reported with the test-bot report.

Someone who likes parsing html ([beautiful soup](www.crummy.com/software/BeautifulSoup/) might help with this) might enjoy this as a project.
 

- *Category:* QA
- *Labels:* Priority-Medium, Testing, Type-Enhancement
- *Time to complete:* 144 hours

<a name="#2812"></a>
### [2812](http://code.google.com/p/sympy/issues/detail?id=2812&q=label%3ACodeInImportedIntoSpreadsheet) - Fix failures found by shuffling tests in test file

This builds on [issue 1594](http://code.google.com/p/sympy/issues/detail?id=1594): once we have the shuffling, we should fix all the failures caused by it. Marking this as a hard task for Code-In, per Aaron's comment on the other issue.
 

- *Category:* QA
- *Time to complete:* 144 hours

<a name="#1941"></a>
### [1941](http://code.google.com/p/sympy/issues/detail?id=1941&q=label%3ACodeInImportedIntoSpreadsheet) - Objects that know how to combine themselves

This is related to <a title="more efficient core"  href="/p/sympy/issues/detail?id=1908">issue 1908</a>.  When I met with Ondrej last summer, we worked on a core where 
objects knew how to combine themselves with respect to Mul and Add.  See the handler branch at 
<a href="http://github.com/certik/sympyx/" rel="nofollow">http://github.com/certik/sympyx/</a>.  The idea originally stemmed from <a title="Arbitrary constant type"  href="/p/sympy/issues/detail?id=1336">issue 1336</a>, but we soon 
discovered that it also simplifies the logic for things like O() (the order function), and oo, which 
combine abnormally with respect to Mul and Add.  This could also be useful for <a title="Improvements for physical units"  href="/p/sympy/issues/detail?id=1940">issue 1940</a>, so that 
the units could tell Mul that they need to stay together without Mul explicitly having to know about 
units.  Right now, Mul.flatten is cluttered with code for handling all these things, and the only way 
to handle additional classes is to either completely separate them from Basic (as with Poly), or to 
add more special case code in Mul.flatten.  

Anyway, if we ever rework the core as suggested in <a title="more efficient core"  href="/p/sympy/issues/detail?id=1908">issue 1908</a> or elsewhere, we should also look into doing this too.
 

- *Category:* Research
- *Time to complete:* 144 hours

<a name="#2765"></a>
### [2765](http://code.google.com/p/sympy/issues/detail?id=2765&q=label%3ACodeInImportedIntoSpreadsheet) - Research ways to do the assumptions system, including removing the old system

See https://github.com/sympy/sympy/wiki/Assumptions and some threads on the mailing list, as well as any issue with the Assumptions label.  We have two assumptions systems in SymPy, the old system, which works like 

```
>>> x = Symbol('x', positive=True)
>>> x.is_positive
True
```

and the new system, which works like

```
>>> ask(Q.positive(x), Q.positive(x))
True
```
 

- *Category:* Research
- *Labels:* Assumptions, 
- *Time to complete:* 144 hours

<a name="#2792"></a>
### [2792](http://code.google.com/p/sympy/issues/detail?id=2792&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate how to employ complexity measures in functions like trigsimp(), etc.

`simplify()` already implements measure argument and uses it to choose over alternative expressions given by pairs of specific simplification routines. However, those specific simplification routines (like `trigsimp()`) don't support measure argument and make arbitrary built-in choices when simplifying expressions. This leads to simplification results that are dependent on the implicit measure built-in into a particular simplification step of a function. Those functions should use a measure to verify whether a candidate simplified expression is really simpler than an input expression. Investigate how to implement measures in those functions (at least in `trigsimp()`) to avoid combinatorial explosion of choices. You may have to employ optimization techniques like greedy algorithms, dynamic programming, meta heuristics, etc. Prepare sample non-trivial inputs, measures and outputs that can be used as tests for the algorithm(s) you will propose.
 

- *Category:* Research
- *Time to complete:* 144 hours

<a name="#1817"></a>
### [1817](http://code.google.com/p/sympy/issues/detail?id=1817&q=label%3ACodeInImportedIntoSpreadsheet) - SymPy Cheat Sheet

See [maillist](http://groups.google.com/group/sympy/browse_thread/thread/f3b1ddc8b6333748)

The idea is to make a cheat sheet for sympy, similar to PSageMath quickref](http://wiki.sagemath.org/quickref)

 

- *Category:* Training
- *Time to complete:* 144 hours

<a name="#2771"></a>
### [2771](http://code.google.com/p/sympy/issues/detail?id=2771&q=label%3ACodeInImportedIntoSpreadsheet) - Write a document showing the difference between SymPy and other mathematical systems: Maple

We should document the differences between SymPy and other mathematical systems.  For Code-In, a task should be for one other system. 

- *Category:* Training
- *Time to complete:* 144 hours

<a name="#2521"></a>
### [2521](http://code.google.com/p/sympy/issues/detail?id=2521&q=label%3ACodeInImportedIntoSpreadsheet) - live.sympy.org isn't so easy to use on a mobile device

I tried the new live.sympy.org on my 1st gen iPod touch (iOS 3).  There are a couple of things that make the usage difficult:

- Pressing both "Return" and "Shift-Return" on the keyboard just creates a newline in the input, regardless of whether the "Enter/Shift-Enter" popup is set to.  You can still enter the expression by pressing the "Evaluate" button, but it would be nice if the keyboard worked.

- There's no way to access the history.  There is no "Control" key on an iPod touch.

- You cannot scroll within a frame in mobile Safari, so you can't access the history of the session beyond a few inputs.

- This may be an inherent problem with the fonts in iOS, but the unicode output of the result of `dsolve(f(x).diff(x, x) + 2*f(x).diff(x) + f(x) - exp(x) + sin(x), f(x))` is a little off.  I'm happy to report that the LaTeX output works great, though.

- There are a few minor issues with the size of things, which would be fixed the best if there were a mobile version of the site.  But this is a lower priority.  If the above items can be fixed, the site as it is will work just fine in a mobile environment.
 

- *Category:* UI
- *Time to complete:* 144 hours

<a name="#2768"></a>
### [2768](http://code.google.com/p/sympy/issues/detail?id=2768&q=label%3ACodeInImportedIntoSpreadsheet) - Add a feed of what people are doing at SymPy Live
It would be cool to have a little feed at the right on live.sympy.org to show what other people are entering, so that people can see what sorts of things are being done.  


It would be cool to have a little feed at the right on live.sympy.org to show what other people are entering, so that people can see what sorts of things are being done.  Of course, you should be able to disable this for your own entries, for privacy reasons.  It should allow you to input the same expression in your session and execute it. 

- *Category:* UI
- *Labels:* Live, Priority-Medium, Type-Defect
- *Time to complete:* 144 hours

<a name="#2772"></a>
### [2772](http://code.google.com/p/sympy/issues/detail?id=2772&q=label%3ACodeInImportedIntoSpreadsheet) - Some UI/GUI for the test runner

It would be cool to have some UI/GUI for the test runner that makes it easier to see the failures when they happen. 

- *Category:* UI
- *Labels:* Priority-Medium, Type-Enhancement
- *Time to complete:* 144 hours

It would be cool to have some UI/GUI for the test runner that makes it easier to see the failures when they happen. E.g. like http://sourceforge.net/apps/mediawiki/cppunit/nfs/project/c/cp/cppunit/c/c2/Qttestrunner_exa.png  

## <a name="#Medium">Medium</a>
<a name="#281"></a>
### [281](http://code.google.com/p/sympy/issues/detail?id=281&q=label%3ACodeInImportedIntoSpreadsheet) - Infinity should not be a subclass of Rational


```py
>>> isinstance(oo, Rational)
True
>>> oo.is_rational
True
```

This is clearly wrong. Infinity is not a rational number.
 

- *Category:* Code
- *Time to complete:* 96 hours

<a name="#363"></a>
### [363](http://code.google.com/p/sympy/issues/detail?id=363&q=label%3ACodeInImportedIntoSpreadsheet) - Add a split() method for sympy expressions

I think a method that does the opposite of reduce(operator, [x,y,...])
would be useful. Something like this:

```py
>>> (x+y+z).split('+')
(x, y+z)
>>> (x+y+z).split('+', flatten=True)
(x, y, z)
```

Various keyword arguments could be added for whether to split rational
numbers, etc. With such options, split() could replace several existing
methods like as_coefficient, as_independent, as_base_exp, as_numer_denom,
etc. It is better to only have to remember a single method.

Using an operator symbol like '+' as argument instead of a class is my
preference as it would be more readable and more versatile ('/' can be used
even though we have no Div class).

A method like this would be especially useful if Add and Mul are changed as
discussed in [issue 362: Possible speed improvements to core](http://code.google.com/p/sympy/issues/detail?id=362), as its interface would be independent of the
underlying representation.
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#716"></a>
### [716](http://code.google.com/p/sympy/issues/detail?id=716&q=label%3ACodeInImportedIntoSpreadsheet) - either tangent_line or is_tangent is wrong


```py
In [1]: e = Ellipse(Point(0,0), 3, 2)

In [2]: t = e.tangent_line(e.random_point())

In [3]: e.is_tangent(t)
Out[3]: False
```

Obviously [2] and [3] are in contradiction. By plotting the result, [2] is
most probably right, so [3] is wrong.
 

- *Category:* Code
- *Time to complete:* 96 hours

<a name="#754"></a>
### [754](http://code.google.com/p/sympy/issues/detail?id=754&q=label%3ACodeInImportedIntoSpreadsheet) - Have re and im call expand(complex=True)

Here is a nice integral that SymPy is able to compute:

```
>>> from sympy import *
>>> var('y')
y
>>> a = integrate((16*y-16)/(y**4-2*y**3+4*y-4), (y, 0, 1))
>>> a = simplify(a)
>>> pprint(a)
                                              ___
-2*log(2) + 2*pi + 2*log(1 + I) + 2*log(1 + \/ 2 ) + 2*log(1 - I) + 2*log(1 -

  ___
\/ 2 ) - 2*pi*I - 2*I*log(1 - I) + 2*I*log(1 + I)

```

Simplifying the answer by hand is straightforward (add up the real and
imaginary parts), but unfortunately, SymPy is unable to do this. (It also
fails to produce a numerical value: a.evalf() -> ValueError.) It seems that
currently re and as_real_imag don't know anything about logarithms.
 

- *Category:* Code
- *Time to complete:* 96 hours

<a name="#2513"></a>
### [2513](http://code.google.com/p/sympy/issues/detail?id=2513&q=label%3ACodeInImportedIntoSpreadsheet) - Create a SymPyDeprecationWarning for deprecated SymPy behavior

DeprecationWarning is turned off by default in Python 2.7, so all of our deprecated behavior that we deprecate with DeprecationWarning is not shown to the majority of our users (unless they are specifically looking for it, they won't find it).  This was done because most users of Python programs can't do anything if the program uses deprecated behavior, so they don't care to see the warning.  But I think most developers don't really do a good job of turning the warnings on, unfortunately.

I think we should create a SymPyDeprecationWarning that subclasses from DeprecationWarning, but is turned on by default in isympy.  See <a title="Turn on deprecation warnings in isympy"  href="/p/sympy/issues/detail?id=2142">issue 2142</a>.  That way, users of scripts that use sympy won't be bothered by them, but people who use isympy, who should be bothered by them in my opinion, will be. This will likely also include the developers of most of those scripts. 

- *Category:* Code
- *Time to complete:* 96 hours

<a name="#2552"></a>
### [2552](http://code.google.com/p/sympy/issues/detail?id=2552&q=label%3ACodeInImportedIntoSpreadsheet) - (1/(x*y)).subs(x*y, whatever) doesn't work
This is doesn't work >>> (1/(x*y)).subs(x*y, 2);1/(x*y). Because >>> (1/(x*y)).args; (1/x, 1/y) automatically changed in Mul class  



Incorrect example:

```py
>>> (1/(x*y)).subs(x*y, 2)
 1 
───
x⋅y
```


This is doesn't work because

```py
>>> (1/(x*y)).args
(1/x, 1/y)
```

 automatically changed in Mul class
 

- *Category:* Code
- *Labels:* Priority-High, Type-Defect
- *Time to complete:* 96 hours

<a name="#2632"></a>
### [2632](http://code.google.com/p/sympy/issues/detail?id=2632&q=label%3ACodeInImportedIntoSpreadsheet) - Add isympy -c qtconsole

You can open the IPython qtconsole with a sympy session by typing `IPython qtconsole --profile=sympy`, but you should also be able to do it by typing `isympy -c ipython-qtconsole`.  Unlike the former, the latter should perhaps not rely on IPython's built-in sympy profile to work.
 

- *Category:* Code
- *Time to complete:* 96 hours

<a name="#2793"></a>
### [2793](http://code.google.com/p/sympy/issues/detail?id=2793&q=label%3ACodeInImportedIntoSpreadsheet) - The dsolve solver for 1st_exact should use integration

The method used by the 1st_exact solver is a nice one to use by hand, but it's kind of flaky.  I didn't realize at the time of writing it that you can actually express the solution using integrals without introducing parameters or dummy integration limits.  This solution is given in Table II of the paper "Symbolic Integration: The Stormy Decade" by Joel Moses.  I was able to download this paper for free from Google Scholar.  If you cannot access it and are interested in fixing this issue, contact me and I will send it to you.
 

- *Category:* Code
- *Time to complete:* 96 hours

<a name="#2794"></a>
### [2794](http://code.google.com/p/sympy/issues/detail?id=2794&q=label%3ACodeInImportedIntoSpreadsheet) - Implement ode solvers from the Moses "Stormy Decade" paper: Almost Linear

See Table II of the paper &quot;Symbolic Integration: The Stormy Decade&quot; by Joel Moses.  Some of these are not implemented yet, in particular, the last three.  

I was able to download this paper for free from Google Scholar.  If you cannot access it and are interested in fixing this issue, contact me and I will send it to you.

See also [issue 2793](http://code.google.com/p/sympy/issues/detail?id=2793).

Each solver should be a separate Code-In task.
 

- *Category:* Code
- *Time to complete:* 96 hours

<a name="#2841"></a>
### [2841](http://code.google.com/p/sympy/issues/detail?id=2841&q=label%3ACodeInImportedIntoSpreadsheet) - integrate() can not integrate the Abs() function, fix it

In Dev version

```
>>> import sympy
>>> x = sympy.Symbol('x')
>>> i = sympy.integrate(sympy.Abs(x), (x, -1, 1))
>>> i.n()


/env/src/sympy/sympy/mpmath/libmp/libmpf.pyc in mpf_abs(s, prec, rnd)
    653     precision. The prec argument can be omitted to generate an
    654     exact result.&quot;&quot;&quot;
--> 655     sign, man, exp, bc = s
    656     if (not man) and exp:
    657         if s == fninf:

TypeError: 'NoneType' object is not iterable
```
 

- *Category:* Code
- *Time to complete:* 96 hours

<a name="#2849"></a>
### [2849](http://code.google.com/p/sympy/issues/detail?id=2849&q=label%3ACodeInImportedIntoSpreadsheet) - Better heuristics and simplification for integral of cos(x)/sin(x)**n and similar

The result of `integrate(cos(x)/sin(x)**n, x)` is
"nice", if n is even, and "ugly", if n is odd
(n is an integer, greater than 1).

Moreover, if n is odd, then `diff(integrate(cos(x)/sin(x)**n, x), x)`
gives a very ugly expression that cannot be converted back to
`cos(x)/sin(x)**n` by simplify.

Example:

```py
>>> diff(integrate(cos(x)/sin(x)**7, x), x)
             5                   3                      
36⋅sin(x)⋅cos (x) - 72⋅sin(x)⋅cos (x) + 36⋅sin(x)⋅cos(x)
────────────────────────────────────────────────────────
                                                2       
       ⎛     6            4            2       ⎞        
       ⎝6⋅cos (x) - 18⋅cos (x) + 18⋅cos (x) - 6⎠        
```

 

- *Category:* Code
- *Time to complete:* 96 hours

<a name="#294"></a>
### [294](http://code.google.com/p/sympy/issues/detail?id=294&q=label%3ACodeInImportedIntoSpreadsheet) - Pass coverage_doctest.py

I think there should soon be documentation in the code for most, if not
all, of the classes and functions, even if it is only a single line. This
can be useful for both the generated API documentation, and through
interactive help (i.e., the help() command in an interactive Python
session). If there is a need for this, I am fine going through all of the
code and documenting everything, or getting a good start on it.
 

- *Category:* Documentation
- *Time to complete:* 96 hours

<a name="#707"></a>
### [707](http://code.google.com/p/sympy/issues/detail?id=707&q=label%3ACodeInImportedIntoSpreadsheet) - move some wikis to github.com/sympy/sympy/wiki

Move all wikis from [code.google.com](http://code.google.com/p/sympy/w/list) to
[github](https://github.com/sympy/sympy/wiki).
So that we have just one source of documentation to reduce confusion.
 

- *Category:* Documentation
- *Time to complete:* 96 hours

<a name="#2470"></a>
### [2470](http://code.google.com/p/sympy/issues/detail?id=2470&q=label%3ACodeInImportedIntoSpreadsheet) - Fix all sphinx errors and warnings

Currently when we issue:

```
$ cd doc
$ make html
```

we get a lot of errors/warnings related to improper syntax in documentation and docstrings:

```
sympy/doc/src/aboutus.txt:: (WARNING/2) Duplicate explicit target name: "more info".
sympy/sympy/core/basic.py:docstring of sympy.core.basic.Basic.atoms:13: (ERROR/3) Inconsistent literal block quoting.
...
```
 

- *Category:* Documentation
- *Time to complete:* 96 hours

<a name="#2770"></a>
### [2770](http://code.google.com/p/sympy/issues/detail?id=2770&q=label%3ACodeInImportedIntoSpreadsheet) - Update stuff that SymPy can do on the homepage

The list of things that SymPy can do on the homepage is not up to date, because we can actually do a lot more things than that.  This should be updated. 

- *Category:* Documentation
- *Time to complete:* 96 hours

<a name="#2779"></a>
### [2779](http://code.google.com/p/sympy/issues/detail?id=2779&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Geometry

Edit the doc-string to add list of other function that are closely related to the query.


This is the list of .py files which contains the functions.

```
sympy/geometry/curve.py
sympy/geometry/ellipse.py
sympy/geometry/entity.py
sympy/geometry/exceptions.py
sympy/geometry/__init__.py
sympy/geometry/line.py
sympy/geometry/point.py
sympy/geometry/polygon.py
sympy/geometry/util.py
```

There are around 150 functions which one needs to understand (the input parameters and final result and not the code) to interrelate them.
 

- *Category:* Documentation
- *Time to complete:* 96 hours

<a name="#2801"></a>
### [2801](http://code.google.com/p/sympy/issues/detail?id=2801&q=label%3ACodeInImportedIntoSpreadsheet) - lambdify() is not mentioned anywhere

lambdify() is one of most important functions in SymPy (for interoperability with numerical libraries the most important). However it's not mentioned anywhere, although it has a good docstring. The result of `git grep` stands for itself:

$ git grep lambdify doc/
doc/src/aboutus.txt:#. Sebastian Krämer: implemented lambdify/numpy/mpmath cooperation, bug fixes, refactoring, lambdifying of matrices, large printing refactoring and bugfixes
doc/src/aboutus.txt:#. Andrew Straw: lambdify() improvements
doc/src/aboutus.txt:#. Matthew Brett: fixes to lambdify
doc/src/modules/physics/mechanics/examples.txt:maximum recursion depth being exceeded; I also tried lambdifying this, and it

lambdify's docstring must be pulled into docs (there is already a generic issue for this), but we also need a good tutorial showing users how to cooperate with NumPy, SciPy etc. This issue (not the only one by the way) was pointed out to me by Fernando Perez during my stay at Berkeley this week, when trying to solve a practical symbolic-numeric problem. SymPy has already *a lot* of features, but unfortunately most of them are deeply buried in the internals of SymPy and known only to its developers. Also we have to check what does ufuncify() do, because it was reported to me that it's extremely slow. 

- *Category:* Documentation
- *Time to complete:* 96 hours

<a name="#2528"></a>
### [2528](http://code.google.com/p/sympy/issues/detail?id=2528&q=label%3ACodeInImportedIntoSpreadsheet) - Update SymPy's Wikipedia article

I just noticed that <a href="http://en.wikipedia.org/wiki/SymPy" rel="nofollow">http://en.wikipedia.org/wiki/SymPy</a> is a little old with its information.  None of it is wrong, but I think the features list could be updated.  It seems to be roughly the same as the features listed at sympy.org and <a href="http://code.google.com/p/sympy/" rel="nofollow">http://code.google.com/p/sympy/</a>, so perhaps those should be updated too.

Also, SymPy's stuff at <a href="http://en.wikipedia.org/wiki/Comparison_of_computer_algebra_systems" rel="nofollow">http://en.wikipedia.org/wiki/Comparison_of_computer_algebra_systems</a> should be updated.  I did notice some of that is wrong. 

- *Category:* Outreach
- *Time to complete:* 96 hours

<a name="#2764"></a>
### [2764](http://code.google.com/p/sympy/issues/detail?id=2764&q=label%3ACodeInImportedIntoSpreadsheet) - Improve our webpage

Our webpage at http://sympy.org/ could probably be made nicer, like with some nice CSS or html5.  The code is at https://github.com/sympy/sympy.github.com   Also, it maybe could use better examples/explanation of what SymPy is.
 

- *Category:* Outreach
- *Time to complete:* 96 hours

<a name="#2787"></a>
### [2787](http://code.google.com/p/sympy/issues/detail?id=2787&q=label%3ACodeInImportedIntoSpreadsheet) - Create sticker for SymPy based on the logo

The sticker should contain SymPy's logo [1], project name and description. Alternative version may skip description. Sticker must be in SVG format.

[1] http://code.google.com/p/sympy/source/browse/#svn%2Fmaterials%2Flogo
 

- *Category:* Outreach
- *Time to complete:* 96 hours

<a name="#2796"></a>
### [2796](http://code.google.com/p/sympy/issues/detail?id=2796&q=label%3ACodeInImportedIntoSpreadsheet) - Package the latest version of SymPy for the major distributions: Debian / Ubuntu

Most distributions have old versions of SymPy packaged (or none at all, eg. openSUSE). These should be updated to the latest version of SymPy (0.7.1 as of now). Ideally, the scripts used to generate these packages should also be saved and uploaded somewhere, so it will be easier to update them to newer versions. I'm marking this for Code-In, but consider that each major distro could be a separate task.

This most likely means deleting the bundled mpmath/ and making SymPy play nice with the distro-provided version. 

- *Category:* Outreach
- *Time to complete:* 96 hours

<a name="#1456"></a>
### [1456](http://code.google.com/p/sympy/issues/detail?id=1456&q=label%3ACodeInImportedIntoSpreadsheet) - use pyflakes to identify simple bugs in sympy and fix them

Example:

```
$ sudo apt-get install pyflakes
$ pyflakes sympy/integrals/
sympy/integrals/integrals.py:10: 'limit' imported but unused
sympy/integrals/integrals.py:13: 'DiracDelta' imported but unused
sympy/integrals/integrals.py:13: 'Heaviside' imported but unused
```
it finds (among other things) that the Heaviside is imported but never
used, so it should be removed.

There is also pychecker, which shows a lot of things similar to this (I can't get pyflakes to work, so I can't say if it 
does more or not).  You can just install and run pychecker sympy --limit 1000 to see them all (it takes a few 
minutes to run).

Note that there are lots of warnings coming from polys/densepolys.py, polys/densetools.py and polys/sparsepolys.py, but these modules are known not to work, cf. issue 2371.
 

- *Category:* QA
- *Labels:* EasyToFix, Priority-Medium, Type-Defect
- *Time to complete:* 96 hours

Pick a good sized module in SymPy (i.e., one of the subdirectories of the sympy/ directory, but not one of the ones that only has a few files in it).  

<a name="#1752"></a>
### [1752](http://code.google.com/p/sympy/issues/detail?id=1752&q=label%3ACodeInImportedIntoSpreadsheet) - setup.py test should run the doctests even when the regular tests fail

Two things annoy me about `./setup.py test`.  First, if a regular test fails, then it does not run the 
doctests.  But this is supposed to be a shortcut to both the regular tests and the doctests in one.  
Second, if you keyboard interrupt during the tests, it then proceeds to run the doctests.  But when I 
keyboard interrupt, I want it to stop the whole script.  

I don't know how easy it would be to change the second item, but the first one should be fixable.
 

- *Category:* QA
- *Labels:* EasyToFix, Priority-High, Testing, Type-Defect
- *Time to complete:* 96 hours

<a name="#2786"></a>
### [2786](http://code.google.com/p/sympy/issues/detail?id=2786&q=label%3ACodeInImportedIntoSpreadsheet) - Fill in missing tests for sympy.physics module in test_args.py

All tests decorated with @SKIP("TODO: sympy.physics") must be fixed.
 

- *Category:* QA
- *Time to complete:* 96 hours

<a name="#1235"></a>
### [1235](http://code.google.com/p/sympy/issues/detail?id=1235&q=label%3ACodeInImportedIntoSpreadsheet) - Problem installing in Windows

I've downloaded the Windows installer, and tries to run the program - but 
I get an error message: "No Python information found in the registry". But 
I have Python installed.

This is what I get when running the Python command in the command line:

"C:\Users\Fredrik\Documents\programme\discalc>PYTHON
Python 2.5.1 (r251:54863, Apr 18 2007, 08:51:08) [MSC v.1310 32 bit 
(Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>"

Thanks for any answer.

The problem is that we need someone with a 64-bit Windows machine to volunteer to do it (see #16).

 

- *Category:* Research
- *Time to complete:* 96 hours

<a name="#2762"></a>
### [2762](http://code.google.com/p/sympy/issues/detail?id=2762&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate ways to improve substitution, pattern matching, etc.

This is related to <a title="Exact, algebraic, and integer_power substitution"  href="/p/sympy/issues/detail?id=2026">issue 2026</a> and this thread on the [mailing list](http://groups.google.com/group/sympy/browse_thread/thread/4a19d0f39f51fda6).  The subs mechanism should be refactored so that it is more flexible.  Also, I believe it should be using the same thing internally as the pattern matching.  

The (Code-In) task here is to study this problem and discuss optimal ways to solve it.  You may also try implementing this (if we agree upon a good solution), perhaps as a separate task.
 

- *Category:* Research
- *Time to complete:* 96 hours

<a name="#2795"></a>
### [2795](http://code.google.com/p/sympy/issues/detail?id=2795&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate a robust way to have translated documentation

Some of the Code-In tasks include translating our documentation to different languages. If this happens, we would need a way to manage all of these files (we might have many languages, after all). It's also important to know when and how much are these files out of date (as they eventually will be). Usually, GUI applications use gettext and have tons of .po files lying around, but I'm not sure that's the right approach for us. Marking this as a Code-In Research task. 

- *Category:* Research
- *Time to complete:* 96 hours

<a name="#2798"></a>
### [2798](http://code.google.com/p/sympy/issues/detail?id=2798&q=label%3ACodeInImportedIntoSpreadsheet) - Research ways to extract statistics from the issue tracker

The issue tracker can provide some valuable statistics about the health of the project - it might be interesting to graph the number of open issues, number of issues per category, the average "age" of the (closed/open) issues, who closes the most issues, the number of issue reports by users (as opposed to developers of SymPy) etc. This likely involves interfacing somehow with the Google API.
 

- *Category:* Research
- *Time to complete:* 96 hours

<a name="#2803"></a>
### [2803](http://code.google.com/p/sympy/issues/detail?id=2803&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate how to make the rewrite framework more flexible

Currently, the rewrite framework only allows `expr.rewrite(function)` (e.g., `cos(x).rewrite(exp)`), and it implements only one rule per function pair.  This should be made more general.  Sometimes, you can't express a rewrite rule with just a function.  Other times, there is more than one way to rewrite one function in terms of another (for example `cos(x) == sqrt(1 - sin(x)) == sin(pi/2 - x))`.  

The issue is to consider ways to make the rewrite framework stronger, but still modular like it is now (so it's easily extensible).
 

- *Category:* Research
- *Time to complete:* 96 hours

<a name="#2790"></a>
### [2790](http://code.google.com/p/sympy/issues/detail?id=2790&q=label%3ACodeInImportedIntoSpreadsheet) - Create examples/short tutorials using IPython's notebook (IPython >= 0.12)

Examples/short tutorials should show how to use SymPy to solve illustrative problems in high school mathematics/physics. Notebooks must contain code split into logical blocks, text cells with problem description and references to other materials, books, videos, etc. 

- *Category:* Training
- *Time to complete:* 96 hours

<a name="#2766"></a>
### [2766](http://code.google.com/p/sympy/issues/detail?id=2766&q=label%3ACodeInImportedIntoSpreadsheet) - Translate tutorial to German

The [tutorial](http://docs.sympy.org/0.7.1/tutorial.html) should be translated into various languages, e.g., Czech, Polish, French, German, etc.
 

- *Category:* Translation
- *Time to complete:* 96 hours

<a name="#2767"></a>
### [2767](http://code.google.com/p/sympy/issues/detail?id=2767&q=label%3ACodeInImportedIntoSpreadsheet) - Improve the interface of SymPy Live

The interface at live.sympy.org should be improved, so that it looks and feels nicer, perhaps using some more advanced html5/css, etc. 

- *Category:* UI
- *Time to complete:* 96 hours

<a name="#2857"></a>
### [2857](http://code.google.com/p/sympy/issues/detail?id=2857&q=label%3ACodeInImportedIntoSpreadsheet) - sqrt(2).is_irrational is None (should be True)

It seems that sqrt(2).is_irrational should return True

Also, in a recent commit (ebe8a7e) it is noted that Add and Mul's implementation was faulty:

```
    The function used to return True if any factor was irrational.
    This is nonsense: neither I*pi, nor sqrt(8)/sqrt(2) are irrational.
    [One might argue about I*pi, but irrational implies real under the
    current assumptions system.]
    
    We now return True iff there is exactly one irrational factor and
    all other factors are rational.
```

In a Mul, any irrationals join together if their args are Rationals:

```
>>> sqrt(2)*sqrt(5)
sqrt(10)
>>> sqrt(S.Half)*sqrt(3)
sqrt(6)/2
>>> sqrt(2)*sqrt(2+sqrt(3))
sqrt(2)*sqrt(sqrt(3) + 2)
```

So the argument about `sqrt(8)/sqrt(2)` doesn't apply. But it does make sense that the only way you can know that something is irrational is to have only one irrational factor since something like `sqrt(2+sqrt(3))*sqrt(2-sqrt(3))` might appear irrational with two irrational factors, but this is just a fancy 1:

```py
>>> sqrt(2-sqrt(3))*sqrt(2+sqrt(3))
sqrt(-sqrt(3) + 2)*sqrt(sqrt(3) + 2)
>>> _.n()
1.00000000000000
```

Perhaps the routine could see if all irrationals present have a Number argument so `sqrt(2)*root(3,3)` could give True for is_irrational.

The same sort of problems exist for Add: while `sqrt(2) + sqrt(6)` is definitely irrational (though sympy gives None for the answer); something like `sqrt(2)/3 + sqrt(-6*sqrt(2) + 11)/3` is, again, just a fancy 1.
 

- *Category:* Code
- *Time to complete:* 96 hours

## <a name="#Easy">Easy</a>
<a name="#615"></a>
### [615](http://code.google.com/p/sympy/issues/detail?id=615&q=label%3ACodeInImportedIntoSpreadsheet) - Fix the occasions where functions are called with wrong name and write tests


```
    /home/matt/hg/sympy/sympy/core/basic_methods.py in __getattr__(cls, name)
    216         try: return MetaBasicMeths.classnamespace[name]
    217         except KeyError: pass
--> 218         raise AttributeError("'%s' object has no attribute '%s'"%
    219                              (cls.__name__, name))
    220 
```

AttributeError: 'Basic' object has no attribute 'Log'.

Some time ago functions were renamed but in many places there are old names
left, this should be fixed soon.

And especially tests need to be written to catch these bugs. Because what is
not tested for is broken.
 

- *Category:* Code
- *Time to complete:* 96 hours

<a name="#654"></a>
### [654](http://code.google.com/p/sympy/issues/detail?id=654&q=label%3ACodeInImportedIntoSpreadsheet) - Remove dead code from _eval_subs()

It seems this piece of code is never (?) executed in sympy since
exp(3*log(x)) canonize to x**3.

```
--- a/sympy/functions/elementary/exponential.py
@@ -13,7 +13,7 @@ class exp(Function):
             raise ArgumentIndexError(self, argindex)

     def inverse(self, argindex=3D1):
-        return S.Log
+        return log

     @classmethod
     def _eval_apply_subs(self, *args):
@@ -124,7 +124,7 @@ class exp(Function):
         arg =3D self.args[0]
         o =3D old
         if isinstance(old, Basic.Pow): # handle (exp(3*log(x))).subs(x*=
*2, z) -&gt; z**(3/2)
-            old =3D exp(old.exp * S.Log(old.base))
+            old =3D exp(old.exp * log(old.base))
```

On the other hand when autoevaluation would be turned off exp(3*log(x))
will be just that -- so there should be a test which constructs
unevaluated exp(3*log(x), evaluate=False) and calls subs.

 

- *Category:* Code
- *Time to complete:* 96 hours

<a name="#1058"></a>
### [1058](http://code.google.com/p/sympy/issues/detail?id=1058&q=label%3ACodeInImportedIntoSpreadsheet) - Classifying formulas


Finish this innovation.

I've written some code for determining the "class" of a formula. The
function classify(expr, x) walks the expression top-down and at each level
classifies it as a function of x. It distinguishes between various classes
of functions, including:

* linear expressions
* polynomials (degree > 1)
* rational functions
* algebraic roots
* exponentials
* logarithms
* trigonometric functions
* etc

It then recursively classifies all subexpressions and returns the path with
the "greatest" complexity. The following test outputs should hopefully make
it more clear:

```py
pi []
1 + 3*x [LINEAR]
3*x + x**2 [POLYNOMIAL]
2*x + exp(1 + 2*x) + exp(4 + 3*x) [LINEAR, EXP, LINEAR]
2*x + (exp(3*x) + exp(1 + x))/(1 + 5*x) [RATIONAL, EXP, LINEAR]
2*x + sin(1 + 2*x)**2 + cos(4 + x)**4 [POLYNOMIAL, TRIGONOMETRIC, LINEAR]
```

 

- *Category:* Code
- *Labels:* Priority-Medium, Type-Enhancement
- *Time to complete:* 48 hours

<a name="#2276"></a>
### [2276](http://code.google.com/p/sympy/issues/detail?id=2276&q=label%3ACodeInImportedIntoSpreadsheet) - integrate() should use the ode module's undetermined coefficients solver when possible

So my comment 8 from <a title="Arbitrary constants in indefinite integration"  href="/p/sympy/issues/detail?id=2219">issue 2219</a> made me realize something.  Consider the following:

```py
>>> integrate(x**2*exp(x)*sin(x), x)
   x           2  x                  x                  2         x
  ℯ ⋅sin(x)   x ⋅ℯ ⋅sin(x)   cos(x)⋅ℯ              x   x ⋅cos(x)⋅ℯ 
- ───────── + ──────────── - ───────── + x⋅cos(x)⋅ℯ  - ────────────
      2            2             2                          2      

>>> dsolve(f(x).diff(x) - x**2*exp(x)*sin(x), f(x), hint='nth_linear_constant_coeff_undetermined_coefficients')
             x           2  x                  x                  2         x
            ℯ ⋅sin(x)   x ⋅ℯ ⋅sin(x)   cos(x)⋅ℯ              x   x ⋅cos(x)⋅ℯ 
f(x) = C₁ - ───────── + ──────────── - ───────── + x⋅cos(x)⋅ℯ  - ────────────
                2            2             2                          2      

>>> %timeit integrate(x**2*exp(x)*sin(x), x)
1 loops, best of 3: 10.7 s per loop

>>>  %timeit dsolve(f(x).diff(x) - x**2*exp(x)*sin(x), f(x), hint='nth_linear_constant_coeff_undetermined_coefficients')
1 loops, best of 3: 232 ms per loop
```

`dsolve()` is way faster because it just computes the necessary form of the integral and solves for the undetermined coefficients.  No complicated integration algorithm is needed.  

So I think if the integral has the correct form, that internally `integrate(expr, x, x, ...)` should use dsolve's internal undetermined coefficient algorithms for solving `f(x).diff(x, x, …)` - expr.  All the necessary stuff is already in ode.py, including the function that checks if expr is of the correct form.
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2427"></a>
### [2427](http://code.google.com/p/sympy/issues/detail?id=2427&q=label%3ACodeInImportedIntoSpreadsheet) - Check for incorrect usage of expr.atoms() and change it to free_symbols

If any code wants to know if there are variables that are free like `x` but not `y` in `Integral(y, (y, 1, x))` then it should use expr.free_symbols, not `.atoms(Symbol)` (since that would have given x and y for the example given). The code should be checked for instances of `.atoms(Symbol)` to see what the author intended and corrected if necessary.
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2534"></a>
### [2534](http://code.google.com/p/sympy/issues/detail?id=2534&q=label%3ACodeInImportedIntoSpreadsheet) - Use "with open" instead of "open … close"
Please see http://code.google.com/p/sympy/issues/detail?id=2534 for full information on this task. Please read https://github.com/sympy/sympy/wiki/gci-2011-landing before completing any tasks for SymPy.  


Now that we don't support Python 2.4, we can use with statement context managers.  One of the best places to use this is when opening a file.  You can do

```py
with open(file) as f:
    do stuff
```
instead of 

```py
f = open(file)
do stuff
f.close()
```

And it's not only more readable, but also the with statement context manager will automatically close the file, even if an exception is raised. 

There are a handful of places in the code where we open() stuff (do git grep "open\(").  Remember that to support the with statement in Python 2.5, you have to add "from __future__ import with_statement" to the top of the file.
 

- *Category:* Code
- *Labels:* EasyToFix, Priority-Medium, Type-Defect
- *Time to complete:* 48 hours

<a name="#2570"></a>
### [2570](http://code.google.com/p/sympy/issues/detail?id=2570&q=label%3ACodeInImportedIntoSpreadsheet) - Remove bare except statements

If you do git grep "except:" you will see that there are several places in the code with bare except statements that should be rewritten to catch explicit exceptions.  To quote the Zen of Python:

Errors should never pass silently.
Unless explicitly silenced.

And to quite PEP 8:

```
- When catching exceptions, mention specific exceptions
      whenever possible instead of using a bare 'except:' clause.

      For example, use:

          try:
              import platform_specific_module
          except ImportError:
              platform_specific_module = None

      A bare 'except:' clause will catch SystemExit and KeyboardInterrupt
      exceptions, making it harder to interrupt a program with Control-C,
      and can disguise other problems.  If you want to catch all
      exceptions that signal program errors, use 'except Exception:'.

      A good rule of thumb is to limit use of bare 'except' clauses to two
      cases:

         1) If the exception handler will be printing out or logging
            the traceback; at least the user will be aware that an
            error has occurred.

         2) If the code needs to do some cleanup work, but then lets
            the exception propagate upwards with 'raise'.
            'try...finally' is a better way to handle this case.
```

To be sure, some of the bare except cases in the code are correct by the above (like the ones in the test runner), but many are not.
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2639"></a>
### [2639](http://code.google.com/p/sympy/issues/detail?id=2639&q=label%3ACodeInImportedIntoSpreadsheet) - The Product() class should not evaluate by default

Unlike other unevaluated operators, Product() is not always unevaluated.  Attempted evaluation should be the job of product().  This is how Sum/summation works:

```py
>>> Product(n, (n, 1, 2))
2
>>> Sum(n, (n, 1, 2))
```

```
  2    
 __    
 \ `   
  )   n
 /_,   
n = 1  
```
```
>>> product(n, (n, 1, 2))
2

>>> summation(n, (n, 1, 2))
3
```
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2683"></a>
### [2683](http://code.google.com/p/sympy/issues/detail?id=2683&q=label%3ACodeInImportedIntoSpreadsheet) - det() is called when inverting matrix through GE

As noted at [maillist](http://groups.google.com/group/sympy/browse_thread/thread/ba37b597b851df7c#), `det()` is called when inverting a `Matrix` with the GE method.  This is used only the check if it is non-degenerate.  This should instead be checked by the output of `rref()`.
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2760"></a>
### [2760](http://code.google.com/p/sympy/issues/detail?id=2760&q=label%3ACodeInImportedIntoSpreadsheet) - latex(symbol_names) not working with ~x

Read this for more information https://github.com/sympy/sympy/pull/674

```py
latex(x**2, symbol_names={x:'x_i'})
```


works fine, but when you try something as

```py
latex(~x, symbol_names={x:'x_i'})
```

it doesn't. Besides, every time you need latex to use x's symbol_name, you need to pass the symbol_names dictionary.

Sage has some nice functionality:

```py
var('sui', latex_name="s_{u,i}")
```

and you don't have to use a special dictionary everytime you need to typeset the symbol.
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2776"></a>
### [2776](http://code.google.com/p/sympy/issues/detail?id=2776&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in integrals

Edit the doc-string to add list of other function that are closely related to the query.


This is the list of .py files which contains the functions.

```
sympy/integrals/deltafunctions.py
sympy/integrals/integrals.py
sympy/integrals/risch.py
sympy/integrals/rationaltools.py
sympy/integrals/trigonometry.py
```

There are around 19 functions which one needs to understand (the input parameters and final result and not the code) to interrelate them.
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2784"></a>
### [2784](http://code.google.com/p/sympy/issues/detail?id=2784&q=label%3ACodeInImportedIntoSpreadsheet) - 1/function() should be printed differently by latex printer

```
>>> latex(1/cos(x))
\operatorname{cos}^{-1}\left(x\right)

pprint(1/cos(x))
  1   
──────
cos(x)
```

should output `\frac{1}{\operator ...}`
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2785"></a>
### [2785](http://code.google.com/p/sympy/issues/detail?id=2785&q=label%3ACodeInImportedIntoSpreadsheet) - Use \functionname instead of \operatorname{functionname} whenever possible

SymPy uniformly uses `\operatorname` when latex printing functions. However, tex engine in matplotlib doesn't support it. It would be convenient to use `\functionname` directly whenever possible (trigonometric and hyperbolic functions, exp, log and maybe other).
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2815"></a>
### [2815](http://code.google.com/p/sympy/issues/detail?id=2815&q=label%3ACodeInImportedIntoSpreadsheet) - Parts of the pyglet plotting module does not follow PEP 8, fix it

The code there is a bit hard to read. It would be nice to have it refactored so it follows PEP8.

There are certain parts that are not pythonic but that's another problem needing more in-depth refactoring. 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2817"></a>
### [2817](http://code.google.com/p/sympy/issues/detail?id=2817&q=label%3ACodeInImportedIntoSpreadsheet) - Make sure all the built-in __methods__ are defined

At http://docs.python.org/reference/datamodel.html, it lists all the `__methods__` that Python works with (like `__int__`, `__contains__`, etc.).  We should go through all of these and make sure they are all defined on `Basic`, `Expr`, or whatever relevant subclass, so that we don't have simple bugs like

```py
>>> long(Integer(3))
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
/Users/aaronmeurer/Documents/python/sympy/sympy/<ipython-input-72-5fff10d216fd> in <module>()
----> 1 long(Integer(3))

TypeError: long() argument must be a string or a number, not 'Integer'
```

Regarding where they should be defined, stuff that makes sense for any object should go on Basic, stuff that makes sense only on mathematical objects (like `__add__` for example) should go on Expr, and stuff that makes sense only for numbers (like `__int__`) should go in `Number`.
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2830"></a>
### [2830](http://code.google.com/p/sympy/issues/detail?id=2830&q=label%3ACodeInImportedIntoSpreadsheet) - checkodesol() should use force=True

```
> @@ -542,7 +542,11 @@ def test_1st_homogeneous_coeff_ode_check3():
>      # (False, x*(log(exp(-LambertW(C1*x))) + LambertW(C1*x))*exp(-LambertW(C1*x) + 1))
>      eq3 = f(x) + (x*log(f(x)/x) - 2*x)*diff(f(x),x)
>      sol3 = Eq(f(x), x*exp(1 - LambertW(C1*x)))
> -    assert checkodesol(eq3, sol3, solve_for_func=False)[0]
> +    assert checkodesol(eq3, sol3, solve_for_func=True)[0]
> +    # and without an assumption about x and f(x), the implicit form doesn't resolve, either:
> +    # (False, (log(f(x)/x) + log(x/f(x)))*f(x))
```

So `checkodesol()` needs to be more aggressive, since `dsolve()` obtains these logarithms by calling `logcombine(force=True)`. An expand with `force=True` should be used on expressions being tested or else (as shown above) terms which should go to zero, don't:

```py
>>> log(f(x)/x) + log(x/f(x))
log(f(x)/x) + log(x/f(x))
>>> _.expand(force=True)
0
```
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2838"></a>
### [2838](http://code.google.com/p/sympy/issues/detail?id=2838&q=label%3ACodeInImportedIntoSpreadsheet) - Move the KroneckerDelta class to another module 

KroneckerDelta would be useful for more than just quantum physics.  I think it should be moved into the functions module and imported with `from sympy import *`.
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#2846"></a>
### [2846](http://code.google.com/p/sympy/issues/detail?id=2846&q=label%3ACodeInImportedIntoSpreadsheet) - Integral.transform should allow a change to a different variable

Integral.transform is confusing, since it requires you to use the same integration variable.  But usually, when we do a transfrom on an integral we change the name of the variable.  It should allow something like

```py
Integral.transform(x, 2*y, y)
```

where y is the new variable.  The third argument would default to the integration variable, so that you can still use the current syntax.

Also, the docstring needs some doctests, which would also make it less confusing.

Related is [issue 2297: Integral manipulations](http://code.google.com/p/sympy/issues/detail?id=2297)
 

- *Category:* Code
- *Time to complete:* 48 hours

<a name="#16"></a>
### [16](http://code.google.com/p/sympy/issues/detail?id=16&q=label%3ACodeInImportedIntoSpreadsheet) - Check and compare an old patch concerning object with indices against current sympy
Please see http://code.google.com/p/sympy/issues/detail?id=16 for full information on this task. <br><br>Please read https://github.com/sympy/sympy/wiki/gci-2011-landing before completing any tasks for SymPy. <br><br>Additional Note(s): Check out comment 32 in the bug report. 


Let's get inspired by ginac. This code should make it easy to compute for
example einstein equations from the (symbolic) metric tensor. We can do it
already now, but it would be nice to type in equations in the index form as
found in the general relativity books and then just plug in a symbolic
matrix for the metric tensor, and it would figure all the rest by itself. 

- *Category:* Documentation
- *Labels:* EasyToFix, Matrices, Priority-Medium, Type-Enhancement
- *Time to complete:* 48 hours

Check out comment 32 in the bug report. 

<a name="#1886"></a>
### [1886](http://code.google.com/p/sympy/issues/detail?id=1886&q=label%3ACodeInImportedIntoSpreadsheet) - Documentation for the Expr class

Expr needs a docstring. The split between Basic and Expr must be explained. 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2115"></a>
### [2115](http://code.google.com/p/sympy/issues/detail?id=2115&q=label%3ACodeInImportedIntoSpreadsheet) - Move stuff from the Google Code SVN to git

Everything from here http://code.google.com/p/sympy/source/browse/ needs to be moved either to the GitHub wiki or the main repo.  Details on how to checkout the files on your computer are here: http://code.google.com/p/sympy/source/checkout.  Does anyone know how to transfer svn to git without losing the history?

By the way, this includes the Google Code wiki pages in it.
 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2160"></a>
### [2160](http://code.google.com/p/sympy/issues/detail?id=2160&q=label%3ACodeInImportedIntoSpreadsheet) - List of dependencies

We should include in the README, and probably in the docs somewhere too, a list of all the "dependencies" of SymPy.  Now, obviously, SymPy's only dependency is Python, but there are several optional dependencies like IPython and gmpy that are not required but extent the capabilities of SymPy if they are installed. 

 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2204"></a>
### [2204](http://code.google.com/p/sympy/issues/detail?id=2204&q=label%3ACodeInImportedIntoSpreadsheet) - Document why unpickling a singleton doesn't return the singleton object with protocol 0 and 1

After pickling and unpickling `pi`, a simple `cos(pi)` no longer nicely simplifies to -1 on its own (it does if you nsimplify it)

Code:

```
$ cat test.py 
from sympy import *
from pickle import *

mypkl = open('test.pkl', 'wb')
dump(pi, mypkl)
mypkl.close()

mypkl = open('test.pkl', 'rb')
picklepi = load(mypkl)
mypkl.close()

print cos(pi)
print cos(picklepi)
print nsimplify(cos(picklepi))

Output:
$ python test.py 
-1
cos(pi)
-1

Expected output:
-1
-1
-1
```
 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2367"></a>
### [2367](http://code.google.com/p/sympy/issues/detail?id=2367&q=label%3ACodeInImportedIntoSpreadsheet) - SymPy's readthedocs documentation is broken

See http://readthedocs.org/docs/sympy/en/latest/  It just shows

"""
This is an automaticaly generated API documentation from SymPy sources.

Click the “modules” (Module Index) link in the top right corner to browse the modules.

Or click the “index” to see an index of all SymPy functions, methods and classes.
"""

and that's it.
 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2597"></a>
### [2597](http://code.google.com/p/sympy/issues/detail?id=2597&q=label%3ACodeInImportedIntoSpreadsheet) - Import all public functions and classes into Sphinx: polys

There are some methods that do have docstrings, but are not shown in the documentation (docs.sympy.org).

For example, method norm in matrices.matrices.py has a docstring, but is not shown in http://docs.sympy.org/dev/modules/matrices.html. I thought that the bad formatting (there is no blank line after the first line of docstring) of the docstring might be the reason for this, but there are other methods with baddly formatted docstrings, that are properly shown in the documentation (e.g. method `is_symmetric` for `matrices.matrices.py`).
 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2599"></a>
### [2599](http://code.google.com/p/sympy/issues/detail?id=2599&q=label%3ACodeInImportedIntoSpreadsheet) - Update isympy manpage

The manpage for isympy (doc/man/isympy) needs to be updated with all the latest options, etc. 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2679"></a>
### [2679](http://code.google.com/p/sympy/issues/detail?id=2679&q=label%3ACodeInImportedIntoSpreadsheet) - Refactor GA* documentation to use doctests (or move it to examples/)

There are some .py files in doc/src/modules/galgebra/GA which have some strange indentation (and aren't valid Python source files either). Aaron also noticed this and they produce (harmless) errors when 2to3 is ran on them. I've finally had a chance to look at them and they seem to be included in the main GA module documentation, GAsympy.txt. In fact, they seem to be used like a doctest - the first part of the file (indented) are the comments that produce the second half of the file (not indented). These should be converted to be actual doctests. 

Those files also haven't been touched since 2009 so it's not clear to me if anyone is even using this part of SymPy now, but fixing the docs shouldn't be too hard and can be a good introduction to SymPy for an interested developer (hence, I'm putting the EasyToFix tag here). Also, I don't think these files are ran as part of the doctest suite which means errors might be creeping in and we'd like to avoid this.

For the record, here are the errors produced when 2to3 is ran on these files:

```
RefactoringTool: Can't parse sympy-py3k/./doc/src/modules/galgebra/GA/reciprocalframeGAtest.py: ParseError: bad input: type=5, value='        ', context=('', (1, 0))
RefactoringTool: Can't parse sympy-py3k/./doc/src/modules/galgebra/GA/headerGAtest.py: ParseError: bad input: type=0, value='', context=('\n', (26, 0))
RefactoringTool: Can't parse sympy-py3k/./doc/src/modules/galgebra/GA/conformalgeometryGAtest.py: ParseError: bad input: type=5, value='        ', context=('', (1, 0))
RefactoringTool: Can't parse sympy-py3k/./doc/src/modules/galgebra/GA/BasicGAtest.py: ParseError: bad input: type=5, value='        ', context=('', (1, 0))
RefactoringTool: Can't parse sympy-py3k/./doc/src/modules/galgebra/GA/hyperbolicGAtest.py: ParseError: bad input: type=5, value='        ', context=('', (1, 0))
```
 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2774"></a>
### [2774](http://code.google.com/p/sympy/issues/detail?id=2774&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Number Theory

Edit the doc-string to add list of other function that are closely related to the query.

Ex. 

```
>>> prime?
Docstring:
    Return the nth prime, with the primes indexed as prime(1) = 2,
    prime(2) = 3, etc.... The nth prime is approximately n*log(n) and
    can never be larger than 2**n.
    
    Reference: http://primes.utm.edu/glossary/xpage/BertrandsPostulate.html
```

This is the present doc-string. One needs to add the following line

```
    See also : isprime, primerange, primepi
```
 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2775"></a>
### [2775](http://code.google.com/p/sympy/issues/detail?id=2775&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Combinotorics 

Edit the doc-string to add list of other function that are closely related to the query.


This is the list of .py files which contains the functions.

```
sympy/combinatorics/generators.py  
sympy/combinatorics/prufer.py
sympy/combinatorics/graycode.py
sympy/combinatorics/permutations.py  
sympy/combinatorics/subsets.py
```

There are around 98(at max) functions which one needs to understand (the input parameters and final result and not the code) to interrelate them.
 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2777"></a>
### [2777](http://code.google.com/p/sympy/issues/detail?id=2777&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in functions

Edit the doc-string to add list of other function that are closely related to the query.


This is the list of .py files which contains the functions.

```
sympy/functions/combinatorial/factorials.py
sympy/functions/combinatorial/numbers.py
sympy/functions/elementary/trigonometric.py  
sympy/functions/elementary/integers.py
sympy/functions/elementary/exponential.py
sympy/functions/elementary/piecewise.py
sympy/functions/elementary/complexes.py
sympy/functions/elementary/miscellaneous.py
sympy/functions/elementary/hyperbolic.py
```

There are around 52 functions which one needs to understand (the input parameters and final result and not the code) to interrelate them.
 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2778"></a>
### [2778](http://code.google.com/p/sympy/issues/detail?id=2778&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in functions/special

Edit the doc-string to add list of other function that are closely related to the query.


This is the list of .py files which contains the functions.

```
sympy/functions/special/zeta_functions.py
sympy/functions/special/delta_functions.py
sympy/functions/special/tensor_functions.py
sympy/functions/special/hyper.py
sympy/functions/special/bsplines.py
sympy/functions/special/spherical_harmonics.py
sympy/functions/special/gamma_functions.py
sympy/functions/special/bessel.py
sympy/functions/special/polynomials.py
sympy/functions/special/error_functions.py
```

There are around 62 functions which one needs to understand (the input parameters and final result and not the code) to interrelate them.
 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2780"></a>
### [2780](http://code.google.com/p/sympy/issues/detail?id=2780&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Matrices

Edit the doc-string to add list of other function that are closely related to the query.

This is the list of .py files which contains the functions.

```
sympy/matrices.py
```

There are around 69 functions which one needs to understand (the input parameters and final result and not the code) to interrelate them.
 

- *Category:* Documentation
- *Time to complete:* 48 hours

<a name="#2763"></a>
### [2763](http://code.google.com/p/sympy/issues/detail?id=2763&q=label%3ACodeInImportedIntoSpreadsheet) - Fix the SymPy Logo

The original logo is found at http://code.google.com/p/sympy/source/browse/#svn%2Fmaterials%2Flogo   The problem is that the transparency is not done correctly on the tail, so that it does not look good unless the background is white.  We need to fix it so that it uses the correct kind of alpha channel, so that it looks good everywhere.  There is a svg image there, though I didn't have much luck with it.
 

- *Category:* Outreach
- *Time to complete:* 48 hours

<a name="#2800"></a>
### [2800](http://code.google.com/p/sympy/issues/detail?id=2800&q=label%3ACodeInImportedIntoSpreadsheet) - Flesh out the SymPy Papers wiki page

We have a page on the wiki [SymPy-Papers](https://github.com/sympy/sympy/wiki/SymPy-Papers) that should list (scientific) papers mentioning SymPy, but it's currently empty. Populating this would be interesting and could also persuade other academics to try out/use SymPy. Google Scholar can be used to track down papers. See also the [thread which originally asked about this](https://groups.google.com/group/sympy/browse_thread/thread/34443bd5708310f2/71c0cc0ba21a19e1?hl=en).

 

- *Category:* Outreach
- *Time to complete:* 48 hours

<a name="#1616"></a>
### [1616](http://code.google.com/p/sympy/issues/detail?id=1616&q=label%3ACodeInImportedIntoSpreadsheet) - Bug in subs


```py
>>> c2,c3,q1p,q2p,c1,s1,s2,s3= symbols('c2 c3 q1p q2p c1 s1 s2 s3')

>>> test=c2**2*q2p*c3 + c1**2*s2**2*q2p*c3 + s1**2*s2**2*q2p*c3 -
c1**2*q1p*c2*s3 - s1**2*q1p*c2*s3

>>> test.subs({c1**2 : 1-s1**2, c2**2 : 1-s2**2, c3**3: 1-s3**2})

ERROR: An unexpected error occurred while tokenizing input           
The following traceback may be corrupted or invalid                  
The error message is: ('EOF in multi-line statement', (22, 0))       

ERROR: An unexpected error occurred while tokenizing input
The following traceback may be corrupted or invalid       
The error message is: ('EOF in multi-line statement', (96, 0))
```

 

- *Category:* QA
- *Time to complete:* 48 hours

<a name="#2493"></a>
### [2493](http://code.google.com/p/sympy/issues/detail?id=2493&q=label%3ACodeInImportedIntoSpreadsheet) - Clean up test_lambdify.py

`test_lambdify.py` has a bunch of try blocks that should be using `raises()`.
 

- *Category:* QA
- *Time to complete:* 48 hours

<a name="#2788"></a>
### [2788](http://code.google.com/p/sympy/issues/detail?id=2788&q=label%3ACodeInImportedIntoSpreadsheet) - Commented out tests should be XFAILed

If you "git grep '# *assert'", you'll see a bunch of tests where the test line is commented out.  These should be changed to be XFAIL tests, so that we can see if they start passing.  Also, they should be double checked to see if they really would start passing (e.g., they don't have syntax errors).
 

- *Category:* QA
- *Time to complete:* 48 hours

<a name="#2157"></a>
### [2157](http://code.google.com/p/sympy/issues/detail?id=2157&q=label%3ACodeInImportedIntoSpreadsheet) - sympy development rules

I think there is a consensus about the requirements for inclusion of a (nontrivial) patch in sympy:

1. All tests have to pass. (Include new tests for new features.)
2. The patch has to be positively reviewed by someone else. (If there a objections, a consensus has to be reached.)
3. Wait at least 24 hours before pushing it in.


I think it should be easily accessible from the website [1](http://sympy.org/development.html), probably from the README too. It should be clear to newcomers that not only contribution is very welcome, but also reviewing patches. (The latter currently lacks somewhat imho.) People new to sympy should not be afraid to review patches.

Maybe there should even be a short **how-to about reviewing patches**.

 

- *Category:* Training
- *Time to complete:* 48 hours

<a name="#2769"></a>
### [2769](http://code.google.com/p/sympy/issues/detail?id=2769&q=label%3ACodeInImportedIntoSpreadsheet) - Make video tutorials for SymPy

We can have several Code-In tasks for this.  Create some video tutorials for SymPy, and upload them to some SymPy channel on YouTube. 

- *Category:* Training
- *Time to complete:* 48 hours

<a name="#2806"></a>
### [2806](http://code.google.com/p/sympy/issues/detail?id=2806&q=label%3ACodeInImportedIntoSpreadsheet) - Add more tips to the tips page (10 tips)

We have a page of tips that we are compiling at [[tips]].  This should be really fleshed out, so that we have enough tips to do something interesting with.

For Code-In, we can create multiple tasks.  Each task (easy) can be to create say ten tips.
 

- *Category:* Training
- *Time to complete:* 48 hours

<a name="#2797"></a>
### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to German

Our webpage can be translated to other languages. Note that this is connected with [issue #2764](http://code.google.com/p/sympy/issues/detail?id=2764), about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change.
 

- *Category:* Translation
- *Time to complete:* 48 hours

<a name="#2797"></a>
### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to French

Our webpage can be translated to other languages. Note that this is connected with [issue #2764](http://code.google.com/p/sympy/issues/detail?id=2764), about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change.
 

- *Category:* Translation
- *Time to complete:* 48 hours

<a name="#2797"></a>
### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Czech

Our webpage can be translated to other languages. Note that this is connected with [issue #2764](http://code.google.com/p/sympy/issues/detail?id=2764), about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change.
 

- *Category:* Translation
- *Time to complete:* 48 hours

<a name="#2797"></a>
### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Polish

Our webpage can be translated to other languages. Note that this is connected with [issue #2764](http://code.google.com/p/sympy/issues/detail?id=2764), about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change.
 

- *Category:* Translation
- *Time to complete:* 48 hours

<a name="#2797"></a>
### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Bulgarian

Our webpage can be translated to other languages. Note that this is connected with [issue #2764](http://code.google.com/p/sympy/issues/detail?id=2764), about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change.
 

- *Category:* Translation
- *Time to complete:* 48 hours

<a name="#2797"></a>
### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Serbian

Our webpage can be translated to other languages. Note that this is connected with [issue #2764](http://code.google.com/p/sympy/issues/detail?id=2764), about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change.
 

- *Category:* Translation
- *Time to complete:* 48 hours

<a name="#2637"></a>
### [2637](http://code.google.com/p/sympy/issues/detail?id=2637&q=label%3ACodeInImportedIntoSpreadsheet) - Unicode Sigma for pretty printed Sum

I've been looking into how to pretty print the Sigma using unicode.  Here's what I've got so far:

This is what we do for ascii:

```
  n         
 __         
 \ `        
  )   2⋅f(k)
 /_,        
k = 1       
```

Here's the best unicode I have so far:

```
   n       
  __       
  ╲       
   )   f(k)
  ╱
  ‾‾      
 k = 1     
```

I couldn't find characters (yet) to replicate ` and , (the new horizontal lines are at a different height).  I also haven't found a better replacement for ).

There are these unicode symbols

```
⎲
⎳
```

(\u23b2 and \u23b3, respectively) which take up more than one character of space in my terminal (both width and height) and would actually look kind of nice for summations of that size.  So this is the issue from https://github.com/sympy/sympy/pull/389 again.  How do we programmatically tell if a symbol takes up more than one character space, and if so, how many?
 

- *Category:* UI
- *Time to complete:* 48 hours

<a name="#2636"></a>
### [2636](http://code.google.com/p/sympy/issues/detail?id=2636&q=label%3ACodeInImportedIntoSpreadsheet) - Pretty print Product

We should pretty print Product with a big capital Pi.  Something like

```
>>> product(f(k), (k, 1, n))
  n
-----
|   | f(k)
|   |
k = 1
```

in ascii, and 

```
>>> product(f(k), (k, 1, n))
  n
┌───┐
│   │ f(k)
│   │
k = 1
```

in unicode. Or, better, for unicode, do

```
  n
┬───┬
│   │ f(k)
│   │
k = 1
```

So it looks more like the capital Pi at http://en.wikipedia.org/wiki/Multiplication#Capital_Pi_notation.  I couldn't find a character as tall as │ but with a horizontal line at the bottom.
 

- *Category:* Code
- *Time to complete:* 48 hours


## Links:
- [[GCI-2011 Landing]]
- [[GCI-2011 Mentors]]
- [CGI-2011 Task list (spreadsheet)](https://docs.google.com/spreadsheet/ccc?key=0AiMKW-ZM-_fedFpSWm51VFBFZkdTRnh3WkhYRndSVXc)
- [GCI-2011 Task list (wiki)](https://github.com/sympy/sympy/wiki/GCI-2011-Task-list)
- [[GCI-2011 Organization Application]]