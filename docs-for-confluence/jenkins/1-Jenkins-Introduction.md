There are numerous ways to execute a test using Stormtest as outlined below;

* 1) Execute under Stormtest Daemon
* 2) Execute locally on Stormtest server from command
* 3) Execute remotely from Stormtest remote client from command line
* 4) Execute locally on Stormtest server from command line via Jenkins
\\
All options are valid and are usefull during different stages of test script development. This wiki will concern itself with the last option i.e. *executing test scripts via Jenkins which will run tests locally on the Stormtest server.*

h2. Jenkins Core Concepts
The default Jenkins page presented after Jenkins installation is as shown below. Before using Jenkins, users should be familiar with some core concepts which are outlined below the diagram.

!jenkins-install-welcome.png|align=center,width=600,height=400!

Referring to the above default Jenkins screen presented upon first installation;

* 1) Everything in Jenkins is referred to as a *job*
* 2) From above default, see there are no jobs defined.
* 3) The process of executing a job on Jenkins is referred to as *Build* the job
* 4) A *job* can be anything from building code, checking server stats, deploying code to production *OR* in our case kicking a test script to execute on Stormtest. 
* 5) Before a *job* can execute there must be a *Build Executor* available
* 6) From above default, there are 2 buid executors defined. This implies if we had say 100 jobs defined we could only execute x2 of those jobs concurrently and the others would have to wait in the *Build Queue*
\\
The remaining pages in this section will detail how to get Jenkins installed and configured for use with Stormtest.
