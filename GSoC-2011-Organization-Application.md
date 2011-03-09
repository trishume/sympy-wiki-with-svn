This is based on the [Google Summer of Code 2010
application](GSoC-2010-Organization-Application) for SymPy to be an
organization.  Please edit this page to update/improve stuff. The
headers below are the questions that we have to answer for the
application.

The application deadline is March 11.  Feel free to edit this page until
that point.  On March 11 I will copy the contents of this page to the
form at [[http://www.google-melange.com/]].

--Aaron

# Organization Name:

SymPy

# Description:

SymPy is a Python library for symbolic mathematics. It aims to become a
full-featured computer algebra system (CAS) while keeping the code as
simple as possible in order to be comprehensible and easily extensible.
SymPy is written entirely in Python and does not require any external
libraries.

SymPy has a vast array of potential applications, from theoretical
physics (atomic physics, quantum field theory, general relativity,
classical mechanics, ...), applied math (solving algebraic and
differential equations, ...), teaching (calculus, integrals,
derivatives, limits, ...), web (it runs on the google app engine) and it
can also be included as a library in any scientific code.

SymPy has a very large, active development team that has increased
non-stop since 2007 (ref: [[http://www.ohloh.net/p/sympy]]) thanks to an
extensible architecture that permits to add features in a modular way.

It is built and tested regularly on all major platforms and all major
architectures to ensure that it can reach the widest possible audience.

# Home page:

[[http://sympy.org/]]

# Main Organization License:

New and Simplified BSD licenses

# Why is your organization applying to participate in GSoC 2011? What do you hope to gain by participating?

From previous experiences, GSoC is a very effective way to get students
attracted to the project, coding on a specific task.

It will be beneficial for the project, since each year this has proven
to give a huge boost to the project, and it will be beneficial for the
students, who will get the chance to write code for an open source
project (and get paid for it).

In the past, SymPy has participated under the umbrella of the Python
Software Foundation, the Space Telescope Science Institute, and Portland
State University.  However, there is more competition for students
applying under an umbrella organization, meaning that SymPy might not
get as many students accepted as we would like or could handle.  Also,
umbrella mentoring organizations may limit what applications are
accepted to work on SymPy based on what they see as being beneficial to
their own organization, instead of directly to SymPy.

# If accepted, would this be your first year participating in GSoC?

It would be our first time participating as a mentoring organization,
but we have sponsored projects in the past under umbrella organizations
(see previous question).

# Did your organization participate in past GSoCs? If so, please summarize your involvement and the successes and challenges of your participation.

The SymPy project participated in 2007 under the umbrella of the Python
Software Foundation, Portland State University and the Space Telescope
Science Institute.  We had five students in total.  All five projects
were successful. All the projects details can be found here:

[[http://code.google.com/p/sympy/wiki/GSoC2007]]

In 2008, we participated under the umbrella of the Python Software
Foundation and we got one student, who was successful. All details are
here:

[[http://code.google.com/p/sympy/wiki/GSoC2008]]

In 2009, we participated under the umbrella of the Python Software
Foundation and Portland State University, for a total of five students.
All but one were successful.  Details are here:

[[http://code.google.com/p/sympy/wiki/GSoC2009]]

In 2010, we participated under the umbrella of the Python Software
Foundation and Portland State University.  There were five students, all
of whom were successful in their projects.  The details are here:

[[http://code.google.com/p/sympy/wiki/GSoC2010]]

A total of fifteen out sixteen projects were successful and they
incredibly boosted SymPy's development. Some of the students who did
this program have continued developing for SymPy after the program
ended, again helping to boost the program.  For example, I myself (Aaron
Meurer) participated in 2009 and 2010, and in 2011, Ondřej Čertík, the
founder of the project and leader, asked me to step up and be the leader
of the project.  I would have never have heard of the project and would
not be doing any work at all for open source were it not for the Google
Summer of Code program.

For almost all of the projects, it is almost certain that they would
have never been coded if it were not for the Google Summer of Code
program, because they were implemented by students who would otherwise
either would not have known about SymPy or else wouldn't be able to
dedicate their summer to working on it because of the stipend.


# If your organization participated in past GSoCs, please let us know the ratio of students passing to students allocated, e.g. 2006: 3/6 for 3 out of 6 students passed in 2006.

2007: 5/5, 2008: 1/1, 2009: 4/5, 2010: 5/5.

# What is the URL for your ideas page?

https://github.com/sympy/sympy/wiki/GSoC2011Ideas ([[GSoC2011Ideas]])

# What is the main development mailing list for your organization? This question will be shown to students who would like to get more information about applying to your organization for GSoC 2011. If your organization uses more than one list, please make sure to include a description of the list so students know which to use.

## Email:

sympy@googlegroups.com

## Website:

http://groups.google.com/group/sympy

# What is the main IRC channel for your organization?

\#sympy in Freenode

# Does your organization have an application template you would like to see students use? If so, please provide it now. Please note that it is a very good idea to ask students to provide you with their contact information as part of your template. Their contact details will not be shared with you automatically via the GSoC 2011 site.

Please see https://github.com/sympy/sympy/wiki/GSoC-2011-Application-Template ([[GSoC-2011-Application-Template]])

# What criteria did you use to select the individuals who will act as mentors for your organization? Please be as specific as possible:

Our mentors will be chosen from members of the community who have shown
themselves to be committed to the development of SymPy.  This means that
they will be familiar both with the code base and with git, so they will
be able to help the students with these well.  Also, if possible, we
will try to choose mentors who are familiar with the concepts that the
student will be implementing.  Often, in SymPy, these can be
mathematically complicated, so it is important to have a mentor who
understands it well, if possible.  And of course, if someone whom we
feel meets the above qualifications wants to mentor a particular
student, we will let him, because that person is the most likely to be the
best person to stick with that student and help him to complete his
project.

# What is your plan for dealing with disappearing students?

To begin with, we will try to pick students who will not disappear.  We
will require that all students who are accepted to have submitted at
least one patch that passes review and is pushed into the code base.
This will show that they are dedicated, because they must be willing to
learn the code base enough to try fixing part of it, and be willing to
stick around for the review process.

We require each student to start a blog if they don't already have one
and to blog once a week about their progress. The mentor for each
student will try to stay in touch more often, by whatever method is best
for the student (email, the mailing list, IRC, etc.), but we will also
try to get the students to stay in touch with the entire community
through the mailing list.  The requirement that students submit a patch
to be accepted will also help us screen students who will likely not be
very communicative with the community.  We will also require that
students push their work up to an online git repository such as GitHub,
so that the mentor as well as everyone in the project can monitor their
progress and to see the things that they are doing, as well as to help
them fix mistakes early.

If despite these things a student disappears, or does not work up to
their potential, the mentor and I (the organization admin) will try to
sit down with the student in an IRC conversation or via some other
medium to try to see what is holding him back and how he can be brought
back on track.  If necessary, we may need to adjust the goals as
originally stated in the student's application, because it is better for
a student to do a reduced amount than to do nothing at all.  If nothing
works, we may be forced to fail the student in his midterm or final
evaluation, but this will be a last resort, because it will be to
everyone's benefit if the student can be brought back on track.

# What is your plan for dealing with disappearing mentors?

We are in frequent contact with all our mentors and we have collaborated
with each other for several years, so we do not expect that such thing
would happen. However, if that happens, Ondřej Čertík has experience
with mentoring several students at once from the year 2007, when SymPy
participated as part of several organizations and even though we had
official mentors at the umbrella organizations, Ondřej was effectively
supervising all 5 students. As can be seen from our GSoC 2007 page:

http://code.google.com/p/sympy/wiki/GSoC2007

All the projects managed to finish successfully.

Ondřej at the time was the project leader, but he has since passed on
the position to me (Aaron Meurer).  I think that if it is necessary, I
could do similar.  Also, other mentors or members of the community could
pick up if a mentor falls out.

This will be more effective than assigning a backup mentor to each
student, because this way anybody can step in and fill in for a mentor
who is not available.  It will also encourage students to interact with
the whole community, and ask the whole community for help (i.e., on the
IRC channel or on the mailing list) if they have a problem, rather than
just one person.  This will help them to become better members of the
community and will also make it easier for the whole community to
monitor their progress.

# What steps will you take to encourage students to interact with your project's community before, during and after the program?

We require all applicants to submit a patch to the project that gets
reviewed and pushed in.  We do not require that this be a particularly
complicated.  In fact, we will reference to them the easy to fix issues
in our tracker:

[[http://code.google.com/p/sympy/issues/list?q=label:EasyToFix]]

This is so that we can make sure that they can submit a patch (if they
can't we teach them at this stage) and also so that we have some
experience how they interact over email. We communicate with them very
frequently before they are accepted, and try to get them involved in our
community. As was discussed in the previous questions, if we find that
the students cannot do these fundamental things, then they will not be
accepted to the program.

During the program, they need to blog once a week and are encouraged to
become active members of our community. The mentors may also choose to
have a meeting with the students regularly to monitor their progress. We
will leave this up to the mentor and the student to schedule, because
they may have problematic schedules to synchronize, but we will
encourage them to do any meeting on our public IRC channel, so that it
is public to the entire community.

After the program is over, the students already have their blogs, which
are synchronized with our planet.sympy.org, and usually if they blogged
interesting things, they already built a nice community around their
blogs, and so the continue blogging about what they do. It all depends
how they like our community and to communicate with others and so we try
hard so that they feel comfortable and will stick around.  We do
encourage all students to stick around and become regular members of the
community.  Sometimes they do, and become valuable contributors and
sometimes they even participate in Google Summer of Code again in future
years.  Other times, they move on to do their own things, though often
they will still sometimes submit bug reports or patches.  We will try to
accept students who are likely to become regular contributors to the
community after the program ends, because that will benefit SymPy the
most.  But we do realize that people can become interested in other
things, so we will not require this of students (if it were even
possible to require such a thing).

# If you are a small or new organization applying to GSoC, please list a larger, established GSoC organization or a Googler that can vouch for you here.

Googlers: Robert Bradshaw (robertwb@google.com), Craig Citro

Organizations: Python Software Foundation, Portland State University

# If you are a large organization who is vouching for a small organization applying to GSoC for their first time this year, please list their name and why you think they'd be good candidates for GSoC here:

N/A

# Anything else you'd like to tell us?

SymPy has been very successful in the Google Summer of Code program
under umbrella programs in the past, and we hope that we can be much
more successful if we are accepted as an organization.

# Backup Admin (Link ID):

certik
