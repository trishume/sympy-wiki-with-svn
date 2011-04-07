## My Information
* Name: Óscar Nájera
* University: Last year undergraduate physics student at Escuela Politécnica Nacional, Ecuador
* Short bio: As a physicist I specialize myself in computational physics, I have worked on molecular dynamics simulations and my main programming language is C/C++, but I have experience in a variety of programing technologies like: Java, bash, PHP, HTML, CSS, Matlab, Python. I just started a project in Solid State Physics/Material Science for studying and simulating Ferroelectric crystals.
* Email najera.oscar (at) gmail [dot] com

## My coding Platform
I've been using Gentoo Linux for the last 5 years, except for compilations times on every update it's a really nice and customizable OS.

## My project

### Goal
Implement a framework where quantum calculations can be done using Dirac Bra-Ket Notation.
### Motivation
Dirac Notation greatly simplifies the treatment of quantum states, while working on a certain problem. But there always comes a time when calculations have to be done, that's when we use computers, but it is a tedious work to write the corresponding wavefuntion and the operator involved and then integrating over the whole space. There are many know quantum systems with analytically solved eigenstates, after implementing those solutions we could use Dirac Notation to call them and do some calculations like:
Expected values:
\( <E>=<n|H|n> \) , \(<x^2> = <n|x^2|n>\)
Matrix elements:
\(V_{mn}=<m|V|n>\)
Probability Amplitudes:
\(P(n)=|<n|\psi>|^2\),\(H_{mn}=|<m|H|n>|^2\)
Projections: \(|n><n|\psi>\), \(\sum_i |i><i|\psi>\)

### Timeline

* **Warm up**(April 25 - May 23) Become familiar with the quantum code base. Design modules to be implemented and discuss them with the sympy community. Contact other GSoC students working in the quantum code base, discuss collaborative work if possible, if needed, if mandatory, for example people working on projects like implementing analytical solutions to QM system, Position and Momentum basis functions, etc.
* **Phase 1**(May 23 - June 27) Implement the inner product of two states \(<\phi|\psi>\), for Cartesian, cylindrical, and spherical coordinates in 1D, 2D, and 3D. This is very sensitive, because Kets are representation independent but for calculations a representation is needed. Thus inner product must be aware of the treated QM system, it's eigenstates and available implemented representations, space dimensions, coordinate system used, etc. (I won't be home from June 1 to June 9, but will compensate working additional hours during weekday and weekends before my trip. Project must be finished on time)
* **Phase 2**(June 27 - July 15) Include operators \(<\phi|H|\psi>\), same as before, hopefully faster development because only operator representations need to be worked on, previous work should take care of the calculations.
* **Phase 3** (July 15 - August 5) Implement as many QM systems as possible: eigenfunctions and their different representations. Implement perturbation theory expansion to second order, etc. As much as possible able to work this this new framework.
* **Phase 4**(August 5 - August 22) Buffer period in cases some elements of the project take longer than expected. Write documentation, examples, tests for the new framework.