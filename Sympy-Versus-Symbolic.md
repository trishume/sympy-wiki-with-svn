


# Introduction

symbolic is a pure Python package for doing symbolic manipulations within Python and is developed by Pearu Peterson <pearu.peterson@gmail.com>. symbolic is available in sympy svn repository, see the branch sympy-research.

You'll know what is sympy:)

As reported in "symbolic versus sympy" thread, basic operations in symbolic is about 200 faster than in sympy. Hence, Pearu have started a review of sympy.core implementation with a aim speeding up sympy.

In this document the implementation differences between symbolic and sympy will be reported.

# Creating symbolic objects

The instances of symbolic objects in symbolic are always created in finalized form while in sympy the instances are created and then evaluated to get the finalized form.

This means that much more operations are used to create symbolic objects in sympy than in symbolic. That is deadly to performance.

The above comes from implementation. symbolic uses __new__ to create symbolic objects while sympy uses __metaclass__ idiom.

# Evaluating hash values

sympy calculates hash value of a symbolic object when its instance is created. symbolic calculates hash values when hash value is requested.  This saves operations when the code does not use hash values.

Is there a reason why sympy cannot use Python hash calculations?