

# Introduction

As everytime with a fork, it's difficult to write "objective" wiki page about it, so for now, we just present opinions of individual people. All of them have write access to this wiki, so that they can change the wiki to reflect their opinions accurately (feel free to modify your opinion at any time - the point is not to show that someone is wrong, but to state our points clearly and maybe arrive at some consensus, also the full history is archived in the svn, so nothing is lost). People are sorted alphabetically.

## Fredrik Johansson

My opinion, like Pearu's, is that it would have been difficult to do the changes directly in sympy as it would break a lot of existing code, and effort would be spent getting that code to run instead of experimenting with the core.

## Kirill Smelkov

Yes, changing fundamental thing breaks a lot of code, but the changes (of course!) shall be targeted to improve the whole thing. Hence the need to bring it to the project. Yes, merging fundamental changes is a pain, but if the merge is kept in mind from the beginning, the pain can be lowered -- changes should be structured into smaller parts, and eventually, some of that smaller parts can be merged without breaking things too much, or at all.
*If* there is a motivation for the merge, everything can be easier, but when no merge is planned -- it is a disaster.

Let's see: what is better -- evolution or revolution?

evolution is changing things incrementally, in small steps and revolution usually breaks a lot of stuff. And this was proved to be bad most of the times.

ok, let's remember the previous "new" core.
What can be said about a merge? was it evolution or revolution?
How much time and effort did it take to restore the project?
Again, my point is that the merge have to be planned from the first minutes of a branch 
and yes, every branch is a fork (sort of micro)
But this works greatly when people intend to merge finally, and try to do their best to cooperate. And on the other way it leads to real forks.


Again, *if* there is a motivation for the merge, people usually try to find a way for their changes to be incorporated in, and they usually assist to port other code to new infrastructure if needed.

From the now-old "new" core we learnt, that a "merge" was just a breakage, and noone from the "new" core developers was intrested to keep thing in shape -- that is to ease and assits in adaptating other !SymPy code.

~~  . . . . . . . . . . . . . . . . . . .                                                                . . . . . . . . . . . . . . . . . . . . . . . . . . . . . ~~

<kirr> It already did -- nothing prevented it to be developed on a branch, and when we switched to [http://www.selenic.com/mercurial/wiki Mercurial] it is much easier to develop on a separate branch, since it is in spirit of distributed development.

<kirr> Spawning a new project *is* release by itself!

<fredrik> i can't say i agree with that

<kirr> You'll find eventually that the amount of changes is *tons* and it is again impossible to "merge" it without breaking things. But at least I and I think Ondrej will object to the breakage. We did it once, and we learnt.

<kirr> separate issue tracker: just tag issues with say sympycore or something like that for easier search/etc...


### Resume

[http://www.selenic.com/mercurial/wiki Mercurial] makes it easy to experiment in a branch.
That is to incrementally develop patches on some topic until they are ready.

Also, it is a good practice to merge ready bits into mainline in the process.

Release-early, release-often can be reformulated here as:

  _MERGE_-_EARLY_, _MERGE_ _OFTEN_


<kirr> The problem is that from the technical side, everything is ok to be in, but from someone's motivation side -- it is not.


== Ondřej Čertík == 

!SymPy uses a development model as described in SympyDevelopment, basically tests must pass and everything should be discussed in Issues, that is very good for a mature project and 
I very stronly believe that is the way to go - team work, open discussion about everything, cooperation. 

There are issues that could be improved though, such as speed, assumptions model, caching issues etc.

Nobody knows what is the best way to resolve these issues,
therefore one must experiment and that may temporarily break lots of
code. Thus such development needs to happen in a separate branch. We started to play with new ideas in the sympy-sandbox branch mainly by Pearu Peterson, but later Pearu decided to create his own project [http://code.google.com/p/sympycore sympycore], which has basically evolved into a fork of !SymPy.

Our plan in !SymPy is to see which ideas are good and which are bad in sympycore, let it settle for a while and then discuss them in Issues and implementing the good ones in !SymPy.  We believe that the way to go is incremental improvements of !SymPy, not a rewrite from scratch - we did that once in August 2006 and it broke a lot of things (some of which aren't working till now, but also some other things started to work), so that's not the way to go.
We also believe that having two incompatible symbolic manipulation libraries in Python is a bad thing. It's sad that sympycore developers don't implement the things directly in !SymPy, so that we need to duplicate their work in many cases, but we will port all good things finally, it will just take longer (in the meantime, some users will prefer to contribute to sympy, some other will choose sympycore).

With our strategy, !SymPy will always work and also it will benefit from new fundamental improvements.

## Pearu Peterson

What Fredrik said above is exactly why it is so difficult to fix
fundamental issues in sympy. Also, I agree with Ondřej that the 
SympyDevelopment model is a very good for a mature project.
From the fact that sympy has fundamental issues follows that
this development model cannot be applied strictly when there are
motivated people who are willing to work on fixing
the fundamental issues.

We all remember the pain of merging the sympy-research branch that
was a rewrite of my symbolic package to meet the interface developed in 
the original sympy. The merge never included all of the features in the branch
nor was all of the original functionality of sympy restored.
This does not sound good and hence the merge is remembered with pain.
However, if I remember correctly, the merge resulted a speedup up to
*150-1500 times* for various operations. I don't think that this kind of speedup
could have been achieved with a normal evolution of sympy. I do think
that the pain of merging was well-grounded and we should not actually
call this as a painful merge but an essential step forward in sympy development,
even when it contradicts a very good development model.

Implementing a CAS from scratch is not an easy task.
In fact, I think this is fundamentally a wrong way of approaching
the problem, i.e. to start with an _implementation_. If there is a
desire to have a CAS for a given programming environment, say Python,
then one should start working out a fundamental model of CAS taking
into account the possibilities and restrictions of the given programming
environment. When the model is worked out only then start implementing it 
as a final step. That would be ideal.

Fortunately, Python is close to being
an ideal programming language for prototype development where one can try
out different ideas and approaches by writing Python code from the beginning.
This is also how I see projects like sympy -- sympy is a prototype project
that aims to provide CAS for Python.
Hopefully in future it will be reliable and fast enough to solve real problems.
Let me repeat: implementing a CAS is not an easy task. Keeping in mind
what's said above, I would claim that too many developers will not
make this task any easier, especially in the early stages of development.

I believe that working out a reasonably good CAS model for Python requires
some vision what the model should include and what methods are suitable for
supporting this model efficiently.
I wrote my first Python program that aimed to perform basic symbolic
manipulations tasks about 9 years ago. After that I have tried to
implement a CAS for Python using very different approaches, starting
from manipulating Python AST trees to achieve some symbolic manipulation
effects, ending with creating Python interfaces to existing CA systems
of other environments such as GiNaC, Maxima using handwritten wrappers
or the Boost toolkit. With this experience in my bag, I dare to say that
I have some vision what the CAS model for Python should include and what
methods are suitable for implementing it in Python. Discussions and all the work
on sympy/sympycore with all of you have been most fruitful in searching
for a "perfect" way to implement a CAS for Python. Hopefully this
research will continue and one day we won't need to worry about changing
the core of sympy but instead work on extending sympy with new concepts and algorithms.


# Reactions

Feel free to add any reactions you want to the above opinions. Feel free to change your opinion above at any time if you think it was not accurate - the point is to arrive at some consensus, or at least explain our motivations.

## Fredrik Johansson

## Kirill Smelkov

## Ondřej Čertík

_ The merge never included all of the features in the branch nor was all of the original functionality of sympy restored. This does not sound good and _

As far as i know, we took the whole core, as you wrote it and simply
ported all modules to it. So all features that you had should now be in
sympy. Which features weren't included?

_ hence the merge is remembered with pain. However, if I remember correctly, the merge resulted a speedup up to 150-1500 times for various operations. I don't think that this kind of speedup could have been achieved with a normal evolution of sympy. I do think that the pain of merging _

I think the main speedup was achieved by using __new__ instead of
__init__ and that should have been done incrementaly, because I spent literally weeks fixing issues with the
new core in sympy and the series still isn't working as it used to be
(it's true that some other problems went away). Some speedup is done
with caching, but as you have shown in sympycore, it is possible to
write fast CAS in python even without caching.

_ was well-grounded and we should not actually call this as a painful merge but an essential step forward in sympy development, even when it contradicts a very good development model. _

I think it was a mistake to do it, in the end it cost me much more
time, than just porting __init__ to _new_ and some other things (there
is also the ordering of the classes - I am not sure if it speeds
things up or down). Also, another very important point is, that people
stopped sending patches to the new core, because it's too complex to
understand. But they used to send patches
to the old core. Maybe it's inevitable for the core to be too complex,
but I still believe it could be done simple and fast.

_ this experience in my bag, I dare to say that I have some vision what the CAS model for Python should include and what methods are suitable for implementing it in Python. Discussions and all the work on _

Well - the new core, now in !SymPy is your (Pearu's) vision. It turned out it still needs more changes. Now you started sympycore, but I really don't see any guarantees that more changes will be needed to it and a new rewrite from scratch will happen? I don't think that's the way. Evolution, as Kirr says, that's the way.

Let me quote part of your email (see sympy mailinglist archives):

_After the merged core is stabilized then we should work hard to keep backward
compatibility as much as possible._

We merged that new core, but you don't seem to agree with this anymore, because sympycore is incompatible with your new core, now in !SymPy.
As to the experience, I am not sure it's that relevant, because I have
a plenty of experience too - I tried to fix your pyginac when you
stopped working on it, then I created swiginac together with Ola, played with ginac a lot
and wrote sympy, also I am quite involved in Sage.calculus. I also
tried and studied all CAS systems in the links on the sympy's webpage.

## Pearu Peterson

I am a bit disappointed that Ondřej feels that the merge was a mistake, I also spent
lots of time on working on it, more than I planned initially but I don't have regrets.
The porting was not complete in the sense that Lambda support was broken after
the merge, for instance.
Since the history of sympy should be available, one can always undo the merge..
But all this should be irrelevant at the moment, we should look to the future.

About the incompatibility between sympy/sympycore: I think this issue can be
easily resolved keeping in mind that they still share the same fundamental ideas:

  * classes are !CamelCase, sympycore has also functions in !CamelCase.
  * expressions are iterable in the same way, that is the fundamental feature that should keep sympy/sympycore extensions compatible or at least easily portable.
  * the module structure is similar, eg sympy is the parent package. In sympycore lots of functionality of sympy.core is moved to sympy.arithmetic package. This refactoring was needed in order to keep sympy.core clean and to be srictly a base package for subpackages like sympy.arithmetic, sympy.logical.symbolic, and sympy.logical.sets.
  * both miss a good assumption model: in !SymPy the assumption model is fragile, in !SympyCore there is no model implemented yet but it provides needed infrastructure for a better assumption model: constructors do not take assumptions and sympycore defines logical concepts.
  * btw, sympycore does not use ordered_classes anymore.. The Basic class in sympycore has been simplified considerably.


# IRC discussion

We were also discussing about our plans on IRC:

```
(04:21:13 PM) ondrej: hi pearu
(04:23:25 PM) ondrej: just got home from mountains
(04:30:01 PM) pearu: hi, nice to meet you here
(04:30:20 PM) ondrej: I didn't get - why cannot you use a direct instance?
(04:30:24 PM) ondrej: (in IS)
(04:31:20 PM) pearu: this is because it is not always possible to import classes from other modules when there is a risk of getting circular imports
(04:31:48 PM) pearu: isinstance(obj, classes.clsname) could be an option
(04:32:19 PM) ondrej: yes, that's what I thought
(04:32:25 PM) pearu: that might be actually optimal
(04:32:52 PM) ondrej: but I think IS will be slower, than is_Add (that is currently in sympycore)
(04:33:18 PM) ondrej: do you have some idea how much it is slower?
(04:33:39 PM) ondrej: (one more function call) I don't have a feeling for these things in python
(04:33:44 PM) pearu: yes, that wil be always be so, I would estimate not more than 6-7times
(04:34:01 PM) ondrej: 7 times? that's a lot
(04:35:01 PM) pearu: calling __getattribute__ (that includes attribute search) plus isinstance call is 8x slower, using IS approach would be faster
(04:35:22 PM) pearu: when IS=isinstance, then it will be 2x slower
(04:35:46 PM) pearu: but I need to test, these estimates can be wrong
(04:36:15 PM) ondrej: 8x slower than using is_Add ?
(04:36:49 PM) ondrej: so the isinstance is actually pretty fast, only is_Add is faster, right?
(04:37:05 PM) pearu: yes, but note that this estimate is about only checking types
(04:37:33 PM) pearu: however, in real apps time spent in checking types can be insignificant
(04:37:48 PM) ondrej: then my proposed docstring is bad - the IS will always be slower, than isinstance
(04:38:08 PM) ondrej: so what is the point of IS than? If it's slower than both isinstance and is_Add
(04:38:13 PM) pearu: nope, when IS=isinstance, they have the same speed
(04:38:22 PM) ondrej: oh I see.
(04:38:28 PM) ondrej: ok, then everything is ok
(04:38:59 PM) ondrej: let's use IS then, so that we can switch it easily anytime we want
(04:39:06 PM) pearu: but this is again at the cost of accessing classes attributes, using is_Add is always the fastest
(04:40:03 PM) ondrej: I think the only way to decide this is to test it in sympycore, how much it slows things down
(04:40:18 PM) ondrej: if it's negligible, we don't have to talk about it
(04:40:19 PM) pearu: yes, I agree, I'll certainly do that
(04:40:43 PM) ondrej: (but if it's negligible, the whole thing with is_Add was not necessary imho, we could use isinstance)
(04:41:30 PM) ondrej: what do you think are the biggest speedups in sympycore? Definitely the fast Add and Mul, and then comparisons imho
(04:41:31 PM) pearu: the isinstance(obj, classes.Add) has only one problem: it reads long
(04:41:40 PM) ondrej: agree
(04:43:01 PM) pearu: but in long term (when the code base will be stable) I think isinstance is also fine, in fact, while working with the functions, isinstance is safest at the moment
(04:43:30 PM) ondrej: yep, I like the idea of having is_Add just for a few classes
(04:45:11 PM) pearu: when talking about speedups, then comparions play a big role as it is used all the time (dictionary lookups, equality checks) and pretty much everywhere
(04:45:48 PM) ondrej: I think so too
(04:46:24 PM) pearu: in sympycore we had to sacrifice __lt__, etc methods for fast comparison so that they cannot be used to generate relational instances, Less, etc must be used directly
(04:46:55 PM) ondrej: is __lt__ some particularly fast?
(04:47:12 PM) ondrej: or why you couldn't use Less for comparisons
(04:47:40 PM) ondrej: (so that you could use list sort, or something?)
(04:48:07 PM) pearu: no, but as soon as a class defines __lt__ method, it will be used by Python for comparisons, the __cmp__ method will be just ignored
(04:48:54 PM) ondrej: but why do you need to compare using < ?
(04:49:11 PM) pearu: for sorting, for instance
(04:51:18 PM) ondrej: yeah.
(04:51:31 PM) pearu: but on the other hand, sorting is used only in generating str values, so it is not a big problem
(04:51:52 PM) pearu: may be it was when Add used to use sorting..
(04:52:20 PM) ondrej: so when you type x+y and y+x, is it stored internally differently?
(04:52:50 PM) pearu: they are stored internally as dictionaries {x:1, y:1}, so, they are the same
(04:52:58 PM) ondrej: ah, I forgot
(04:53:19 PM) ondrej: but then the x and y need to have hashes working
(04:53:52 PM) pearu: yes, hashing is another thing that affects performance noticable
(04:54:07 PM) ondrej: the oldcore used to use hashes.
(04:54:58 PM) ondrej: so comparisons is in fact done using hashes, right?
(04:55:47 PM) pearu: I believe that using builtin hash methods is faster, like Symbol uses str.__hash__, Add uses frozenset.__hash__, etc
(04:56:20 PM) ondrej: yes, the builtin hash is faster
(04:56:31 PM) ondrej: how do you calculate hash of (x+y)**2?
(04:56:49 PM) ondrej: I used to have issues with this.
(04:56:55 PM) pearu: hashes are not guaranteed to be unique enough
(04:57:02 PM) ondrej: ok then.
(04:57:13 PM) ondrej: but it fails then sometimes, doesn't it?
(04:57:49 PM) ondrej: (the builtin hash is unique enough for our purposes imho)
(04:58:07 PM) pearu: what do you mean? hashing is needed for fast dictionary lookups, finially strict comparison is needed anyway
(04:58:32 PM) ondrej: I thought you just compare the dictionaries
(04:58:46 PM) ondrej: like {..} == {..}
(04:59:01 PM) pearu: yes
(04:59:05 PM) ondrej: yeah, and the __cmp__ method gets executed
(04:59:08 PM) ondrej: and there you compare directly
(04:59:12 PM) ondrej: ok, that makes sense
(04:59:19 PM) ondrej: we used to compare the hashes in the oldcore
(05:00:14 PM) pearu: the basic property of a hash values is that the equal objects share the hash value but the reverse may not be true
(05:00:31 PM) ondrej: of course. that's ok for lookups
(05:01:07 PM) ondrej: it sucks, that sympy is so buggy now. when I tried to port Mul and Add, it completely broke down. I need to disentangle the assumptions, but leave it in there in some nice (maybe slow) form, because sympy uses them quite a lot as I discovered
(05:01:31 PM) pearu: yes, I know
(05:02:08 PM) ondrej: also there is the caching problem. it's related, so it needs to be fixed at once.
(05:02:27 PM) pearu: when I tried to fix sympy core issues I got also frustrated because of so many dependencies that need to be taken care when changing core a bit
(05:03:05 PM) ondrej: yeah, but you think that sympycore will be different, when you port all the modules?
(05:03:10 PM) pearu: in sympycore we decided not to use caching until things will be stable and covered with good unittests
(05:03:45 PM) pearu: probably not, but I don;t have plans to port the modules
(05:04:21 PM) ondrej: so what are your plans?
(05:05:24 PM) ondrej: in sympy it was your decision to use caching from the beginning - but I too didn't see the danger. but I think when I fix the assumptions, it should be possible to turn caching on and off easily.
(05:05:40 PM) pearu: may fundametnal plan is to have a stable core module with all necessary features needed for extensions
(05:05:51 PM) ondrej: right
(05:06:09 PM) ondrej: but without the extensions, it is not easy to see that it has all the necessary featurures
(05:06:27 PM) pearu: caching is not bad, just finding bugs from other parts will be difficult when caching is turned on
(05:06:52 PM) ondrej: with the newcore in sympy, I thought it has all the featurees, and you too imho. But it didn't, it was just hard to see it
(05:07:41 PM) pearu: well, I think with current sympy/sympycore we know moreorless what features will be important
(05:07:59 PM) ondrej: yeah, that's true
(05:09:16 PM) ondrej: sympy is getting more integrated in SAGE. my plan is to be able to easily switch maxima and sympy in SAGE. this will discover a hell lot of new bugs
(05:10:05 PM) ondrej: if we could make sympy let's say just 2 or 4 times slower than maxima, it'd be fine
(05:10:27 PM) pearu: I think that we cannot be sure that core covers all the important features until we have done all the implementations, for example, the problem of assumptions seemed to have an easy solution using is_.. attributes but as soon as more complicated assumptions will be needed, the used assumption model breaks down
(05:10:54 PM) ondrej: and more complicated assumptions will be needed
(05:11:11 PM) pearu: yes, I totally agree
(05:11:21 PM) ondrej: another thing - you seem to depend on python2.5 only - I think a lot of people still use python2.4
(05:11:56 PM) ondrej: I think just imports are better in python2.5 and "with"
(05:12:55 PM) pearu: yes, I think relative imports are important to ensure that the right modules are loaded
(05:12:58 PM) ondrej: the imports are not an issue. And the "with" - that could be used for assumptions, but imho the core and sympy could be made in python2.4 (users can use 2.5 and "with" in their own code)
(05:13:30 PM) ondrej: (I think the imports can be done robust in 2.4 too)
(05:14:53 PM) pearu: My thinking is that when sympycore will be stable, then it can be ported back to 2.4 when it will be an issue for many users, may be by this time everybody uses 2.5 anyway
(05:15:31 PM) pearu: also, I think that some of the new features in Python actually simplify writing sympy-kind of package
(05:15:45 PM) ondrej: yeah, that's true
(05:16:11 PM) ondrej: btw, are you taking part in the scipy sprint right now?
(05:16:21 PM) pearu: decorators and metaclasses have simplified many things, especially in function/operator support
(05:16:36 PM) ondrej: those are in 2.4 too, aren't they?
(05:16:39 PM) pearu: no, I cannot travel with my leg
(05:16:48 PM) ondrej: I mean over IRC
(05:17:25 PM) pearu: I am always logged in in sympy IRC, so, over IRC I'll be available
(05:20:18 PM) ondrej: yes. but I was talking about scipy sprint
(05:20:21 PM) ondrej: :)
(05:22:03 PM) pearu: ahh, ok :)
(05:22:52 PM) pearu: you know, I am new to IRC and my first attempts to log in scipy IRC failed
(05:23:14 PM) ondrej: I see.
(05:23:21 PM) ondrej: btw, did you read Suresh email on sympy list?
(05:23:32 PM) pearu: I am surpriced that even got sympy IRC working, still don't know if I have it correctly setup
(05:24:08 PM) pearu: yes
(05:24:20 PM) ondrej: I think we need to keep it simple, so that people can join in
(05:24:30 PM) pearu: agree
(05:24:55 PM) ondrej: that I don't understand it, that doesn't mean anything, I am not a genius. But other people should understand it.
(05:25:15 PM) pearu: but I think we are still searching a simple way to implement sympy
(05:25:25 PM) pearu: I think nobody wants to write a complex code
(05:25:33 PM) ondrej: yep
(05:25:39 PM) pearu: when starting, everything is simple antil the code crows
(05:25:47 PM) ondrej: the oldcore was definitely simpler. but slow.
(05:26:38 PM) pearu: I'd say there will be always payoffs, but sympycore is also simpler than sympy
(05:27:00 PM) pearu: I am currently working on implifying function support in sympycore
(05:28:19 PM) ondrej: that's why I think we should have just port nice things iterativelyk, instead of moving to the new core, because now it's very difficult to simplify it
(05:29:05 PM) pearu: iterative simplication is one approach, another very efficient simplification approach is refactoring
(05:29:57 PM) ondrej: yeah. ok, I'll try to do some work tonight.
(05:30:05 PM) pearu: in sympy many modules depend on each others internals, in sympycore I have tried to refactor different functionalities to separate modules
(05:31:00 PM) pearu: I have also found that documenting internals helps to simplify the code as then one sees what is important and what code is actually needed
(05:32:27 PM) ondrej: yeah. but it's still a lot of work to port it again to sympy
(05:34:49 PM) pearu: I don't see other ways, as you see yourself when trying to improve sympy with respect to assumptions and Add/Mul stuff, the task is not easy even within the same package
(05:35:59 PM) pearu: in sympycore I initially though that creating a new sympy.core package will be enough but now it is basically three packages: sympy.core, sympy.arithmetic, sympy.logic
(05:36:39 PM) pearu: the hope was that sympy could just grab sympycore sympy.core package and be done with upgrading
(05:37:00 PM) ondrej: I know.
(05:37:27 PM) pearu: but this can only work when both packages are properly refactored and core packages are stable in their interface
(05:38:01 PM) ondrej: Agree.
(05:38:37 PM) ondrej: but my strategy is to attract people to help us. it's just too much work for one or two people
(05:38:49 PM) ondrej: so it needs to do the job now.
(05:39:14 PM) fredrik3 [i=fredrik@gamma.kvi.sgsnet.se] entered the room.
(05:39:31 PM) pearu: I think for core part, few people that too many is better, in extending the sympy, more people are better
(05:39:43 PM) fredrik3 is now known as fredrik
(05:39:49 PM) pearu: that: read than
(05:40:50 PM) pearu: hi fredrik, do you want to see the whole discussion? I can copypaste it to email
(05:41:23 PM) fredrik: no, but thanks
(05:41:34 PM) pearu: ok
(05:42:37 PM) ondrej: let's put the discussion into the wiki?
(05:42:38 PM) fredrik: my 2c is just that IS is never going to be faster than isinstance in the best case, and therefore i don't see a benefit with it
```

See also a blogspot explaining the relation between sympycore and sympy and Sage:

http://ondrejcertik.blogspot.com/2008/01/sympysympycore-pure-python-up-to-5x.html