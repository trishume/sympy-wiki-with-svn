

# Introduction

!SymPy can be used in !TeXmacs. To run a session just select `Insert/Session/SymPy` and `sympy]` prompt will show up to you. If you can't find !SymPy under `Insert/Session/` menu, then select `Insert/Session/Other` and type `sympy` and press return twice.

Currently supported features include:

  * latex printing of expressions and containers
  * exception handling (display of top-most error)
  * last captured output via '`_`' variable
  * multi-line input expressions

!TeXmacs encodes new-lines as spaces so we must use heuristics to know where a multi-line expression is broken. As a result you can't use more than one space in a sequence. However you can and must indent your expression using standard Pyhon rules (see examples for explanation).

# Sample session

[http://mattpap.webd.pl/sympy/tm_sympy.png]