

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
- *Category:* Code
- *Time to complete:* 144 hours

### [2319](http://code.google.com/p/sympy/issues/detail?id=2319&q=label%3ACodeInImportedIntoSpreadsheet) - LaTeX input
- *Category:* Code
- *Time to complete:* 144 hours

### [2626](http://code.google.com/p/sympy/issues/detail?id=2626&q=label%3ACodeInImportedIntoSpreadsheet) - Piecewise should use a different syntax for "otherwise"
- *Category:* Code
- *Time to complete:* 144 hours

### [2773](http://code.google.com/p/sympy/issues/detail?id=2773&q=label%3ACodeInImportedIntoSpreadsheet) - Implement the trigsimp algorithm by fu et al
- *Category:* Code
- *Time to complete:* 144 hours

### [2789](http://code.google.com/p/sympy/issues/detail?id=2789&q=label%3ACodeInImportedIntoSpreadsheet) - minpoly should work with roots of unity in exponential form
- *Category:* Code
- *Time to complete:* 144 hours

### [1594](http://code.google.com/p/sympy/issues/detail?id=1594&q=label%3ACodeInImportedIntoSpreadsheet) - bin/test --random should also shuffle tests inside a file
Also it is related with issue 1594: once we have the shuffling, we should fix all the failures caused by it. Marking this as a hard task for Code-In, per Aaron's comment on the other issue. 

- *Category:* QA
- *Labels:* Priority-Medium, Testing, Type-Defect
- *Time to complete:* 144 hours

### [2791](http://code.google.com/p/sympy/issues/detail?id=2791&q=label%3ACodeInImportedIntoSpreadsheet) - Allow to manage slow tests better with our test runner
Currently slow tests are simply skipped, but this makes it hard to actually run them. There should be a decorator for this (e.g. @slow) that would all to to run such tests when give an extra option to bin/test or test() (--slow and slow=True, respectively). It should be also possible to specify a timeout for slow tests so that they do not hang test runner. It should be also possible to press Ctrl+C (KeyboardInterrupt) to kill a slow test without killing test runner. There should be statistics added at the end which would tell how many slow tests were run, how many timed out and maybe other. Also, almost all skipped tests (or maybe all) are currently skipped because they are slow, so after this is implemented, they should all be converted. 

- *Category:* QA
- *Labels:* Priority-Medium, Testing, Type-Enhancement
- *Time to complete:* 144 hours

### [2799](http://code.google.com/p/sympy/issues/detail?id=2799&q=label%3ACodeInImportedIntoSpreadsheet) - coverage testing should be part of the bot test
- *Category:* QA
- *Labels:* Priority-Medium, Testing, Type-Enhancement
- *Time to complete:* 144 hours

### [2812](http://code.google.com/p/sympy/issues/detail?id=2812&q=label%3ACodeInImportedIntoSpreadsheet) - Fix failures found by shuffling tests in test file
- *Category:* QA
- *Time to complete:* 144 hours

### [1941](http://code.google.com/p/sympy/issues/detail?id=1941&q=label%3ACodeInImportedIntoSpreadsheet) - Objects that know how to combine themselves
- *Category:* Research
- *Time to complete:* 144 hours

### [2765](http://code.google.com/p/sympy/issues/detail?id=2765&q=label%3ACodeInImportedIntoSpreadsheet) - Research ways to do the assumptions system, including removing the old system
- *Category:* Research
- *Labels:* Assumptions, 
- *Time to complete:* 144 hours

### [2792](http://code.google.com/p/sympy/issues/detail?id=2792&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate how to employ complexity measures in functions like trigsimp(), etc.
- *Category:* Research
- *Time to complete:* 144 hours

### [1817](http://code.google.com/p/sympy/issues/detail?id=1817&q=label%3ACodeInImportedIntoSpreadsheet) - SymPy Cheat Sheet
- *Category:* Training
- *Time to complete:* 144 hours

### [2771](http://code.google.com/p/sympy/issues/detail?id=2771&q=label%3ACodeInImportedIntoSpreadsheet) - Write a document showing the difference between SymPy and other mathematical systems: Maple
- *Category:* Training
- *Time to complete:* 144 hours

### [2521](http://code.google.com/p/sympy/issues/detail?id=2521&q=label%3ACodeInImportedIntoSpreadsheet) - live.sympy.org isn't so easy to use on a mobile device
- *Category:* UI
- *Time to complete:* 144 hours

### [2768](http://code.google.com/p/sympy/issues/detail?id=2768&q=label%3ACodeInImportedIntoSpreadsheet) - Add a feed of what people are doing at SymPy Live
It would be cool to have a little feed at the right on live.sympy.org to show what other people are entering, so that people can see what sorts of things are being done.  

- *Category:* UI
- *Labels:* Live, Priority-Medium, Type-Defect
- *Time to complete:* 144 hours

### [2772](http://code.google.com/p/sympy/issues/detail?id=2772&q=label%3ACodeInImportedIntoSpreadsheet) - Some UI/GUI for the test runner
- *Category:* UI
- *Labels:* Priority-Medium, Type-Enhancement
- *Time to complete:* 144 hours

It would be cool to have some UI/GUI for the test runner that makes it easier to see the failures when they happen. E.g. like http://sourceforge.net/apps/mediawiki/cppunit/nfs/project/c/cp/cppunit/c/c2/Qttestrunner_exa.png  

## <a name="#Medium">Medium</a>
### [281](http://code.google.com/p/sympy/issues/detail?id=281&q=label%3ACodeInImportedIntoSpreadsheet) - Infinity should not be a subclass of Rational
- *Category:* Code
- *Time to complete:* 96 hours

### [363](http://code.google.com/p/sympy/issues/detail?id=363&q=label%3ACodeInImportedIntoSpreadsheet) - Add a split() method for sympy expressions
- *Category:* Code
- *Time to complete:* 48 hours

### [716](http://code.google.com/p/sympy/issues/detail?id=716&q=label%3ACodeInImportedIntoSpreadsheet) - either tangent_line or is_tangent is wrong
- *Category:* Code
- *Time to complete:* 96 hours

### [754](http://code.google.com/p/sympy/issues/detail?id=754&q=label%3ACodeInImportedIntoSpreadsheet) - Have re and im call expand(complex=True)
- *Category:* Code
- *Time to complete:* 96 hours

### [2513](http://code.google.com/p/sympy/issues/detail?id=2513&q=label%3ACodeInImportedIntoSpreadsheet) - Create a SymPyDeprecationWarning for deprecated SymPy behavior
- *Category:* Code
- *Time to complete:* 96 hours

### [2552](http://code.google.com/p/sympy/issues/detail?id=2552&q=label%3ACodeInImportedIntoSpreadsheet) - (1/(x*y)).subs(x*y, whatever) doesn't work
This is doesn't work >>> (1/(x*y)).subs(x*y, 2);1/(x*y). Because >>> (1/(x*y)).args; (1/x, 1/y) automatically changed in Mul class  

- *Category:* Code
- *Labels:* Priority-High, Type-Defect
- *Time to complete:* 96 hours

### [2632](http://code.google.com/p/sympy/issues/detail?id=2632&q=label%3ACodeInImportedIntoSpreadsheet) - Add isympy -c qtconsole
- *Category:* Code
- *Time to complete:* 96 hours

### [2793](http://code.google.com/p/sympy/issues/detail?id=2793&q=label%3ACodeInImportedIntoSpreadsheet) - The dsolve solver for 1st_exact should use integration
- *Category:* Code
- *Time to complete:* 96 hours

### [2794](http://code.google.com/p/sympy/issues/detail?id=2794&q=label%3ACodeInImportedIntoSpreadsheet) - Implement ode solvers from the Moses "Stormy Decade" paper: Almost Linear
- *Category:* Code
- *Time to complete:* 96 hours

### [2841](http://code.google.com/p/sympy/issues/detail?id=2841&q=label%3ACodeInImportedIntoSpreadsheet) - integrate() can not integrate the Abs() function, fix it
- *Category:* Code
- *Time to complete:* 96 hours

### [2849](http://code.google.com/p/sympy/issues/detail?id=2849&q=label%3ACodeInImportedIntoSpreadsheet) - Better heuristics and simplification for integral of cos(x)/sin(x)**n and similar
- *Category:* Code
- *Time to complete:* 96 hours

### [294](http://code.google.com/p/sympy/issues/detail?id=294&q=label%3ACodeInImportedIntoSpreadsheet) - Pass coverage_doctest.py
- *Category:* Documentation
- *Time to complete:* 96 hours

### [707](http://code.google.com/p/sympy/issues/detail?id=707&q=label%3ACodeInImportedIntoSpreadsheet) - move some wikis to github.com/sympy/sympy/wiki
- *Category:* Documentation
- *Time to complete:* 96 hours

### [2470](http://code.google.com/p/sympy/issues/detail?id=2470&q=label%3ACodeInImportedIntoSpreadsheet) - Fix all sphinx errors and warnings
- *Category:* Documentation
- *Time to complete:* 96 hours

### [2770](http://code.google.com/p/sympy/issues/detail?id=2770&q=label%3ACodeInImportedIntoSpreadsheet) - Update stuff that SymPy can do on the homepage
- *Category:* Documentation
- *Time to complete:* 96 hours

### [2779](http://code.google.com/p/sympy/issues/detail?id=2779&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Geometry
- *Category:* Documentation
- *Time to complete:* 96 hours

### [2801](http://code.google.com/p/sympy/issues/detail?id=2801&q=label%3ACodeInImportedIntoSpreadsheet) - lambdify() is not mentioned anywhere
- *Category:* Documentation
- *Time to complete:* 96 hours

### [2528](http://code.google.com/p/sympy/issues/detail?id=2528&q=label%3ACodeInImportedIntoSpreadsheet) - Update SymPy's Wikipedia article
- *Category:* Outreach
- *Time to complete:* 96 hours

### [2764](http://code.google.com/p/sympy/issues/detail?id=2764&q=label%3ACodeInImportedIntoSpreadsheet) - Improve our webpage
- *Category:* Outreach
- *Time to complete:* 96 hours

### [2787](http://code.google.com/p/sympy/issues/detail?id=2787&q=label%3ACodeInImportedIntoSpreadsheet) - Create sticker for SymPy based on the logo
- *Category:* Outreach
- *Time to complete:* 96 hours

### [2796](http://code.google.com/p/sympy/issues/detail?id=2796&q=label%3ACodeInImportedIntoSpreadsheet) - Package the latest version of SymPy for the major distributions: Debian / Ubuntu
- *Category:* Outreach
- *Time to complete:* 96 hours

### [1456](http://code.google.com/p/sympy/issues/detail?id=1456&q=label%3ACodeInImportedIntoSpreadsheet) - use pyflakes to identify simple bugs in sympy and fix them
- *Category:* QA
- *Labels:* EasyToFix, Priority-Medium, Type-Defect
- *Time to complete:* 96 hours

Pick a good sized module in SymPy (i.e., one of the subdirectories of the sympy/ directory, but not one of the ones that only has a few files in it).  

### [1752](http://code.google.com/p/sympy/issues/detail?id=1752&q=label%3ACodeInImportedIntoSpreadsheet) - setup.py test should run the doctests even when the regular tests fail
- *Category:* QA
- *Labels:* EasyToFix, Priority-High, Testing, Type-Defect
- *Time to complete:* 96 hours

### [2786](http://code.google.com/p/sympy/issues/detail?id=2786&q=label%3ACodeInImportedIntoSpreadsheet) - Fill in missing tests for sympy.physics module in test_args.py
- *Category:* QA
- *Time to complete:* 96 hours

### [1235](http://code.google.com/p/sympy/issues/detail?id=1235&q=label%3ACodeInImportedIntoSpreadsheet) - Problem installing in Windows
- *Category:* Research
- *Time to complete:* 96 hours

### [2762](http://code.google.com/p/sympy/issues/detail?id=2762&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate ways to improve substitution, pattern matching, etc.
- *Category:* Research
- *Time to complete:* 96 hours

### [2795](http://code.google.com/p/sympy/issues/detail?id=2795&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate a robust way to have translated documentation
- *Category:* Research
- *Time to complete:* 96 hours

### [2798](http://code.google.com/p/sympy/issues/detail?id=2798&q=label%3ACodeInImportedIntoSpreadsheet) - Research ways to extract statistics from the issue tracker
- *Category:* Research
- *Time to complete:* 96 hours

### [2803](http://code.google.com/p/sympy/issues/detail?id=2803&q=label%3ACodeInImportedIntoSpreadsheet) - Investigate how to make the rewrite framework more flexible
- *Category:* Research
- *Time to complete:* 96 hours

### [2790](http://code.google.com/p/sympy/issues/detail?id=2790&q=label%3ACodeInImportedIntoSpreadsheet) - Create examples/short tutorials using IPython's notebook (IPython >= 0.12)
- *Category:* Training
- *Time to complete:* 96 hours

### [2766](http://code.google.com/p/sympy/issues/detail?id=2766&q=label%3ACodeInImportedIntoSpreadsheet) - Translate tutorial to German
- *Category:* Translation
- *Time to complete:* 96 hours

### [2767](http://code.google.com/p/sympy/issues/detail?id=2767&q=label%3ACodeInImportedIntoSpreadsheet) - Improve the interface of SymPy Live
- *Category:* UI
- *Time to complete:* 96 hours

### [2857](http://code.google.com/p/sympy/issues/detail?id=2857&q=label%3ACodeInImportedIntoSpreadsheet) - sqrt(2).is_irrational is None (should be True)
- *Category:* Code
- *Time to complete:* 96 hours

## <a name="#Easy">Easy</a>
### [615](http://code.google.com/p/sympy/issues/detail?id=615&q=label%3ACodeInImportedIntoSpreadsheet) - Fix the occasions where functions are called with wrong name and write tests
- *Category:* Code
- *Time to complete:* 96 hours

### [654](http://code.google.com/p/sympy/issues/detail?id=654&q=label%3ACodeInImportedIntoSpreadsheet) - Remove dead code from _eval_subs()
- *Category:* Code
- *Time to complete:* 96 hours

### [1058](http://code.google.com/p/sympy/issues/detail?id=1058&q=label%3ACodeInImportedIntoSpreadsheet) - Classifying formulas
- *Category:* Code
- *Labels:* Priority-Medium, Type-Enhancement
- *Time to complete:* 48 hours

### [2276](http://code.google.com/p/sympy/issues/detail?id=2276&q=label%3ACodeInImportedIntoSpreadsheet) - integrate() should use the ode module's undetermined coefficients solver when possible
- *Category:* Code
- *Time to complete:* 48 hours

### [2427](http://code.google.com/p/sympy/issues/detail?id=2427&q=label%3ACodeInImportedIntoSpreadsheet) - Check for incorrect usage of expr.atoms() and change it to free_symbols
- *Category:* Code
- *Time to complete:* 48 hours

### [2534](http://code.google.com/p/sympy/issues/detail?id=2534&q=label%3ACodeInImportedIntoSpreadsheet) - Use "with open" instead of "open … close"
Please see http://code.google.com/p/sympy/issues/detail?id=2534 for full information on this task. Please read https://github.com/sympy/sympy/wiki/gci-2011-landing before completing any tasks for SymPy.  

- *Category:* Code
- *Labels:* EasyToFix, Priority-Medium, Type-Defect
- *Time to complete:* 48 hours

### [2570](http://code.google.com/p/sympy/issues/detail?id=2570&q=label%3ACodeInImportedIntoSpreadsheet) - Remove bare except statements
- *Category:* Code
- *Time to complete:* 48 hours

### [2639](http://code.google.com/p/sympy/issues/detail?id=2639&q=label%3ACodeInImportedIntoSpreadsheet) - The Product() class should not evaluate by default
- *Category:* Code
- *Time to complete:* 48 hours

### [2683](http://code.google.com/p/sympy/issues/detail?id=2683&q=label%3ACodeInImportedIntoSpreadsheet) - det() is called when inverting matrix through GE
- *Category:* Code
- *Time to complete:* 48 hours

### [2760](http://code.google.com/p/sympy/issues/detail?id=2760&q=label%3ACodeInImportedIntoSpreadsheet) - latex(symbol_names) not working with ~x
- *Category:* Code
- *Time to complete:* 48 hours

### [2776](http://code.google.com/p/sympy/issues/detail?id=2776&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in integrals
- *Category:* Code
- *Time to complete:* 48 hours

### [2784](http://code.google.com/p/sympy/issues/detail?id=2784&q=label%3ACodeInImportedIntoSpreadsheet) - 1/function() should be printed differently by latex printer
- *Category:* Code
- *Time to complete:* 48 hours

### [2785](http://code.google.com/p/sympy/issues/detail?id=2785&q=label%3ACodeInImportedIntoSpreadsheet) - Use \functionname instead of \operatorname{functionname} whenever possible
- *Category:* Code
- *Time to complete:* 48 hours

### [2815](http://code.google.com/p/sympy/issues/detail?id=2815&q=label%3ACodeInImportedIntoSpreadsheet) - Parts of the pyglet plotting module does not follow PEP 8, fix it
- *Category:* Code
- *Time to complete:* 48 hours

### [2817](http://code.google.com/p/sympy/issues/detail?id=2817&q=label%3ACodeInImportedIntoSpreadsheet) - Make sure all the built-in __methods__ are defined
- *Category:* Code
- *Time to complete:* 48 hours

### [2830](http://code.google.com/p/sympy/issues/detail?id=2830&q=label%3ACodeInImportedIntoSpreadsheet) - checkodesol() should use force=True
- *Category:* Code
- *Time to complete:* 48 hours

### [2838](http://code.google.com/p/sympy/issues/detail?id=2838&q=label%3ACodeInImportedIntoSpreadsheet) - Move the KroneckerDelta class to another module 
- *Category:* Code
- *Time to complete:* 48 hours

### [2846](http://code.google.com/p/sympy/issues/detail?id=2846&q=label%3ACodeInImportedIntoSpreadsheet) - Integral.transform should allow a change to a different variable
- *Category:* Code
- *Time to complete:* 48 hours

### [16](http://code.google.com/p/sympy/issues/detail?id=16&q=label%3ACodeInImportedIntoSpreadsheet) - Check and compare an old patch concerning object with indices against current sympy
Please see http://code.google.com/p/sympy/issues/detail?id=16 for full information on this task. <br><br>Please read https://github.com/sympy/sympy/wiki/gci-2011-landing before completing any tasks for SymPy. <br><br>Additional Note(s): Check out comment 32 in the bug report. 

- *Category:* Documentation
- *Labels:* EasyToFix, Matrices, Priority-Medium, Type-Enhancement
- *Time to complete:* 48 hours

Check out comment 32 in the bug report. 

### [1886](http://code.google.com/p/sympy/issues/detail?id=1886&q=label%3ACodeInImportedIntoSpreadsheet) - Documentation for the Expr class
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2115](http://code.google.com/p/sympy/issues/detail?id=2115&q=label%3ACodeInImportedIntoSpreadsheet) - Move stuff from the Google Code SVN to git
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2160](http://code.google.com/p/sympy/issues/detail?id=2160&q=label%3ACodeInImportedIntoSpreadsheet) - List of dependencies
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2204](http://code.google.com/p/sympy/issues/detail?id=2204&q=label%3ACodeInImportedIntoSpreadsheet) - Document why unpickling a singleton doesn't return the singleton object with protocol 0 and 1
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2367](http://code.google.com/p/sympy/issues/detail?id=2367&q=label%3ACodeInImportedIntoSpreadsheet) - SymPy's readthedocs documentation is broken
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2597](http://code.google.com/p/sympy/issues/detail?id=2597&q=label%3ACodeInImportedIntoSpreadsheet) - Import all public functions and classes into Sphinx: polys
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2599](http://code.google.com/p/sympy/issues/detail?id=2599&q=label%3ACodeInImportedIntoSpreadsheet) - Update isympy manpage
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2679](http://code.google.com/p/sympy/issues/detail?id=2679&q=label%3ACodeInImportedIntoSpreadsheet) - Refactor GA* documentation to use doctests (or move it to examples/)
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2774](http://code.google.com/p/sympy/issues/detail?id=2774&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Number Theory
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2775](http://code.google.com/p/sympy/issues/detail?id=2775&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Combinotorics 
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2777](http://code.google.com/p/sympy/issues/detail?id=2777&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in functions
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2778](http://code.google.com/p/sympy/issues/detail?id=2778&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in functions/special
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2780](http://code.google.com/p/sympy/issues/detail?id=2780&q=label%3ACodeInImportedIntoSpreadsheet) - ``See Also`` feature in Matrices
- *Category:* Documentation
- *Time to complete:* 48 hours

### [2763](http://code.google.com/p/sympy/issues/detail?id=2763&q=label%3ACodeInImportedIntoSpreadsheet) - Fix the SymPy Logo
- *Category:* Outreach
- *Time to complete:* 48 hours

### [2800](http://code.google.com/p/sympy/issues/detail?id=2800&q=label%3ACodeInImportedIntoSpreadsheet) - Flesh out the SymPy Papers wiki page
- *Category:* Outreach
- *Time to complete:* 48 hours

### [1616](http://code.google.com/p/sympy/issues/detail?id=1616&q=label%3ACodeInImportedIntoSpreadsheet) - Bug in subs
- *Category:* QA
- *Time to complete:* 48 hours

### [2493](http://code.google.com/p/sympy/issues/detail?id=2493&q=label%3ACodeInImportedIntoSpreadsheet) - Clean up test_lambdify.py
- *Category:* QA
- *Time to complete:* 48 hours

### [2788](http://code.google.com/p/sympy/issues/detail?id=2788&q=label%3ACodeInImportedIntoSpreadsheet) - Commented out tests should be XFAILed
- *Category:* QA
- *Time to complete:* 48 hours

### [2157](http://code.google.com/p/sympy/issues/detail?id=2157&q=label%3ACodeInImportedIntoSpreadsheet) - sympy development rules
- *Category:* Training
- *Time to complete:* 48 hours

### [2769](http://code.google.com/p/sympy/issues/detail?id=2769&q=label%3ACodeInImportedIntoSpreadsheet) - Make video tutorials for SymPy
- *Category:* Training
- *Time to complete:* 48 hours

### [2806](http://code.google.com/p/sympy/issues/detail?id=2806&q=label%3ACodeInImportedIntoSpreadsheet) - Add more tips to the tips page (10 tips)
- *Category:* Training
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to German
- *Category:* Translation
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to French
- *Category:* Translation
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Czech
- *Category:* Translation
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Polish
- *Category:* Translation
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Bulgarian
- *Category:* Translation
- *Time to complete:* 48 hours

### [2797](http://code.google.com/p/sympy/issues/detail?id=2797&q=label%3ACodeInImportedIntoSpreadsheet) - Translate our webpage to Serbian
- *Category:* Translation
- *Time to complete:* 48 hours

### [2637](http://code.google.com/p/sympy/issues/detail?id=2637&q=label%3ACodeInImportedIntoSpreadsheet) - Unicode Sigma for pretty printed Sum
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