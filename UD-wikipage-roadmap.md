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

#### Likely deprecated.

These pages has unknown usage. Or even misleading how the SymPy works now.

1. [Integration](https://github.com/sympy/sympy/wiki/Femtec2009-examples). 
(Correct title too)
2. [[Ideas]] ???
3. [Polynomials-Module](https://github.com/sympy/sympy/wiki/Polynomials-Module)
4. [[Git-hg-rosetta-stone]] - incorrect sympy repository `git://git.sympy.org/sympy.git`
5. [[Million-digits-of-pi]] - may be


#### With bugs (issues must be)

Pages that contains tests, which are failed because of SymPy bugs, so it is for issues. (And it silly SKIPs them now)

1. Totorial

    `(5*x**2 + 3*x).match(p*x**2 + q*x)`
    Got:
        `{p_: 3/x, q_: 5*x}`

#### With bugs (unexplained reasons, requiring research.)

This pages contains fails for unexplained reasons (may be depricated usage), requiring research.

[[Geometry-Module]]

#### GSoC and so on.

#### Under Development pages, or proposals.

[[Assumptions]]
[[Elastic-Layer-Analysis-(ELA)]]
[[Infinities-and-Singularities]] Tom Bachmann's proposals about infinities and singularities.
[[Mathtest]] (test)
[[MediaWiki test]] (test)
