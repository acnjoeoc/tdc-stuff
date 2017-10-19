Default installation of Jenkins is straight forward and is outlined in below steps;

* 1) Download and Install *git* for Windows
* 2) Download and Install *puttygen* for Windows
* 3) Install python module *python-jenkins*
* 4) Download and Install *Jenkins* for Windows
\\
----
_*PLEASE NOTE all of the above setup steps have already been performed. So really the remainder of this section is more for reference than anything else*_
----
\\
h2. 1) Download and Install *git* for Windows
----
Jenkins needs git pre-installed.
* 1) Download git installer *Git-2.14.2.3-64-bit.exe* from *"https://git-scm.com/download/win"*
* 2) Install git by executing the *Git-2.14.2.3-64-bit.exe* installer and selecting all default options

h2. 2) Download and Install *puttygen* for Windows
----
This utility will be used to generate SSH keys which will allow communication between Jenkins server and GitHub when access to the TDC Git repositories is required.
* 1) Download putty installer *putty-64bit-0.70-installer.msi* from *"http://www.putty.org"*
* 2) Install putty by executing the *putty-64bit-0.70-installer.msi* installer and selecting all default options

h2. 3) Install python module *python-jenkins*
----
Jenkins will need to execute python scripts which will automatically control Jenkins tasks. As such the module *python-jenkins* needs to be added to the installed python. This can be achieved by openning a command prompt and executiing following command;

* > python -m pip install python-jenkins

h2. 4) Download and Install *Jenkins* for Windows
----
* 1) From *"https://jenkins.io/download/"* select the windows Long Term Support (LTS) to download. At the time of writing this wiki that latest LTS version is 2.73.2.
* 2) Unzip the downloaded *jenkins-2.73.2.zip*
* 3) Select the *jenkins.msi* installer to start installation. Select all default options when presented during installation.
* 4) When presented with the screen shown below, choose the default highlighted option to *Install Suggested Plugins*. (Later we will install other plug-ins.)
!jenkins-install-plug-ins.png|align=center,width=400,height=300!
* 5) Next you will be presented with the screen shown below, *Create First Admin User*. Usually this is the person who is performing the installation. And so I have already setup myself as the first user / ADMIN. (More details on users will be provided later)
!jenkins-install-create-first-admin.png|align=center,width=400,height=300!
* 6) Once you entered *First Admin* details you will be presented with the below screen, indicating the installation has completed successfully;
!jenkins-install-complete.png|align=center,width=400,height=300!
* 7) Click on the *Start Using Jenkins* button to launch Jenkins and you will be presented with the *Welcome* screen shown below;
!jenkins-install-welcome.png|align=center,width=400,height=300!





