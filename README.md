# CLI Git
## Git configuration
Configure your global git credential:
```
git config --global user.email youremail@gmail.com
git config --global user.name "yourusername"
```
Configure your local git credential. That is to say reserved credential for the repository corrispondig to the current folder (these will not affect your global credential):
```
git config --local user.email youremail@gmail.com
git config --local user.name "yourusername"
```
## Turn a folder into a git repository
Initialize a folder as git repository:
```
git init <repository>
```
## Cloning a remote repository from GitHub to local machine
Clone on your local machine a remote repository:
```
git clone <https://github.com/owner-username/repository-name>
```
## Git status
Know the current status of the repository in the current branch (name of current branch and changes):
```
git status
```
## Push & pull
Push local commits to origin:
```
git push
```
Pull changes from origin to your local machine:
```
git pull
```
## Create a new branch
Create a new branch from the last commit:
```
git branch <new-branch>
```
Another equivalent command (not recommended*):
```
git checkout -b <new-branch>
```
Create a branch from an older commit (due some need):
```
git branch <new-branch-name> <SHA>
```
Where SHA is a code that uniquely identify a commit. That code is easily available on graphical git interface, such as GitHub Desktop.

Create new local branch that keeps track of changes of a remote branch:
```
git checkout --track origin/<branch>
```
or equivalently:
```
git checkout -t origin/<branch>
```
## Publish branch
Publish a branch on the remote repository:
```
git push -u origin <local-branch>
```
## Switch between branch
The correct command to switch from a branch to the other is:
```
git switch <destination-branch>
```
Another equivalent command (not recommended*):
```
git checkout <destination-branch>
```
## Rename a branch
Rename the current working branch:
```
git branch -m <new-branch>
```
Rename a branch from any location:
```
git branch <old-branch> <new-branch>
```
Rename a remote branch
```
git push origin --delete <old-branch>
git push -u origin <new-branch>
```

not recommended* = it is also often used the ```git checkout``` command to do many different actions between branches, so it is easy to get confused using that. However, we must remember these instructions because a lot of graphical git integration use ```checkout``` keyword referring, for example, to the branch switch operation.