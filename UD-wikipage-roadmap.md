<!-- wikitest skip -->

# UD Wikipages roadmap

## Introduction

This page describe current situation with wiki pages, and what (and whom) to do with them.

## Current situation

### Classification of pages

#### Not formated pages.

Not formated at all. And they have a bad view. And ./wikitest, btw,  does not find out any examples into them.

[[Euroscipy2008-examples]]
[[Finding-roots-of-polynomials]]
[[Geometric-Algebra-Module]]
[[ODEnotes]]
[[Profiler-output]]
[[Related-software]] - links are incorrect.
[[Scipy2008-examples]]
[[Symbolic-integration]]

#### Pages with incorrect title or filename.

Reasons:
1) github wiki generate index page [Pages](https://github.com/sympy/sympy/wiki/_pages) by parsing title of page.
2) Not standard file names (a wild amount of GsOC pages with different dialects of writtings of tiles or file names)

- [Integration](https://github.com/sympy/sympy/wiki/Femtec2009-examples)  ???

- [Google Code-In 2011](https://github.com/sympy/sympy/wiki/GCI-2011-Landing) -  title must 'GCI 2011 Landing'
- [Organization description](https://github.com/sympy/sympy/wiki/GCI-2011-Organization-Application) - title must 'GCI 2011 Organization Application' or 'GCI 2011 Organization description'
- [Expanding on the ODEs](https://github.com/sympy/sympy/wiki/GSoC-2011-Application-Gregory-Ksionda) - incorrect title.
- [About me](https://github.com/sympy/sympy/wiki/GSoC-2011-Report-Gilbert-Gede:-PyDy) - incorrect title.
- [About](https://github.com/sympy/sympy/wiki/Gsoc-2011-report-jeremias-yehdegho:-implementing-f5) - incorrect title.
- [About Me](https://github.com/sympy/sympy/wiki/Gsoc-2011-report-saptarshi-mandal:-combinatorics-package-for-sympy)  - incorrect title.
- [About](https://github.com/sympy/sympy/wiki/Gsoc-2011-report-sherjil-ozair:-symbolic-linear-algebra)  - incorrect title.
- [About Me Introduction GSoC Review](https://github.com/sympy/sympy/wiki/GSoC-2011-Report-Tom-Bachmann:-Definite-Integration) - incorrect title.

- [Introduction](https://github.com/sympy/sympy/wiki/Matrix-Expressions) - incorrect title.
- [[Random-Variables]] ??? compare with [[GSoC 2011 Application Matthew Rocklin: Random Variables]] and [[GSoC 2011 Report Matthew Rocklin: Random Variables]]

#### Likely deprecated or draft.

These pages has unknown usage. Or even misleading how the SymPy works now.

1. [Integration](https://github.com/sympy/sympy/wiki/Femtec2009-examples). 
(Correct title too)
1. [[Ideas]] ???
1. [Polynomials-Module](https://github.com/sympy/sympy/wiki/Polynomials-Module)
1. [[Git-hg-rosetta-stone]] - incorrect sympy repository `git://git.sympy.org/sympy.git`
1. [[Million-digits-of-pi]] - may be depricated.
1. [[Ray-transfer-matrix-calculations]] - may be depricated, or under development, or not well formatted.
1. [[Roadmap]] or [[Plan-for-SymPy-1.0]] - one page is actual?
1. [[Sage-Symbench]] - may be depricated.
1. [[SymPy-in-the-news]] - add news (2008 the last one)
1. [[SymPy Papers]] - add papers (This task have [issue](http://code.google.com/p/sympy/issues/detail?id=2800) in the issue tracker.)
1. [[Technical-References]] - may be to add some references?
1. [[DocstringsModules referenceTutorial]] - draft

#### With bugs (issues must be)

Pages that contains tests, which are failed because of SymPy bugs, so it is for issues. (And it silly SKIPs them now)

1. Totorial

    `(5*x**2 + 3*x).match(p*x**2 + q*x)`
    Got:
        `{p_: 3/x, q_: 5*x}`

#### With bugs (unexplained reasons, requiring research.)

This pages contains fails for unexplained reasons (may be depricated usage), requiring research.

- [[Geometry-Module]]
- [[Number-Theory-in-SymPy]]

#### GSoC and so on.

#### Under Development theme, or proposals.

- [[Assumptions]]
- [[Elastic-Layer-Analysis-(ELA)]]
- [[Infinities-and-Singularities]] Tom Bachmann's proposals about infinities and singularities.
- [[Mathtest]] (test page)
- [[MediaWiki test]] (test page)
- [[Rest test]] (test page)
- [[Sandbox]] 
- [[SCSP Branches]]
- [[SCSP-Issues]]
- [[Some-notes-regarding-Permutation-Groups]]
- [[Strategy-to-set-up-the-structure-of-the-new-Matrix-module]]
- [[sympy-series]] -
- [[table-test]] (test page)
- [[UD - Function expansions and series]]
- [[UD - Function expansions and series - definitions]]
- [[UD - Function expansions and series - current situation and applications]]
- [[UD - Function expansions and series - user interface]
- [[UD Under Development]]
- [[UD Wikipages roadmap]]