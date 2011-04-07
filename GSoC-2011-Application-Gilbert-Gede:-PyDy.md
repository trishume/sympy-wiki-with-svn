# Gilbert Gede
 gilbertgede@gmail.com / ggede@ucdavis.edu
2nd year PhD student at UC Davis in Mechanical & Aerospace Engineering

I’ve taken UC Davis’s graduate courses in dynamics and multibody dynamics, and am really excited to work on software that would help me and others in working on these problems.  Some problems I’ve studied include the dynamic equations for include the bicycle, a bicycle with a flywheel, a unicycle with a control moment gyroscope, and the two-circle roller (or oloid).  
I have experience in the design and manufacture of mechanical structures, thermo-fluid systems, and medical devices.

My current research at Davis is in optimization, specifically optimal control.  I’ve been using SciPy’s optimization module for my work and comparing it with Matlab’s optimization toolbox.  
I’ve also worked with and designed Kalman filters for attitude (orientation) estimation.  I wrote Python code to implement a Kalman filter for an inertial measurement unit; this is at my github page. This is designed to work in conjunction with a microcontroller (I’ve used both Arduino and mbed microcontrollers with the code).  Additionally, I am in the Sports Biomechanics Lab at UC Davis, working with a number of other graduate students, all doing dynamics research.  

I currently use C/C++, Python, Matlab, and Mathematica. I plan to work full-time on PyDy over the summer, starting June 13th, and by the end of the summer use it for my research. I currently work under OS X or Linux, use VIM and have begun integrating git into my workflow. 
github page: https://github.com/gilbertgede
# Project Description

PyDy (Python Dynamics) is a computational tool built to easily compute complex symbolic kinematic relationships and symbolically derive equations of motion for systems governed by Newton’s laws of motion. The resulting symbolic equations of motion (as opposed to purely numerical methods of model derivation) provide advantages for model manipulation and clearer interpretation of the system dynamics.  This is useful to physicists, engineers, astronomers and anyone concerned with the motion of bodies.

SymPy provides core symbolic manipulation, while PyDy implements the class hierarchy specifically oriented to the analysis of systems of rigid bodies and particles. PyDy computes the kinematic relationships among reference frames easily and intuitively. By managing the kinematics (which becomes complicated in multi-body systems), PyDy allows the analyst to quickly derive equations of motion in a symbolic form, which are immediately useful for a variety of tasks such as simulation, animation, stability analysis, and control system design.  Using SymPy’s features, the software acts a bookkeeper for the thousands of symbolic algebraic and calculus computations that have traditionally been done by hand. Understanding and analysis of multibody systems is a fundamental aspect of much of the work done in applied sciences and engineering. It allows for analytical design optimization, based on the dynamic behavior of a system.  Additionally, these concepts are critical elements of physics and engineering education and can be used as a tool to help teach kinematics and dynamics.

The primary goals of the project are to redefine the object structure of PyDy such that the kinetic, kinematic, inertial, and dynamic aspects of Newtonian mechanics are clearly separated into independent entities.  This is desperately needed in PyDy because the current class structure muddles all of these aspects of Newtonian mechanics into classes with logically unrelated attributes.  As a result, it is very difficult for others to use and extend PyDy.  Once this is performed, I will merge these features into a classical physics module of SymPy.  Additionally I will improve the documentation, tests and examples, and increase the user and contributor base. These are described in detail below.

## Kinetic classes
For our purposes, kinetics refers to the forces and torques (the causes of the motion) applied to particles and rigid bodies (i.e, the left hand side of the Newton-Euler equations of motion).  Classes that will be defined here include a Force class and a Torque class.  Currently in PyDy force and torque vector quantities are attributes of fundamentally kinematic quantities.  For example the Point class currently has a force attribute.  These two need to be clearly separated so that each of aspect of PyDy is usable independently.  By separating these classes, it will become easier to use and extend PyDy.
  
## Kinematic classes
PyDy is designed to quickly manipulate kinematic relationships of bodies in space. It does this by building two trees structures, one for the relative position of points, and another for the relative orientation of reference frames.  The two main existing kinematic classes are the Point and ReferenceFrame class.  These two classes should be usable without any reference to any Kinetic, Inertial, or Dynamic classes, so the goal for this section will be to overhaul the class design so that the only attributes of these classes are attributes relevant to kinematics specifically.  Examples of attributes that need to find a new home are the force attribute of the Point class and the torque attribute of the ReferenceFrame class.

Kinematic attributes that should be included in the Point class include position, velocity, and acceleration, while attributes that belong with the ReferenceFrame class include orientation, angular velocity, and angular acceleration.  The details of the representation and tree relationships (i.e., a point is positioned relative to another point or points) of these quantities will be defined such that the ease of use (see example below) will be preserved.
## Inertial classes

Two inertial class will define the mass and inertia of a particle and/or rigid body.  The mass attribute is trivial in that it can be represented using Sympy’s symbol class.  The inertia can be represented using a 3x3 Sympy matrix class, although care needs to be taken to clearly define which reference frame this matrix is defined in (typically it is the body fixed frame, but not always).  
Particle and RigidBody Classes

These two classes will effectively be container classes of the previous three class objects and will serve to organize the system.  For example, the Particle will have three attributes: a Point class, a mass, and a Force class.  By collecting these three aspects of the Newton-Euler equations into one cohesive unit, formulation of the equations of motion for a system with many particles and/or rigid bodies will be greatly simplified. 
## Dynamic methods

PyDy was originally designed to implement Kane's method for forming the equations of motion, as this method is well suited for computer automation and it automatically eliminates workless constraints.  This will be changed to allow the use of different methods for deriving the equations of motion.  The existing functionality for Kane’s method will be separated (aspects particular to Kane’s method won’t be present in the attributes of the ReferenceFrame class, for example) so that other methods of forming the dynamic equations can be implemented, such as Lagrange’s, Hamilton’s, Gibbs-Appell or traditional Newton-Euler. 
In summary, the class structure specific to dynamics will be untied from the classes specific to kinetics, kinematics, and inertia.  The benefit of this will be design clarity, improved ease of use and improved extensibility.
## Additional Functionality

Interfacing code to other tools allow the equations to be output in a variety of useful formats:  LaTeX, C/C++, Fortran, Matlab/Octave, and SciPy.  This can build on the SymPy efforts of code generation. The equations of motion can used in simulation, linear analysis, and animation tools, many of which are already available in the python scientific computation world. PyDy already has the capability to generate code for numerical integration of the equations of motion using SciPy (scipy.integrate.odeint) and has built in functionality that allows for easy animation of reference frames, points, rigid bodies and particles.
## Users and Contributors

The restructuring of the object model and including the the software as a module into SymPy will open the doors to many more users and contributors. The new object model and functionality will make it easier for people of different backgrounds and methodologies to adopt the software for their kinematic and dynamic computations. Being included in the distribution of SymPy will make  the software available for more users. These alone are not enough to ensure the creation of a successful tool; there are plans to introduce the software directly to scientists and educators at our school and other schools.

UC Davis is unique in offering the capabilities to build a base of users and contributors to SymPy/PyDy. There are many undergraduate courses taught each year from physics 101 to advanced dynamics of potential users of the software. Furthermore, we teach approximately 25 students per year the specifics of Kane’s method and symbolic derivation of multi-body equations of motion. This base of students from the past 30 years are prime users and contributors to the SymPy project.  I will work with professors and departments at UC Davis so that the software can be shown to many of these students. 
## Example

The utility of software like PyDy becomes readily apparent once the system in question has a bit more complex kinematic relationships than a standard Physics 101 problem (although PyDy can handle simple problems just fine, too). For example, the following code shows how PyDy can compute the dot products, cross products, and time derivatives of a body rotated in 3D and SymPy takes care of all the symbolic algebra for us.

>>> from pydy import * 

>>> N = NewtonianReferenceFrame('N') 

>>> (x1,x2,x3), (x1d,x2d,x3d) = N.declare_coords('x', 3) 

>>> A = N.rotate("A", "BODY312", (x1, x2, x3))  # create a new frame "A" by body fixed 3-1-2 (x1, x2, x3) rotations. 

>>> print dot(A[1], N[2])     # Dot product 
cos(x3(t))*sin(x1(t)) + cos(x1(t))*sin(x2(t))*sin(x3(t)) 

>>> print cross(A[1], N[2])   # Cross product 
(-sin(x1(t))*sin(x3(t)) + cos(x1(t))*cos(x3(t))*sin(x2(t)))*a2> + 
cos(x1(t))*cos(x2(t))*a3> 

>>> print dt(A[3], N)         # Time derivative of A[3] in N 
(x1d*sin(x2(t)) + x3d)*a1> + (-x2d*cos(x3(t)) + 
x1d*cos(x2(t))*sin(x3(t)))*a2> 

>>>  print dt(dt(A[3], N), N) # Second time derivative of A[3] in N 
((-x2d*cos(x3(t)) + x1d*cos(x2(t))*sin(x3(t)))*(-x2d*sin(x3(t)) - 
x1d*cos(x2(t))*cos(x3(t))) + x1dd*sin(x2(t)) + x1d*x2d*cos(x2(t)) + 
x3dd)*a1> + ((x1d*sin(x2(t)) + x3d)*(x2d*sin(x3(t)) + 
x1d*cos(x2(t))*cos(x3(t))) - x2dd*cos(x3(t)) + x2d*x3d*sin(x3(t)) + 
x1dd*cos(x2(t))*sin(x3(t)) + x1d*x3d*cos(x2(t))*cos(x3(t)) - 
x1d*x2d*sin(x2(t))*sin(x3(t)))*a2> - (2*x1d*x3d*sin(x2(t)) - 
2*x1d*x2d*cos(x2(t))*cos(x3(t))*sin(x3(t)) + x3d**2 + 
x1d**2*sin(x2(t))**2 + x2d**2*cos(x3(t))**2 + 
x1d**2*cos(x2(t))**2*sin(x3(t))**2)*a3> 
# Long Term Goals

Replace Autolev (currently used multibody dynamics software) for use in generation of equations of motion for all projects in the lab (10/1/2011)
Grow the user base (100 users by 4/1/2012)
Grow the development base (3-5 regular contributors by 4/1/2012)
Make the project self sustaining -- this means it needs to be valuable and organized enough that if current project maintainers were to walk away from it without notice that somebody else would and could pick it up -- this means good documentation, clean code, and thorough testing of functionality.

# Summer Roadmap

PyDy Development Planning. Keeping the Roadmap and Project Description in mind, decide on how the existing code can be reused and integrated into SymPy.  This will include familiarization with SymPy and planning the class structure reorganization, so coding can start right away during the GSoC.  
Class structure reorganization.  Currently objects specific to kinematics, kinetics, and inertia have attributes that are specific to dynamics and/or the method associated with deriving the equations of motion.  A comprehensive class analysis of all objects is needed so that clear separation of functionality can be achieved.  To be specific, PyDy needs to be restructured for the following reasons:
Enable symbolic 3D vector analysis to be performed without needing to specify anything related to dynamics.  This is a very general type of analysis that is commonly encountered in math, physics, and engineering curriculum.  Making this easy to use will certainly bring more users to Sympy.
Clearly defining and separating classes from the three distinct aspects of classical mechanics:  kinetic, inertia, and kinematic aspects.  By cleanly separating these three aspects, they can all be used independently.
Create the Particle and RigidBody classes as container classes for the types of classes relevant to the Newton-Euler equations.
Equations of motion for systems with kinematic constraints (holonomic or nonholonomic) are dealt with very differently by the different dynamic approaches.  These kinematic constraints need to be managed separate from the dynamics, but their inclusion in the kinematics portion of PyDy needs to be done in a generic way that is usable by the different approaches to formulating dynamic equations.  These constraints introduce closed loops in the kinematic tree and these closed loops need to be identified and handled appropriately.  The class design will include appropriate classes or class methods to handle these types of constraints.
Defining an fairly strict API for how to describe a dynamics problem and ensure all examples illustrate follow the same approach.
Improve Functionality:  Once the class structure is reorganized and cleanly defined, adding new functionality will become much easier.  New functionality that is needed in PyDy includes:
Adding quaternions as a way to describe orientation.
Implementing the kinematic differential equations for all 24 of the Euler Angle conventions.
Implementing kinematic differential equations for quaternions.
Intelligently handle kinematic constraints in a way that is user friendly.  Most holonomic constraints are nonlinear, while most nonholonomic constraints are linear in the time derivatives of the coordinates.  Each of these constraints pose unique symbolic implementation challenges.
Implement Kane’s approach for directly deriving linearized equations of motion.  Stability analysis or linear feedback control design is the end goal of many analysts, and in this case directly deriving linear equations is extremely beneficial.
Implement Kane’s approach for deriving steady equations of motion.
Improve code generation capabilities.  If numerical analysis of equations generated by PyDy is desired, there are certain standard forms the equations should be put in (i.e., for integrating ODE’s the equations need to be in first order form with a function that defines the right hand side of dx/dt = f(t,x)).  Clearly define a way to identify which quantities/equations should be “output”, and the format in which they should be output for use with the most common scientific packages (Scipy/Numpy/GSL/OpenOpt/Matlab/Octave/Simulink).
Equation of motion unittests.  Currently, there are no unittests for the equations of motion that are generated by PyDy.  These need to be implemented so that as changes and refinements to algorithms are made, it can be ensured that the correct equations are still being derived.  The first tests of the motion equation derivation will be for simple systems, such as a particle, a pendulum, a double pendulum, and a rolling disc, all of which have well known and published equations of motion.
Integration into Sympy.  Make PyDy a module of sympy/physics/classical and clearly document all functionality.  This step will involve improving PyDy documentation by adding it to the Sympy site and creating a Sphinx site for more detailed PyDy examples.
Building more examples of use. -- ideas include 4-bar linkage, point foot walkers, spacecraft or aircraft models, systems with closed kinematic loops.
Implement LaTeX printing of symbolic vector quantities. It is a common task to perform symbolic manipulation and then output LaTeX code, so PyDy will be extended to output specialized LaTeX printing of 3D vector quantities. 
Submit a paper to Journal of Open Research Computation.  The paper will illustrate how PyDy works and that it correctly performs kinematic and dynamic analysis of many common systems.


### Summer Timeline

Before Summer:  Sympy familiarization and planning of PyDy Class Structure Reorganization and Design.
Week 1 - Week 2: Class Structure Reorganization Implementation
Week 3 - Week 4: Improve Functionality
Week 5: Equation of motion unittests
Week 6: Integration into Sympy
Week 7 - Week 8: Building more examples of use
Week 9 - Week 10: Implement LaTeX printing of symbolic vector quanitites
Week 11 - Week 12:  Polish and submit journal paper and verify documentation and test coverage.