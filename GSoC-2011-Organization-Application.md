So far, this is just a copy of the Google Summer of Code 2010 application for SymPy to be an organization.  Please edit this page to update/improve stuff. The headers below are the questions that we have to answer for the application. 

The application deadline is March 11.  Feel free to edit this page until that point.  On March 11 I will copy the contents of this page to the form at [http://www.google-melange.com/](http://www.google-melange.com/).

--Aaron

# Organization Name:

SymPy

# Description:

SymPy is a Python library for symbolic mathematics. It aims to become a full-featured computer algebra system (CAS) while keeping the code as simple as possible in order to be comprehensible and easily extensible. SymPy is written entirely in Python and does not require any external libraries.

SymPy has a vast array of potential applications, from theoretical physics (atomic physics, quantum field theory, general relativity, classical mechanics, ...), applied math (solving algebraic and differential equations, ...), teaching (calculus, integrals, derivatives, limits, ...), web (it runs on the google app engine) and it can also be included as a library in any scientific code.

SymPy has a very large, active development team that has increased non-stop since 2007 (ref: [http://www.ohloh.net/p/sympy](http://www.ohloh.net/p/sympy)) thanks to an extensible architecture that permits to add features in a modular way.

It is built and tested regularly on all major platforms and all major architectures to ensure to reach the widest possible audience. 

# Home page:

http://sympy.org/

# Main Organization License:

New and Simplified BSD licenses

# Why is your organization applying to participate in GSoC 2011? What do you hope to gain by participating?

From previous experiences, GSoC is a very effective way to get students attracted to the project, coding on a specific task.

It will be beneficial for the project, since each year this has proven to give a huge boost to the project, and it will be beneficial for the students, who will get the chance to write code for an open source project (and get paid for it). 

In the past, SymPy has participated under the umbrella of the Python Software Foundation, the Space Telescope Science Institute, and Portland State University.  However, there is more competition for students applying under an umbrella organization, meaning that SymPy might not get as many students accepted as we would like or could handle.  Also, umbrella mentoring organizations may limit what applications are accepted to work on SymPy based on what they see as being beneficial to their own organization, instead of directly to SymPy.  

# If accepted, would this be your first year participating in GSoC? 
Yes
 
# Did your organization participate in past GSoCs? If so, please summarize your involvement and the successes and challenges of your participation.

The SymPy project participated in 2007 as part of the Python Software Foundation, Portland State University and the Space Telescope Science Institute and we had 5 students in total. All the projects details and can be found here:

http://code.google.com/p/sympy/wiki/GSoC2007

In GSoC 2008, we participated as part of the Python Software Foundation and we got 1 student, all details are here:

http://code.google.com/p/sympy/wiki/GSoC2008

In GSoC 2009, we participated as part of the Python Software Foundation and Portland State University, for a total of 5 students.  Details are here:

http://code.google.com/p/sympy/wiki/GSoC2009 

10 projects were successful and they incredibly boosted SymPy's development. Some of the students who did this program have continued developing for SymPy after the program ended, again helping to boost the program.  
If your organization participated in past GSoCs, please let us know the ratio of students passing to students allocated, e.g. 2006: 3/6 for 3 out of 6 students passed in 2006.
    
2007: 5/5
2008: 1/1
2009: 4/5

Note that this was under the umbrella organizations PSF, STSI, and PSU.      

# If your organization participated in past GSoCs, please let us know the ratio of students passing to students allocated, e.g. 2006: 3/6 for 3 out of 6 students passed in 2006.

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

Please see http://wiki.sympy.org/wiki/GSoC2010_Application_Template

# What criteria did you use to select the individuals who will act as mentors for your organization? Please be as specific as possible:

Our mentors will be chosen from members of the community who have shown themselves to be committed to the development of SymPy.  This means that they will be familiar with the code base and with git, so they will be able to help the students with these well.  Also, if possible, we will try to choose mentors who are familiar with the concepts that the student will be implementing.  Often, in SymPy, these can be mathematically complicated, so it is important to have a mentor who understands it well, if possible.  

# What is your plan for dealing with disappearing students?

To begin with, we will try to pick students who will not disappear.  We will require that all students who are accepted to have submitted at least one patch that passes review and is accepted by the projects.  This will show that they are dedicated and are willing to learn the code base enough to try fixing part of it.  

We stay in touch with all the students and we require them to blog once a week about their progress. The mentor for each student will try to stay in touch more often, by whatever method is best for the student (email, the mailing list, IRC, etc.).  We will also require that students push their work up to an online git repository such as github, so that the mentor as well as everyone in the project can monitor their progress and to see the things that they are doing, as well as to help them fix mistakes early.  

# What is your plan for dealing with disappearing mentors?

We are in frequent contact with all our mentors and we have collaborated with each other for several years, so we do not expect that such thing would happen. However, if that happens, Ondrej Certik has experience with mentoring several students at once from the year 2007, when SymPy participated as part of several organizations and even though we had official mentors at the umbrella organizations, Ondrej was effectively supervising all 5 students. As can be seen from our GSoC 2007 page:

http://code.google.com/p/sympy/wiki/GSoC2007

All the projects managed to finish successfully. So in the very unlikely case of a disappearing mentor, Ondrej will supervise the student and it should not be a problem. 

# What steps will you take to encourage students to interact with your project's community before, during and after the program?

We require all applicants to find some easy to fix issue in our tracker:

http://code.google.com/p/sympy/issues/list?q=label:EasyToFix

and send a patch to our project fixing it, so that we can make sure that they can submit a patch (if they can't we teach them at this stage) and also so that we have some experience how they interact over email. We communicate with them very frequently before they are accepted, and try to get them involved in our community. During the program, they need to blog once a week and are encouraged to become active members of our community.

After the program is over, the students already have their blogs and they are synchronized with our planet.sympy.org and usually if they blogged interesting things, they already built a nice community around their blogs, and so the continue blogging about what they do. It all depends how they like our community and to communicate with others and so we try hard so that they feel comfortable and will stick around. 

# If you are a small or new organization applying to GSoC, please list a larger, established GSoC organization or a Googler that can vouch for you here. 

**We need to fill this part out!**

# If you are a large organization who is vouching for a small organization applying to GSoC for their first time this year, please list their name and why you think they'd be good candidates for GSoC here: 

N/A

# Anything else you'd like to tell us? 

SymPy has been very successful in the Google Summer of Code program under umbrella programs in the past, and we hope that we can be much more successful if we are accepted as an organization.  

# Backup Admin (Link ID):

**Who wants to do this (Mateusz or Ondrej)?**
