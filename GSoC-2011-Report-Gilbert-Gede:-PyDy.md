#About Me#
My name is Gilbert Gede; at the start of GSoC 2011, I had just finished my second year as a PhD student at the University of California, Davis in the Mechanical and Aerospace Engineering department. I work in the Sports Biomechanics Lab at UCD, where we analyze dynamic systems.

#Introduction#
The goal of this project was to create a submodule which would assist in generating symbolic equations of motion for complex multibody systems, using Kane's Method [Kane, Thomas R., and David A. Levinson. Dynamics, Theory and Applications. New York: McGraw-Hill, 1985. Print.]. This would be accomplished by creating of a 3-space vector class with the ability to perform multi-reference frame calculus. With the creation of some auxiliary classes, the previously defined vector operations could be used to generate the equations of motion.

#GSoC Project#
A significant portion of the project was creation of classes to assist in the computation of equations of motion; documentation and instruction on how to use these classes was another important part of the project. Also, the project was originally called PyDy, but now is referred to as physics/mechanics (which is where it is located).

There is more functionality than what is described below. Here I intend to give an overview of some of the work done, rather than a complete description of everything. More information will be located in the sphinx-documentation once my code is merged; additionally there is information in the blog I wrote in during the summer: http://gilbertgede.wordpress.com/tag/gsoc-2011/

##Vector/ReferenceFrame##
One of the core elements of this submodule was the `Vector`/`ReferenceFrame` pair of classes. This is only designed to work in 3-space, and was constructed as such. Each ReferenceFrame has a set of 3 basis vectors which are orthonormal. Every Vector is a combination of measure numbers and basis vectors from different reference frames. A number of methods and operations were written to re-express vectors in different reference frames, take derivatives in different reference frames, or do algebraic operations including various vector products.

`ReferenceFrame` stores a variety of information to allow for these operations, such as direction cosine matrices relating pairs of `ReferenceFrame`'s and the angular velocity between these two frames (which is in fact a `Vector`).

Reading the documentation page for physics/mechanics/vectors will give more information into how `Vector` is implemented. One important piece of information is that no SymPy classes were extended in the creation of `ReferenceFrame` and `Vector`. This meant not all of the functionality in SymPy's Basic was inherited, but was necessary in order to allow for proper vector algebra to be possibly implemented.

##Additional Classes##
Additional classes were created to facilitate with creation of equations of motion, such as `Dyad` to represent the rotational inertia of bodies, and `Point` to keep track of the position, velocities, and accelerations of points in different `ReferenceFrame`'s. Container classes were also constructed, `RigidBody` and `Particle`, to represent a rigid body and a particle. Finally, a class `Kane` was created, used for actually forming the equations of motion; it takes in the relevant information (forces and bodies) and generates equations.

Custom printers also had to be created in order to print out certain quantities correctly. Time-varying quantities such as coordinates and velocities are represented by SymPy functions of time(`symbols('t')`). Rather than printing out the complete expression in every case, the `(t)` was dropped. In addition, instead of printing the derivatives of these values as `Derivative(q(t), t)`, they are printed as `q'`. This also had to be extended to pretty printing, and latex representations.

##Documentation##
Due to the somewhat nuanced nature of using Kane's Method to formulate equations of motion for multibody systems, creating documentation which would allow users to understand how to use this code was important. Documentation was written covering basic vector operations and calculus, kinematics, masses & inertias, and Kane's Method. Examples were also provided, as well as some plans for future development, and some advanced functionality described.

#Status at Time of Writing#
Currently, the code has been written and has an open pull request. Not everything originally put forth in the application has been completed; a function for generating code output for numerical has not been written, nor has the proposed journal paper.

As for functionality of the code, it seems that I have been successful. A system we have been studying in our lab is the bicycle (assuming a rigidly attached rider and no slip between the wheels and grounds). The code in physics/mechanics has successfully created non-linear equations of motion, linearized them, substituted numerical values, and evaluated the eigenvalues. These calculated eigenvalues matched reference values to machine precision.

#Future Work & Recommendations#
Future work that needs to happen is completion of the pull request. After that, generating a function for code output for numerical integration needs to be done. Writing a journal paper is of lower priority, but still an objective. Other work for the future is described in the documentation under future development.

For future Summer of Code students, I have a few recommendations.

**1:** Plan multiple milestones, each of which could constitute a pull request. I did not do this. I chose a point midway through the summer and opened a pull request. While the pull request was open, I continued development, which included changing some very significant behavior of the code in the pull request but left other features in an incomplete state. Eventually the pull request was updated when those features were completed, but that was at the end of the summer and the pull request open is now ~12k lines (although some of that includes pictures).

**2:** To avoid changing behavior partway through development, plan the interfaces beforehand. This gets said often, but can be hard to do. One of the issues I faced was having an idea of of how I wanted things to behave, testing if it was implementable with a crude interface, and when finding it was implementable, going ahead with said crude interface. Things would have worked out better if upon finding out my plans were implementable, I worked right away to determine an appropriate interface and use that.

**3:** Make commits intelligently. Use 'git log' to see what other people have done regarding how much detail they went into in a message, etc. Don't use 'git commit -m <stuff about your commit>'. If you follow recommendation 1, hopefully you'll have less commits in your first pull request, making it easier to correct them and learn from those changes.