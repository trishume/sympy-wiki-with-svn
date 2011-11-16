# Combinatorics Module

<!-- wikitest release,master -->

## Introduction

The combinatorics module intends to provide much of the features of Combinatorica and the computational group theory module of Mathematica. An aim for the future is to provide functionality provided in GAP that may be missing in Mathematica.

## Available Entities

The following entities are currently available in the combinatorics module:

* Permutation
* Graph

### Permutation
The permutation module currently provides much of the features detailed in http://reference.wolfram.com/mathematica/guide/Permutations.html
Docstrings,doctests and tests are missing and all algorithms assume that the permutation is in the linear representation
and elements are 0 indexed. This restriction can be very easily handled and the module can be made completely symbolic
by using a dict instead of a list as a container for the permutation.

There are three rankings supported: lexicographical, Trotter-Johnson and Myrvold-Ruskey;
the latter, called here `nonlex`, is in linear time.
For a full API listing and an explanation of the methods and their return values please view the documentation that comes with SymPy or visit the API listing available in the [git repository](https://github.com/sympy/sympy).

## Example Usage
The following Python session gives one an idea of how to work with the permutation module.

```python
    >>> from sympy.combinatorics.permutations import Permutation
    >>> x = Permutation([0,1,2,3])
    >>> x.rank_nonlex()
    23
    >>> x.inversions()
    0
    >>> x = Permutation([ [0,1],[2,3] ])
    >>> x.cyclic_form
    [[0, 1], [2, 3]]
    >>> x.array_form
    [1, 0, 3, 2]
    >>> x*(~x) == Permutation([0,1,2,3])
    True
    >>> x = Permutation([range(10)])
    >>> x.order()
    10
    >>> x**10 == Permutation(range(10))
    True
```

Other additional features such as displaying Rothe diagrams will depend on presence of other container
structures, such as the tableform by Ondrej.

## Graph usage example

## Future work
Permutation groups, Schreier sims, computational group theoretic algorithms, partitions and subsets.