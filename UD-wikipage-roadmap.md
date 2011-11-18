# UD Wikipages roadmap

## Introduction

This page describe current situation with wiki pages, and what (and whom) to do with them.

## Current situation

### Classification of pages

#### Not formated pages.

Not formated at all. And they have a bad view. And ./wikitest, btw,  does not find out any examples into them.

#### Pages with incorrect title or filename.

Reasons:
1) github wiki generate index page [Pages](https://github.com/sympy/sympy/wiki/_pages) by parsing title of page.
2) Not standard file names (a wild amount of GsOC pages with different dialects of writtings of tiles or file names)

#### Likely deprecated.

These pages has unknown usage. Or even misleading how the SymPy works now.

1. (Integration)[https://github.com/sympy/sympy/wiki/Polynomials-Module]. 
(Correct title too)
2. [Polynomials-Module](https://github.com/sympy/sympy/wiki/Polynomials-Module)

#### With bugs (issues must be)

Pages that contains tests, which are failed because of SymPy bugs, so it is for issues. (And it silly SKIPs them now)

1. Totorial
    '''
        >>> (5*x**2 + 3*x).match(p*x**2 + q*x)
    Got:
        {p_: 3/x, q_: 5*x}
    '''

#### With bugs (unexplained reasons, requiring research.)

This pages contains fails for unexplained reasons, requiring research.

#### GSoC and so on.

#### Pages 