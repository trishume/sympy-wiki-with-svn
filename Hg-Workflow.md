

--- Most of this page is now *obsoleted* by [http://docs.sympy.org/sympy-patches-tutorial.html SymPy Patches Tutorial] ---

-------

This serves as a quick cookbook. For detailed tutorial about Hg and !SymPy, see the [http://code.google.com/p/sympy/wiki/Mercurial Mercurial] wiki.


# Download Hg

```
$ hg clone http://hg.sympy.org/sympy/
```

# Hack

Implement new features, tests, bugfixes. Commit
```
hg ci
```
as many times as you want.

Make sure your `~/.hgrc` contains your username and email, that goes into the patch:
```
[ui]
username = Ondrej Certik <ondrej@somewhere.com>
```

# Publish your patches

What has changed?
```
hg out
```
Create one (or a few) nice patches from all your commits (i.e. join some commits together to form logical chunks to be easier to review && apply):
```
hg qimport -r tip
hg qimport -r qparent
hg qimport -r qparent
...
hg qpop
hg qpop
...
hg qfold 1516
hg qfold 1517
...
```
edit the log message
```
hg qrefresh -e
```
Send it to list:
```
hg email -o
```

# Other

Because empty files cannot be represented in standard patches, you need to use this
```
[diff]
git = true
```
in your `~/.hgrc` to enable "git patches".

## how to convert from MQ to regular changesets

```
hg qdelete -r qbase:qtip
```

# Links

## How to setup the email

Then you need to put this to your ~/.hgrc:
```
[email]
to = sympy-patches@googlegroups.com
from = Ondrej Certik <your@email>
method = /usr/sbin/sendmail
```
more info here:
http://code.google.com/p/sympy/issues/detail?id=451

## How to apply patches directly from Mail Client

For Mutt, put something like the following into .muttrc:
```
folder-hook =sympy-patches/ 'macro pager A "<pipe-entry>(umask 022; hg -R ~/src/sympy/sympy import -)<enter>"'
```

Then, when you press 'A', a patch will be imported into sympy repository.


## other

http://selenic.com/pipermail/mercurial/2007-March/012580.html

## Notes

This was the conversation on #sympy. The documentation here should be improved according to:
```
<kirr> Seems reasonable.
<ondrej> and let the subclasses redefine the taylor term to provide a super fast series, if there is some better algorithm
<ondrej> particular classes in I have inmind is exp and log
<ondrej> how do you see it with the article?
<kirr> agree
<ondrej> Zlm seems to be working now.
<kirr> I only spoke about leading_term -- let's cleanup all functions along the way (and write tests), or delay it in the issue
<ondrej> yep
<kirr> OK, please commit your version of Ylm -- we'll enhance it incrementally.
<ondrej> yes.
<ondrej> btw, how do you retrieve the patch from sympy-patches to try it?
<ondrej> using your email client (which one)?
<kirr> I use mutt, but I still had not setup it properly.
<kirr> I know there is a way to bind save/"!hg import whatever" to only one key.
<ondrej> Maybe I could just upload it to my public hg repository at hg.certik.cz and then you can just pull
<kirr> When I'll setup it -- I'll write to wiki.
<kirr> Yes, it is ok
<ondrej> yes please
<kirr> Where is youre repo
<kirr> ?
<ondrej> it's not there yet
<ondrej> but that's the spirit of mercurial, right? to have many repositories around and pulling from each others
<kirr> Yes. (BTW: we even can have repositories for patches itself -- versioned MQ)
<kirr> exactly
<ondrej> yes - I wrote something to the wiki
<ondrej> please enhance it with your experiences:
<ondrej> http://code.google.com/p/sympy/wiki/HgWorkflow
<ondrej> when I have like 10 commits, it sucks to enter hg qfold 1516 manually for each commit to fold them
<ondrej> is there a way to do it with just one command?
<kirr> I think it is: use MQ from the beginning
<kirr> it is -> there is
<ondrej> another question: when I do hg qimport -r qparent and I want to take it back - I am screwed, because hg qdelete deletes the patch and (!) the commit
<ondrej> so why not to just use MQ for all sympy? I am missing the point why there are commits and MQ
<kirr> 1: what do you mean by 'take it back' 2: queues are used when you are *working* on a patch itself, do 1,2,3, fix 4, refresh, clean it up, so it seems reasonably good, meets common criteria (to change one semantic thing etc), then you include it in the main repo, and it is immutable.
<ondrej> 1: see the wiki - it happened to me that I executed the hg qimport too many times (usually once more than I wanted)
<kirr> 1: I see, let me think
<ondrej> 1: so 1) is not needed, when the correct way to work is 2:, right?
<ondrej> I thought one should work by using commits and then fold them and send them. so you propose to use MQ to create a nice patch, then commit and send? right, makes sense.
<kirr> 1: maybe 'hg qdel --rev' ? did not tried it though.
<ondrej> I think that deletes the patch and the commit
<kirr> 2: Yes, I propose this. (but commit -> qpush)
<kirr> 1: wait
<ondrej> 2: and you can do versioned MQ? so you just commit to MQ, so you don't lose your work
<ondrej> I need to learn it
<kirr> 1: No, it leaves it in place, just stop managin it in MQ. '--rev XXX' is important!
<kirr> 2: yes ('hg qinit -c', 'hg qcommit')
<kirr> 2: And export it as usual HG repo!
<kirr> :)
<ondrej> I see
<ondrej> I see - so hg ci is never used?
<kirr> yes
<kirr> or seldomly
<kirr> for simple things
<ondrej> I didn't know it
<kirr> It is just a matter of style.
<ondrej> I am going to read the mercurial docs again
<kirr> If there was something like ammend for commit it would be nice. But there is no amment in pure HG right now.
<ondrej> like to change commit to qcommit?
<kirr> With darcs, when I'm working on a patch, I'm not afraid I didn't commit some parts of the patch, or commited extra changes. I always can amend the patch (that is re-commit it, but not from scratch -- using already committed version as a base)
<kirr> And MQ just provide this behaviour -- it is very convenient.
<kirr> Let me clarify:
<kirr> 1: When working on something, let's use MQ from the beggining.
<kirr> Split the change into logical chunks and let them live in their own patches.
<ondrej> yes, that's how I understand it
<kirr> 2: when working on patches, qrefresh them as many times as you see fit.
<ondrej> but if you look here for example: http://www.selenic.com/mercurial/wiki/index.cgi/UnderstandingMercurial, they don't use MQ
<kirr> 3: In the end of the day, use qcommit to save your work in MQ, and allow others to clone your patches, and contribute to patches through usual pull/push/whatever
<ondrej> I need to learn how the MQ with commits work
<kirr> 4: When patches are 'done' (i.e. reviewed, enhanced, etc) -- include them into the trunk, and qdel from MQ
<ondrej> right - that's very clever - because so far I committed them and it sucks
<ondrej> because I have them and I need to reclone the whole repo to work on somethin else
<ondrej> but actually I should probably clone the repo anyway
<ondrej> but MQ allows easily to turn the patch on and off and modify it according to the review. that's the main advantage
<ondrej> ok, we need to put this info into the wiki together with exact HG commands
<kirr> No, you don't have to: just use 'hg up rev' (where rev is the revision you want to start working from)
<ondrej> right, actually you are right, didn't occur to me
<kirr> But it is the preferrence
<kirr> One important think: frankly speaking HG user interface suck a bit
<ondrej> compared to darcs?
<ondrej> or git?
<kirr> It misses one important (for me, and I think for others) feature compared to darcs and git: one cannot interactively qrefresh a patch -- that is to chose which hunks go into the patch, and which do not.
<kirr> But I hope I'll get my hands dirty and code it
<ondrej> yes, that would be awesome!
<kirr> We already have 'hg record', and this needs to be adapted for queues
<ondrej> what I like on mercurial is that it's in python and not the perl/C mess as git
<kirr> Yes. For me, it was a killer feature which stopped me from adapting git or hg. and as you say HG is more friendly for hacking than git (at least for pythoners:) )
<ondrej> what is the difference between your hg record for queues (when you implement it) and the hg qcommit
<ondrej> I see - the qcommit commits everything, right? but record allows you to pick
<kirr> Say I've changed a lot of lines in some file -- some of them need to go to the patch, but others was used for debugging (which I usually want to be in place), or should go into another patch. with record I could interactively chose which hunks (elementary diffs) should go in, and which should not.
<kirr> to be -> to left
<kirr> to be in place
<ondrej> you can use two patches - one for debugging and one for the core patch
<ondrej> I find it cleaner
<ondrej> you can easily turn on and off the debugging by turning on and off the debugging patch
<kirr> Yes, exactly. But usually I just work on the code, and then go to refreshing.
<ondrej> right
<kirr> I have file.py with (1 - debugging changes, 2 - semantic changes). How should I refresh debug.patch and semantic.patch?
<ondrej> you just turn the debug.patch off, qrefresh (it will go to semantic.patch) and that's it, as far as I understant
<kirr> qrefresh allows al changes to the file go in, but I want to split it into 1 and 2, and I don't want to interrupt my thinking constanly qpop/qpushing while developing
<ondrej> oh I see now
<ondrej> that is not possible yet
<kirr> Yes. Maybe it seems strange/unneede for CVS/SVN/etc ... people, but once tried you'll can't live without it
<kirr> It is *very* handy
<ondrej> I see. I never tried that
<kirr> And easily implemented (I hope)
<ondrej> but you are right - you just split the patch in two, right?
<kirr> Please clarify
<ondrej> you work on the code (semantic + debug) and then you do hg qrecord and it will allow you to split semantic to one patch and debug to another patch, right?
<kirr> BTW: how to retrieve IRC logs? We could refine some parts into wiki.
<kirr> Yes, exactly
<ondrej> I just copy & paste
<ondrej> from my irc client
<kirr> And it is *very* handy (Sorry for saying this again, but this technique raises the quality)
<ondrej> but then you also need a feature to move one hunk from one patch to another patch (if you made a mistake during hg qrecord)
<ondrej> sure - but it should be that hard to implement - and you already implement something in hg
<ondrej> should -> shouldn't
<ondrej> and can you also pull and push MQ?
<kirr> Seems, so, but I think there are external patch editors and this needs in ~1% of times. I did it by hand, when neede
<ondrej> right
<kirr> Do you mean hg pull/ push to sync repositories? If so -- yes
<ondrej> yes
<ondrej> because using the sympy-patches for syncing sucks
<kirr> Yes, .hg/patches/ is an HG repo itself
<ondrej> but using hg pull is ok
<ondrej> so all I and you need is to setup your sympy-devel repo at our own servers (not the official hg.sympy.org) and we can pull from each other easily
<kirr> Sympy-patches should be used for call for review. Nothing prevents to say in introductory mail that "this is take-N of feature SMTH. You can get the patch queue at URL"
<ondrej> yep
<kirr> But reviewing in plain mail client is nonetheless handy
<ondrej> btw - when commiting just one commit for a review - it doesn't ask me for the introductory message
<ondrej> yes, yes, for review, sympy-patches is ok
<kirr> Seems like a bug or misfeature in "hg email". There should at least be a possibility to force it to do so by hand.
<ondrej> ok, enough talk, I am going to commit those patches and paste this conversation to a wiki
<ondrej> and we'll clean it up later
<kirr> Yes, perfection is the enemy of good.
```
