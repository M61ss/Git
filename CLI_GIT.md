# CLI Git
This is a fast guide to use cli Git. Writing this module I assume that you have already an idea of what is Git and its purpose, but you are confused about its working and benefits.

It is also useful to learn how to use a lot of graphical interfaces because they use a very similar terminology to describe available operations with Git. An example of complete and easy to use graphical interface is GitHub Desktop.

To get sure if Git is installed, run this command:
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

**What is ```"code --wait"```?**
\
```code``` is the command to give to the shell to normally run VS Code (if you added it to PATH). In this case you need to specify the option ```--wait``` because you have to tell to the shell to wait until you close the new VS Code instance that will be open whenever Git needs an operation of text editing.
## Edit global default settings
After setting up the default Git editor, it is possible to manage more easily Git's settings running this command:
```
git config --global -e
```
As you can see trying this command on your machine, when you open a file running a Git command, Git wait the closure of that before starting to work again. This feature is given by the optioin ```--wait``` as you said a little while ago.

You can verify yourself that Git's settings that appears on the file opened by this command are only those you have already modified at least one time using command line, so this method is useful only if you want to modify or check some settings that, for example, you want to change or you don't remember.
## Handle end of lines
Assuming that CRLF stands for "Carriage Return Line Feed", you can guess what setting ```core.autocrlf``` refers to. 
\
It is very important to set correctly this default setting because it give to Git the ability to translate Windows's carriage return (\n\r) into macOS/Linux's carriage return (\n) and vice versa. Without this option, it can be mistakes when two machines that use different types of carriage return modify the same file. Git fix end of lines consistently with the type of carriage return you specify that your OS supports.

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
This command will create ann hidden folder called ```.git```. Inside it you can find all informations you need about your repository, such as ```config``` file.
## Cloning a remote repository to local machine
Clone on your local machine a remote repository:
```
git clone <url-remote-repository>
```
## Git status
Know the current status of the repository in the current branch (name of current branch, changes and changes ready to commit):
```
git status
```
For a more compact view:
```
git status -s
```
Where ```-s``` stands for "short".
## Commit
A commit is a snapshot of your project taken at the time that you submit that.
\
Commit added changes:
```
git commit -m "Commit message"
```
It is mandatory to write a short meaningful message that describe what your changes affect.
\
If you don't specify ```-m``` followed by your message like that:
```
git commit
```
Git will open the default editor that you specified in the configuration (otherwise, it will open another text editor chosen by itself) and it will wait until you edited, then closed the file ```COMMIT_EDITMSG```. In this case, you have the possibility to write a short description (corrisponding to the message given from command-line), but also a long description separating lines like that:
```
Short description

Long description
```
All lines which starts with ```#``` will be ignored.

Let's learn how to add or remove file to commit.
## Add file to commit
Add files to commit:
```
git add <file1> <file2> <...>
```
It is also possible to use metacharacters to match multiple files.
\
For example:
```
git add *
# or using patterns
git add *.txt
# or you can add the entire directory
git add .
```
## Staging area
When you add a new file or its changes to commit, you are putting them into the **staging area**.
\
It is a mid-area, between the current status of the repository (this status is called **working directory**) and the condition of it since last commit, where you must put all files or their changes which you decided to get into your next commit.
\
If you want to add some files or their changes to your next commit, you must stage them. This means that file changes are located into the working directory, but they are not put automatically in staging area.
\
It is important to notice that, if the file has been already staged at least once previously (so in this case it is called "**tracked**", otherwise "**untracked**"), it will be kept into the staging area as well as we added to it last time. Its changes will not be added until we add them instead.
\
Do not get confused by syntax: it is true that when you use the ```git add``` command, it seems that you are adding files everytime to the staging area, but it is not exaclty what it is happening. Actually, if you already added a new file previously, then subsequently you are adding **changes** applied to it, because it as an entity was already located in the staging area. It is a basic notion to understand how ```.gitignore``` works.

Get a compact list of files contained inside the staging area:
```
git ls-files
```
*Warning*: if you modify the ```.gitignore``` file, Git keeps tracking changes, so, if you accidentally added files to ignore into staging area, you have to remove those from there (read in the section below to get to know how to remove that from there).

If you don't need to keep one or more files unstaged, so you can use this fast command:
```
git commit -am "Commit message"
# or, if you need to add a long description using the editor
git commit -a
```
## Diff tool
Know what changes has been applied to files that we have in the staging area the is going in the next commit:
```
git diff --staged
```
Let's see an example output:
```
diff --git a/file1 b/file1
index badfb70..47c3216 100644
--- a/file1     # --- indicates that is the old version of the file
+++ b/file1     # +++ indicates that is the new version of the file
@@ -1,3 +1,5 @@     # - indicates the block size before changes, + after them. The format is: columns,rows.
 this
 file
 test
+another    # Here you can see changes (+ if has been added something, - if remove)
+word
```
This way to display changes organize them into blocks that starts with ```@@ -columns,rows +columns,rows @@``` where ```-columns,rows``` indicates how many columns and rows the modified block had before changes, then ```+columns,rows``` show the number of columns and rows that the block will have if changes will be accepted.

Know changes that we haven't added to the staging area:
```
git diff
```

If you don't want to get mad, consider to install a GUI Git implementation to check more easily changes. You can config a default editor to inspect modifications runnig these commands:
```
git config --global diff.tool vscode 
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
```
Where the first command gives to the difftool the arbitrary name "vscode" and the second one sets the command to run in the shell when ```git diff``` command will be run. ```--diff``` option specify that you need to run VS Code in diff mode, ```$LOCAL``` and ```$REMOTE``` environment variables contain respectively old and new copies of files.
\
Verify everytime that configuration is correct using ```git config --global -e```.

Use the just configured difftool to check changes:
```
git difftool --staged
# or
git difftool
```
## Restore
Restore a file from the staging area to the working directory:
```
git restore --staged <file1> <file2> <...>
# or using patterns
git restore --staged *.txt
# or you can restore the entire directory
git restore --staged .
```
Discard changes in working directory (restore a file to its status since last commit):
```
git restore <file1> <file2> <...>
# or using patterns
git restore *.txt
# or you can restore the entire directory
git restore .
```
Another equivalent command (not recommended, see troubleshooting section):
```
git checkout -- <file>
```
All changes made on that file since last commit will be all deleted.

*Warning*: if you are adding a file for the first time (so it is untracked), Git doesn't have a previous version of it, so it will be left untouched. If you want to remove that, you can use the command:
```
git clean
# probably it will prompt an error message because the operation is unsafe
# so, if you are sure of what you are doing, type this command
git clean -fd
```
Where ```-f``` expands in ```--force``` to give avoid the error message and ```-d``` stands for "directory", so directory will be removed too.

Restore a file to one of its previous snapshot:
```
git restore --source=<branch>~n <file>
```
## Remove a file
Removing a file it is a bit complicated because you need to be so careful looking the place from which you are removing that file, then consequences of your actions between working directory, staging area and repository. 

Delete a file from working directory:
```
git rm <file1> <file2> <...>
# or using patterns
git rm *.txt
# or deleting a directory
gir rm -r <dir>
```
Where ```-r``` stands for "recursive".

*Warning*: using this command you are deleting the file from both working directory and staging area. If you want to remove that only from working directory, you must use classical commands of your system shell.

To remove files from a repository, you need to add changes (this case they are delete operations) to the staging area, then commit.

Remove a file from the staging area:
```
git rm --cached <file>
# or (for directory)
git rm -r --cahced <dir> 
```
*Warning*: the old name of the staging area is **index**. So, if you find in a documentation this term, remember that it refers to staging area.
## Repository history
Get the commits's history (sorted from the latest to the earliest):
```
git log
```
Reverse the sort order:
```
git log --reverse
```
Get a more compact view:
```
git log --oneline
```
Every commit is identified by a SHA. It is useful, for examle, to restore the repository to a older commit. See next sections to learn more about that.
## Show commit
Show changes that has been apported into a specific commit:
```
git show <SHA>
# or
git show HEAD~n
# to have a quick look to changes of lastest commit
git show HEAD
```
Where ```HEAD``` is by default a pointer to the lastest commit and ```n``` must to be an integer that specify of how many commits do you want to go back.

If you don't want to see differences, but only the final file version, type this command:
```
git show HEAD~n:filepath
```
Where the scope of ```filepath``` starts at the repository's main directory.

Show the entire directory tree of a repository:
```
git ls-tree HEAD~n
```
In the output files will be maked as ```blob``` and directories as ```tree```. Take a look to the section below to learn about Git objects. 
## Git objects
Git is a database that has its own objects. These are:
* Commits;
* Blobs (files);
* Trees (diretories);
* Tags.

So frequently you will run into this strange terminology.
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

It is also often used the ```Git checkout``` command to do many different actions between branches, so it is easy to get confused using that. However, you must remember these instructions because a lot of graphical Git integration use ```checkout``` keyword referring, for example, to the branch switch operation.

**How much big has to be a commit?**

The answer is not easy to define, but please do not be so psychopath to make a commit for every 3 lines that you change in your file. At the same way it is fool to commit once a year, potentially after changing 1 milion lines of code.
\
It is a good practice commit when is meaningful to do that. For example, if you are working on a website, it is logical to commit after building the intestation, then another commit can be about the body, another about webpage animations, etc.

If you would to define a rule, you could say that is useful to commit when you reached a state of the project that you want to record.
\
Working this way it is useful to have the possibility to go back to a previous software version for many reasons. For example, you reached an impasse and have been apported too much changes to use simply CTRL+Z (command+z), so you want to return to a stable version of the software.

**Why should I keep some file unstaged while I am committing?**

It is very important to do commits with a logical sense. So, if you work on more block of code that each one has a distinct function into the software you are working on, it is strongly recommended to commit severaly changes applied on each block. The only way to do this is to add to the commit files of the block ready to commit, so to keep others **unstaged**, then do the first commit.

**It is necessary to type the entire commit's SHA?**

No.
\
It is uneasy to type the entire SHA of a commit, so it is possible to type fewer characters as long as  we don't have another commit that match with them.

**How can I get Git interface prettier?**

First of all, consider to use a GUI Git implementations, such as GitHub Desktop, Visual Studio Code or Visual Studio Git integration, etc. (a lot of IDE or editors integrate Git).
\
However, if you want to get command-line Git prettier you can install, on Windows, posh-git or, on Mac, Zhs with Git plugin (posh-git at 58% Coverage... maybe unstable? Be careful).