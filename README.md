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