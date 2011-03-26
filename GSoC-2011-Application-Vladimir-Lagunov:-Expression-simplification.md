.

# About me
## Contacts
Vladimir Lagunov, 21 years, living in Russia, Novosibirsk.

Studying in magistracy of Novosibirsk state technical university, Faculty of Automatics and Computer Engineering.

How to contact me:

* email and xmpp: lagunov.vladimir _at_ gmail.com

* xmpp: werehuman _at_ jabber.ru

## Coding skills
I prefer Python for my programs: i’m familiar with python much more than with other languages. But also i can write on C++, and i’m somewhat familiar with C, Java, JavaScript, PHP, Haskell.
I worked with Django and Twisted.Web.

I have no large list of big projects. My first average (more that 200 lines) program on Python was a xmpp-chat bot for quiz game, i wrote it 3 years ago. In this three years i slightly earned by improving one site based on Django and wrote a lot of small but useful scripts for myself. Or useless but funny pieces of code like http://pastebin.com/ngRaMCVQ , that i used in internet “holywars”. Now i’m writing web-interface for my master’s thesis on twisted.web.

My experience doesn’t limited by Python only. My bachelor’s work was an DirectConnect client, written in Java and Swing (but this client doesn’t works as i wanted). Also i have some experience with C++ and Qt (concretely with QtGui and QtNetwork), and of course i can work with PyQt4/PySide.

# My tasks
## Why i want to improve SymPy?
When i was looking on GSoC projects list, my choice fell on SymPy because:

* It is a Python. I like Python.

* My masters work is very strongly associated with symbolic computations.

Alas, i am not a good mathematician, but i think i am good python programmer. Also i am not good mathematician not because i am stupid man, but because earlier i didn't show interest to math. But everything changes.

## What to improve?
I have learned about SymPy just a week ago, but in few days of usage i have found some defects in simplification module. You don't need a lot of time to find that - just look to unittests. Other example: current trigonomethrical simplification can reduce `sin(x)**2 + cos(x)**2` to `1`, but can't reduce `2*sin(x)*cos(x)` into `sin(2*x)`.

Expression simplification is an inalienable part of whole SymPy, all other components of framework are using these functional. Improving of expression simplification will affect on all parts of SymPy.

Probably when i'll start improving simplification, i'll need to work around rewriting. For example, now sympy throws attribute error when you try `sinh(x).rewrite(sinh, exp)` (but these transformation exists ![sinh to exp](http://upload.wikimedia.org/math/6/e/f/6ef2fb6c375403a85f31ddb1e73fee2e.png))

And of course i think that expression simplification doesn't needs big math knowledges like ODE, but much more interesting than porting to python3, so i can cope this problem.

## Shedule

TODO: i need to read more SymPy code than i've read before drafting schedule.