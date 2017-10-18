After successful installation Jenkins needs to be configured before it can be used. The steps outlined below will transform the default Jenkins page (Left side of image) to the required setup for use with Stormtest (Right side of image)

!jenkins-config-before-after.png|align=center!

h2. Step to Configure Jenkins
Steps to configure Jenkins for use with Stormtest are as listed below. Detailed step explanations can be found below the list;
* 1) Add users to Jenkins
* 2) Increase number of build executors
* 3) Prevent Jenkins log style overwriting Stormtest style
* 4) Install custom plugins
* 5) Change Jenkins Root Directories
* 6) Create Blank jobs
* 7) Create Official View
* 8) Create SSH keys for Jenkins
* 9) Add public key to GitHub account
* 10) Configure *RunTestOnSlot* job
* 11) Configure *RunTestSuite* job
\\
----
_*PLEASE NOTE all of the above setup steps have already been performed. So really the remainder of this section is more for reference than anything else*_
----
\\
h2. 1) Add users to Jenkins
----
* 1) From Jenkins left hand menu select *Manage Jenkins* and then scroll down page to option *Manage Users* and select it. The page presented is as shown below and will only show the single entry of the *Default Admin* user as that was the user who installed Jenkins;

!jenkins-config-single-user.png|align=center,width=600,height=400!

* 2) To add new user click *Create User* and enter details on the screen presented for the new user.
* 3) On the TDC Jenkins instance the following users have been created. Note user *jenkins* is the user who will execute formal test runs on the TDC setup.

!jenkins-config-tdc-users.png|align=center,width=600,height=400!

* 4) Now we need to assign permissions to the new users.
* 5) Go to Jenkins menu *Manage Jenkins* and select *Configure Global Security*. On this page under *Authorization* select *Matrix-based Security*. This will present a matrix of permissions assigned per user. On first invocation the list of user will only present two entries as outline below;

!jenkins-config-security-default.png|align=center,width=600,height=400!

* 6) Add new users to *Matrix-based Security* and select appropriate permissions as required based on user expected usage. Currently TDC Jenkins has the following configuration;

!jenkins-config-tdc-security.png|align=center,width=600,height=400!

*NB* Don't forget to save any changes before leaving page.

h2. 2) Increase number of build executors
----
As explained in the section *1-Jenkins-Intorduction* by default there are only 2 *Build Executors* available. We will need to inceease this to 16 build executors where each executor will run a *test job* targetted to one slot on the Stormtest rack. To increase the number of build executors do the following;
* 1) Go to Jenkins menu *Manage Jenkins* and select *Configure System*. 
* 2) On the page presented, modify the entry *# no of executors* from 2 to 16
* 3) *SAVE* changes.

h2. 3) Prevent Jenkins log style overwriting Stormtest style
----
By default Jenkins has it's own style for decorating artifacts from buids. To prevent Jenkins overwriting Stormtest sytles for test logs the change highlighted in yellow in below diagram needs to be made to the core *jenkins.xml* file which can be found @ C:\Program Files (x86)\Jenkins;

!jenkins-config-jenkins-xml.png|align=center!


h2. 4) Install custom plugins
----
During the installation of Jenkins (Refer: 2-Jenkins-Installation) we selected to install a default set if plug-ins for Jenkins, ones which the Jenkins community recommended. Now we need to install the following additional plug-ins;
\\
* Build-name-setter
* Throttle Concurrent Builds Plug-in
* Rebuilder
\\
* 1) To install any plug-in, simply go to Jenkins main menu "Manage Jenkins" and on the page presented selecte the *Manage Plugins* option. Once this page is presented clik on the *Available Plugins* tab to get the following page;

!jenkins-config-plugins-available.png|align=center!

* 2) Enter first few letters of plugin into the Filter box on top right hand side of page to narrow the listing of plugins. Following shows example when trying to find the *Rebuilder* plugin;

!jenkins-config-plugins-select.png|align=center!

* 3) Select the rebuilder and cick on *Install without restart* button. You should confirm the successfull installation by observing the blue icon after the plugin as indicated below;

!jenkins-config-plugins-success.png|align=center!

* 4) Repeat selection for all plugins listed above.

h2. 5) Change Jenkins Root Directories
----
JOEOC - TODO

h2. 6) Create Blank jobs
----
As outlined in section *1-Jenkins-Introduction* to do anything in Jenkins we first need to create a *job*. For our purposes we will need two jobs to be created as follows;
* 1) *RunTestOnSlot* job will provided ability to schedule a test run of a single test on any slot on the Stormtest Rack.
* 2) *RunTestSuite* job will provide ability to schedule a test suite to be executed across the Stormtest Rack.

A *job* e.g. *RunTestOnSlot* can be created by following steps;
* 1) From the Jenkins main menu select "New Item". The page presented allows user to select from a list of job item templates. For our purpose we willuse the *Freestyle project* template and in later sections outlined below we will customize as required. 
* 2) Enter name "RunTestOnSlot" into *Title* box.
!jenkins-config-job-create.png|align=center!
* 3) Click on the *OK* button and the *job* page is presented.
* 4) Enter the description/purpose of the *job* into the *Description* field.
!jenkins-config-job-desc.png|align=center!
* 5) Click on *Save* to save the new *RunTestOnSlot* job.
* 6) Repeat above steps to create the *RunTestSuite* job

h2. 7) Create Official View
----
As more and more jobs are created, some will be used for personal developer needs and others represent formal/official jobs. We can separate the jobs into specific *Views*. By default all jobs are visible under the *All* tab on Jenkins home page. In this section we will create a new *View* called *Official* to list all formal/official jobs.
* 1) From Jenkins main page select the *+* symbol next to the *All* tab. This will open the *New VIew* page.
* 2) Enter the name for the new view in the *View name* box
* 3) Select the radio button *List View* 
!jenkins-config-view-create.png|align=center!
* 4) Press "OK" and in the presented page under *Jobs* select the jobs which should appear for this *View*
!jenkins-config-view-select-jobs.png|align=center!
* 5) "Save" the changes
* 6) In time more "Views" can be added as needed e.g. "SANITY", "REGRESSION", "PERFORMANCE", "OTA", "AGING", "TIMESHIFT", "NPVR", etc...

h2. 8) Create SSH keys for Jenkins
----
For our test jobs to be of any use they will need to clone the TDC Git repository from GitHub. To facilate this SSH keys for Jenkins will need to be created and the public key will need to be added to GitHub while the private key will be need to be added to each Jenkins job which requires GitHub access (Refer to Sections 8 & 9 below).
_*Note: The nesessary tool "puttygen" would have been installed already as per instructions in section "2-Jenkins-Installation"*_ 
* 1) From a command prompt, launch putty key generator via > puttygen
!jenkins-config-putty-gen.png|align=center,width=400,height=300!
* 2) Select *Generate* from the putty applet. Follow instructions i.e. make random mouse movements while key is being generated in the box.
* 3) Enter a passphrase for the generated key.
!jenkins-config-putty-key.png|align=center,width=400,height=300!
* 4) Select to save the private key and call the file *"id_rsa.ppk"*
* 5) Select to save the public key and call the file *"id_rsa_public.ppk"*

h2. 9) Add public key to GitHub account
----
To allow Jenkins to gain access to the TDC GitHub repository, it is necessary to add the public part of the SSH keys just generated in previous section to an account on GitHub. Currently at the time of writing the key has been added to contractor oconnor@tdc.dk account *however* it will shortly be added to Thomas von Eyben (teve@tdc.dk) account as well.
* 1) Login into your account on GitHub and select *settings* page. On page presented select *SSH and GPG Keys*
!jenkins-config-github-ssh-keys.png|align=center,width=400,height=300!
* 2) Select new and enter *"tdc-jenkins"* into description box so that you know what this key refers to in future. 
* 3) Launch *puttygen* and load the keys previous generated by selecting the *load* option and selecting the private key file *id_rsa.ppk* previously saved on the Stormtest rack.
* 4) From putty appliction copy the public key, which would have loaded from previous step and paste it into the *key* box on GitHub page.
!jenkins-config-github-ssh-new.png|align=center,width=400,height=300!
* 5) Click on the *Add SSH Key* button on GitHub page and you should see a page similar to below picture. Note the key symbol is black in color, once the first Jenkins job uses this key the symbol will change color to green indicating successful SSH access.
!jenkins-config-github-ssh-saved.png|align=center,width=400,height=300!
* 6) You can exit GitHub now.

h2. 10) Configure *RunTestOnSlot* job
----
JOEOC - TODO

h2. 11) Configure *RunTestSuite* job
----
JOEOC - TODO

