


# March - Proposal and Application Process

I decided to apply for the Summer of Code only right at the beginning of the application period, after seeing a story on Digg. If I were to do it again, I would have started at least a month earlier. Once I had made the determination to do it, the first step was to go through the mentoring organization list several times, narrowing it down to just a few projects that seemed most interesting.

In the past year, I had fallen in love with Python after many years of programming almost exclusively in C++, so that was a fundamental heuristic for my search. [http://code.google.com/p/sympy SymPy] caught my eye because I had discovered and tried it a few weeks prior, and I saw great potential in a CAS organized as a library rather than an environment. I have also done a lot of work with 3D graphics, so I was hoping to find something which could use that knowledge as well.

I looked at the code base and came up with a few ideas. Since I was taking Calculus III, and have little knowledge of higher-math, I wanted to do something that wasn't too math-intensive but would still be useful. I wanted to be able to visualize and interact with some of the things I was currently studying, such as the gradient and surface normals. I also wanted to have a free graphing calculator which could be extended to do symbolic computations rather than the approximations that my TI-89 does. Seeing that [http://code.google.com/p/sympy SymPy] had no plotting interface, I thought it would make a fun project which would meet my objectives.

So at this point I e-mailed Ondrej about this and a few other ideas. We got along really well, and I now see that this relationship was crucial to being accepted into the program. You can find my proposal [http://docs.google.com/Doc?id=ajjnc8fmpmkr_27gcckgt here]. I made sure to set out:

   1. The deliverable functionality I wanted to provide.
   1. Who would benefit from my project.
   1. How I would accomplish my project.
   1. A scheduling forecast for the key components.

With Ondrej's help, I submitted my application to as many organizations as possible, since [http://code.google.com/p/sympy SymPy] was not itself a mentoring organization, but could be funded under several of them. 

# April and May - Acceptance and Preparation

My application was ultimately accepted under the Python Software Foundation, and Ondrej became my project mentor. During the next few weeks, I made sure to stay in contact with him, and also began to explore possibilities. I also started my first [http://straightupcoding.blogspot.com/2007/04/google-summer-of-code-2007-with-sympy.html blog]. One of the conditions of my acceptance was that I would leverage matplotlib for my initial implementation. Starting with some interface code Fabian had written, I had this done by the [http://straightupcoding.blogspot.com/2007/05/new-direction-for-sympy-graphing.html second week of May], but it was clear that if I wanted to allow [http://code.google.com/p/sympy SymPy] to be used as a symbolic graphing calculator, I would need to roll [http://straightupcoding.blogspot.com/2007/06/vision-for-extensible-visualization.html my own plotting interface].

[http://www.bgjorgensen.com/images/gsoc/mplot3d-wave.jpg]

# June - Plotting Implementation with GLUT

[http://straightupcoding.blogspot.com/2007/06/sympy-plot-now-available-in-svn.html My first plotting implementation] from scratch used PyOpenGL and GLUT, which is a library for easily creating OpenGL applications. This was a quick success, and I was able to produce pretty pictures, but I was unhappy with the console interaction; GLUT is a single-threaded event-driven library, which was not commensurable with my goal of allowing the plot to be interacted with programmatically through an interactive shell or a script while being displayed in a separate window.

[http://bgjorgensen.com/images/gsoc/first-sympy-plot.png]

# July - I Discover Pyglet and Create Fatal Crash-bugs

I explored a variety of solutions and alternatives, and this was really a low-point for the project. At one point I was afraid that there wasn't any Python library which had capabilities like I wanted. Using a [http://straightupcoding.blogspot.com/2007/07/pyopengl-is-dead-to-me-where-are-all-3d.html provocatively-titled blog post], I was able to solicit suggestions I hadn't already heard of, and this led me to discover Pyglet. Pyglet didn't have multi-threaded windowing built-in, but I could see that it was at least a possibility.

I wrestled with Pyglet for about a week, and emerged with exactly what I wanted. I then spent the remainder of July implementing the interface and plotting modes I had planned. Also around this time, a large body of bugs began to accumulate. Luckily, members of the project would notice them quickly when I did not, and were very good in letting me know via our Google code bug tracking system. One particularly devious bug had me very nervous when it started crashing Ondrej's xserver consistently, but fortunately (for me at least), it turned out to be a bug in the Debian Xlib package.

[http://bgjorgensen.com/images/gsoc/ding-dong-surface-thumb.png]

# August - Features and Speed Optimizations

The first three weeks of August went by way too quickly. In this time, I added some new features such as labeled axes, translation, and perhaps most importantly custom color maps. However, it was really slow. After some optimization missteps (focusing too much on Big O complexity and not enough on the coefficients), I finally discovered that the true source of my hinderance was in using the arbitrarily precise calculation mechanisms of [http://code.google.com/p/sympy SymPy] when I could get away with much less precision for on-screen rendering.

After implementing a function which converts [http://code.google.com/p/sympy SymPy] expressions into equivalent Python lambda functions which use Python's math library, I saw an order-of-magnitude speed boost. So the lesson of this month was that top-level Big O complexity is not always the culprit for slow performance.

[http://bgjorgensen.com/images/gsoc/colors-tutorial-3.png]

# What I Haven't Gotten Around To (Yet)

I've really enjoyed working with the [http://code.google.com/p/sympy SymPy] project, and plan to continue my involvement with it. Due to some of the UI progress hiccups in July, I didn't get around to my secondary project goal, which was to develop what I have termed "Cool Calculus III Visualizations", which was intended to be a few simple examples which plotted functions as well as interesting properties, such as gradient vectors and symbolically calculated extrema.

In my application, I said that I would use remaining time in August to accomplish this, and it is now the eve of the last day of SoC. It is somewhat of a consolation that the [http://code.google.com/p/sympy SymPy] project was more interested in the actual plotting module and probably not very interested in these demos, but this was one of my personal ambitions and I am disappointed to have missed it. I do hope to pursue it, however. A few weeks ago there was a suggestion along these lines for the visualization of matrix transformations. Since I'm going to be taking linear algebra starting tomorrow morning, this is something I want to follow up on.

I also hope that in the coming weeks I can integrate Jason Gedge's geometry module (also a SoC 2007 project) with plotting. This shouldn't be too hard, which is part of the reason I've put it at lower priority.

*Update:* a few hours after I wrote this, I managed to create a simple visualization of the gradient. This is encouraging, because it shows that the capabilities I wanted are in the framework.

[http://bgjorgensen.com/images/gsoc/sympy-plot-gradient.png]

# Conclusions

I have thoroughly enjoyed this project. I have learned a lot about writing Python code, but even more about working on a medium-sized open-source project. I benefited from eager testing by members of the project, who were quick to find bugs and possible improvements. My only regret is that I wasn't more involved in the social aspect of the project. I think that this is mostly because my work focused on graphics and user interface, and was therefore fairly far-removed from the algorithmic and mathematical work being done in most other parts of the project. Even so, I had a great time, and look forward to working for the [http://code.google.com/p/sympy SymPy] project in the future.

Thanks again to Google (especially Leslie H.), the PSF, and Ondrej.