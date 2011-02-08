<pre>
 In [1]: M = Matrix(4, 4, lambda i,j: i*j+1)
 
 In [2]: M.eigenvals()
 Out[2]: 
 ⎧      ⎽⎽⎽⎽                 ⎽⎽⎽⎽   ⎫
 ⎨9 - ╲╱ 61 : 1, 0: 2, 9 + ╲╱ 61 : 1⎬
 ⎩                                  ⎭
 
 In [3]: M = Matrix(4, 4, lambda i,j: i*j+2)
 
 In [4]: M.eigenvals()
 Out[4]: {2: 1, 0: 2, 20: 1}
 
 In [5]: M = Matrix(4, 4, lambda i,j: i*j+3)
 
 In [6]: M.eigenvals()
 Out[6]: 
 ⎧       ⎽⎽⎽⎽⎽            ⎽⎽⎽⎽⎽         ⎫
 ⎨13 - ╲╱ 109 : 1, 13 + ╲╱ 109 : 1, 0: 2⎬
 ⎩                                      ⎭
 
 In [7]: M
 Out[7]: 
 ⎡ 3  3  3  3⎤
 ⎢ 3  4  5  6⎥
 ⎢ 3  5  7  9⎥
 ⎣ 3  6  9 12⎦
 
 In [8]: M = Matrix(4, 4, lambda i,j: i*j+x)
 
 In [9]: M
 Out[9]: 
 ⎡    x     x     x     x⎤
 ⎢    x 1 + x 2 + x 3 + x⎥
 ⎢    x 2 + x 4 + x 6 + x⎥
 ⎣    x 3 + x 6 + x 9 + x⎦
 
 In [10]: M.eigenvals()
 Out[10]: 
 ⎧             ⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽                        ⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽⎽   ⎫
 ⎪            ╱                  2                        ╱                  2    ⎪
 ⎨          ╲╱  196 + 32*x + 16*x                       ╲╱  196 + 32*x + 16*x     ⎬
 ⎪7 + 2*x + ───────────────────────: 1, 0: 2, 7 + 2*x - ───────────────────────: 1⎪
 ⎩                     2                                           2              ⎭
 
</pre>
Such things are really tedious to do by hand, but in SymPy one can do them just fine.
