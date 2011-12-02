

This page shows the `curvilinear_coordinates.py` example, which demonstrates how to use sympy to calculate metric tensors (and other things like a laplace operator) in curvilinear coordinates.

```
$ python examples/advanced/curvilinear_coordinates.py
________________________________________________________________________________
Transformation: polar
ρ = ρ⋅cos(φ)
φ = ρ⋅sin(φ)
Jacobian:
⎡cos(φ)  -ρ⋅sin(φ)⎤
⎢                 ⎥
⎣sin(φ)  ρ⋅cos(φ) ⎦
metric tensor g_{ij}:
⎡1  0 ⎤
⎢     ⎥
⎢    2⎥
⎣0  ρ ⎦
inverse metric tensor g^{ij}:
⎡1  0 ⎤
⎢     ⎥
⎢   1 ⎥
⎢0  ──⎥
⎢    2⎥
⎣   ρ ⎦
det g_{ij}:
 2
ρ 
Laplace:
                 2                           
d               d                            
──(f(ρ, φ))   ─────(f(ρ, φ))      2          
dρ            dφ dφ              d           
─────────── + ────────────── + ─────(f(ρ, φ))
     ρ               2         dρ dρ         
                    ρ                        
________________________________________________________________________________
Transformation: cylindrical
ρ = ρ⋅cos(φ)
φ = ρ⋅sin(φ)
z = z
Jacobian:
⎡cos(φ)  -ρ⋅sin(φ)  0⎤
⎢                    ⎥
⎢sin(φ)  ρ⋅cos(φ)   0⎥
⎢                    ⎥
⎣  0         0      1⎦
metric tensor g_{ij}:
⎡1  0   0⎤
⎢        ⎥
⎢    2   ⎥
⎢0  ρ   0⎥
⎢        ⎥
⎣0  0   1⎦
inverse metric tensor g^{ij}:
⎡1  0   0⎤
⎢        ⎥
⎢   1    ⎥
⎢0  ──  0⎥
⎢    2   ⎥
⎢   ρ    ⎥
⎢        ⎥
⎣0  0   1⎦
det g_{ij}:
 2
ρ 
Laplace:
                    2                                                     
d                  d                                                      
──(f(ρ, φ, z))   ─────(f(ρ, φ, z))      2                   2             
dρ               dφ dφ                 d                   d              
────────────── + ───────────────── + ─────(f(ρ, φ, z)) + ─────(f(ρ, φ, z))
      ρ                   2          dρ dρ               dz dz            
                         ρ                                                
________________________________________________________________________________
Transformation: spherical
ρ = ρ⋅cos(φ)⋅sin(θ)
θ = ρ⋅sin(φ)⋅sin(θ)
φ = ρ⋅cos(θ)
Jacobian:
⎡cos(φ)⋅sin(θ)  ρ⋅cos(φ)⋅cos(θ)  -ρ⋅sin(φ)⋅sin(θ)⎤
⎢                                                ⎥
⎢sin(φ)⋅sin(θ)  ρ⋅cos(θ)⋅sin(φ)  ρ⋅cos(φ)⋅sin(θ) ⎥
⎢                                                ⎥
⎣   cos(θ)         -ρ⋅sin(θ)            0        ⎦
metric tensor g_{ij}:
⎡1  0       0     ⎤
⎢                 ⎥
⎢    2            ⎥
⎢0  ρ       0     ⎥
⎢                 ⎥
⎢        2    2   ⎥
⎣0  0   ρ ⋅sin (θ)⎦
inverse metric tensor g^{ij}:
⎡1  0       0     ⎤
⎢                 ⎥
⎢   1             ⎥
⎢0  ──      0     ⎥
⎢    2            ⎥
⎢   ρ             ⎥
⎢                 ⎥
⎢           1     ⎥
⎢0  0   ──────────⎥
⎢        2    2   ⎥
⎣       ρ ⋅sin (θ)⎦
det g_{ij}:
 4    2   
ρ ⋅sin (θ)
Laplace:
   2                                      2                                                         
  d                   d                  d                 d                                        
─────(f(ρ, θ, φ))   2⋅──(f(ρ, θ, φ))   ─────(f(ρ, θ, φ))   ──(f(ρ, θ, φ))⋅cos(θ)      2             
dθ dθ                 dρ               dφ dφ               dθ                        d              
───────────────── + ──────────────── + ───────────────── + ───────────────────── + ─────(f(ρ, θ, φ))
         2                 ρ                2    2                2                dρ dρ            
        ρ                                  ρ ⋅sin (θ)            ρ ⋅sin(θ)                          
________________________________________________________________________________
Transformation: rotating disk
t = t
x = x⋅cos(t⋅w) - y⋅sin(t⋅w)
y = x⋅sin(t⋅w) + y⋅cos(t⋅w)
z = z
Jacobian:
⎡             1                   0          0      0⎤
⎢                                                    ⎥
⎢-w⋅x⋅sin(t⋅w) - w⋅y⋅cos(t⋅w)  cos(t⋅w)  -sin(t⋅w)  0⎥
⎢                                                    ⎥
⎢w⋅x⋅cos(t⋅w) - w⋅y⋅sin(t⋅w)   sin(t⋅w)  cos(t⋅w)   0⎥
⎢                                                    ⎥
⎣             0                   0          0      1⎦
metric tensor g_{ij}:
⎡     2  2    2  2              ⎤
⎢1 + w ⋅x  + w ⋅y   -w⋅y  w⋅x  0⎥
⎢                               ⎥
⎢      -w⋅y          1     0   0⎥
⎢                               ⎥
⎢       w⋅x          0     1   0⎥
⎢                               ⎥
⎣        0           0     0   1⎦
inverse metric tensor g^{ij}:
⎡ 1       w⋅y       -w⋅x     0⎤
⎢                             ⎥
⎢           2  2         2    ⎥
⎢w⋅y   1 + w ⋅y    -x⋅y⋅w    0⎥
⎢                             ⎥
⎢             2        2  2   ⎥
⎢-w⋅x   -x⋅y⋅w    1 + w ⋅x   0⎥
⎢                             ⎥
⎣ 0        0          0      1⎦
det g_{ij}:
1
Laplace:
               2                                  2                          2                          2                          2                       
⎛     2  2⎞   d                    ⎛     2  2⎞   d                          d                          d                          d                        
⎝1 + w ⋅x ⎠⋅─────(f(t, x, y, z)) + ⎝1 + w ⋅y ⎠⋅─────(f(t, x, y, z)) + w⋅y⋅─────(f(t, x, y, z)) + w⋅y⋅─────(f(t, x, y, z)) - w⋅x⋅─────(f(t, x, y, z)) - w⋅x⋅
            dy dy                              dx dx                      dx dt                      dt dx                      dy dt                      

   2                             2                             2                      2                      2                
  d                         2   d                         2   d                      d                      d                 
─────(f(t, x, y, z)) - x⋅y⋅w ⋅─────(f(t, x, y, z)) - x⋅y⋅w ⋅─────(f(t, x, y, z)) + ─────(f(t, x, y, z)) + ─────(f(t, x, y, z))
dt dy                         dy dx                         dx dy                  dt dt                  dz dz               
________________________________________________________________________________
Transformation: parabolic
σ = σ⋅τ
     2    2
    τ    σ 
τ = ── - ──
    2    2 
Jacobian:
⎡τ   σ⎤
⎢     ⎥
⎣-σ  τ⎦
metric tensor g_{ij}:
⎡ 2    2         ⎤
⎢σ  + τ      0   ⎥
⎢                ⎥
⎢          2    2⎥
⎣   0     σ  + τ ⎦
inverse metric tensor g^{ij}:
⎡   1            ⎤
⎢───────     0   ⎥
⎢ 2    2         ⎥
⎢σ  + τ          ⎥
⎢                ⎥
⎢            1   ⎥
⎢   0     ───────⎥
⎢          2    2⎥
⎣         σ  + τ ⎦
det g_{ij}:
   2  2    4    4
2⋅σ ⋅τ  + σ  + τ 
Laplace:
   2                2                                                                                  
  d                d                 ⎛     2      3⎞ d                   ⎛     2      3⎞ d             
─────(f(σ, τ))   ─────(f(σ, τ))      ⎝4⋅σ⋅τ  + 4⋅σ ⎠⋅──(f(σ, τ))         ⎝4⋅τ⋅σ  + 4⋅τ ⎠⋅──(f(σ, τ))   
dσ dσ            dτ dτ                               dσ                                  dτ            
────────────── + ────────────── + ───────────────────────────────── + ─────────────────────────────────
    2    2           2    2       ⎛ 2    2⎞ ⎛   2  2      4      4⎞   ⎛ 2    2⎞ ⎛   2  2      4      4⎞
   σ  + τ           σ  + τ        ⎝σ  + τ ⎠⋅⎝4⋅σ ⋅τ  + 2⋅σ  + 2⋅τ ⎠   ⎝σ  + τ ⎠⋅⎝4⋅σ ⋅τ  + 2⋅σ  + 2⋅τ ⎠
________________________________________________________________________________
Transformation: elliptic
μ = a⋅cos(ν)⋅cosh(μ)
ν = a⋅sin(ν)⋅sinh(μ)
Jacobian:
⎡a⋅cos(ν)⋅sinh(μ)  -a⋅cosh(μ)⋅sin(ν)⎤
⎢                                   ⎥
⎣a⋅cosh(μ)⋅sin(ν)  a⋅cos(ν)⋅sinh(μ) ⎦
metric tensor g_{ij}:
⎡ 2    2        2       2     2       2                                              ⎤
⎢a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)                      0                    ⎥
⎢                                                                                    ⎥
⎢                                            2    2        2       2     2       2   ⎥
⎣                    0                      a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)⎦
inverse metric tensor g^{ij}:
⎡                     2    2        2       2     2       2                                                                                                
⎢                    a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)                                                                                             
⎢──────────────────────────────────────────────────────────────────────────────────                                          0                             
⎢   4    2        2       2        2       4    4        4       4     4       4                                                                           
⎢2⋅a ⋅cos (ν)⋅cosh (μ)⋅sin (ν)⋅sinh (μ) + a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)                                                                        
⎢                                                                                                                                                          
⎢                                                                                                         2    2        2       2     2       2            
⎢                                                                                                        a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)         
⎢                                        0                                           ──────────────────────────────────────────────────────────────────────
⎢                                                                                       4    2        2       2        2       4    4        4       4     
⎣                                                                                    2⋅a ⋅cos (ν)⋅cosh (μ)⋅sin (ν)⋅sinh (μ) + a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh

            ⎤
            ⎥
            ⎥
            ⎥
            ⎥
            ⎥
            ⎥
            ⎥
────────────⎥
4       4   ⎥
 (μ)⋅sin (ν)⎦
det g_{ij}:
   4    2        2       2        2       4    4        4       4     4       4   
2⋅a ⋅cos (ν)⋅cosh (μ)⋅sin (ν)⋅sinh (μ) + a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)
Laplace:
                                                           2                                                                                    2          
            ⎛ 2    2        2       2     2       2   ⎞   d                                      ⎛ 2    2        2       2     2       2   ⎞   d           
            ⎝a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)⎠⋅─────(f(μ, ν))                           ⎝a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)⎠⋅─────(f(μ, ν))
                                                        dμ dμ                                                                                dν dν         
────────────────────────────────────────────────────────────────────────────────── + ──────────────────────────────────────────────────────────────────────
   4    2        2       2        2       4    4        4       4     4       4         4    2        2       2        2       4    4        4       4     
2⋅a ⋅cos (ν)⋅cosh (μ)⋅sin (ν)⋅sinh (μ) + a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)   2⋅a ⋅cos (ν)⋅cosh (μ)⋅sin (ν)⋅sinh (μ) + a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh

                                                                                                                                                           
               ⎛ 2    2        2       2     2       2   ⎞ ⎛     4    3        4                4     4       3                4     2       3        2    
               ⎝a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)⎠⋅⎝- 4⋅a ⋅cos (ν)⋅sinh (μ)⋅sin(ν) + 4⋅a ⋅cosh (μ)⋅sin (ν)⋅cos(ν) - 4⋅a ⋅cosh (μ)⋅sin (ν)⋅sinh (μ)⋅
                                                                                                                                                           
──────────── + ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
4       4                   ⎛   4    2        2       2        2       4    4        4       4     4       4   ⎞ ⎛   4    2        2       2        2      
 (μ)⋅sin (ν)                ⎝2⋅a ⋅cos (ν)⋅cosh (μ)⋅sin (ν)⋅sinh (μ) + a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)⎠⋅⎝4⋅a ⋅cos (ν)⋅cosh (μ)⋅sin (ν)⋅sinh (μ) + 

                                                                                                                                                           
            4    3        2        2          ⎞ d             ⎛ 2    2        2       2     2       2   ⎞ ⎛   4    4        3                 4     3      
cos(ν) + 4⋅a ⋅cos (ν)⋅cosh (μ)⋅sinh (μ)⋅sin(ν)⎠⋅──(f(μ, ν))   ⎝a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin (ν)⎠⋅⎝4⋅a ⋅cos (ν)⋅sinh (μ)⋅cosh(μ) + 4⋅a ⋅cosh (μ)⋅si
                                                dν                                                                                                         
─────────────────────────────────────────────────────────── + ─────────────────────────────────────────────────────────────────────────────────────────────
   4    4        4         4     4       4   ⎞                             ⎛   4    2        2       2        2       4    4        4       4     4       4
2⋅a ⋅cos (ν)⋅sinh (μ) + 2⋅a ⋅cosh (μ)⋅sin (ν)⎠                             ⎝2⋅a ⋅cos (ν)⋅cosh (μ)⋅sin (ν)⋅sinh (μ) + a ⋅cos (ν)⋅sinh (μ) + a ⋅cosh (μ)⋅sin 

                                                                                                          
 4                 4    2        3       2                 4    2       2        3           ⎞ d          
n (ν)⋅sinh(μ) + 4⋅a ⋅cos (ν)⋅cosh (μ)⋅sin (ν)⋅sinh(μ) + 4⋅a ⋅cos (ν)⋅sin (ν)⋅sinh (μ)⋅cosh(μ)⎠⋅──(f(μ, ν))
                                                                                               dμ         
──────────────────────────────────────────────────────────────────────────────────────────────────────────
   ⎞ ⎛   4    2        2       2        2         4    4        4         4     4       4   ⎞             
(ν)⎠⋅⎝4⋅a ⋅cos (ν)⋅cosh (μ)⋅sin (ν)⋅sinh (μ) + 2⋅a ⋅cos (ν)⋅sinh (μ) + 2⋅a ⋅cosh (μ)⋅sin (ν)⎠             
```