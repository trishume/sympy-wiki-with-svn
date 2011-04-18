# Matrices eigenvalues

<!-- wikitest release,master (pretty_print) -->

```py
    >>> from sympy.matrices import Matrix
    >>> M = Matrix(4, 4, lambda i,j: i*j+1)
    >>> M.eigenvals()
                 ____           ____    
    {0: 2, 9 + \/ 61 : 1, 9 - \/ 61 : 1}
```

```py
    >>> M = Matrix(4, 4, lambda i,j: i*j+2)
    >>> M.eigenvals()
    {0: 2, 2: 1, 20: 1}
```

```py
    >>> M = Matrix(4, 4, lambda i,j: i*j+3)
    >>> M.eigenvals()
                  _____            _____    
    {0: 2, 13 + \/ 109 : 1, 13 - \/ 109 : 1}
    >>> M
    [3  3  3  3 ]
    [           ]
    [3  4  5  6 ]
    [           ]
    [3  5  7  9 ]
    [           ]
    [3  6  9  12]
```

```py
 >>> from sympy.abc import x
 >>> M = Matrix(4, 4, lambda i,j: i*j+x)
 >>> M
 [x    x      x      x  ]
 [                      ]
 [x  1 + x  2 + x  3 + x]
 [                      ]
 [x  2 + x  4 + x  6 + x]
 [                      ]
 [x  3 + x  6 + x  9 + x]

 >>> M.eigenvals()
                     _____________________                  ___________________
                    /                   2                  /                   
                  \/  -80*x + (14 + 4*x)                 \/  -80*x + (14 + 4*x)
 {0: 2, 7 + 2*x + ------------------------: 1, 7 + 2*x - ----------------------
                             2                                      2          
 <BLANKLINE>
 __    
 2     
 <BLANKLINE>
 --: 1}
 <BLANKLINE>
```

Such things are really tedious to do by hand, but in SymPy one can do them just fine.
