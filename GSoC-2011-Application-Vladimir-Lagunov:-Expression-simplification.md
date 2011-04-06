# GSoC 2011 Application Vladimir Lagunov: Expression simplification

# About me
## Contacts
Vladimir Lagunov, 21 years, living in Russia, Novosibirsk.

Studying in magistracy of Novosibirsk state technical university, Faculty of Automatics and Computer Engineering.

How to contact me:

* email and xmpp: lagunov.vladimir _at_ gmail.com

* xmpp: werehuman _at_ jabber.ru

## Coding skills
I prefer Python for my programs: i’m familiar with python much more than with other languages. Also i can write on C++, and i’m somewhat familiar with C, Java, JavaScript, PHP, Haskell.
I worked with Django and Twisted.Web.

I have no large list of big projects. My first intermediate (more that 200 lines) program on Python was a xmpp-chat bot for quiz game, i wrote it 3 years ago. During last years i slightly earned by improving one site based on Django and wrote a lot of small but useful scripts for myself. Or useless but funny pieces of code like http://pastebin.com/ngRaMCVQ , that i used in internet “holywars”. Now i’m writing web-interface for my master’s thesis on twisted.web.

My experience doesn’t limited by Python only. My bachelor’s work was a DirectConnect client, written in Java and Swing (but this client doesn’t works as i wanted). Also i have some experience in C++ and Qt (concretely with QtGui and QtNetwork), and of course i can work with PyQt4/PySide.

# My tasks
## Why i want to improve SymPy?
When i was looking on GSoC projects list, my choice fell on SymPy because:

* It is a Python. I like Python.

* My masters work is very strongly associated with symbolic computations.

Alas, i am not a good mathematician, but i think i am good python programmer. I'm not good in math because earlier i didn't show interest in it, but everything have changed.

And of course i think that expression simplification doesn't need big math knowledges like ODE, but much more interesting than porting to python3, so i can cope this problem.

## What to improve?
I have learned about SymPy just a week ago, but in few days of usage i have found some defects in simplification module. You don't need a lot of time to find that - just look to unittests of `ratsimp()`. Other example: current trigonomethrical simplification can reduce `sin(x)**2 + cos(x)**2` to `1`, but can't reduce `2*sin(x)*cos(x)` to `sin(2*x)`.

Expression simplification is an inalienable part of whole SymPy, all other components of framework are using these functional. Improving of expression simplification will affect on all parts of SymPy.

Probably when i'll start improving simplification, i'll need to work on rewriting. For example, now sympy throws attribute error when you try `sinh(x).rewrite(sinh, exp)` (but these transformation exists \(sinh(x) = \frac 1 2 \left( e^x + e^{-x} \right) \))

## Shedule

TODO: This shedule is fuzzy, review it later.

1. Extend rewrite patterns of functions in one week
2. Improve trigsimp() in three weeks
    1. Simplifying one function with one argument to other function with other argument (for example \(sin(2x) = 2 sin(x) cos(x) \))
    2. Expanding amount of conversion procedures
    2. Smart substitutions, that reduces expression size and doesn't enlarge it.
    3. Tests
2. Write function expandtrig(), that makes arguments of trigonometrical functions in specified expression as simple as possible (for example expanding \(sin(2x)\)). Two weeks.
3. Improve ratsimp() in two weeks. Earlier this step was the first in my shedule, but it can overlap with polys12 branch, so it better to work on ratsimp() after merging polys12 with master.
    1. Proper fraction reducing
    2. Grouping symbols in expression for getting shorter result
    2. More tests
4. Improve simplify() in three weeks
    1. Implement checking which sub-simplify functions are giving good results
    2. Using rewrite patterns internally in simplify()
    3. Tests
5. Improve other simplifiers if need be.