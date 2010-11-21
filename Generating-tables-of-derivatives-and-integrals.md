## Description

This example shows how SymPy can be used to automatically generate tables of, for instance, derivatives and integrals. We print the output in TeX (replacing the $-signs in the TeX output with `\` `[` `\` `]`-tags and subtracting `\operatorname` commands for display on the wiki).

```py
from sympy import *

def derivative_table(functions, x):
    for f in functions:
        s = printing.latex(Eq(Derivative(f, x), diff(f, x)))
        print ":<math>" + s[1:-1] + "</math>", "\n"

def integral_table(functions, x):
    for f in functions:
        s = printing.latex(Eq(Integral(f,x), integrate(f, x)))
        print ":<math>" + s[1:-1] + "</math>", "\n"

var('x')

print "### Derivatives"
derivative_table([cos(x)/(1 + sin(x)**i) for i in range(1, 5)], x)

print "### Integrals"
integral_table([x**i * exp(i*x) for i in range(1, 5)], x)
```

## Output

### Derivatives

\[ \frac{\partial}{\partial x}\left(\frac{\cos\left(x\right)}{1 + \sin\left(x\right)}\right) = - \frac{\sin\left(x\right)}{1 + \sin\left(x\right)} - \frac{\cos^{2}\left(x\right)}{\left(1 + \sin\left(x\right)\right)^{2}} \]

\[ \frac{\partial}{\partial x}\left(\frac{\cos\left(x\right)}{1 + \sin^{2}\left(x\right)}\right) = - \frac{\sin\left(x\right)}{1 + \sin^{2}\left(x\right)} - 2 \frac{\cos^{2}\left(x\right) \sin\left(x\right)}{\left(1 + \sin^{2}\left(x\right)\right)^{2}} \]

\[ \frac{\partial}{\partial x}\left(\frac{\cos\left(x\right)}{1 + \sin^{3}\left(x\right)}\right) = - \frac{\sin\left(x\right)}{1 + \sin^{3}\left(x\right)} - 3 \frac{\cos^{2}\left(x\right) \sin^{2}\left(x\right)}{\left(1 + \sin^{3}\left(x\right)\right)^{2}} \]

\[ \frac{\partial}{\partial x}\left(\frac{\cos\left(x\right)}{1 + \sin^{4}\left(x\right)}\right) = - \frac{\sin\left(x\right)}{1 + \sin^{4}\left(x\right)} - 4 \frac{\cos^{2}\left(x\right) \sin^{3}\left(x\right)}{\left(1 + \sin^{4}\left(x\right)\right)^{2}} \]

### Integrals

\[ \int x {e}^{x}\,dx = - {e}^{x} + x {e}^{x} \]

\[ \int {x}^{2} {e}^{2 x}\,dx = \frac{1}{4} {e}^{2 x} + \frac{1}{2} {x}^{2}{e}^{2 x} - \frac{1}{2} x {e}^{2 x} \]

\[ \int {x}^{3} {e}^{3 x}\,dx = - \frac{2}{27} {e}^{3 x} - \frac{1}{3} {x}^{2} {e}^{3 x} + \frac{1}{3} {x}^{3} {e}^{3 x} + \frac{2}{9} x {e}^{3 x} \]

\[ \int {x}^{4} {e}^{4 x}\,dx = \frac{3}{128} {e}^{4 x} - \frac{3}{32} x {e}^{4 x} - \frac{1}{4} {x}^{3} {e}^{4 x} + \frac{1}{4} {x}^{4} {e}^{4 x} + \frac{3}{16} {x}^{2} {e}^{4 x} \]
