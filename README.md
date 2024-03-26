# CLI Git
This is a fast guide to use cli git. It is also useful to learn how to use a lot of graphical interfaces because they use a very similar terminology to describe available operations with git. An example of complete and easy to use graphical interface is GitHub Desktop.

To get sure if git is installed or not, run this command:
```
git --version
```
If the output is the git version, you have git. Otherwise, you need to install that.
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
git clone <url-remote-repository>
```
## Git status
Know the current status of the repository in the current branch (name of current branch, changes and changes ready to commit):
```
git status
```
## Add or remove file to commit
Add a file to commit:
```
git add <file>
```
Remove file from a commit:
```
git reset <file>
```
## Discard changes
Discard changes in working directory (restore a file to its status since last commit):
```
git restore <file>
```
Another equivalent command (not recommended*):
```
git checkout -- <file>
```
All changes made on that file since last commit will be all deleted.
## Commit
Commit added changes:
```
git commit -m "Commit message"
```
## Add remote repository
If you cloned your local repository from a remote one, you don't need to use this command, the origin will be set by default at the url used to clone.

Otherwise, add a remote repository as "origin":
```
git remote add origin <url-remote-repository>
```
It is true that you can use an arbitrary name instead of "origin"... but why? At your own risk.
## Push & pull
Push local commits on main to origin for the first time (this command is needed only in some cases):
```
git push -u origin <url-remote-repository>
```
Where ```-u``` expands in ```--set-upstream```.

Push local commits to origin:
```
git push
```
Push branch's local commits to origin (only if doesn't exists a remote branch with the same name):
```
git push origin <branch>
```
If exists a remote branch with the same name and your intention is to push on that, run simply ```git push```.

Pull changes from origin to your local main:
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
git checkout -t origin/<branch>
```
Where ```-t``` expands in ```--track```.
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