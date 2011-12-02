

# Why Mercurial?

Mercurial is much better than Subversion. With svn, one has to implement a new feature locally, then test it and then commit, but the quality of such a commit is much lower than with Mercurial (hg), that is distributed, which means everyone can commit locally and thus won't be afraid of losing his changes. One commits several times locally, looks at the changes, tests them, reverts them etc., until one is satisfied with the result. Only then "commits the svn way" (which is called pushing in Mercurial). 

Another advantage is that all Mercurial repositories are equal and thus have all history and one can work offline as long as one wishes. 

I (Ondrej) am quite hesitant to try new things when the old ones work and work well (Subversion works very well), but Mercurial is really superior to Subversion. It's like a working [http://en.wikipedia.org/wiki/%C5%A0koda_105/120/125 Škoda 120] and working [http://en.wikipedia.org/wiki/BMW_E91 BMW].

Read hgbook:

http://hgbook.red-bean.com/

and watch this video from the author of Mercurial:

http://video.google.com/videoplay?docid=-7724296011317502612

# Details

Web:

http://hg.sympy.org/sympy/

Mercurial:
```
$ hg clone http://hg.sympy.org/sympy/
```

## usage

The same as with Subversion:
```
$ cd sympy
$ hg up
0 files updated, 0 files merged, 0 files removed, 0 files unresolved
$ echo "sympy is awesome" >> README
$ hg st
M README
$ hg di
diff -r 70c13b5a9986 README
--- a/README    Fri Oct 19 06:33:11 2007 +0000
+++ b/README    Sat Oct 20 13:40:29 2007 +0200
@@ -110,3 +110,4 @@ joined the development during the summer
 joined the development during the summer 2007 and he has made SymPy much more
 competitive by rewriting the core from scratch, that has made it from 10x to
 100x faster. 
+sympy is awesome
$ hg ci -m "README was incredibly improved"
$ hg log -r tip
changeset:   1535:173e12b16e48
tag:         tip
user:        Ondrej Certik <ondrej@certik.cz>
date:        Sat Oct 20 13:40:49 2007 +0200
summary:     README was incredibly improved

$
```

The difference is that all of this happens locally and thus you can work offline (in the underground, in the plane, airport, bus, forrest, anywhere).

--- Most of the following is now *obsoleted* by [http://docs.sympy.org/sympy-patches-tutorial.html SymPy Patches Tutorial] ---

-------

## how to commit the svn way

It's called pushing.
```
$ hg out
comparing with http://hg.sympy.org/sympy/
searching for changes
changeset:   1535:173e12b16e48
tag:         tip
user:        Ondrej Certik <ondrej@certik.cz>
date:        Sat Oct 20 13:40:49 2007 +0200
summary:     README was incredibly improved

$ hg push
pushing to http://hg.sympy.org/sympy/
searching for changes
ssl required
```
Accessing the repository over http is read only. Create for example a bundle:
```
$ hg bundle /tmp/mysuper.patch
```
and send it to Issues, or the mailinglist. We'll review it and either apply or help you improve it. You can also use the `hg email` when you configure it (see `hg help email`).

Some long time active !SymPy developers have a write access using ssh, change "http://" to "ssh://hg@" like this:
```
$ hg out ssh://hg@hg.sympy.org/sympy/
comparing with ssh://hg@hg.sympy.org/sympy/
searching for changes
changeset:   1535:173e12b16e48
tag:         tip
user:        Ondrej Certik <ondrej@certik.cz>
date:        Sat Oct 20 13:40:49 2007 +0200
summary:     README was incredibly improved

$ hg push ssh://hg@hg.sympy.org/sympy/
pushing to ssh://hg@hg.sympy.org/sympy/
searching for changes
remote: adding changesets
remote: adding manifests
remote: adding file changes
remote: added 1 changesets with 1 changes to 1 files
```
You can make this default by changing the `.hg/hgrc` from:
```
[paths]
default = http://hg.sympy.org/sympy/
```
to:
```
[paths]
default = ssh://hg@hg.sympy.org/sympy/
```

## Useful info

 * [http://hgbook.red-bean.com/hgbookch12.html Mercurial Queues] extension can be of great  help while working on your patches.
 * when using ssh:// transport, it is convenient to use ssh-agent.
 * "ssh -A" can be helpful if you want to reach the repository from a not-so-trusted host.
 * [http://wiki.pylonshq.com/display/pylonscookbook/Mercurial+for+Subversion+Users  Mercurial for Subversion Users] Howto.
 * See also HgWorkflow.