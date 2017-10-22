As of today Sunday 22 Oct 2017 the feature branch *feature/humax-1.60.ui* has been merged into the *master* branch and this mean the *master* branch is finally the *HEAD* of our development.
\\
Going forward each developer will need to following the guidelines outlined below when modifying/creating new tests.

h2. Formal Git Work Flow
!tdc-git-branching.png|align=center,width=600,height=400!
# Each developer to create their owb development branch
## First time create a development branch for yourself
### git checkout -b joe_dev
### git push -u origin joe_dev
## If branch already created previously and you are cloning from new you will need to checkout development branch
### git checkout -b joe_dev remotes/origin/joe_dev
# At this stage you are in your dev branch. Always update to master prior to starting any major work
## git merge master
## resolve any conflict locally in your dev branch
# At this stage your dev branch *joe_dev* in this example is upto date with *master* so you can perform development work now on your branch
# Once development is complete or you need to verify development to date you should execute your Jenkins job. *Note* I have create a Jenkins job for each of use as listed below. Each of these jobs points to your own development branch.
## _thomasRunTestOnSlot
## _sarithaRunTestOnSlot
## _joeRunTestOnSlot
# Only when your personal Jenkins job passes and you are happy that current feature is complete you can merge your changes to master
## git checkout master
## git merge joe_dev
## Resolve any conflicts using git mergtool
### Ensure good GUI merge tool is setup e.g.
### git config —global merge.tool meld
## git merge tool
# After conflicts are resolved push to master
## git push
# Final step involves execute test using the *official* Jenkins job *RunTestOnSlot*. This job is setup to only pull from the master branch.
# If the official job is successful you are finshed
