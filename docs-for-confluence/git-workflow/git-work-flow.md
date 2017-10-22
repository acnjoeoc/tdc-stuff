As of today Sunday 22 Oct 2017 the feature branch *feature/humax-1.60.ui* has been merged into the *master* branch meaning the *master* branch is finally now the *HEAD* of our development. *Going forward each developer will need to following the guidelines outlined below when modifying/creating new tests.*

h2. Formal Git Work Flow
!tdc-git-branching.png|align=center,width=700,height=300!
# Each developer to create their own development branch
## First time creation of a development branch;
### > git checkout -b joe_dev
### > git push -u origin joe_dev
## If branch already created previously and you are cloning from new you will need to checkout the development branch;
### > git checkout -b joe_dev remotes/origin/joe_dev
# At this stage you are in your dev branch. Always update to master prior to starting any work;
## > git merge master
## resolve any conflict locally in your dev branch
# At this stage your dev branch *[joe_dev]* in our example is upto date with *[master]* so you can now start development work.
# Once development is complete or you need to verify development thus far you should execute your Jenkins job. *Note* there exists a Jenkins job for each user which pulls from the users branch. The jobs can be found @ *"http://192.168.39.59:8080/"* and are namely;
## _thomasRunTestOnSlot
## _sarithaRunTestOnSlot
## _joeRunTestOnSlot
# Only when your personal Jenkins job passes and you are happy that current feature is complete you can merge your changes to master
## > git checkout master
## > git merge joe_dev
## Resolve any conflicts using: > git mergtool
### Ensure good GUI merge tool of your choice (there are many kdiff3, meld, vi etc...)  is setup e.g.
### > git config —global merge.tool meld
## > git merge tool
# After conflicts are resolved push to master
## > git push
# Final step involves execute test using the *official* Jenkins job *RunTestOnSlot*. This job is setup to only pull from the master branch.
# If the official job is successful you are finshed

