

# GCI-2011 Task list


The source if this page is based on the [google-malange](https://docs.google.com/spreadsheet/ccc?key=0AiMKW-ZM-_fedFpSWm51VFBFZkdTRnh3WkhYRndSVXc#gid=0) spreadsheet.

## Categories

<ul>
    <li><a href="##Hard">Hard</a></li>
    <li><a href="##Medium">Medium</a></li>
    <li><a href="##Easy">Easy</a></li>
</ul>

## <a name="#Hard">Hard</a>
### [93](http://code.google.com/p/sympy/issues/detail?id=93&q=label%3ACodeInImportedIntoSpreadsheet) - Square root denesting
<pre>
Just an idea: implement the &quot;square root denesting&quot; ideas of
<a href="http://www.almaden.ibm.com/cs/people/fagin/symb85.pdf" rel="nofollow">http://www.almaden.ibm.com/cs/people/fagin/symb85.pdf</a>
doesn't look to complicated.
I am happy to work on this after the prettyprinter works: that we can see what we are doing :-)

- Jurjen 
</pre>

- *Category:* Code
- *Time to complete:* 144 hours

### [2319](http://code.google.com/p/sympy/issues/detail?id=2319&q=label%3ACodeInImportedIntoSpreadsheet) - LaTeX input
<pre>
So my friend pointed out to me that WolphramAlpha lets you enter any LaTeX formula, and it will parse it and evaluate it.  I think we should have a parser that lets us do the same thing. In his case, he takes notes in LaTeX and does all of his homework in it, and he was able to just paste an expression from his homework into WolphramAlpha and it did if for him. 
</pre>

- *Category:* Code
- *Time to complete:* 144 hours

### [2626](http://code.google.com/p/sympy/issues/detail?id=2626&q=label%3ACodeInImportedIntoSpreadsheet) - Piecewise should use a different syntax for "otherwise"
<pre>
This is something that's been bothering me for a while.  Piecewise has the following syntax (I quote the docstring):

Usage
=====
  Piecewise( (expr,cond), (expr,cond), ... )
    - Each argument is a 2-tuple defining a expression and condition
    - The conds are evaluated in turn returning the first that is True.
      If any of the evaluated conds are not determined explicitly False,
      e.g. x &lt; 1, the function is returned in symbolic form.
    - If the function is evaluated at a place where all conditions are False,
      a ValueError exception will be raised.
    - Pairs where the cond is explicitly False, will be removed.

Examples
========
  &gt;&gt;&gt; from sympy import Piecewise, log
  &gt;&gt;&gt; from sympy.abc import x
  &gt;&gt;&gt; f = x**2
  &gt;&gt;&gt; g = log(x)
  &gt;&gt;&gt; p = Piecewise( (0, x&lt;-1), (f, x&lt;=1), (g, True))
  &gt;&gt;&gt; p.subs(x,1)
  1
  &gt;&gt;&gt; p.subs(x,5)
  log(5)

The problem is the use of (g, True) for the &quot;otherwise&quot; condition.  The problem is that if a conditional reduces to True, then this will be interpreted as an &quot;otherwise&quot; condition rather than returning it.  

In [7]: Piecewise((f(x), x &lt; 0), (x, 1 &gt; 0))
Out[7]: 
⎧f(x)  for x &lt; 0
⎨               
⎩ x    otherwise

This is also inconsistant in that it treats it correctly if only one condition is given:

In [6]: Piecewise((x, 1 &gt; 0))
Out[6]: x

But this is just because it looks like an &quot;otherwise&quot; condition with no other conditions.  

By the way, slightly related is <a title="Piecewise does not work when not given an &quot;otherwise&quot; condition"  href="/p/sympy/issues/detail?id=2567">issue 2567</a>.  

Unfortunately, this means breaking the syntax of Piecewise, but I think it should be done, as I'm quite convinced that the current way is wrong.

What's a better syntax?  Here's what Maple does:

piecewise(cond_1, f_1, cond_2, f_2, ..., cond_n, f_n, f_otherwise)

Although their conditions and functions are backwards (I like very much our (expr, cond) syntax), I think that making the last term the otherwise condition might work.

Or another option would be to make the otherwise condition a single element tuple.  This would have the advantage of potentially allowing Piecewise to return a Tuple without syntactical confusion.  

Indeed, I like this second option better.  So let's:

- Allow Piecewise((expr, cond), ..., (otherwise_expr,)) syntax
- Make Piecewise use the above syntax internally (i.e., for .args)
- Deprecate Piecewise(expr, cond), ..., (otherwise_expr, True)) syntax

This should be done before the next release, so we can start a deprecation cycle. 
</pre>

- *Category:* Code
- *Time to complete:* 144 hours

### [2773](http://code.google.com/p/sympy/issues/detail?id=2773&q=label%3ACodeInImportedIntoSpreadsheet) - Implement the trigsimp algorithm by fu et al
<pre>
Implement the algorithm for trigonometric simplification from the paper &quot;Automated and readable simplification of trigonometric expressions&quot; by Fu, et. al. (you should be able to find the paper for free from Google Scholar, otherwise email me and I will send it to you). 
</pre>

- *Category:* Code
- *Time to complete:* 144 hours

### [2789](http://code.google.com/p/sympy/issues/detail?id=2789&q=label%3ACodeInImportedIntoSpreadsheet) - minpoly should work with roots of unity in exponential form
<pre>
In [12]: minpoly(exp(I*pi/8))
ERROR: An unexpected error occurred while tokenizing input
The following traceback may be corrupted or invalid
The error message is: ('EOF in multi-line statement', (16, 0))
---------------------------------------------------------------------------
NotAlgebraic                              Traceback (most recent call last)
/Users/aaronmeurer/Documents/python/sympy/sympy/&lt;ipython-input-12-73afdce8b677&gt; in &lt;module&gt;()
----&gt; 1 minpoly(exp(I*pi/8))

/Users/aaronmeurer/Documents/python/sympy/sympy/sympy/polys/numberfields.pyc in minimal_polynomial(ex, x, **args)
    129         result = ex.q*x - ex.p
    130     else:
--&gt; 131         F = [x - bottom_up_scan(ex)] + mapping.values()
    132         G = groebner(F, symbols.values() + [x], order='lex')
    133 

/Users/aaronmeurer/Documents/python/sympy/sympy/sympy/polys/numberfields.pyc in bottom_up_scan(ex)
    117                 return symbols[ex.root]
    118 
--&gt; 119         raise NotAlgebraic(&quot;%s doesn't seem to be an algebraic number&quot; % ex)
    120 
    121     polys = args.get('polys', False)

NotAlgebraic: exp(I*pi/8) doesn't seem to be an algebraic number

But this is a root of x**16 - 1.  I don't know how minpoly works internally if this can be done in a general fashion for exponentials nested inside other expressions (like e.g., sqrt(1 + exp(I*pi/8))).

Marking as Code-In difficulty hard because this is a nontrivial algorithm, especially for a high school student. 
</pre>

- *Category:* Code
- *Time to complete:* 144 hours

### [1594](http://code.google.com/p/sympy/issues/detail?id=1594&q=label%3ACodeInImportedIntoSpreadsheet) - bin/test --random should also shuffle tests inside a file
Also it is related with issue 1594: once we have the shuffling, we should fix all the failures caused by it. Marking this as a hard task for Code-In, per Aaron's comment on the other issue. 

<pre>
Currently it only shuffles the test files, not the test functions. 
</pre>

- *Category:* QA
- *Labels:* Priority-Medium, Testing, Type-Defect
- *Time to complete:* 144 hours

### [2791](http://code.google.com/p/sympy/issues/detail?id=2791&q=label%3ACodeInImportedIntoSpreadsheet) - Allow to manage slow tests better with our test runner
Currently slow tests are simply skipped, but this makes it hard to actually run them. There should be a decorator for this (e.g. @slow) that would all to to run such tests when give an extra option to bin/test or test() (--slow and slow=True, respectively). It should be also possible to specify a timeout for slow tests so that they do not hang test runner. It should be also possible to press Ctrl+C (KeyboardInterrupt) to kill a slow test without killing test runner. There should be statistics added at the end which would tell how many slow tests were run, how many timed out and maybe other. Also, almost all skipped tests (or maybe all) are currently skipped because they are slow, so after this is implemented, they should all be converted. 

<pre>
Currently slow tests are simply skipped, but this makes it hard to actually run them. There should be a decorator for this (e.g. @slow) that would all to to run such tests when give an extra option to bin/test or test() (--slow and slow=True, respectively). It should be also possible to specify a timeout for slow tests so that they do not hang test runner. It should be also possible to press Ctrl+C (KeyboardInterrupt) to kill a slow test without killing test runner. There should be statistics added at the end which would tell how many slow tests were run, how many timed out and maybe other. 
</pre>

- *Category:* QA
- *Labels:* Priority-Medium, Testing, Type-Enhancement
- *Time to complete:* 144 hours

### [2799](http://code.google.com/p/sympy/issues/detail?id=2799&q=label%3ACodeInImportedIntoSpreadsheet) - coverage testing should be part of the bot test
<pre>
Two things on my wish list for testing;

1) a coverage fingerprint of master would be compared to a given branch's coverage profile to make sure that no line has become uncovered.

2) a report of lines added that are not covered would be reported with the test-bot report.

Someone who likes parsing html (beautiful soup (*) might help with this) might enjoy this as a project. Google CodeIn?

(*) www.crummy.com/software/BeautifulSoup/ 
</pre>

- *Category:* QA
- *Labels:* Priority-Medium, Testing, Type-Enhancement
- *Time to complete:* 144 hours

### [2812](http://code.google.com/p/sympy/issues/detail?id=2812&q=label%3ACodeInImportedIntoSpreadsheet) - Fix failures found by shuffling tests in test file
<pre>
This builds on <a title="bin/test --random should also shuffle tests inside a file"  href="/p/sympy/issues/detail?id=1594">issue 1594</a>: once we have the shuffling, we should fix all the failures caused by it. Marking this as a hard task for Code-In, per Aaron's comment on the other issue. 
</pre>

- *Category:* QA
- *Time to complete:* 144 hours

### [1941](http://code.google.com/p/sympy/issues/detail?id=1941&q=label%3ACodeInImportedIntoSpreadsheet) - Objects that know how to combine themselves
<pre>
This is related to <a title="more efficient core"  href="/p/sympy/issues/detail?id=1908">issue 1908</a>.  When I met with Ondrej last summer, we worked on a core where 
objects knew how to combine themselves with respect to Mul and Add.  See the handler branch at 
<a href="http://github.com/certik/sympyx/" rel="nofollow">http://github.com/certik/sympyx/</a>.  The idea originally stemmed from <a title="Arbitrary constant type"  href="/p/sympy/issues/detail?id=1336">issue 1336</a>, but we soon 
discovered that it also simplifies the logic for things like O() (the order function), and oo, which 
combine abnormally with respect to Mul and Add.  This could also be useful for <a title="Improvements for physical units"  href="/p/sympy/issues/detail?id=1940">issue 1940</a>, so that 
the units could tell Mul that they need to stay together without Mul explicitly having to know about 
units.  Right now, Mul.flatten is cluttered with code for handling all these things, and the only way 
to handle additional classes is to either completely separate them from Basic (as with Poly), or to 
add more special case code in Mul.flatten.  

Anyway, if we ever rework the core as suggested in <a title="more efficient core"  href="/p/sympy/issues/detail?id=1908">issue 1908</a> or elsewhere, we should also look 
into doing this too. 
</pre>

- *Category:* Research
- *Time to complete:* 144 hours

### [2765](http://code.google.com/p/sympy/issues/detail?id=2765&q=label%3ACodeInImportedIntoSpreadsheet) - Research ways to do the assumptions system, including removing the old system
<pre>
See <a href="https://github.com/sympy/sympy/wiki/Assumptions" rel="nofollow">https://github.com/sympy/sympy/wiki/Assumptions</a> and some threads on the mailing list, as well as any issue with the Assumptions label.  We have two assumptions systems in SymPy, the old system, which works like 

&gt;&gt;&gt; x = Symbol('x', positive=True)
&gt;&gt;&gt; x.is_positive
True

and the new system, which works like

&gt;&gt;&gt; ask(Q.positive(x), Q.positive(x))
True 
</pre>

- *Category:* Research
- *Labels:* Assumptions, 
- *Time to complete:* 144 hours

### [2792](http://code.google.com/p/sympy/issues/detail?id=2792&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate how to employ complexity measures in functions like trigsimp(), etc.
<pre>
simplify() already implements measure argument and uses it to choose over alternative expressions given by pairs of specific simplification routines. However, those specific simplification routines (like trigsimp()) don't support measure argument and make arbitrary built-in choices when simplifying expressions. This leads to simplification results that are dependent on the implicit measure built-in into a particular simplification step of a function. Those functions should use a measure to verify whether a candidate simplified expression is really simpler than an input expression. Investigate how to implement measures in those functions (at least in trigsimp()) to avoid combinatorial explosion of choices. You may have to employ optimization techniques like greedy algorithms, dynamic programming, meta heuristics, etc. Prepare sample non-trivial inputs, measures and outputs that can be used as tests for the algorithm(s) you will propose. 
</pre>

- *Category:* Research
- *Time to complete:* 144 hours

### [1817](http://code.google.com/p/sympy/issues/detail?id=1817&q=label%3ACodeInImportedIntoSpreadsheet) - SymPy Cheat Sheet
<pre>
See <a href="http://groups.google.com/group/sympy/browse_thread/thread/f3b1ddc8b6333748" rel="nofollow">http://groups.google.com/group/sympy/browse_thread/thread/f3b1ddc8b6333748</a>

The idea is to make a cheat sheet for sympy, similar to <a href="http://wiki.sagemath.org/quickref" rel="nofollow">http://wiki.sagemath.org/quickref</a>.  

Maybe if we have a doc-day 2010... 
</pre>

- *Category:* Training
- *Time to complete:* 144 hours

### [2771](http://code.google.com/p/sympy/issues/detail?id=2771&q=label%3ACodeInImportedIntoSpreadsheet) - Write a document showing the difference between SymPy and other mathematical systems: Maple
<pre>
We should document the differences between SymPy and other mathematical systems.  For Code-In, a task should be for one other system. 
</pre>

- *Category:* Training
- *Time to complete:* 144 hours

### [2521](http://code.google.com/p/sympy/issues/detail?id=2521&q=label%3ACodeInImportedIntoSpreadsheet) - live.sympy.org isn't so easy to use on a mobile device
<pre>
I tried the new live.sympy.org on my 1st gen iPod touch (iOS 3).  There are a couple of things that make the usage difficult:

- Pressing both &quot;Return&quot; and &quot;Shift-Return&quot; on the keyboard just creates a newline in the input, regardless of whether the &quot;Enter/Shift-Enter&quot; popup is set to.  You can still enter the expression by pressing the &quot;Evaluate&quot; button, but it would be nice if the keyboard worked.

- There's no way to access the history.  There is no &quot;Control&quot; key on an iPod touch.

- You cannot scroll within a frame in mobile Safari, so you can't access the history of the session beyond a few inputs.

- This may be an inherent problem with the fonts in iOS, but the unicode output of the result of dsolve(f(x).diff(x, x) + 2*f(x).diff(x) + f(x) - exp(x) + sin(x), f(x)) is a little off.  I'm happy to report that the LaTeX output works great, though.

- There are a few minor issues with the size of things, which would be fixed the best if there were a mobile version of the site.  But this is a lower priority.  If the above items can be fixed, the site as it is will work just fine in a mobile environment. 
</pre>

- *Category:* UI
- *Time to complete:* 144 hours

### [2768](http://code.google.com/p/sympy/issues/detail?id=2768&q=label%3ACodeInImportedIntoSpreadsheet) - Add a feed of what people are doing at SymPy Live
It would be cool to have a little feed at the right on live.sympy.org to show what other people are entering, so that people can see what sorts of things are being done.  

<pre>
It would be cool to have a little feed at the right on live.sympy.org to show what other people are entering, so that people can see what sorts of things are being done.  Of course, you should be able to disable this for your own entries, for privacy reasons.  It should allow you to input the same expression in your session and execute it. 
</pre>

- *Category:* UI
- *Labels:* Live, Priority-Medium, Type-Defect
- *Time to complete:* 144 hours

### [2772](http://code.google.com/p/sympy/issues/detail?id=2772&q=label%3ACodeInImportedIntoSpreadsheet) - Some UI/GUI for the test runner
<pre>
It would be cool to have some UI/GUI for the test runner that makes it easier to see the failures when they happen. 
</pre>

- *Category:* UI
- *Labels:* Priority-Medium, Type-Enhancement
- *Time to complete:* 144 hours

It would be cool to have some UI/GUI for the test runner that makes it easier to see the failures when they happen. E.g. like http://sourceforge.net/apps/mediawiki/cppunit/nfs/project/c/cp/cppunit/c/c2/Qttestrunner_exa.png  

## <a name="#Medium">Medium</a>
### [281](http://code.google.com/p/sympy/issues/detail?id=281&q=label%3ACodeInImportedIntoSpreadsheet) - Infinity should not be a subclass of Rational
<pre>
&gt;&gt;&gt; isinstance(oo, Rational)
True
&gt;&gt;&gt; oo.is_rational
True

This is clearly wrong. Infinity is not a rational number. 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

### [363](http://code.google.com/p/sympy/issues/detail?id=363&q=label%3ACodeInImportedIntoSpreadsheet) - Add a split() method for sympy expressions
<pre>
I think a method that does the opposite of reduce(operator, [x,y,...])
would be useful. Something like this:

&gt;&gt;&gt; (x+y+z).split('+')
(x, y+z)
&gt;&gt;&gt; (x+y+z).split('+', flatten=True)
(x, y, z)
&gt;&gt;&gt; (x+y+z).split('*')
(x+y+z,)
&gt;&gt;&gt; (x+y+z).split('*', coefficient=True)
(1, x+y+z)
&gt;&gt;&gt; (x/y).split('/')
(x, y)
&gt;&gt;&gt; (x*y).split('/')
(x, 1/y)
&gt;&gt;&gt; (x**2).split('**')
(x, 2)

Various keyword arguments could be added for whether to split rational
numbers, etc. With such options, split() could replace several existing
methods like as_coefficient, as_independent, as_base_exp, as_numer_denom,
etc. It is better to only have to remember a single method.

Using an operator symbol like '+' as argument instead of a class is my
preference as it would be more readable and more versatile ('/' can be used
even though we have no Div class).

A method like this would be especially useful if Add and Mul are changed as
discussed in <a title="Possible speed improvements to core"  href="/p/sympy/issues/detail?id=362">issue 362</a>, as its interface would be independent of the
underlying representation. 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [716](http://code.google.com/p/sympy/issues/detail?id=716&q=label%3ACodeInImportedIntoSpreadsheet) - either tangent_line or is_tangent is wrong
<pre>
In [1]: e = Ellipse(Point(0,0), 3, 2)

In [2]: t = e.tangent_line(e.random_point())

In [3]: e.is_tangent(t)
Out[3]: False


Obviously [2] and [3] are in contradiction. By plotting the result, [2] is
most probably right, so [3] is wrong. 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

### [754](http://code.google.com/p/sympy/issues/detail?id=754&q=label%3ACodeInImportedIntoSpreadsheet) - Have re and im call expand(complex=True)
<pre>
Here is a nice integral that SymPy is able to compute:

&gt;&gt;&gt; from sympy import *
&gt;&gt;&gt; var('y')
y
&gt;&gt;&gt; a = integrate((16*y-16)/(y**4-2*y**3+4*y-4), (y, 0, 1))
&gt;&gt;&gt; a = simplify(a)
&gt;&gt;&gt; pprint(a)
                                              ___
-2*log(2) + 2*pi + 2*log(1 + I) + 2*log(1 + \/ 2 ) + 2*log(1 - I) + 2*log(1 -

  ___
\/ 2 ) - 2*pi*I - 2*I*log(1 - I) + 2*I*log(1 + I)

Simplifying the answer by hand is straightforward (add up the real and
imaginary parts), but unfortunately, SymPy is unable to do this. (It also
fails to produce a numerical value: a.evalf() -&gt; ValueError.) It seems that
currently re and as_real_imag don't know anything about logarithms:

&gt;&gt;&gt; re(a)
-2*log(2) + 2*pi + 2*log(1 + 2**(1/2)) + re(2*log(1 + I) + 2*log(1 - I) +
2*log(1 - 2**(1/2)) - 2*I*log(1 - I) + 2*I*log(1 + I))
&gt;&gt;&gt; a.as_real_imag()
(pi + 2*log(1 + I) - 2*I*log(1 + I) + log(2) + log(1 + 2**(1/2)) + log(1 -
2**(1/2)), 2*log(2))
&gt;&gt;&gt; a.expand(complex=True)
pi + 2*log(1 + I) - 2*I*log(1 + I) + 2*I*log(2) + log(2) + log(1 +
2**(1/2)) + log(1 - 2**(1/2))

I was thinking of fixing this, but I'm not sure where the right place is.
According to re(), &quot;This function performs only elementary analysis and so
it will fail to decompose properly more complicated expressions. If
completely simplified result is needed then use Basic.as_real_imag() or
perform complex expansion on instance of this function.&quot; This doesn't even
seem to be correct: re() actually performs some analysis, while
Basic.as_real_imag() only looks for multiples of I without further
analysis. Then there is _eval_expand_complex, which seems to use an
entirely separate implementation (I tried implementing _eval_expand_complex
in log, which didn't affect the output of re or as_real_imag() -- in fact,
implementing it didn't even make a.expand(complex=True) work).

I think there should be only one function that implements expansion of an
expression into real and imaginary parts, and this should be used by re,
im, as_real_imag, expand(complex=True), etc (are there others?). It should
use a recursive algorithm and overloading a single method in a custom class
should be enough to make all these functions work.

Last, we may want to add a heuristic to simplify() that splits the
expression into real and imaginary parts, simplifies those separately, and
adds them together. 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

### [2513](http://code.google.com/p/sympy/issues/detail?id=2513&q=label%3ACodeInImportedIntoSpreadsheet) - Create a SymPyDeprecationWarning for deprecated SymPy behavior
<pre>
DeprecationWarning is turned off by default in Python 2.7, so all of our deprecated behavior that we deprecate with DeprecationWarning is not shown to the majority of our users (unless they are specifically looking for it, they won't find it).  This was done because most users of Python programs can't do anything if the program uses deprecated behavior, so they don't care to see the warning.  But I think most developers don't really do a good job of turning the warnings on, unfortunately.

I think we should create a SymPyDeprecationWarning that subclasses from DeprecationWarning, but is turned on by default in isympy.  See <a title="Turn on deprecation warnings in isympy"  href="/p/sympy/issues/detail?id=2142">issue 2142</a>.  That way, users of scripts that use sympy won't be bothered by them, but people who use isympy, who should be bothered by them in my opinion, will be. This will likely also include the developers of most of those scripts. 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

### [2552](http://code.google.com/p/sympy/issues/detail?id=2552&q=label%3ACodeInImportedIntoSpreadsheet) - (1/(x*y)).subs(x*y, whatever) doesn't work
This is doesn't work >>> (1/(x*y)).subs(x*y, 2);1/(x*y). Because >>> (1/(x*y)).args; (1/x, 1/y) automatically changed in Mul class  

<pre>
In [1]: (1/(x*y)).subs(x*y, 2)
Out[1]: 
 1 
───
x⋅y 
</pre>

- *Category:* Code
- *Labels:* Priority-High, Type-Defect
- *Time to complete:* 96 hours

### [2632](http://code.google.com/p/sympy/issues/detail?id=2632&q=label%3ACodeInImportedIntoSpreadsheet) - Add isympy -c qtconsole
<pre>
You can open the IPython qtconsole with a sympy session by typing &quot;IPython qtconsole --profile=sympy&quot;, but you should also be able to do it by typing &quot;isympy -c ipython-qtconsole&quot;.  Unlike the former, the latter should perhaps not rely on IPython's built-in sympy profile to work. 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

### [2793](http://code.google.com/p/sympy/issues/detail?id=2793&q=label%3ACodeInImportedIntoSpreadsheet) - The dsolve solver for 1st_exact should use integration
<pre>
The method used by the 1st_exact solver is a nice one to use by hand, but it's kind of flaky.  I didn't realize at the time of writing it that you can actually express the solution using integrals without introducing parameters or dummy integration limits.  This solution is given in Table II of the paper &quot;Symbolic Integration: The Stormy Decade&quot; by Joel Moses.  I was able to download this paper for free from Google Scholar.  If you cannot access it and are interested in fixing this issue, contact me and I will send it to you. 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

### [2794](http://code.google.com/p/sympy/issues/detail?id=2794&q=label%3ACodeInImportedIntoSpreadsheet) - Implement ode solvers from the Moses "Stormy Decade" paper: Almost Linear
<pre>
See Table II of the paper &quot;Symbolic Integration: The Stormy Decade&quot; by Joel Moses.  Some of these are not implemented yet, in particular, the last three.  

I was able to download this paper for free from Google Scholar.  If you cannot access it and are interested in fixing this issue, contact me and I will send it to you.

See also <a title="The dsolve solver for 1st_exact should use integration"  href="/p/sympy/issues/detail?id=2793">issue 2793</a>.

Each solver should be a separate Code-In task. 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

### [2841](http://code.google.com/p/sympy/issues/detail?id=2841&q=label%3ACodeInImportedIntoSpreadsheet) - integrate() can not integrate the Abs() function, fix it
<pre>
In Dev version

&gt;&gt;&gt; import sympy
&gt;&gt;&gt; x = sympy.Symbol('x')
&gt;&gt;&gt; i = sympy.integrate(sympy.Abs(x), (x, -1, 1))
&gt;&gt;&gt; i.n()

/env/src/sympy/sympy/core/evalf.pyc in evalf(self, n, subs, maxn, chop, strict, quad, verbose)
   1022             options['quad'] = quad
   1023         try:
-&gt; 1024             result = evalf(self, prec+4, options)
   1025         except NotImplementedError:
   1026             # Fall back to the ordinary evalf


/env/src/sympy/sympy/core/evalf.pyc in evalf(x, prec, options)
    954     try:
    955         rf = evalf_table[x.func]
--&gt; 956         r = rf(x, prec, options)
    957     except KeyError:
    958         #r = finalize_complex(x._eval_evalf(prec)._mpf_, fzero, prec)


/env/src/sympy/sympy/core/evalf.pyc in evalf_integral(expr, prec, options)
    741     maxprec = options.get('maxprec', INF)
    742     while 1:
--&gt; 743         result = do_integral(expr, workprec, options)
    744         accuracy = complex_accuracy(result)
    745         if accuracy &gt;= prec or workprec &gt;= maxprec:

/env/src/sympy/sympy/core/evalf.pyc in do_integral(expr, prec, options)
    706             quadrature_error = MINUS_INF
    707         else:
--&gt; 708             result, quadrature_error = quadts(f, [xlow, xhigh], error=1)
    709             quadrature_error = fastlog(quadrature_error._mpf_)
    710 

/env/src/sympy/sympy/mpmath/calculus/quadrature.pyc in quadts(ctx, *args, **kwargs)
    784         &quot;&quot;&quot;
    785         kwargs['method'] = 'tanh-sinh'
--&gt; 786         return ctx.quad(*args, **kwargs)
    787 
    788     def quadgl(ctx, *args, **kwargs):

/env/src/sympy/sympy/mpmath/calculus/quadrature.pyc in quad(ctx, f, *points, **kwargs)
    741             ctx.prec += 20
    742             if dim == 1:
--&gt; 743                 v, err = rule.summation(f, points[0], prec, epsilon, m, verbose)
    744             elif dim == 2:
    745                 v, err = rule.summation(lambda x: \

/env/src/sympy/sympy/mpmath/calculus/quadrature.pyc in summation(self, f, points, prec, epsilon, max_degree, verbose)
    230                     print(&quot;Integrating from %s to %s (degree %s of %s)&quot; % \
    231                         (ctx.nstr(a), ctx.nstr(b), degree, max_degree))
--&gt; 232                 results.append(self.sum_next(f, nodes, degree, prec, results, verbose))
    233                 if degree &gt; 1:
    234                     err = self.estimate_error(results, prec, epsilon)

/env/src/sympy/sympy/mpmath/calculus/quadrature.pyc in sum_next(self, f, nodes, degree, prec, previous, verbose)
    302         else:
    303             S = self.ctx.zero
--&gt; 304         S += self.ctx.fdot((w,f(x)) for (x,w) in nodes)
    305         return h*S
    306 

/env/src/sympy/sympy/mpmath/ctx_mp_python.pyc in fdot(ctx, A, B, conjugate)
    923         hasattr_ = hasattr
    924         types = (ctx.mpf, ctx.mpc)
--&gt; 925         for a, b in A:
    926             if type(a) not in types: a = ctx.convert(a)
    927             if type(b) not in types: b = ctx.convert(b)

/env/src/sympy/sympy/mpmath/calculus/quadrature.pyc in &lt;genexpr&gt;((x, w))
    302         else:
    303             S = self.ctx.zero
--&gt; 304         S += self.ctx.fdot((w,f(x)) for (x,w) in nodes)
    305         return h*S
    306 

/env/src/sympy/sympy/core/evalf.pyc in f(t)
    679 
    680         def f(t):
--&gt; 681             re, im, re_acc, im_acc = evalf(func, mp.prec, {'subs':{x:t}})
    682 
    683             have_part[0] = re or have_part[0]

/env/src/sympy/sympy/core/evalf.pyc in evalf(x, prec, options)
    954     try:
    955         rf = evalf_table[x.func]
--&gt; 956         r = rf(x, prec, options)
    957     except KeyError:
    958         #r = finalize_complex(x._eval_evalf(prec)._mpf_, fzero, prec)


/env/src/sympy/sympy/core/evalf.pyc in evalf_abs(expr, prec, options)
    140 
    141 def evalf_abs(expr, prec, options):
--&gt; 142     return get_abs(expr.args[0], prec, options)
    143 
    144 def evalf_re(expr, prec, options):

/env/src/sympy/sympy/core/evalf.pyc in get_abs(expr, prec, options)
    125         return libmp.mpc_abs((re, im), prec), None, re_acc, None
    126     else:
--&gt; 127         return mpf_abs(re), None, re_acc, None
    128 
    129 def get_complex_part(expr, no, prec, options):

/env/src/sympy/sympy/mpmath/libmp/libmpf.pyc in mpf_abs(s, prec, rnd)
    653     precision. The prec argument can be omitted to generate an
    654     exact result.&quot;&quot;&quot;
--&gt; 655     sign, man, exp, bc = s
    656     if (not man) and exp:
    657         if s == fninf:

TypeError: 'NoneType' object is not iterable 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

### [2849](http://code.google.com/p/sympy/issues/detail?id=2849&q=label%3ACodeInImportedIntoSpreadsheet) - Better heuristics and simplification for integral of cos(x)/sin(x)**n and similar
<pre>
The result of integrate(cos(x)/sin(x)**n, x) is
&quot;nice&quot;, if n is even, and &quot;ugly&quot;, if n is odd
(n is an integer, greater than 1).

Moreover, if n is odd, then diff(integrate(cos(x)/sin(x)**n, x), x)
gives a very ugly expression that cannot be converted back to
cos(x)/sin(x)**n by simplify.

Example:
In [136]: diff(integrate(cos(x)/sin(x)**7, x), x)
             5                   3                      
36⋅sin(x)⋅cos (x) - 72⋅sin(x)⋅cos (x) + 36⋅sin(x)⋅cos(x)
────────────────────────────────────────────────────────
                                                2       
       ⎛     6            4            2       ⎞        
       ⎝6⋅cos (x) - 18⋅cos (x) + 18⋅cos (x) - 6⎠        

Gabor Takacs 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

### [294](http://code.google.com/p/sympy/issues/detail?id=294&q=label%3ACodeInImportedIntoSpreadsheet) - Pass coverage_doctest.py
<pre>
This may have been mentioned before, but I'm creating an issue specific for it.

I think there should soon be documentation in the code for most, if not
all, of the classes and functions, even if it is only a single line. This
can be useful for both the generated API documentation, and through
interactive help (i.e., the help() command in an interactive Python
session). If there is a need for this, I am fine going through all of the
code and documenting everything, or getting a good start on it. 
</pre>

- *Category:* Documentation
- *Time to complete:* 96 hours

### [707](http://code.google.com/p/sympy/issues/detail?id=707&q=label%3ACodeInImportedIntoSpreadsheet) - move some wikis to github.com/sympy/sympy/wiki
<pre>
Move all wikis, that have an equivalent on wiki.sympy.org to it? I.e. let's
remove

<a href="http://code.google.com/p/sympy/wiki/Tutorial" rel="nofollow">http://code.google.com/p/sympy/wiki/Tutorial</a>

and similar, and update all links to wiki.sympy.org?

So that we have just one source of documentation to reduce confusion. 
</pre>

- *Category:* Documentation
- *Time to complete:* 96 hours

### [2470](http://code.google.com/p/sympy/issues/detail?id=2470&q=label%3ACodeInImportedIntoSpreadsheet) - Fix all sphinx errors and warnings
<pre>
Currently when we issue:

$ cd doc
$ make html

we get a lot of errors/warnings related to improper syntax in documentation and docstrings:

/home/mateusz/repo/git/sympy/doc/src/aboutus.txt:: (WARNING/2) Duplicate explicit target name: &quot;more info&quot;.
/home/mateusz/repo/git/sympy/sympy/core/basic.py:docstring of sympy.core.basic.Basic.atoms:13: (ERROR/3) Inconsistent literal block quoting.
/home/mateusz/repo/git/sympy/sympy/core/basic.py:docstring of sympy.core.basic.Basic.atoms:18: (WARNING/2) Literal block expected; none found.
/home/mateusz/repo/git/sympy/sympy/core/basic.py:docstring of sympy.core.basic.Basic.atoms:22: (ERROR/3) Inconsistent literal block quoting.
/home/mateusz/repo/git/sympy/sympy/core/basic.py:docstring of sympy.core.basic.Basic.atoms:39: (ERROR/3) Inconsistent literal block quoting.
/home/mateusz/repo/git/sympy/sympy/core/basic.py:docstring of sympy.core.basic.Basic.atoms:48: (ERROR/3) Inconsistent literal block quoting.
/home/mateusz/repo/git/sympy/sympy/core/basic.py:docstring of sympy.core.basic.Basic.atoms:60: (ERROR/3) Inconsistent literal block quoting.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.as_coeff_add:16: (WARNING/2) Inline emphasis start-string without end-string.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.as_coeff_mul:16: (WARNING/2) Inline emphasis start-string without end-string.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.as_independent:4: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.as_independent:7: (WARNING/2) Block quote ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.compute_leading_term:5: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.compute_leading_term:7: (WARNING/2) Block quote ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.is_polynomial:3: (WARNING/2) Inline emphasis start-string without end-string.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.is_polynomial:3: (WARNING/2) Inline emphasis start-string without end-string.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.series:17: (WARNING/2) Block quote ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.series:18: (WARNING/2) Block quote ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.series:29: (WARNING/2) Block quote ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.series:30: (WARNING/2) Block quote ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/core/expr.py:docstring of sympy.core.expr.Expr.series:31: (WARNING/2) Block quote ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/core/add.py:docstring of sympy.core.add.Add.primitive:4: (SEVERE/4) Unexpected section title.

Example
=======
/home/mateusz/repo/git/sympy/doc/src/modules/core.txt:29: (WARNING/2) Explicit markup ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/doc/src/modules/evalf.txt:38: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/functions/elementary/miscellaneous.py:docstring of sympy.functions.elementary.miscellaneous.Min:4: (SEVERE/4) Unexpected section title.

Example
-------
/home/mateusz/repo/git/sympy/sympy/functions/elementary/miscellaneous.py:docstring of sympy.functions.elementary.miscellaneous.Min:27: (SEVERE/4) Unexpected section title.

See Also
--------
/home/mateusz/repo/git/sympy/sympy/functions/elementary/miscellaneous.py:docstring of sympy.functions.elementary.miscellaneous.Max:21: (SEVERE/4) Unexpected section title.

Example
-------
/home/mateusz/repo/git/sympy/sympy/functions/elementary/miscellaneous.py:docstring of sympy.functions.elementary.miscellaneous.Max:53: (SEVERE/4) Unexpected section title.

Algorithm
---------
/home/mateusz/repo/git/sympy/sympy/functions/elementary/miscellaneous.py:docstring of sympy.functions.elementary.miscellaneous.Max:80: (SEVERE/4) Unexpected section title.

See Also
--------
/home/mateusz/repo/git/sympy/sympy/functions/elementary/complexes.py:docstring of sympy.functions.elementary.complexes.sign:3: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/functions/special/delta_functions.py:docstring of sympy.functions.special.delta_functions.DiracDelta:5: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/functions/special/delta_functions.py:docstring of sympy.functions.special.delta_functions.DiracDelta:6: (WARNING/2) Block quote ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/functions/special/delta_functions.py:docstring of sympy.functions.special.delta_functions.Heaviside:4: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/functions/special/delta_functions.py:docstring of sympy.functions.special.delta_functions.Heaviside:5: (WARNING/2) Block quote ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/functions/special/delta_functions.py:docstring of sympy.functions.special.delta_functions.Heaviside:7: (WARNING/2) Enumerated list ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/functions/elementary/miscellaneous.py:docstring of sympy.functions.elementary.miscellaneous.Max:58: (ERROR/3) Unknown target name: &quot;1&quot;.
/home/mateusz/repo/git/sympy/doc/src/modules/logic.txt:15: (WARNING/2) Inline substitution_reference start-string without end-string.
/home/mateusz/repo/git/sympy/doc/src/modules/logic.txt:44: (WARNING/2) error while formatting arguments for sympy.logic.boolalg.Xor: Xor is not a Python function
/home/mateusz/repo/git/sympy/doc/src/modules/logic.txt:46: (WARNING/2) error while formatting arguments for sympy.logic.boolalg.Nand: Nand is not a Python function
/home/mateusz/repo/git/sympy/doc/src/modules/logic.txt:48: (WARNING/2) error while formatting arguments for sympy.logic.boolalg.Nor: Nor is not a Python function
/home/mateusz/repo/git/sympy/doc/src/modules/logic.txt:50: (WARNING/2) error while formatting arguments for sympy.logic.boolalg.Equivalent: Equivalent is not a Python function
/home/mateusz/repo/git/sympy/sympy/matrices/matrices.py:docstring of sympy.matrices.matrices.Matrix.print_nonzero:6: (ERROR/3) Inconsistent literal block quoting.
/home/mateusz/repo/git/sympy/sympy/printing/fcode.py:docstring of sympy.printing.fcode.fcode:10: (WARNING/2) Definition list ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/printing/fcode.py:docstring of sympy.printing.fcode.fcode:12: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/printing/fcode.py:docstring of sympy.printing.fcode.fcode:13: (WARNING/2) Block quote ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/sympy/simplify/simplify.py:docstring of sympy.simplify.simplify.collect:119: (ERROR/3) Inconsistent literal block quoting.
/home/mateusz/repo/git/sympy/doc/src/modules/simplify.txt:2: WARNING: duplicate object description of sympy.simplify.simplify.powsimp, other instance in /home/mateusz/repo/git/sympy/doc/src/gotchas.txt, use :noindex: for one of them
/home/mateusz/repo/git/sympy/doc/src/modules/simplify.txt:2: WARNING: duplicate object description of sympy.simplify.cse_main.cse, other instance in /home/mateusz/repo/git/sympy/doc/src/modules/rewriting.txt, use :noindex: for one of them
/home/mateusz/repo/git/sympy/sympy/solvers/ode.py:docstring of sympy.solvers.ode.ode_1st_homogeneous_coeff_best:14: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/solvers/ode.py:docstring of sympy.solvers.ode.ode_1st_homogeneous_coeff_subs_dep_div_indep:49: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/solvers/ode.py:docstring of sympy.solvers.ode.ode_Liouville:5: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/solvers/ode.py:docstring of sympy.solvers.ode.ode_Liouville:30: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/solvers/ode.py:docstring of sympy.solvers.ode.ode_separable:33: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/solvers/ode.py:docstring of sympy.solvers.ode:40: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/sympy/tensor/indexed.py:docstring of sympy.tensor.indexed.Indexed.ranges:3: (WARNING/2) Inline literal start-string without end-string.
/home/mateusz/repo/git/sympy/sympy/utilities/autowrap.py:docstring of sympy.utilities.autowrap.autowrap:25: (WARNING/2) Inline interpreted text or phrase reference start-string without end-string.
/home/mateusz/repo/git/sympy/doc/src/tutorial.txt:99: (WARNING/2) Explicit markup ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/doc/src/tutorial.txt:112: (ERROR/3) Unexpected indentation.
/home/mateusz/repo/git/sympy/doc/src/tutorial.txt:113: (WARNING/2) Block quote ends without a blank line; unexpected unindent.
/home/mateusz/repo/git/sympy/doc/src/tutorial.txt:114: (WARNING/2) Block quote ends without a blank line; unexpected unindent.

I have a branch (well, one commit) that fixes all those problems, but one (the first one). I will have to rebase it over master and I will submit a pull request. 
</pre>

- *Category:* Documentation
- *Time to complete:* 96 hours

### [2770](http://code.google.com/p/sympy/issues/detail?id=2770&q=label%3ACodeInImportedIntoSpreadsheet) - Update stuff that SymPy can do on the homepage
<pre>
The list of things that SymPy can do on the homepage is not up to date, because we can actually do a lot more things than that.  This should be updated. 
</pre>

- *Category:* Documentation
- *Time to complete:* 96 hours

### [2779](http://code.google.com/p/sympy/issues/detail?id=2779&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Geometry
<pre>
Edit the doc-string to add list of other function that are closely related to the query.


This is the list of .py files which contains the functions.

sympy/geometry/curve.py
sympy/geometry/ellipse.py
sympy/geometry/entity.py
sympy/geometry/exceptions.py
sympy/geometry/__init__.py
sympy/geometry/line.py
sympy/geometry/point.py
sympy/geometry/polygon.py
sympy/geometry/util.py

There are around 150 functions which one needs to understand (the input parameters and final result and not the code) to interrelate them. 
</pre>

- *Category:* Documentation
- *Time to complete:* 96 hours

### [2801](http://code.google.com/p/sympy/issues/detail?id=2801&q=label%3ACodeInImportedIntoSpreadsheet) - lambdify() is not mentioned anywhere
<pre>
lambdify() is one of most important functions in SymPy (for interoperability with numerical libraries the most important). However it's not mentioned anywhere, although it has a good docstring. The result of `git grep` stands for itself:

$ git grep lambdify doc/
doc/src/aboutus.txt:#. Sebastian Krämer: implemented lambdify/numpy/mpmath cooperation, bug fixes, refactoring, lambdifying of matrices, large printing refactoring and bugfixes
doc/src/aboutus.txt:#. Andrew Straw: lambdify() improvements
doc/src/aboutus.txt:#. Matthew Brett: fixes to lambdify
doc/src/modules/physics/mechanics/examples.txt:maximum recursion depth being exceeded; I also tried lambdifying this, and it

lambdify's docstring must be pulled into docs (there is already a generic issue for this), but we also need a good tutorial showing users how to cooperate with NumPy, SciPy etc. This issue (not the only one by the way) was pointed out to me by Fernando Perez during my stay at Berkeley this week, when trying to solve a practical symbolic-numeric problem. SymPy has already *a lot* of features, but unfortunately most of them are deeply buried in the internals of SymPy and known only to its developers. Also we have to check what does ufuncify() do, because it was reported to me that it's extremely slow. 
</pre>

- *Category:* Documentation
- *Time to complete:* 96 hours

### [2528](http://code.google.com/p/sympy/issues/detail?id=2528&q=label%3ACodeInImportedIntoSpreadsheet) - Update SymPy's Wikipedia article
<pre>
I just noticed that <a href="http://en.wikipedia.org/wiki/SymPy" rel="nofollow">http://en.wikipedia.org/wiki/SymPy</a> is a little old with its information.  None of it is wrong, but I think the features list could be updated.  It seems to be roughly the same as the features listed at sympy.org and <a href="http://code.google.com/p/sympy/" rel="nofollow">http://code.google.com/p/sympy/</a>, so perhaps those should be updated too.

Also, SymPy's stuff at <a href="http://en.wikipedia.org/wiki/Comparison_of_computer_algebra_systems" rel="nofollow">http://en.wikipedia.org/wiki/Comparison_of_computer_algebra_systems</a> should be updated.  I did notice some of that is wrong. 
</pre>

- *Category:* Outreach
- *Time to complete:* 96 hours

### [2764](http://code.google.com/p/sympy/issues/detail?id=2764&q=label%3ACodeInImportedIntoSpreadsheet) - Improve our webpage
<pre>
Our webpage at <a href="http://sympy.org/" rel="nofollow">http://sympy.org/</a> could probably be made nicer, like with some nice CSS or html5.  The code is at <a href="https://github.com/sympy/sympy.github.com" rel="nofollow">https://github.com/sympy/sympy.github.com</a>.  Also, it maybe could use better examples/explanation of what SymPy is. 
</pre>

- *Category:* Outreach
- *Time to complete:* 96 hours

### [2787](http://code.google.com/p/sympy/issues/detail?id=2787&q=label%3ACodeInImportedIntoSpreadsheet) - Create sticker for SymPy based on the logo
<pre>
The sticker should contain SymPy's logo [1], project name and description. Alternative version may skip description. Sticker must be in SVG format.

[1] <a href="http://code.google.com/p/sympy/source/browse/#svn%2Fmaterials%2Flogo" rel="nofollow">http://code.google.com/p/sympy/source/browse/#svn%2Fmaterials%2Flogo</a> 
</pre>

- *Category:* Outreach
- *Time to complete:* 96 hours

### [2796](http://code.google.com/p/sympy/issues/detail?id=2796&q=label%3ACodeInImportedIntoSpreadsheet) - Package the latest version of SymPy for the major distributions: Debian / Ubuntu
<pre>
Most distributions have old versions of SymPy packaged (or none at all, eg. openSUSE). These should be updated to the latest version of SymPy (0.7.1 as of now). Ideally, the scripts used to generate these packages should also be saved and uploaded somewhere, so it will be easier to update them to newer versions. I'm marking this for Code-In, but consider that each major distro could be a separate task.

This most likely means deleting the bundled mpmath/ and making SymPy play nice with the distro-provided version. 
</pre>

- *Category:* Outreach
- *Time to complete:* 96 hours

### [1456](http://code.google.com/p/sympy/issues/detail?id=1456&q=label%3ACodeInImportedIntoSpreadsheet) - use pyflakes to identify simple bugs in sympy and fix them
<pre>
Example:

sudo apt-get install pyflakes

$ pyflakes sympy/integrals/
sympy/integrals/rationaltools.py:3: 'div' imported but unused
sympy/integrals/rationaltools.py:121: redefinition of unused 'symbols' from
line 3
sympy/integrals/risch.py:4: 'Pow' imported but unused
sympy/integrals/risch.py:5: 'Function' imported but unused
sympy/integrals/risch.py:7: 'Atom' imported but unused
sympy/integrals/risch.py:8: 'Integer' imported but unused
sympy/integrals/deltafunctions.py:2: 'Symbol' imported but unused
sympy/integrals/deltafunctions.py:2: 'S' imported but unused
sympy/integrals/deltafunctions.py:2: 'Wild' imported but unused
sympy/integrals/integrals.py:2: 'Pow' imported but unused
sympy/integrals/integrals.py:9: 'apart' imported but unused
sympy/integrals/integrals.py:10: 'limit' imported but unused
sympy/integrals/integrals.py:13: 'DiracDelta' imported but unused
sympy/integrals/integrals.py:13: 'Heaviside' imported but unused
sympy/integrals/integrals.py:111: redefinition of unused 'limit' from line 10
sympy/integrals/__init__.py:8: 'integrate' imported but unused
sympy/integrals/__init__.py:8: 'line_integrate' imported but unused
sympy/integrals/__init__.py:8: 'Integral' imported but unused
sympy/integrals/tests/test_rationaltools.py:4: 'log_to_atan' imported but
unused
sympy/integrals/tests/test_rationaltools.py:4: 'log_to_real' imported but
unused
sympy/integrals/tests/test_rationaltools.py:4: 'ratint_ratpart' imported
but unused
sympy/integrals/tests/test_lineintegrals.py:1: 'cos' imported but unused
sympy/integrals/tests/test_lineintegrals.py:1: 'Integral' imported but unused
sympy/integrals/tests/test_lineintegrals.py:1: 'sympify' imported but unused
sympy/integrals/tests/test_lineintegrals.py:1: 'integrate' imported but unused
sympy/integrals/tests/test_lineintegrals.py:1: 'diff' imported but unused
sympy/integrals/tests/test_lineintegrals.py:1: 'pi' imported but unused
sympy/integrals/tests/test_lineintegrals.py:1: 'sin' imported but unused
sympy/integrals/tests/test_integrals.py:1: redefinition of unused 'atan'
from line 1
sympy/integrals/tests/test_integrals.py:1: 'I' imported but unused
sympy/integrals/tests/test_integrals.py:5: 'skip' imported but unused
sympy/integrals/tests/test_integrals.py:5: 'XFAIL' imported but unused


it finds (among other things) that the Heaviside is imported but never
used, so it should be removed. 
</pre>

- *Category:* QA
- *Labels:* EasyToFix, Priority-Medium, Type-Defect
- *Time to complete:* 96 hours

Pick a good sized module in SymPy (i.e., one of the subdirectories of the sympy/ directory, but not one of the ones that only has a few files in it).  

### [1752](http://code.google.com/p/sympy/issues/detail?id=1752&q=label%3ACodeInImportedIntoSpreadsheet) - setup.py test should run the doctests even when the regular tests fail
<pre>
Two things annoy me about ./setup.py test.  First, if a regular test fails, then it does not run the 
doctests.  But this is supposed to be a shortcut to both the regular tests and the doctests in one.  
Second, if you keyboard interrupt during the tests, it then proceeds to run the doctests.  But when I 
keyboard interrupt, I want it to stop the whole script.  

I don't know how easy it would be to change the second item, but the first one should be fixable. 
</pre>

- *Category:* QA
- *Labels:* EasyToFix, Priority-High, Testing, Type-Defect
- *Time to complete:* 96 hours

### [2786](http://code.google.com/p/sympy/issues/detail?id=2786&q=label%3ACodeInImportedIntoSpreadsheet) - Fill in missing tests for sympy.physics module in test_args.py
<pre>
All tests decorated with @SKIP(&quot;TODO: sympy.physics&quot;) must be fixed. 
</pre>

- *Category:* QA
- *Time to complete:* 96 hours

### [1235](http://code.google.com/p/sympy/issues/detail?id=1235&q=label%3ACodeInImportedIntoSpreadsheet) - Problem installing in Windows
<pre>
Hi!

I've downloaded the Windows installer, and tries to run the program - but 
I get an error message: &quot;No Python information found in the registry&quot;. But 
I have Python installed.

This is what I get when running the Python command in the command line:

&quot;C:\Users\Fredrik\Documents\programme\discalc&gt;PYTHON
Python 2.5.1 (<a href="/p/sympy/source/detail?r=251">r251</a>:54863, Apr 18 2007, 08:51:08) [MSC v.1310 32 bit 
(Intel)] on win32
Type &quot;help&quot;, &quot;copyright&quot;, &quot;credits&quot; or &quot;license&quot; for more information.
&gt;&gt;&gt;&quot;

Thanks for any answer. 
</pre>

- *Category:* Research
- *Time to complete:* 96 hours

### [2762](http://code.google.com/p/sympy/issues/detail?id=2762&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate ways to improve substitution, pattern matching, etc.
<pre>
This is related to <a title="Exact, algebraic, and integer_power substitution"  href="/p/sympy/issues/detail?id=2026">issue 2026</a> and this thread on the mailing list (<a href="http://groups.google.com/group/sympy/browse_thread/thread/4a19d0f39f51fda6" rel="nofollow">http://groups.google.com/group/sympy/browse_thread/thread/4a19d0f39f51fda6</a>).  The subs mechanism should be refactored so that it is more flexible.  Also, I believe it should be using the same thing internally as the pattern matching.  

The (Code-In) task here is to study this problem and discuss optimal ways to solve it.  You may also try implementing this (if we agree upon a good solution), perhaps as a separate task. 
</pre>

- *Category:* Research
- *Time to complete:* 96 hours

### [2795](http://code.google.com/p/sympy/issues/detail?id=2795&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate a robust way to have translated documentation
<pre>
Some of the Code-In tasks include translating our documentation to different languages. If this happens, we would need a way to manage all of these files (we might have many languages, after all). It's also important to know when and how much are these files out of date (as they eventually will be). Usually, GUI applications use gettext and have tons of .po files lying around, but I'm not sure that's the right approach for us. Marking this as a Code-In Research task. 
</pre>

- *Category:* Research
- *Time to complete:* 96 hours

### [2798](http://code.google.com/p/sympy/issues/detail?id=2798&q=label%3ACodeInImportedIntoSpreadsheet) - Research ways to extract statistics from the issue tracker
<pre>
The issue tracker can provide some valuable statistics about the health of the project - it might be interesting to graph the number of open issues, number of issues per category, the average &quot;age&quot; of the (closed/open) issues, who closes the most issues, the number of issue reports by users (as opposed to developers of SymPy) etc. This likely involves interfacing somehow with the Google API. 
</pre>

- *Category:* Research
- *Time to complete:* 96 hours

### [2803](http://code.google.com/p/sympy/issues/detail?id=2803&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate how to make the rewrite framework more flexible
<pre>
Currently, the rewrite framework only allows expr.rewrite(function) (e.g., cos(x).rewrite(exp)), and it implements only one rule per function pair.  This should be made more general.  Sometimes, you can't express a rewrite rule with just a function.  Other times, there is more than one way to rewrite one function in terms of another (for example cos(x) == sqrt(1 - sin(x)) == sin(pi/2 - x)).  

The issue is to consider ways to make the rewrite framework stronger, but still modular like it is now (so it's easily extensible). 
</pre>

- *Category:* Research
- *Time to complete:* 96 hours

### [2790](http://code.google.com/p/sympy/issues/detail?id=2790&q=label%3ACodeInImportedIntoSpreadsheet) - Create examples/short tutorials using IPython's notebook (IPython >= 0.12)
<pre>
Examples/short tutorials should show how to use SymPy to solve illustrative problems in high school mathematics/physics. Notebooks must contain code split into logical blocks, text cells with problem description and references to other materials, books, videos, etc. 
</pre>

- *Category:* Training
- *Time to complete:* 96 hours

### [2766](http://code.google.com/p/sympy/issues/detail?id=2766&q=label%3ACodeInImportedIntoSpreadsheet) - Translate tutorial to German
<pre>
The tutorial (<a href="http://docs.sympy.org/0.7.1/tutorial.html" rel="nofollow">http://docs.sympy.org/0.7.1/tutorial.html</a>) should be translated into various languages, e.g., Czech, Polish, French, German, etc. 
</pre>

- *Category:* Translation
- *Time to complete:* 96 hours

### [2767](http://code.google.com/p/sympy/issues/detail?id=2767&q=label%3ACodeInImportedIntoSpreadsheet) - Improve the interface of SymPy Live
<pre>
The interface at live.sympy.org should be improved, so that it looks and feels nicer, perhaps using some more advanced html5/css, etc. 
</pre>

- *Category:* UI
- *Time to complete:* 96 hours

### [2857](http://code.google.com/p/sympy/issues/detail?id=2857&q=label%3ACodeInImportedIntoSpreadsheet) - sqrt(2).is_irrational is None (should be True)
<pre>
It seems that sqrt(2).is_irrational should return True

Also, in a recent commit (ebe8a7e) it is noted that Add and Mul's implementation was faulty:

    The function used to return True if any factor was irrational.
    This is nonsense: neither I*pi, nor sqrt(8)/sqrt(2) are irrational.
    [One might argue about I*pi, but irrational implies real under the
    current assumptions system.]
    
    We now return True iff there is exactly one irrational factor and
    all other factors are rational.

In a Mul, any irrationals join together if their args are Rationals:

&gt;&gt;&gt; sqrt(2)*sqrt(5)
sqrt(10)
&gt;&gt;&gt; sqrt(S.Half)*sqrt(3)
sqrt(6)/2
&gt;&gt;&gt; sqrt(2)*sqrt(2+sqrt(3))
sqrt(2)*sqrt(sqrt(3) + 2)

So the argument about sqrt(8)/sqrt(2) doesn't apply. But it does make sense that the only way you can know that something is irrational is to have only one irrational factor since something like `sqrt(2+sqrt(3))*sqrt(2-sqrt(3))` might appear irrational with two irrational factors, but this is just a fancy 1:

&gt;&gt;&gt; sqrt(2-sqrt(3))*sqrt(2+sqrt(3))
sqrt(-sqrt(3) + 2)*sqrt(sqrt(3) + 2)
&gt;&gt;&gt; _.n()
1.00000000000000

Perhaps the routine could see if all irrationals present have a Number argument so `sqrt(2)*root(3,3)` could give True for is_irrational.

The same sort of problems exist for Add: while `sqrt(2) + sqrt(6)` is definitely irrational (though sympy gives None for the answer); something like `sqrt(2)/3 + sqrt(-6*sqrt(2) + 11)/3` is, again, just a fancy 1. 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

## <a name="#Easy">Easy</a>
### [615](http://code.google.com/p/sympy/issues/detail?id=615&q=label%3ACodeInImportedIntoSpreadsheet) - Fix the occasions where functions are called with wrong name and write tests
<pre>
/home/matt/hg/sympy/sympy/functions/elementary/exponential.py in
_eval_subs(self, old, new)
    125         o = old
    126         if isinstance(old, Basic.Pow): # handle
(exp(3*log(x))).subs(x**2, z) -&gt; z**(3/2)
--&gt; 127             old = exp(old.exp * S.Log(old.base))
    128         if isinstance(old, exp):
    129             b,e = self.as_base_exp()

/home/matt/hg/sympy/sympy/core/basic.py in __getattr__(self, clsname)
   1293         obj = Singleton.__dict__.get(clsname)
   1294         if obj is None:
-&gt; 1295             cls = getattr(Basic, clsname)
   1296             assert issubclass(cls, Singleton),`cls`
   1297             obj = cls()

/home/matt/hg/sympy/sympy/core/basic_methods.py in __getattr__(cls, name)
    216         try: return MetaBasicMeths.classnamespace[name]
    217         except KeyError: pass
--&gt; 218         raise AttributeError(&quot;'%s' object has no attribute '%s'&quot;%
    219                              (cls.__name__, name))
    220 

AttributeError: 'Basic' object has no attribute 'Log'

Some time ago functions were renamed but in many places there are old names
left, this should be fixed soon. 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

### [654](http://code.google.com/p/sympy/issues/detail?id=654&q=label%3ACodeInImportedIntoSpreadsheet) - Remove dead code from _eval_subs()
<pre>
&gt; &gt; diff --git a/sympy/functions/elementary/exponential.py b/sympy/functions=
/elementary/exponential.py
&gt; &gt; --- a/sympy/functions/elementary/exponential.py
&gt; &gt; +++ b/sympy/functions/elementary/exponential.py
&gt; &gt; @@ -13,7 +13,7 @@ class exp(Function):
&gt; &gt;              raise ArgumentIndexError(self, argindex)
&gt; &gt;
&gt; &gt;      def inverse(self, argindex=3D1):
&gt; &gt; -        return S.Log
&gt; &gt; +        return log
&gt; &gt;
&gt; &gt;      @classmethod
&gt; &gt;      def _eval_apply_subs(self, *args):
&gt; &gt; @@ -124,7 +124,7 @@ class exp(Function):
&gt; &gt;          arg =3D self.args[0]
&gt; &gt;          o =3D old
&gt; &gt;          if isinstance(old, Basic.Pow): # handle (exp(3*log(x))).subs(x*=
*2, z) -&gt; z**(3/2)
&gt; &gt; -            old =3D exp(old.exp * S.Log(old.base))
&gt; &gt; +            old =3D exp(old.exp * log(old.base))
&gt; &gt;          if isinstance(old, exp):
&gt; &gt;              b,e =3D self.as_base_exp()
&gt; &gt;              bo,eo =3D old.as_base_exp()
&gt;=20
&gt; I would suggest to either write tests, or remove the code.
&gt;=20
&gt; But yes, this patch can go in, but unless there are tests for this, I
&gt; don't see any point of having such a code.

It seems this piece of code is never (?) executed in sympy since
exp(3*log(x)) canonize to x**3.

On the other hand when autoevaluation would be turned off exp(3*log(x))
will be just that -- so there should be a test which constructs
unevaluated exp(3*log(x)) and calls subs.

I'm not sure how to do it now, please advise. 
</pre>

- *Category:* Code
- *Time to complete:* 96 hours

### [1058](http://code.google.com/p/sympy/issues/detail?id=1058&q=label%3ACodeInImportedIntoSpreadsheet) - Classifying formulas
<pre>
I've written some code for determining the &quot;class&quot; of a formula. The
function classify(expr, x) walks the expression top-down and at each level
classifies it as a function of x. It distinguishes between various classes
of functions, including:

* linear expressions
* polynomials (degree &gt; 1)
* rational functions
* algebraic roots
* exponentials
* logarithms
* trigonometric functions
* etc

It then recursively classifies all subexpressions and returns the path with
the &quot;greatest&quot; complexity. The following test outputs should hopefully make
it more clear:

pi []
1 + 3*x [LINEAR]
3*x + x**2 [POLYNOMIAL]
(1 + pi)*(5 + 4*x) [LINEAR]
(1 + pi)*(5 + E*(pi + 8*x)) [LINEAR]
(1 + 2*x)*(5 + 4*x) [POLYNOMIAL]
1/x [RATIONAL]
1/(1 + 2*x) [RATIONAL]
1/(2*x + x**2) [RATIONAL]
(1 + x)/(1 - x) [RATIONAL]
(4 + x)/(2*x + x**2) [RATIONAL]
(4 + x)/(2*x + x**2) + x**2 [RATIONAL]
x**2*(4 + x)/(2*x + x**2) [RATIONAL]
(1 + 3*x)**(1/2) [ROOT, LINEAR]
x**(3/2) [ROOT, LINEAR]
x**pi [EXP, LINEAR, LOG]
2*x + exp(1 + 2*x) + exp(4 + 3*x) [LINEAR, EXP, LINEAR]
2*x + (exp(3*x) + exp(1 + x))/(1 + 5*x) [RATIONAL, EXP, LINEAR]
2*x + sin(1 + 2*x)**2 + cos(4 + x)**4 [POLYNOMIAL, TRIGONOMETRIC, LINEAR]
2*x + (sin(1 + 2*x)**2 + cos(4 + x)**4)/(1 + 5*x) [RATIONAL, TRIGONOMETRIC,
LINEAR]
2**x [EXP, LINEAR]
x**x [EXP, LOG, LINEAR]
(1 + 2*x)**x [EXP, LOG, LINEAR]
(1 + acosh(x))**x [EXP, LOG, LINEAR, INVHYPERBOLIC, LINEAR]
exp(exp(x)) [EXP, EXP, LINEAR]
exp(exp(1/x)) [EXP, EXP, RATIONAL]
exp(exp(x)) + exp(exp(1/x)) [LINEAR, EXP, EXP, RATIONAL]
exp(gamma(x)**2) [EXP, POLYNOMIAL, NONELEMENTARY, LINEAR]

(The trailing LINEAR for f(a*x+b) could perhaps be dropped when a*x+b is
actually precisely x.)

The classification gives an ordering roughly similar to (though more coarse
than) that used in integral tables like Gradshteyn and Ryzhik. I think this
could be used by various symbolic algorithms to decide which heuristic
algorithms to try. For example, integrate could choose heuristics among
these (and other) cases:

[POLYNOMIAL] -- use a polynomial integrator
[RATIONAL] -- use a rational integrator
[LINEAR ROOT, LINEAR] -- try looking up a direct formula in a table
[LINEAR, NONELEMENTARY, LINEAR] -- try looking up a formula in a table
[POLYNOMIAL, TRIGONOMETRIC, LINEAR] -- try the integrator for trigonometric
polynomials

There is a clear advantage to the fact that only a single pass through the
expression is required, instead of requiring every heuristic to &quot;smell&quot; the
expression. So it becomes cheaper to have lots of special-purpose heuristics.

The output can also be used to determine whether a function is elementary,
transcendental, etc.

What do you think? Where should the code go, does it need improvements,
should the SYMBOLS perhaps be something else (e.g. strings)? Maybe return
an object with __eq__, __le__ methods etc so that computed classifications
can be compared more easily in terms of the complexity() measure? 
</pre>

- *Category:* Code
- *Labels:* Priority-Medium, Type-Enhancement
- *Time to complete:* 48 hours

### [2276](http://code.google.com/p/sympy/issues/detail?id=2276&q=label%3ACodeInImportedIntoSpreadsheet) - integrate() should use the ode module's undetermined coefficients solver when possible
<pre>
So my comment 8 from <a title="Arbitrary constants in indefinite integration"  href="/p/sympy/issues/detail?id=2219">issue 2219</a> made me realize something.  Consider the following:

In [242]: integrate(x**2*exp(x)*sin(x), x)
Out[242]: 
   x           2  x                  x                  2         x
  ℯ ⋅sin(x)   x ⋅ℯ ⋅sin(x)   cos(x)⋅ℯ              x   x ⋅cos(x)⋅ℯ 
- ───────── + ──────────── - ───────── + x⋅cos(x)⋅ℯ  - ────────────
      2            2             2                          2      

In [245]: dsolve(f(x).diff(x) - x**2*exp(x)*sin(x), f(x), hint='nth_linear_constant_coeff_undetermined_coefficients')
Out[245]: 
             x           2  x                  x                  2         x
            ℯ ⋅sin(x)   x ⋅ℯ ⋅sin(x)   cos(x)⋅ℯ              x   x ⋅cos(x)⋅ℯ 
f(x) = C₁ - ───────── + ──────────── - ───────── + x⋅cos(x)⋅ℯ  - ────────────
                2            2             2                          2      

In [246]: %timeit integrate(x**2*exp(x)*sin(x), x)
1 loops, best of 3: 10.7 s per loop

In [247]: %timeit dsolve(f(x).diff(x) - x**2*exp(x)*sin(x), f(x), hint='nth_linear_constant_coeff_undetermined_coefficients')
1 loops, best of 3: 232 ms per loop

dsolve() is way faster because it just computes the necessary form of the integral and solves for the undetermined coefficients.  No complicated integration algorithm is needed.  

So I think if the integral has the correct form, that internally integrate(expr, x, x, ...) should use dsolve's internal undetermined coefficient algorithms for solving f(x).diff(x, x, …) - expr.  All the necessary stuff is already in ode.py, including the function that checks if expr is of the correct form. 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2427](http://code.google.com/p/sympy/issues/detail?id=2427&q=label%3ACodeInImportedIntoSpreadsheet) - Check for incorrect usage of expr.atoms() and change it to free_symbols
<pre>
If any code wants to know if there are variables that are free like x but not y in Integral(y, (y, 1, x)) then it should use expr.free_symbols, not .atoms(Symbol) (since that would have given x and y for the example given). The code should be checked for instances of .atoms(Symbol) to see what the author intended and corrected if necessary. 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2534](http://code.google.com/p/sympy/issues/detail?id=2534&q=label%3ACodeInImportedIntoSpreadsheet) - Use "with open" instead of "open … close"
Please see http://code.google.com/p/sympy/issues/detail?id=2534 for full information on this task. Please read https://github.com/sympy/sympy/wiki/gci-2011-landing before completing any tasks for SymPy.  

<pre>
Now that we don't support Python 2.4, we can use with statement context managers.  One of the best places to use this is when opening a file.  You can do

with open(file) as f:
    do stuff

instead of 

f = open(file)
do stuff
f.close()

And it's not only more readable, but also the with statement context manager will automatically close the file, even if an exception is raised. 

There are a handful of places in the code where we open() stuff (do git grep &quot;open\(&quot;).  Remember that to support the with statement in Python 2.5, you have to add &quot;from __future__ import with_statement&quot; to the top of the file. 
</pre>

- *Category:* Code
- *Labels:* EasyToFix, Priority-Medium, Type-Defect
- *Time to complete:* 48 hours

### [2570](http://code.google.com/p/sympy/issues/detail?id=2570&q=label%3ACodeInImportedIntoSpreadsheet) - Remove bare except statements
<pre>
If you do git grep &quot;except:&quot; you will see that there are several places in the code with bare except statements that should be rewritten to catch explicit exceptions.  To quote the Zen of Python:

Errors should never pass silently.
Unless explicitly silenced.

And to quite PEP 8:

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

To be sure, some of the bare except cases in the code are correct by the above (like the ones in the test runner), but many are not. 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2639](http://code.google.com/p/sympy/issues/detail?id=2639&q=label%3ACodeInImportedIntoSpreadsheet) - The Product() class should not evaluate by default
<pre>
Unlike other unevaluated operators, Product() is not always unevaluated.  Attempted evaluation should be the job of product().  This is how Sum/summation works:

In [2]: Product(n, (n, 1, 2))
Out[2]: 2

In [3]: Sum(n, (n, 1, 2))
Out[3]: 
  2    
 __    
 \ `   
  )   n
 /_,   
n = 1  

In [4]: product(n, (n, 1, 2))
Out[4]: 2

In [5]: summation(n, (n, 1, 2))
Out[5]: 3 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2683](http://code.google.com/p/sympy/issues/detail?id=2683&q=label%3ACodeInImportedIntoSpreadsheet) - det() is called when inverting matrix through GE
<pre>
As noted at <a href="http://groups.google.com/group/sympy/browse_thread/thread/ba37b597b851df7c#" rel="nofollow">http://groups.google.com/group/sympy/browse_thread/thread/ba37b597b851df7c#</a>, det() is called when inverting a Matrix with the GE method.  This is used only the check if it is non-degenerate.  This should instead be checked by the output of rref(). 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2760](http://code.google.com/p/sympy/issues/detail?id=2760&q=label%3ACodeInImportedIntoSpreadsheet) - latex(symbol_names) not working with ~x
<pre>
Read this for more information
<a href="https://github.com/sympy/sympy/pull/674" rel="nofollow">https://github.com/sympy/sympy/pull/674</a>

latex(x**2, symbol_names={x:'x_i'})

works fine, but when you try something as

latex(~x, symbol_names={x:'x_i'})

it doesn't. Besides, every time you need latex to use x's symbol_name, you need to pass the symbol_names dictionary.

Sage has some nice functionality:
var('sui', latex_name=&quot;s_{u,i}&quot;)

and you don't have to use a special dictionary everytime you need to typeset the symbol. 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2776](http://code.google.com/p/sympy/issues/detail?id=2776&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in integrals
<pre>
Edit the doc-string to add list of other function that are closely related to the query.


This is the list of .py files which contains the functions.

sympy/integrals/deltafunctions.py
sympy/integrals/integrals.py
sympy/integrals/risch.py
sympy/integrals/rationaltools.py
sympy/integrals/trigonometry.py

There are around 19 functions which one needs to understand (the input parameters and final result and not the code) to interrelate them. 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2784](http://code.google.com/p/sympy/issues/detail?id=2784&q=label%3ACodeInImportedIntoSpreadsheet) - 1/function() should be printed differently by latex printer
<pre>
In [1]: latex(1/cos(x))
Out[1]: \operatorname{cos}^{-1}\left(x\right)

In [2]: pprint(1/cos(x))
  1   
──────
cos(x)

[1] should output \frac{1}{\operator ...} 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2785](http://code.google.com/p/sympy/issues/detail?id=2785&q=label%3ACodeInImportedIntoSpreadsheet) - Use \functionname instead of \operatorname{functionname} whenever possible
<pre>
SymPy uniformly uses \operatorname when latex printing functions. However, tex engine in matplotlib doesn't support it. It would be convenient to use \functionname directly whenever possible (trigonometric and hyperbolic functions, exp, log and maybe other). 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2815](http://code.google.com/p/sympy/issues/detail?id=2815&q=label%3ACodeInImportedIntoSpreadsheet) - Parts of the pyglet plotting module does not follow PEP 8, fix it
<pre>
The code there is a bit hard to read. It would be nice to have it refactored so it follows PEP8.

There are certain parts that are not pythonic but that's another problem needing more in-depth refactoring. 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2817](http://code.google.com/p/sympy/issues/detail?id=2817&q=label%3ACodeInImportedIntoSpreadsheet) - Make sure all the built-in __methods__ are defined
<pre>
At <a href="http://docs.python.org/reference/datamodel.html" rel="nofollow">http://docs.python.org/reference/datamodel.html</a>, it lists all the __methods__ that Python works with (like __int__, __contains__, etc.).  We should go through all of these and make sure they are all defined on Basic, Expr, or whatever relevant subclass, so that we don't have simple bugs like

In [72]: long(Integer(3))
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
/Users/aaronmeurer/Documents/python/sympy/sympy/&lt;ipython-input-72-5fff10d216fd&gt; in &lt;module&gt;()
----&gt; 1 long(Integer(3))

TypeError: long() argument must be a string or a number, not 'Integer'

Regarding where they should be defined, stuff that makes sense for any object should go on Basic, stuff that makes sense only on mathematical objects (like __add__ for example) should go on Expr, and stuff that makes sense only for numbers (like __int__) should go in Number. 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2830](http://code.google.com/p/sympy/issues/detail?id=2830&q=label%3ACodeInImportedIntoSpreadsheet) - checkodesol() should use force=True
<pre>
&gt; @@ -542,7 +542,11 @@ def test_1st_homogeneous_coeff_ode_check3():
&gt;      # (False, x*(log(exp(-LambertW(C1*x))) + LambertW(C1*x))*exp(-LambertW(C1*x) + 1))
&gt;      eq3 = f(x) + (x*log(f(x)/x) - 2*x)*diff(f(x),x)
&gt;      sol3 = Eq(f(x), x*exp(1 - LambertW(C1*x)))
&gt; -    assert checkodesol(eq3, sol3, solve_for_func=False)[0]
&gt; +    assert checkodesol(eq3, sol3, solve_for_func=True)[0]
&gt; +    # and without an assumption about x and f(x), the implicit form doesn't resolve, either:
&gt; +    # (False, (log(f(x)/x) + log(x/f(x)))*f(x))

So checkodesol() needs to be more aggressive, since dsolve() obtains these logarithms by calling logcombine(force=True). An expand with force=True should be used on expressions being tested or else (as shown above) terms which should go to zero, don't:

&gt;&gt;&gt; log(f(x)/x) + log(x/f(x))
log(f(x)/x) + log(x/f(x))
&gt;&gt;&gt; _.expand(force=True)
0 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2838](http://code.google.com/p/sympy/issues/detail?id=2838&q=label%3ACodeInImportedIntoSpreadsheet) - Move the KroneckerDelta class to another module 
<pre>
KroneckerDelta would be useful for more than just quantum physics.  I think it should be moved into the functions module and imported with &quot;from sympy import *&quot;. 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [2846](http://code.google.com/p/sympy/issues/detail?id=2846&q=label%3ACodeInImportedIntoSpreadsheet) - Integral.transform should allow a change to a different variable
<pre>
Integral.transform is confusing, since it requires you to use the same integration variable.  But usually, when we do a transfrom on an integral we change the name of the variable.  It should allow something like

Integral.transform(x, 2*y, y)

where y is the new variable.  The third argument would default to the integration variable, so that you can still use the current syntax.

Also, the docstring needs some doctests, which would also make it less confusing.

Related is <a title="Integral manipulations"  href="/p/sympy/issues/detail?id=2297">issue 2297</a>. 
</pre>

- *Category:* Code
- *Time to complete:* 48 hours

### [16](http://code.google.com/p/sympy/issues/detail?id=16&q=label%3ACodeInImportedIntoSpreadsheet) - Check and compare an old patch concerning object with indices against current sympy
Please see http://code.google.com/p/sympy/issues/detail?id=16 for full information on this task. <br><br>Please read https://github.com/sympy/sympy/wiki/gci-2011-landing before completing any tasks for SymPy. <br><br>Additional Note(s): Check out comment 32 in the bug report. 

<pre>
Let's get inspired by ginac. This code should make it easy to compute for
example einstein equations from the (symbolic) metric tensor. We can do it
already now, but it would be nice to type in equations in the index form as
found in the general relativity books and then just plug in a symbolic
matrix for the metric tensor, and it would figure all the rest by itself. 
</pre>

- *Category:* Documentation
- *Labels:* EasyToFix, Matrices, Priority-Medium, Type-Enhancement
- *Time to complete:* 48 hours

Check out comment 32 in the bug report. 

### [1886](http://code.google.com/p/sympy/issues/detail?id=1886&q=label%3ACodeInImportedIntoSpreadsheet) - Documentation for the Expr class
<pre>
Expr needs a docstring. The split between Basic and Expr must be explained. 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2115](http://code.google.com/p/sympy/issues/detail?id=2115&q=label%3ACodeInImportedIntoSpreadsheet) - Move stuff from the Google Code SVN to git
<pre>
Everything from here <a href="http://code.google.com/p/sympy/source/browse/" rel="nofollow">http://code.google.com/p/sympy/source/browse/</a> needs to be moved either to the GitHub wiki or the main repo.  Details on how to checkout the files on your computer are here: <a href="http://code.google.com/p/sympy/source/checkout" rel="nofollow">http://code.google.com/p/sympy/source/checkout</a>.  Does anyone know how to transfer svn to git without losing the history?

By the way, this includes the Google Code wiki pages in it. 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2160](http://code.google.com/p/sympy/issues/detail?id=2160&q=label%3ACodeInImportedIntoSpreadsheet) - List of dependencies
<pre>
We should include in the README, and probably in the docs somewhere too, a list of all the &quot;dependencies&quot; of SymPy.  Now, obviously, SymPy's only dependency is Python, but there are several optional dependencies like IPython and gmpy that are not required but extent the capabilities of SymPy if they are installed. 

I am putting this here instead of just doing it and making a pull request because I don't know exactly how things work with things like numpy and scipy, and I also don't know if I am forgetting anything.  So far, I have this:

&quot;&quot;&quot;
Dependencies
------------

One of the fundamental design decisions behind SymPy is that it should not have any external dependencies besides Python to install.  Therefore, the only real &quot;dependency&quot; of SymPy is an installation of Python 2.4, 2.5, 2.6, or 2.7 (note that Python 2.4 support is deprecated and will no longer work in the next release).

However, there are several packages that are not required to use SymPy, but that will enhance SymPy if they are installed.  These packages are:

- IPython (<a href="http://ipython.scipy.org/moin/" rel="nofollow">http://ipython.scipy.org/moin/</a>).  IPython is a third party Python interactive shell that has many more features over the built-in Python interactive shell, such as tab-completetion and [what other important features should I mention here?].  If IPython is installed, isympy will automatically use it.  Otherwise, it will fall back to the regular Python interactive shell.  You can override this behavior by setting the -c option to isympy, like `isympy -c python`.

- gmpy (<a href="http://code.google.com/p/gmpy/" rel="nofollow">http://code.google.com/p/gmpy/</a>). gmpy is a Python wrapper around the GNU Multiple Precision Arithmetic Library (GMP). If gmpy is installed, it may make certain operations in SymPy faster, because it will use gmpy as the ground type instead of the built-in Python ground types.  If gmpy is not installed, it will fall back to the default Python ground types.  You can override this behavior by setting the SYMPY_GROUND_TYPES environment variable, such as `SYMPY_GROUND_TYPES=python isympy`. [Note: this should be an option to isympy!]

- Cython. [What exactly is the situation with Cython?]

- Numpy. [Ditto]

- Scipy. [Ditto]

- [Code generation dependencies?]

- [Other dependencies?]

Note that mpmath and pyglet, our floating point and plotting libraries respectively, are included with SymPy, so it is unnecessary to install them.  Indeed, SymPy will always use the version of mpmath or pyglet that comes with SymPy, even if a newer version is installed in the system.  This is done for compatibility reasons.

&quot;&quot;&quot;

OK, the text in [] are comments.  I need help from others writing the rest of this.  Note that I do not want to include any development dependencies here (like Sphinx), because the user does not care about that (maybe we could have that list somewhere else in our development docs).   

But basically for the others, explain what happens when they are installed and what happens when they are not (and how to override, if relevant).  

I just realized that the best way to do this would be through the wiki.  So if anyone has anything to add to this, please do it at <a href="https://github.com/sympy/sympy/wiki/Dependencies" rel="nofollow">https://github.com/sympy/sympy/wiki/Dependencies</a>.  And then when we have it finished we can add it to the README and regular docs. 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2204](http://code.google.com/p/sympy/issues/detail?id=2204&q=label%3ACodeInImportedIntoSpreadsheet) - Document why unpickling a singleton doesn't return the singleton object with protocol 0 and 1
<pre>
After pickling and unpickling pi, a simple cos(pi) no longer nicely simplifies to -1 on its own (it does if you nsimplify it)

Code:
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
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2367](http://code.google.com/p/sympy/issues/detail?id=2367&q=label%3ACodeInImportedIntoSpreadsheet) - SymPy's readthedocs documentation is broken
<pre>
See <a href="http://readthedocs.org/docs/sympy/en/latest/" rel="nofollow">http://readthedocs.org/docs/sympy/en/latest/</a>.  It just shows

&quot;&quot;&quot;
This is an automaticaly generated API documentation from SymPy sources.

Click the “modules” (Module Index) link in the top right corner to browse the modules.

Or click the “index” to see an index of all SymPy functions, methods and classes.
&quot;&quot;&quot;

and that's it. 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2597](http://code.google.com/p/sympy/issues/detail?id=2597&q=label%3ACodeInImportedIntoSpreadsheet) - Import all public functions and classes into Sphinx: polys
<pre>
There are some methods that do have docstrings, but are not shown in the documentation (docs.sympy.org).

For example, method norm in matrices.matrices.py has a docstring, but is not shown in <a href="http://docs.sympy.org/dev/modules/matrices.html" rel="nofollow">http://docs.sympy.org/dev/modules/matrices.html</a>. I thought that the bad formatting (there is no blank line after the first line of docstring) of the docstring might be the reason for this, but there are other methods with baddly formatted docstrings, that are properly shown in the documentation (e.g. method is_symmetric for matrices.matrices.py). 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2599](http://code.google.com/p/sympy/issues/detail?id=2599&q=label%3ACodeInImportedIntoSpreadsheet) - Update isympy manpage
<pre>
The manpage for isympy (doc/man/isympy) needs to be updated with all the latest options, etc. 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2679](http://code.google.com/p/sympy/issues/detail?id=2679&q=label%3ACodeInImportedIntoSpreadsheet) - Refactor GA* documentation to use doctests (or move it to examples/)
<pre>
There are some .py files in doc/src/modules/galgebra/GA which have some strange indentation (and aren't valid Python source files either). Aaron also noticed this and they produce (harmless) errors when 2to3 is ran on them. I've finally had a chance to look at them and they seem to be included in the main GA module documentation, GAsympy.txt. In fact, they seem to be used like a doctest - the first part of the file (indented) are the comments that produce the second half of the file (not indented). These should be converted to be actual doctests. 

Those files also haven't been touched since 2009 so it's not clear to me if anyone is even using this part of SymPy now, but fixing the docs shouldn't be too hard and can be a good introduction to SymPy for an interested developer (hence, I'm putting the EasyToFix tag here). Also, I don't think these files are ran as part of the doctest suite which means errors might be creeping in and we'd like to avoid this.

For the record, here are the errors produced when 2to3 is ran on these files:

RefactoringTool: Can't parse sympy-py3k/./doc/src/modules/galgebra/GA/reciprocalframeGAtest.py: ParseError: bad input: type=5, value='        ', context=('', (1, 0))
RefactoringTool: Can't parse sympy-py3k/./doc/src/modules/galgebra/GA/headerGAtest.py: ParseError: bad input: type=0, value='', context=('\n', (26, 0))
RefactoringTool: Can't parse sympy-py3k/./doc/src/modules/galgebra/GA/conformalgeometryGAtest.py: ParseError: bad input: type=5, value='        ', context=('', (1, 0))
RefactoringTool: Can't parse sympy-py3k/./doc/src/modules/galgebra/GA/BasicGAtest.py: ParseError: bad input: type=5, value='        ', context=('', (1, 0))
RefactoringTool: Can't parse sympy-py3k/./doc/src/modules/galgebra/GA/hyperbolicGAtest.py: ParseError: bad input: type=5, value='        ', context=('', (1, 0)) 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2774](http://code.google.com/p/sympy/issues/detail?id=2774&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Number Theory
<pre>
Edit the doc-string to add list of other function that are closely related to the query.

Ex. 

&gt;&gt;&gt; prime?
Docstring:
    Return the nth prime, with the primes indexed as prime(1) = 2,
    prime(2) = 3, etc.... The nth prime is approximately n*log(n) and
    can never be larger than 2**n.
    
    Reference: <a href="http://primes.utm.edu/glossary/xpage/BertrandsPostulate.html" rel="nofollow">http://primes.utm.edu/glossary/xpage/BertrandsPostulate.html</a>

## This is the present doc-string. One needs to add the following line

    See also : isprime, primerange, primepi 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2775](http://code.google.com/p/sympy/issues/detail?id=2775&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Combinotorics 
<pre>
Edit the doc-string to add list of other function that are closely related to the query.


This is the list of .py files which contains the functions.

sympy/combinatorics/generators.py  
sympy/combinatorics/prufer.py
sympy/combinatorics/graycode.py
sympy/combinatorics/permutations.py  
sympy/combinatorics/subsets.py

There are around 98(at max) functions which one needs to understand (the input parameters and final result and not the code) to interrelate them. 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2777](http://code.google.com/p/sympy/issues/detail?id=2777&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in functions
<pre>
Edit the doc-string to add list of other function that are closely related to the query.


This is the list of .py files which contains the functions.

sympy/functions/combinatorial/factorials.py
sympy/functions/combinatorial/numbers.py
sympy/functions/elementary/trigonometric.py  
sympy/functions/elementary/integers.py
sympy/functions/elementary/exponential.py
sympy/functions/elementary/piecewise.py
sympy/functions/elementary/complexes.py
sympy/functions/elementary/miscellaneous.py
sympy/functions/elementary/hyperbolic.py

There are around 52 functions which one needs to understand (the input parameters and final result and not the code) to interrelate them. 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2778](http://code.google.com/p/sympy/issues/detail?id=2778&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in functions/special
<pre>
Edit the doc-string to add list of other function that are closely related to the query.


This is the list of .py files which contains the functions.

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

There are around 62 functions which one needs to understand (the input parameters and final result and not the code) to interrelate them. 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2780](http://code.google.com/p/sympy/issues/detail?id=2780&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Matrices
<pre>
Edit the doc-string to add list of other function that are closely related to the query.

This is the list of .py files which contains the functions.

sympy/matrices.py

There are around 69 functions which one needs to understand (the input parameters and final result and not the code) to interrelate them. 
</pre>

- *Category:* Documentation
- *Time to complete:* 48 hours

### [2763](http://code.google.com/p/sympy/issues/detail?id=2763&q=label%3ACodeInImportedIntoSpreadsheet) - Fix the SymPy Logo
<pre>
The original logo is found at <a href="http://code.google.com/p/sympy/source/browse/#svn%2Fmaterials%2Flogo" rel="nofollow">http://code.google.com/p/sympy/source/browse/#svn%2Fmaterials%2Flogo</a>.  The problem is that the transparency is not done correctly on the tail, so that it does not look good unless the background is white.  We need to fix it so that it uses the correct kind of alpha channel, so that it looks good everywhere.  There is a svg image there, though I didn't have much luck with it. 
</pre>

- *Category:* Outreach
- *Time to complete:* 48 hours

### [2800](http://code.google.com/p/sympy/issues/detail?id=2800&q=label%3ACodeInImportedIntoSpreadsheet) - Flesh out the SymPy Papers wiki page
<pre>
We have a page on the wiki[1] that should list (scientific) papers mentioning SymPy, but it's currently empty. Populating this would be interesting and could also persuade other academics to try out/use SymPy. Google Scholar can be used to track down papers. See also the thread which originally asked about this[2].


[1] <a href="https://github.com/sympy/sympy/wiki/SymPy-Papers" rel="nofollow">https://github.com/sympy/sympy/wiki/SymPy-Papers</a>
[2] <a href="https://groups.google.com/group/sympy/browse_thread/thread/34443bd5708310f2/71c0cc0ba21a19e1?hl=en" rel="nofollow">https://groups.google.com/group/sympy/browse_thread/thread/34443bd5708310f2/71c0cc0ba21a19e1?hl=en</a> 
</pre>

- *Category:* Outreach
- *Time to complete:* 48 hours

### [1616](http://code.google.com/p/sympy/issues/detail?id=1616&q=label%3ACodeInImportedIntoSpreadsheet) - Bug in subs
<pre>
In [1]: c2,c3,q1p,q2p,c1,s1,s2,s3= symbols('c2 c3 q1p q2p c1 s1 s2 s3')

In [2]: test=c2**2*q2p*c3 + c1**2*s2**2*q2p*c3 + s1**2*s2**2*q2p*c3 -
c1**2*q1p*c2*s3 - s1**2*q1p*c2*s3

In [3]: test.subs({c1**2 : 1-s1**2, c2**2 : 1-s2**2, c3**3: 1-s3**2})
ERROR: An unexpected error occurred while tokenizing input           
The following traceback may be corrupted or invalid                  
The error message is: ('EOF in multi-line statement', (22, 0))       

ERROR: An unexpected error occurred while tokenizing input
The following traceback may be corrupted or invalid       
The error message is: ('EOF in multi-line statement', (96, 0))

---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)

/home/luke/lib/python/sympy/&lt;ipython console&gt; in &lt;module&gt;()

/home/luke/lib/python/sympy/sympy/core/basic.pyc in subs(self, *args)
   1021             sequence = args[0]                               
   1022             if isinstance(sequence, dict):                   
-&gt; 1023                 return self._subs_dict(sequence)             
   1024             elif isinstance(sequence, (list, tuple)):        
   1025                 return self._subs_list(sequence)             

/home/luke/lib/python/sympy/sympy/core/basic.pyc in _subs_dict(self, sequence)
   1111                 subst.append(pattern)                                 
   1112         subst.reverse()                                               
-&gt; 1113         return self._subs_list(subst)                                 
   1114                                                                       
   1115     def _seq_subs(self, old, new):                                    

/home/luke/lib/python/sympy/sympy/core/basic.pyc in _subs_list(self, sequence)
   1064         for old, new in sequence:                                     
   1065             if hasattr(result, 'subs'):                               
-&gt; 1066                 result = result.subs(old, new)                        
   1067         return result                                                 
   1068                                                                       

/home/luke/lib/python/sympy/sympy/core/basic.pyc in subs(self, *args)
   1028         elif len(args) == 2:                                 
   1029             old, new = args                                  
-&gt; 1030             return self._subs_old_new(old, new)              
   1031         else:                                                
   1032             raise TypeError(&quot;subs accepts either 1 or 2 arguments&quot;)

/home/luke/lib/python/sympy/sympy/core/cache.pyc in wrapper(*args, **kw_args)
     83         except KeyError:                                             
     84             pass                                                     
---&gt; 85         func_cache_it_cache[k] = r = func(*args, **kw_args)          
     86         return r                                                     
     87                                                                      

/home/luke/lib/python/sympy/sympy/core/basic.pyc in _subs_old_new(self,
old, new)
   1037         old = sympify(old)                                        
      
   1038         new = sympify(new)                                        
      
-&gt; 1039         return self._eval_subs(old, new)                          
      
   1040                                                                   
      
   1041     def _eval_subs(self, old, new):                               
      

/home/luke/lib/python/sympy/sympy/core/add.pyc in _eval_subs(self, old, new)
    310                     ret_set = self_set - old_set                    
    311                     return Add(new, coeff_self, -coeff_old,
*[s._eval_subs(old, new) for s in ret_set])
--&gt; 312         return self.__class__(*[s._eval_subs(old, new) for s in
self.args])                            
    313                                                                   
                                    
    314     @cacheit                                                      
                                    

/home/luke/lib/python/sympy/sympy/core/mul.pyc in _eval_subs(self, old, new)
    809                     # collect commutative terms                     

    810                     else:
--&gt; 811                         comms_final.remove(ele)
    812                                                
    813                 # continue only if all commutative terms in old are
present


ValueError: list.remove(x): x not in list

In [4]: test.subs({c1**2 : 1-s1**2})
Out[4]:                             
         2 ⎛      2⎞             ⎛      2⎞            2            2   2  
            2
c₃⋅q2p⋅s₂ ⋅⎝1 - s₁ ⎠ - c₂⋅q1p⋅s₃⋅⎝1 - s₁ ⎠ + c₃⋅q2p⋅c₂  + c₃⋅q2p⋅s₁ ⋅s₂  -
c₂⋅q1p⋅s₃⋅s₁ 

In [5]: test.subs({c2**2 : 1-s2**2})
ERROR: An unexpected error occurred while tokenizing input
The following traceback may be corrupted or invalid       
The error message is: ('EOF in multi-line statement', (22, 0))

ERROR: An unexpected error occurred while tokenizing input
The following traceback may be corrupted or invalid       
The error message is: ('EOF in multi-line statement', (96, 0))

---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)

/home/luke/lib/python/sympy/&lt;ipython console&gt; in &lt;module&gt;()

/home/luke/lib/python/sympy/sympy/core/basic.pyc in subs(self, *args)
   1021             sequence = args[0]                               
   1022             if isinstance(sequence, dict):                   
-&gt; 1023                 return self._subs_dict(sequence)             
   1024             elif isinstance(sequence, (list, tuple)):        
   1025                 return self._subs_list(sequence)             

/home/luke/lib/python/sympy/sympy/core/basic.pyc in _subs_dict(self, sequence)
   1111                 subst.append(pattern)                                 
   1112         subst.reverse()                                               
-&gt; 1113         return self._subs_list(subst)                                 
   1114                                                                       
   1115     def _seq_subs(self, old, new):                                    

/home/luke/lib/python/sympy/sympy/core/basic.pyc in _subs_list(self, sequence)
   1064         for old, new in sequence:                                     
   1065             if hasattr(result, 'subs'):                               
-&gt; 1066                 result = result.subs(old, new)                        
   1067         return result                                                 
   1068                                                                       

/home/luke/lib/python/sympy/sympy/core/basic.pyc in subs(self, *args)
   1028         elif len(args) == 2:                                 
   1029             old, new = args                                  
-&gt; 1030             return self._subs_old_new(old, new)              
   1031         else:                                                
   1032             raise TypeError(&quot;subs accepts either 1 or 2 arguments&quot;)

/home/luke/lib/python/sympy/sympy/core/cache.pyc in wrapper(*args, **kw_args)
     83         except KeyError:                                             
     84             pass                                                     
---&gt; 85         func_cache_it_cache[k] = r = func(*args, **kw_args)          
     86         return r                                                     
     87                                                                      

/home/luke/lib/python/sympy/sympy/core/basic.pyc in _subs_old_new(self,
old, new)
   1037         old = sympify(old)                                        
      
   1038         new = sympify(new)                                        
      
-&gt; 1039         return self._eval_subs(old, new)                          
      
   1040                                                                   
      
   1041     def _eval_subs(self, old, new):                               
      

/home/luke/lib/python/sympy/sympy/core/add.pyc in _eval_subs(self, old, new)
    310                     ret_set = self_set - old_set                    
    311                     return Add(new, coeff_self, -coeff_old,
*[s._eval_subs(old, new) for s in ret_set])
--&gt; 312         return self.__class__(*[s._eval_subs(old, new) for s in
self.args])                            
    313                                                                   
                                    
    314     @cacheit                                                      
                                    

/home/luke/lib/python/sympy/sympy/core/mul.pyc in _eval_subs(self, old, new)
    809                     # collect commutative terms                     

    810                     else:
--&gt; 811                         comms_final.remove(ele)
    812                                                
    813                 # continue only if all commutative terms in old are
present


ValueError: list.remove(x): x not in list

In [6]: test.subs({c3**2 : 1-s3**2})
ERROR: An unexpected error occurred while tokenizing input
The following traceback may be corrupted or invalid       
The error message is: ('EOF in multi-line statement', (22, 0))

ERROR: An unexpected error occurred while tokenizing input
The following traceback may be corrupted or invalid       
The error message is: ('EOF in multi-line statement', (96, 0))

---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)

/home/luke/lib/python/sympy/&lt;ipython console&gt; in &lt;module&gt;()

/home/luke/lib/python/sympy/sympy/core/basic.pyc in subs(self, *args)
   1021             sequence = args[0]                               
   1022             if isinstance(sequence, dict):                   
-&gt; 1023                 return self._subs_dict(sequence)             
   1024             elif isinstance(sequence, (list, tuple)):        
   1025                 return self._subs_list(sequence)             

/home/luke/lib/python/sympy/sympy/core/basic.pyc in _subs_dict(self, sequence)
   1111                 subst.append(pattern)                                 
   1112         subst.reverse()                                               
-&gt; 1113         return self._subs_list(subst)                                 
   1114                                                                       
   1115     def _seq_subs(self, old, new):                                    

/home/luke/lib/python/sympy/sympy/core/basic.pyc in _subs_list(self, sequence)
   1064         for old, new in sequence:                                     
   1065             if hasattr(result, 'subs'):                               
-&gt; 1066                 result = result.subs(old, new)                        
   1067         return result                                                 
   1068                                                                       

/home/luke/lib/python/sympy/sympy/core/basic.pyc in subs(self, *args)
   1028         elif len(args) == 2:
   1029             old, new = args
-&gt; 1030             return self._subs_old_new(old, new)
   1031         else:
   1032             raise TypeError(&quot;subs accepts either 1 or 2 arguments&quot;)

/home/luke/lib/python/sympy/sympy/core/cache.pyc in wrapper(*args, **kw_args)
     83         except KeyError:
     84             pass
---&gt; 85         func_cache_it_cache[k] = r = func(*args, **kw_args)
     86         return r
     87

/home/luke/lib/python/sympy/sympy/core/basic.pyc in _subs_old_new(self,
old, new)
   1037         old = sympify(old)
   1038         new = sympify(new)
-&gt; 1039         return self._eval_subs(old, new)
   1040
   1041     def _eval_subs(self, old, new):

/home/luke/lib/python/sympy/sympy/core/add.pyc in _eval_subs(self, old, new)
    310                     ret_set = self_set - old_set
    311                     return Add(new, coeff_self, -coeff_old,
*[s._eval_subs(old, new) for s in ret_set])
--&gt; 312         return self.__class__(*[s._eval_subs(old, new) for s in
self.args])
    313
    314     @cacheit

/home/luke/lib/python/sympy/sympy/core/mul.pyc in _eval_subs(self, old, new)
    809                     # collect commutative terms

    810                     else:
--&gt; 811                         comms_final.remove(ele)
    812
    813                 # continue only if all commutative terms in old are
present


ValueError: list.remove(x): x not in list

In [7]: 
</pre>

- *Category:* QA
- *Time to complete:* 48 hours

### [2493](http://code.google.com/p/sympy/issues/detail?id=2493&q=label%3ACodeInImportedIntoSpreadsheet) - Clean up test_lambdify.py
<pre>
test_lambdify.py has a bunch of try blocks that should be using raises(). 
</pre>

- *Category:* QA
- *Time to complete:* 48 hours

### [2788](http://code.google.com/p/sympy/issues/detail?id=2788&q=label%3ACodeInImportedIntoSpreadsheet) - Commented out tests should be XFAILed
<pre>
If you &quot;git grep '# *assert'&quot;, you'll see a bunch of tests where the test line is commented out.  These should be changed to be XFAIL tests, so that we can see if they start passing.  Also, they should be double checked to see if they really would start passing (e.g., they don't have syntax errors). 
</pre>

- *Category:* QA
- *Time to complete:* 48 hours

### [2157](http://code.google.com/p/sympy/issues/detail?id=2157&q=label%3ACodeInImportedIntoSpreadsheet) - sympy development rules
<pre>
I think there is a consensus about the requirements for inclusion of a (nontrivial) patch in sympy:

1. All tests have to pass. (Include new tests for new features.)
2. The patch has to be positively reviewed by someone else. (If there a objections, a consensus has to be reached.)
3. Wait at least 24 hours before pushing it in.


I think it should be easily accessible from the website [1], probably from the README too. It should be clear to newcomers that not only contribution is very welcome, but also reviewing patches. (The latter currently lacks somewhat imho.) People new to sympy should not be afraid to review patches.

Maybe there should even be a short how-to about reviewing patches.

What do you think?


[1] <a href="http://sympy.org/development.html" rel="nofollow">http://sympy.org/development.html</a> 
</pre>

- *Category:* Training
- *Time to complete:* 48 hours

### [2769](http://code.google.com/p/sympy/issues/detail?id=2769&q=label%3ACodeInImportedIntoSpreadsheet) - Make video tutorials for SymPy
<pre>
We can have several Code-In tasks for this.  Create some video tutorials for SymPy, and upload them to some SymPy channel on YouTube. 
</pre>

- *Category:* Training
- *Time to complete:* 48 hours

### [2806](http://code.google.com/p/sympy/issues/detail?id=2806&q=label%3ACodeInImportedIntoSpreadsheet) - Add more tips to the tips page (10 tips)
<pre>
We have a page of tips that we are compiling at <a href="https://github.com/sympy/sympy/wiki/tips" rel="nofollow">https://github.com/sympy/sympy/wiki/tips</a>.  This should be really fleshed out, so that we have enough tips to do something interesting with.

For Code-In, we can create multiple tasks.  Each task (easy) can be to create say ten tips. 
</pre>

- *Category:* Training
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to German
<pre>
Our webpage can be translated to other languages. Note that this is connected with <a title="Improve our webpage"  href="/p/sympy/issues/detail?id=2764">issue #2764</a>, about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change. 
</pre>

- *Category:* Translation
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to French
<pre>
Our webpage can be translated to other languages. Note that this is connected with <a title="Improve our webpage"  href="/p/sympy/issues/detail?id=2764">issue #2764</a>, about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change. 
</pre>

- *Category:* Translation
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Czech
<pre>
Our webpage can be translated to other languages. Note that this is connected with <a title="Improve our webpage"  href="/p/sympy/issues/detail?id=2764">issue #2764</a>, about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change. 
</pre>

- *Category:* Translation
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Polish
<pre>
Our webpage can be translated to other languages. Note that this is connected with <a title="Improve our webpage"  href="/p/sympy/issues/detail?id=2764">issue #2764</a>, about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change. 
</pre>

- *Category:* Translation
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Bulgarian
<pre>
Our webpage can be translated to other languages. Note that this is connected with <a title="Improve our webpage"  href="/p/sympy/issues/detail?id=2764">issue #2764</a>, about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change. 
</pre>

- *Category:* Translation
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Serbian
<pre>
Our webpage can be translated to other languages. Note that this is connected with <a title="Improve our webpage"  href="/p/sympy/issues/detail?id=2764">issue #2764</a>, about improving our webpage: if someone is working on that, there's likely no point in translating the page as it'll change. 
</pre>

- *Category:* Translation
- *Time to complete:* 48 hours

### [2637](http://code.google.com/p/sympy/issues/detail?id=2637&q=label%3ACodeInImportedIntoSpreadsheet) - Unicode Sigma for pretty printed Sum
<pre>
I've been looking into how to pretty print the Sigma using unicode.  Here's what I've got so far:

This is what we do for ascii:
  n         
 __         
 \ `        
  )   2⋅f(k)
 /_,        
k = 1       

Here's the best unicode I have so far:

   n       
  __       
  ╲       
   )   f(k)
  ╱
  ‾‾      
 k = 1     

I couldn't find characters (yet) to replicate ` and , (the new horizontal lines are at a different height).  I also haven't found a better replacement for ).

There are these unicode symbols

⎲
⎳

(\u23b2 and \u23b3, respectively) which take up more than one character of space in my terminal (both width and height) and would actually look kind of nice for summations of that size.  So this is the issue from <a href="https://github.com/sympy/sympy/pull/389" rel="nofollow">https://github.com/sympy/sympy/pull/389</a> again.  How do we programmatically tell if a symbol takes up more than one character space, and if so, how many? 
</pre>

- *Category:* UI
- *Time to complete:* 48 hours

### [2636](http://code.google.com/p/sympy/issues/detail?id=2636&q=label%3ACodeInImportedIntoSpreadsheet) - Pretty print Product
- *Category:* Code
- *Time to complete:* 48 hours


## Links:
- [[GCI-2011 Landing]]
- [[GCI-2011 Mentors]]
- [CGI-2011 Task list (spreadsheet)](https://docs.google.com/spreadsheet/ccc?key=0AiMKW-ZM-_fedFpSWm51VFBFZkdTRnh3WkhYRndSVXc)
- [GCI-2011 Task list (wiki)](https://github.com/sympy/sympy/wiki/GCI-2011-Task-list)
- [[GCI-2011 Organization Application]]