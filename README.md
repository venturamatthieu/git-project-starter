Global Config

git config --global user.name "FirstName LastName"
git config --global user.email youremail@domain.extension

Use ssh key, 
Projet with Git  
========================

Command line, code, etc



1) Global Informations 
----------------------------------

Project Structure branches by convention 

Required :

- master
	
	git branch master

- develop 

	git branch develop

Extra :

- feature-xxx
- release-xxx
- hotfixes-xxx

Convention name for versionning

	1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0

Clone your project 

	git clone git@github.com:yourrepo/yourprojectname.git

Where my code is stored, basicaly is just one remote, orgin. But you could have more than one remote with on each more than one branch....

	git remote -v




2) How to commit 
----------------------------------

First you have to select the branch 

	git checkout develop

After add new file to your local git
	git add .
	git commit -am "Add, Fix "

Then send your code to remote directory

	git push origin develop

If you want compare two branch 
	git diff <source_branch> <target_branch> 


2) How to manage branch - global
----------------------------------

First, you have to check all informations about your branch
	
	git branch -a

Add a new branch 
	
	git branch [name_of_your_new_branch]

Add a new branch and jump it

	git checkout -b [name_of_your_new_branch]

Merge a branch
	
	git checkout branch-orgine
	git merge --no-ff new-branch

Using --no-ff, means that you keep information about this branch even after delete

Remove a branch

	git branch -d branch



2) Manage branch - Feature (only develop branch)
----------------------------------------------

So first, you have to create a new branch. By convention, feature-xxx (xxx means version number like 1.2)

	git checkout -b feature-xxx develop 

When your modifications are over, merge push and delete this temporary branch

	git checkout develop
	git merge --no-ff feature-xxx 

	git branch -d feature-xxx 
	git push origin develop


3) Manage branch - Release (master or dev branch)
--------------------------------------------------

This branch is usefull to manage versioning on your apps.

So first, you have to create a new branch. By convention, release-xxxX (xxxX means version number like 1.2)

	git checkout -b release-xxxx 

When your modifications are over, merge push and delete this temporary branch

	bump-version.sh xxx
	git commit -a -m "Bumped version number to xxx"

	git checkout master
	git merge --no-ff release-xxx
	
	git tag -a xxx 'the Release xxx with ....'

	git checkout develop
	git merge --no-ff release-xxx

	git branch -d release-xxx


bump-version.sh is a file using to set the version number on your app (add code on readme and add tag)


4) Manage branch - Hotfix (master or dev branch)
--------------------------------------------------

This branch is usefull to fix fastly some critical bug for production.

So first, you have to create a new branch. By convention, hotfix-xxxX (xxxX means version number like 1.2.1)

	git checkout -b hotfix-xxxx 

When your modifications are over, merge push and delete this temporary branch

	git checkout -b hotfix-1.2.1 master

	./bump-version.sh 1.2.1
	git commit -a -m "Bumped version number to 1.2.1"

	git commit -m "Fixed severe production problem"

	git checkout master
	git merge --no-ff hotfix-1.2.1
	git tag -a 1.2.1 -m 'the Hotfix 1.2.1 with ....'


	git checkout develop
	git merge --no-ff hotfix-1.2.1
	git branch -d hotfix-1.2.1


5) Manage tag
--------------------------------------------------

List all tags on the repo

	git tag

Add new tag on a branch 

	git tag -a 1.0.0-alpha -m 'the initial release'
	git push origin --tags

This command if you dont have information, tag will be automaticaly generated by git.
git push origin : tempTag
