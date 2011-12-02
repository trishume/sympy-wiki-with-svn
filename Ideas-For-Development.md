

Here are some ideas where sympy could be effectively used. All of those are things that can be done in Maple/Mathematica, but it is much more convenient and easier to have it in Python.

All the things which are written as Mathematica or Maple modules.
As an example, why Sympy is a better approach than Maple, look into http://sympy.googlecode.com/svn/trunk/doc/gruntz.pdf, page 131, there is a code for computing symbolic limits in the Maple language. Then look into http://sympy.googlecode.com/svn/trunk/sym/modules/limits.py, which does the same thing (I used the Maple code as a reference). Sympy code is shorter and cleaner.

  * for a real world example, look at the sources of http://www.feyncalc.org/ for doing quantum field theory (QFT) calculations, it's a larger library, written in a comletely messy Mathematica language. Another thing is, that even though feyncalc is opensource, it depends on Mathematica, which is a very expensive product. To have some feeling what kind of equations need to be solved in QFT, look here: http://www.feyncalc.org/download/examples/vacuumselfenergy/ or http://www.feyncalc.org/download/examples/csaba/qQ-VV.html

  * port [http://grtensor.phy.queensu.ca/ GRTensorII] to !SymPy
  * port [http://metric.iem.csic.es/Martin-Garcia/xAct/ xTensor] to !SymPy
  * port all of this: http://metric.iem.csic.es/Martin-Garcia/xAct/xPert/index.html

  * anything, where the calculation is standard, but tedious. Examples:
    * computing an area of a surface that is given parametrically
    * finding solutions to partial differential equations in the form of series
    * deriving the Einstein equations in general relativity from the metric tensor


There are many areas, where a symbolic manipulation library can be used. But it must be much easier to use it (and extend it) than Maple or Mathematica is.