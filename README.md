# CLI Git
This is a fast guide to use cli Git. It is also useful to learn how to use a lot of graphical interfaces because they use a very similar terminology to describe available operations with Git. An example of complete and easy to use graphical interface is GitHub Desktop.

To get sure if Git is installed or not, run this command:
```
git --version
```
If the output is the Git version, you have Git. Otherwise, you need to install that.
## Git configuration
You can configure your Git default settings with 3 different scopes:
* ```--system```: all users and their repositories using that machine inherit specified settings;
* ```--global```: all repositories of the current user inherit specified settings. If there were already set different settings at system level, please note that global level has priority on those.
* ```--local```: the current working repository get specified settings. Local level has priority on system and global levels.

Most used mid-user Git configuration is:
```
git config --global user.name "yourusername"
git config --global user.email youremail@gmail.com
git config --global core.editor "code --wait"
```
Where ```core.editor``` is used to set the default editor. This case I am using Visual Studio Code. For use an editor this way, you have to added it to PATH when you installed that or you should add it before run this command.

```code``` is the command to give to the shell to normally run VS Code (if you added it to PATH). In this case you need to specify the option ```--wait``` because we have to tell to the shell to wait until we close the new VS Code instance that will be open whenever Git needs an operation of text editing.
## Edit global default settings
After setting up the default Git editor, it is possible to manage more easily Git's settings running this command:
```
git config --global -e
```
As you can see, when you open a file running a Git command, Git wait the closure of that before starting to work again. This feature is given by the optioin ```--wait``` as we said a little while ago.

You can verify yourself that Git's settings that appears on the file opened by this command are only those you have already modified at least one time using command line, so this method is useful only if you want to modify or check some settings that, for example, you want to change or you don't remember.
## Handle end of lines
CRLF stands for "Carriage Return Line Feed". It is important to set correctly the default setting named ```core.autocrlf``` because it give to Git the ability to translate Windows's carriage return (\n\r) into macOS/Linux's carriage return (\n) and vice versa. Without this option, it can be mistakes when two machines that use different types of carriage return modify the same file. Git fix end of lines consistently with the type of carriage return we specify that our OS supports.

You can set this option running the following command:
```
git config --global core.autocrlf true       # for Windows
git config --global core.autocrlf input      # for macOS/Linux
```
## Other configuration options
To know other configuration options available, you can examine the manual page using:
```
git config --help
```
Or command-line quick help using:
```
git config -h
```
## Turn a folder into a Git repository
Initialize a folder as Git repository:
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
Another equivalent command (not recommended, see troubleshooting section):
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
Another equivalent command (not recommended, see troubleshooting section):
```
git checkout -b <new-branch>
```
Create a branch from an older commit (due some need):
```
git branch <new-branch-name> <SHA>
```
Where SHA is a code that uniquely identify a commit. That code is easily available on graphical Git interface, such as GitHub Desktop.

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
Another equivalent command (not recommended, see troubleshooting section):
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
## Troubleshooting
**Why some commands are marked as "not recommended"?**

It is also often used the ```Git checkout``` command to do many different actions between branches, so it is easy to get confused using that. However, we must remember these instructions because a lot of graphical Git integration use ```checkout``` keyword referring, for example, to the branch switch operation.

**How can I get command line Git interface prettier?**

To get command-line Git prettier you can install, on Windows, posh-git or, on Mac, Zhs with Git plugin (posh-git at 58% Coverage... maybe unstable? Be careful).