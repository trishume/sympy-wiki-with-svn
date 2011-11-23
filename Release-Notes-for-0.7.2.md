# Release Notes for SymPy 0.7.2
These are the release notes for SymPy 0.7.2. SymPy 0.7.0 was released on December 1, 2011. (**TODO**)

## Backwards compatibility breaks
-KroneckerDelta class is moved from sympy/physics/quantum/kronecker.py to sympy/functions/special/tensor_functions.py.

-Merged the KroneckerDelta class in sympy/physics/secondquant.py with the class above.

-Dij class in sympy/functions/special/tensor_functions.py is replaced with KroneckerDelta.


## Major Changes
### Python 3 support
SymPy now supports Python 3. The officially supported version is 3.2, but 3.1 should also work in a pinch. The Python 3-compatible tarballs will be provided separately, but it's also possible to download Python 2 code and convert it manually, via the bin/use2to3 utility. See the README for more information.

### PyPy support
SymPy also supports the latest version of PyPy (1.6). However, NumPy is disabled completely when running with PyPy, as it only has partial support for it. 

### Combinatorics
A new module called Combinatorics was added which is the result of a successful GSoC project. It attempts to replicate the functionality of Combinatorica and currently has full featured support for Permutations, Subsets, Gray codes and Prufer Codes.

## Other Changes

A new module `gaussopt` was added supporting the most basic constructions from Gaussian optics (ray tracing matrices, geometric rays and Gaussian beams).

In addition to the more noticeable changes listed above, there have been numerous other smaller additions, improvements and bug fixes in the **TODO** commits in this release. See the git log for a full list of all changes. The command `git log sympy-0.7.1..sympy-0.7.2` will show all commits made between this release and the last. You can also see the issues closed since the last release [here](). (**TODO**: update this if release date changes)
## Authors

The following people contributed at least one patch to this release (names are given in alphabetical order by last name). A total of 35 people contributed to this release. People with a * by their names contributed a patch for the first time for this release. Six people contributed for the first time for this release. **TODO**: This was written on Nov 15th, we should check if something changed right before the actual release (i.e., new GCI contributors).

Thanks to everyone who contributed to this release!


* Tom Bachmann
* Raoul Bourquin*
* Ondřej Čertík
* Roberto Colistete-Jr*
* Renato Coutinho
* Luis Garcia*
* Gilbert Gede
* Brian Granger
* Gert-Ludwig Ingold*
* Fredrik Johansson
* Stefan Krastanov
* Priit Laes
* Tim Lahey
* Ronan Lamy
* Tomo Lazovich
* Dale Lukas Peterson
* Sam Magura
* Saptarshi Mandal
* Miha Marolt*
* Aaron Meurer
* Jason Moore
* Mateusz Paprocki
* Vladimir Perić
* Mario Pernici
* Nicolas Pourcelot
* Julien Rioux*
* Matthew Rocklin
* Nikhil Sarda
* Chris Smith
* Prafullkumar P. Tale (Hector)
* Alexey U. Gudchenko
* Srinivas Vasudevan
* Sean Vig
* Luca Weihs
* Jeremias Yehdegho