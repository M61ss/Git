## Turn a folder into a Git repository

Initialize a folder as Git repository:

```bash
git init <repository>
```

This command will create ann hidden folder called `.git`. Inside it you can find all information you need about your repository, such as `config` file.

## Cloning a remote repository to local machine

Clone on your local machine a remote repository:

```bash
git clone <url-remote-repository>
```

## Git status

Know the current status of the repository in the current branch (name of current branch, changes and changes ready to commit):

```bash
git status
```

For a more compact view:

```bash
git status -s
```

Where `-s` stands for "short".

## Commit

A commit is a snapshot of your project taken at the time that you submit that.
\
Commit added changes:

```bash
git commit -m "Commit message"
```

It is mandatory to write a short meaningful message that describe what your changes affect.
\
If you don't specify `-m` followed by your message like that:

```bash
git commit
```

Git will open the default editor that you specified in the configuration (otherwise, it will open another text editor chosen by itself) and it will wait until you edited, then closed the file `COMMIT_EDITMSG`. In this case, you have the possibility to write a short description (corresponding to the message given from command-line), but also a long description separating lines like that:

```bash
Short description

Long description
```

All lines which starts with `#` will be ignored.

Let's learn how to add or remove file to commit.

## Add file to commit

Add files to commit:

```bash
git add <file1> <file2> <...>
```

It is also possible to use metacharacters to match multiple files.
\
For example:

```bash
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
Do not get confused by syntax: it is true that when you use the `git add` command, it seems that you are adding files every time to the staging area, but it is not exactly what it is happening. Actually, if you already added a new file previously, then subsequently you are adding **changes** applied to it, because it as an entity was already located in the staging area. It is a basic notion to understand how `.gitignore` works.

Get a compact list of files contained inside the staging area:

```bash
git ls-files
```

> [!WARNING]
> If you modify the `.gitignore` file, Git keeps tracking changes, so, if you accidentally added files to ignore into staging area, you have to remove those from there (read in the section below to get to know how to remove that from there).

If you don't need to keep one or more files unstaged, so you can use this fast command:

```bash
git commit -am "Commit message"
# or, if you need to add a long description using the editor
git commit -a
```

## Diff tool

Know what changes has been applied to files that we have in the staging area the is going in the next commit:

```bash
git diff --staged
```

Let's see an example output:

```bash
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

This way to display changes organize them into blocks that starts with `@@ -columns,rows +columns,rows @@` where `-columns,rows` indicates how many columns and rows the modified block had before changes, then `+columns,rows` show the number of columns and rows that the block will have if changes will be accepted.

Know changes that we haven't added to the staging area:

```bash
git diff
```

If you don't want to get mad, consider to install a GUI Git implementation to check more easily changes. You can config a default editor to inspect modifications runnig these commands:

```bash
git config --global diff.tool vscode
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
```

Where the first command gives to `difftool` the arbitrary name "vscode" and the second one sets the command to run in the shell when `git diff` command will be run. `--diff` option specify that you need to run VS Code in diff mode, `$LOCAL` and `$REMOTE` environment variables contain respectively old and new copies of files.
\
Verify every time that configuration is correct using `git config --global -e`.

Use the just configured `difftool` to check changes:

```bash
git difftool --staged
# or
git difftool
```

## Restore

Restore a file from the staging area to the working directory:

```bash
git restore --staged <file1> <file2> <...>
# or using patterns
git restore --staged *.txt
# or you can restore the entire directory
git restore --staged .
```

Discard changes in working directory (restore a file to its status since last commit):

```bash
git restore <file1> <file2> <...>
# or using patterns
git restore *.txt
# or you can restore the entire directory
git restore .
```

Another equivalent command (not recommended, see troubleshooting section):

```bash
git checkout -- <file>
```

All changes made on that file since last commit will be all deleted.

> [!WARNING]
> If you are adding a file for the first time (so it is untracked), Git doesn't have a previous version of it, so it will be left untouched. If you want to remove that, you can use the command:
>
> ```bash
> git clean
> # probably it will prompt an error message because the operation is unsafe
> # so, if you are sure of what you are doing, type this command
> git clean -fd
> ```
>
> Where `-f` expands in `--force` to give avoid the error message and `-d` stands for "directory", so directory will be removed too.

Restore a file to one of its previous snapshot:

```bash
git restore --source=<branch>~n <file>
```

## Remove a file

Removing a file it is a bit complicated because you need to be so careful looking the place from which you are removing that file, then consequences of your actions between working directory, staging area and repository.

Delete a file from working directory:

```bash
git rm <file1> <file2> <...>
# or using patterns
git rm *.txt
# or deleting a directory
gir rm -r <dir>
```

Where `-r` stands for "recursive".

> [!WARNING]
> Using this command you are deleting the file from both working directory and staging area. If you want to remove that only from working directory, you must use classical commands of your system shell.

To remove files from a repository, you need to add changes (this case they are delete operations) to the staging area, then commit.

Remove a file from the staging area:

```bash
git rm --cached <file>
# or (for directory)
git rm -r --cahced <dir>
```

> [!WARNING]
> The old name of the staging area is **index**. So, if you find in a documentation this term, remember that it refers to staging area.

## Repository history

Get the commits's history (sorted from the latest to the earliest):

```bash
git log
```

Reverse the sort order:

```bash
git log --reverse
```

Get a more compact view:

```bash
git log --oneline
```

Every commit is identified by a SHA. It is useful, for example, to restore the repository to a older commit. See next sections to learn more about that.

## Show commit

Show changes that has been produced into a specific commit:

```bash
git show <SHA>
# or
git show HEAD~n
# to have a quick look to changes of latest commit
git show HEAD
```

Where `HEAD` is by default a pointer to the latest commit and `n` must to be an integer that specify of how many commits do you want to go back.

If you don't want to see differences, but only the final file version, type this command:

```bash
git show HEAD~n:filepath
```

Where the scope of `filepath` starts at the repository's main directory.

Show the entire directory tree of a repository:

```bash
git ls-tree HEAD~n
```

In the output files will be made as `blob` and directories as `tree`. Take a look to the section below to learn about Git objects.

## Git objects

Git is a database that has its own objects. These are:

- Commits;
- Blobs (files);
- Trees (directories);
- Tags.

So frequently you will run into this strange terminology.

## Add remote repository

If you cloned your local repository from a remote one, you don't need to use this command, the origin will be set by default at the url used to clone.

Otherwise, add a remote repository as "origin":

```bash
git remote add origin <url-remote-repository>
```

It is true that you can use an arbitrary name instead of "origin"... but why? At your own risk.

## Push & pull

Push local commits on main to origin for the first time (this command is needed only in some cases):

```bash
git push -u origin <url-remote-repository>
```

Where `-u` expands in `--set-upstream`.

Push local commits to origin:

```bash
git push
```

Push branch's local commits to origin (only if doesn't exists a remote branch with the same name):

```bash
git push origin <branch>
```

If exists a remote branch with the same name and your intention is to push on that, run simply `git push`.

Pull changes from origin to your local main:

```bash
git pull
```
