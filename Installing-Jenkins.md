This page will document the steps I used to install Jenkins, so that they can be reproduced if needed. Links and a copy of the required instructions are provided.

***

First I followed this page to install Jenkins: https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu

Installation:

```bash
wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo echo "deb http://pkg.jenkins-ci.org/debian binary/" > /etc/apt/sources.list.d/jenkins.list
sudo aptitude update
sudo aptitude install jenkins
```

What does this package do?

    Jenkins will be launched as a daemon up on start. See /etc/init.d/jenkins for more details.
    The 'jenkins' user is created to run this service.
    Log file will be placed in /var/log/jenkins/jenkins.log. Check this file if you are troubleshooting Jenkins.
    /etc/default/jenkins will capture configuration parameters for the launch.
    By default, Jenkins listen on port 8080. Access this port with your browser to start configuration.

***

After that, I followed this guide to enable security: https://wiki.jenkins-ci.org/display/JENKINS/Standard+Security+Setup

    Go to the system configuration screen (http://server/jenkins/configure) and choose "enable security"
    Select "Jenkins's own user database" as the security realm
    Select "Matrix-based security" as the authorization
    Give anonymous user the read access
    In the text box below the table, type in your user name (you'd be creating this later) and click "add"
    Give yourself a full access by checking the entire row for your user name
    Scroll all the way to the bottom, click "save"

At this point, you'll be taken back to the top page, and Jenkins is successfully secured. Now you need to create an user account for yourself.

    Click "login" link at the top right portion of the page
    Choose "create an account"
    Use the user name you've used in the above step, and fill in the rest.

***

You'll want to install some plugins now: Github and the Python plugin (to enable a "Python build step") at least.

Then I followed the Tox guide on working with Jenkins: http://tox.testrun.org/en/latest/example/jenkins.html

* create a “multi-configuration” job, give it a name of your choice

* configure your repository so that Jenkins can pull it

* (optional) configure multiple nodes so that tox-runs are performed on multiple hosts

* configure axes by using TOXENV as an axis name and as values provide space-separated test environment names you want Jenkins/tox to execute.

* add a Python-build step with this content (see also next example):

```python
import tox
tox.cmdline() # environment is selected by ``TOXENV`` env variable
```

* check Publish JUnit test result report and enter **/junit-*.xml as the pattern so that Jenkins collects test results in the JUnit XML format.  (we don't do this currently)

***

A bit of a problem now is how to make the tox.ini file available to Jenkins. In the end, the best solution I've found is to put a tox.ini file in the Jenkins home directory (/var/lib/jenkins) and copy that over as a build step. So, add an "execute shell" build step before the Python one with "cp -f ~/tox.ini ./tox.ini". Not the cleanest solution but it works.

Then it'll probably complain "Please tell me who you are". Apparently, git tries to do some tags (why??) and needs to be setup to do so. The following should be enough:

```bash
su jenkins
git config --global user.email "some@email.com"
git config --global user.name "Jenkins CI Server"
```