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
git init repository-name
```
## Cloning a remote repository from GitHub to local machine
Clone on your local machine a remote repository:
```
git clone https://github.com/owner-username/repository-name
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
git branch new-branch-name
```
Create a branch from an older commit (due some need):
```
git branch new-branch-name SHA
```
Where SHA is a code that uniquely identify a commit. That code is easily available on graphical git interface, such GitHub Desktop.