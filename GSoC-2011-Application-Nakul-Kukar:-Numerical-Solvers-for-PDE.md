**Implementation of Numerical PDE Solvers in SymPy**

_Nakul Kukar_

_Indian Institute of Space Science and Technology, India_

**Application for Google Summer of Code 2011**

**Abstract**

I intend to implement PDE solvers in SymPy, which rely upon numerical methods to find solutions to these equations. Since SymPy has very basic functionality in place to handle PDEs at present, hence I believe that inclusion of such solvers would greatly enhance the versatility of SymPy’s PDE Module. The main aim at present is to implement some very basic PDEs which could be quickly solved by very simple yet efficient Finite Difference solvers.

**Project Description**

Partial Differential Equations are widely used to model numerous phenomena in physics, chemistry, etc. Most importantly they describe all sorts of fluid and energy flows occurring in everyday engineering applications. Hence there is ample thrust on developing ways to solve these PDEs. Numerical methods are most commonly used to solve these PDEs, but these methods are so complex that they need to be coded, so that we can use computing abilities of computers to obtain solutions. 

SymPy can serve as an ideal platform to implement such methods as its PDE module is quite nascent and holds potential for very massive development. However, as the complexity of PDE increases, the method required to solve it also becomes increasingly complex. Inclusion of such complex methods tend to make the code highly resource intensive and pose the problem of huge memory requirements too. Inclusion of Riemann Solvers or solvers for Euler equations would make SymPy unnecessarily heavy and complex at the present stage. It may even lead to a complete overhaul of the present framework of the PDE module in SymPy which is being avoided for the present project.

Therefore in light of the above problem, I aim to implement some basic Finite Difference solvers to solve simple elliptic, parabolic and hyperbolic PDEs. I am choosing ‘simple’ PDEs as they are easier to solve and very elegant finite difference methods exist to solve them. The specific PDEs that I am thinking of implementing are 1-D Heat Equation (Parabolic) with or without source term, 2-D Poisson Equation (Elliptic), 1-D 1st Order Wave Equation (Hyperbolic), and at a later stage maybe Schrodinger Wave Equation. 

I am looking at implementing both explicit and implicit solvers. Presence of both kinds of schemes would further enhance SymPy’s functionality. Some specific schemes that I have in mind are DuFort-Frankel Scheme or Euler (Explicit) and Crank-Nicholson Scheme (Implicit) for parabolic PDEs. Then Upwind and Lax-Wendroff Schemes (both Explicit) can be coded for hyperbolic PDEs and 2nd Order Central Discretization for elliptic PDEs. As Schrodinger Equation is also a hyperbolic PDE we can use it as a test case for testing the schemes coded for hyperbolic PDEs. Schrodinger Equation however would require some thought and discussion with the mentor before its implementation.

Regarding the linear algebraic solvers for the implicit solvers, I am thinking of using any one of Pysparse or petsc4py. Even MpMath’s linear algebra routine can be used or developed further for this purpose. The final decision about this can be taken after discussing with the mentors, once I am selected for this project. An algorithm which I intend to code can be like this:

(u_i^(n+1)) = (u_i^(n-1)) + (2α Δt/(Δx^2 ) ((u_(i+1)^n) - (u_i^(n-1)) - (u_i^(n+1)) + u_(i-1)^n ))

This is the algorithm for explicit Dufort-Frankel Scheme that I intend to code. It models 1-D heat equation by taking Initial Condition and Boundary Conditions for u and value of α from the user. Using these inputs evolution of temperature field (u) with time can be modeled using above algorithm. Output would constitute of temperature data at various points, at a particular time step and plots depicting evolution of temperature field with time. Other algorithms for different PDEs are also based on similar lines.

**Method of Approach**

I would cater to three issues during this project. Firstly I would implement an easy to use interface for the numerical solvers in SymPy for the users. The interface could be command line based but should be pretty straight forward to comprehend as very simple and small number of inputs are required for such basic PDEs that I am thinking of coding. This interface should be flexible enough to allow users to make some minor changes to the solver in order to effectively use it to solve their specific PDE. While this is done, it should however be kept in mind that for developing the solvers further or to implement new solvers, still compliance with SymPy’s present framework and editing of its core code would be necessary.

Then I would implement the finite difference solvers for elliptic, parabolic and hyperbolic PDEs. This would require much of the coding but can be done rapidly due to my experience and background in writing such solvers. Most of my time would be used for implementing a modular and flexible interface. Finally I would test and validate the coded solvers and the test cases that would be used could very well become tutorials for this new functionality of SymPy.

**Timeline**

April-May: Before the Coding starts I would go through the source code and comprehend SymPy’s architecture.

May to 1st week of June: I would select a PDE, like heat equation or 1-D linear hyperbolic equation and would code it in Python so that it is giving acceptable outputs.

2nd to 3rd week of June: As I have my final exams during these weeks, I won’t be able to work at full capacity, so I would just try to modify the syntax of above solver to make it compatible with SymPy’s source code.

4th week of June to 2nd week of July: Before the midterm evaluation, I would use the above coded PDE as basis for designing the new interface to input data and test it.

3rd week of July to – 1st week of August: I intend to code 4 to 5 more PDE solvers and seamlessly merge the new interface with them and merge these new solvers with SymPy’s platform.

1st week of August to final closing date: I would test the new solvers and put in place the ‘tutorials’ for these solvers in the SymPy’s documentation.

**Project Deliverables**

Creation of the modular and flexible user interface for the numerical solvers.

Implementation of 4-5 finite difference solvers for parabolic and elliptic PDEs.

Inclusion of tutorials for these solvers in SymPy’s documentation.

**Benefits for SymPy**

Enhancement of SymPy’s capabilities leading to more functionality for the users.

Easy future development of SymPy’s numerical solver module possible, due to scope of incorporation of more solvers which are also based upon similar architecture as the ones coded during this project.

Evaluation of SymPy as to how efficiently its code uses the available computing resources as fast computation would also become a major concern for SymPy after the inclusion of numerical solvers for PDEs. 

**About Me**

I am an undergraduate student of Aerospace Engineering at Indian Institute of Space Science and Technology, India. I have studied various subjects relevant to this project like Computaional Fluid Dynamics (focused on FDM for subsonic and supersonic flows), Computaional Gas Dynamics (focused on FVM for Supersonic Flows), and Numerical Methods to solve Partial Diffrential Equations. I have also studied FVM for subsonic (both compressible and incompressible) flows. In addition I also have fundamental knowledge of FEM as applied to structures. I have also been working, on my own, for past two years on Computational Fluid Dynamics (CFD).

My work has included simulating, both internal and external flows, of interest in Aerospace Engineering. I have also worked on coding numerical solvers for such flows, which are primarily governed by complex PDEs, in C++ and Octave. The solvers that I have coded are based on Finite Difference and Finite Volume Methods. I also have experience of developing the capabilities of a CFD software, OpenFOAM, further by coding a solver for supersonic combustion in syntax compatible with the software and using its pre-defined libraries and modules and its I/O Streams. Presently I am working on implementing a numerical solver for Supersonic Combustion in CUDA.

**Platform for Coding**

I have downloaded and installed SymPy on Windows as well as Linux (Ubuntu-10.10). If I am selected for this project, I would be doing entire coding on Ubuntu.

**Other Commitments**

I have final semester exams from 10th to 20th June. During this time I won’t be able to contribute fully to my project. For the rest of the coding period (May-August), I can conveniently devote around 40 hrs./week for the project.