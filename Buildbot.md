## Buildbot

[[http://buildbot.sympy.org/]] (currently not running).

Documentation: [[http://buildbot.net/repos/release/docs/buildbot.html]].

### Installing build slave

```bash
$ wajig install buildbot
$ sudo adduser buildslave
$ sudo su buildslave
$ cd
$ buildbot create-slave Buildbot buildbot.sympy.org:9989 august passwd
mkdir /home/buildslave/Buildbot
chdir /home/buildslave/Buildbot
creating Makefile.sample
mkdir /home/buildslave/Buildbot/info
Creating info/admin, you need to edit it appropriately
Creating info/host, you need to edit it appropriately
Please edit the files in /home/buildslave/Buildbot/info appropriately.
buildslave configured in /home/buildslave/Buildbot
$ cd Buildbot
$ vim buildbot.tac  # adjust your password/name
$ vim info/host    # describe your host
$ vim info/admin  # your email
```

Then setup the slave on server, just add the following line:
```
BuildSlave("august", "password"),
```
to `c["slaves"]`. Then again on the slave:
```bash
$ buildbot start .
```

### Local installation

```bash
$ tar xzf python2.4.tar.gz
$ cd python2.4
$ ./configure --prefix=/home/buildslave/py2.4
$ make 
$ make install
```

And do this for python 2.5, 2.6 and 2.7 as well. Then install all necessary packages (i.e. setuptools, py.test using `py2.4/bin/python setup.py install`)

Don't forget to install zlib before installing python, otherwise the zlib module will be missing and it is required by setuptools.

### Other

This sends a patch to a server:
```bash
$ buildbot try --diff=0001-Make-exp-I-oo-return-nan.patch --connect=ssh --tryhost=li21-74.members.linode.com\
--username=buildmaster --builder=buildbot-full --trydir=Buildbot/jobdir
using 'ssh' connect method
job created
job has been delivered
not waiting for builds to finish
```

This triggers a commit change:
```bash
$ buildbot sendchange --master buildbot.sympy.org:9989 --u changer some_files
change sent successfully
```
