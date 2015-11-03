Global Config

git config --global user.name "FirstName LastName"
git config --global user.email youremail@domain.extension

Use ssh key, 

Project Structure

- master
- develop
- feature-xxx
- release-xxx
- hotfixes-xxx

Convention name for versionning

1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0

Starter 

git clone git@github.com:yourrepo/yourprojectname.git





Commit 





Branch Management 

//Show all Branch
git branch -a


//Dev side - add feature (only dev branch)


///create

git checkout -b feature-xxx develop 
//Switched to a new branch "feature-xxx "

///merge

git checkout develop
//Switched to branch 'develop'

git merge --no-ff feature-xxx 
//Updating ea1b82a..05e9557 (Summary of changes)

git branch -d feature-xxx 
//Deleted branch feature-xxx  (was 05e9557).

git push origin develop




//Master side - add release (master and dev branch)
Usefull to pass in production

///create 

git checkout -b release-xxx 
//Switched to a new branch "release-xxx"

bump-version.sh xxx
//Files modified successfully, version bumped to xxx.

git commit -a -m "Bumped version number to xxx"
//[release-1.2 74d9424] Bumped version number to xxx
//1 files changed, 1 insertions(+), 1 deletions(-)

///merge - master

git checkout master
//Switched to branch 'master'

git merge --no-ff release-xxx
//Merge made by recursive.
//(Summary of changes)

git tag -a xxx

///merge - develop
git checkout develop
git merge --no-ff release-1.2

//Remove branch
git branch -d release-1.2
//Deleted branch release-1.2 (was ff452fe).


//Master side - add hotfix (master and dev branch)
Usefull to fix quickly a bug in production

///Create 

git checkout -b hotfix-1.2.1 master
//Switched to a new branch "hotfix-1.2.1"

./bump-version.sh 1.2.1
//Files modified successfully, version bumped to 1.2.1.

git commit -a -m "Bumped version number to 1.2.1"
//[hotfix-1.2.1 41e61bb] Bumped version number to 1.2.1

git commit -m "Fixed severe production problem"

git checkout master

git checkout master
//Switched to branch 'master'

git merge --no-ff hotfix-1.2.1
//Merge made by recursive.
//(Summary of changes)

git tag -a 1.2.1


git checkout develop
//Switched to branch 'develop'

git merge --no-ff hotfix-1.2.1
//Merge made by recursive.

git branch -d hotfix-1.2.1
//Deleted branch hotfix-1.2.1 (was abbe5d6).


Tag

git tag -a 1.0.0-alpha -m 'the initial release'
git push origin --tags
git push origin : tempTag

git tag