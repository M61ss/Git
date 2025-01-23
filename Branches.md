# Git branches

Git branches are very important to cooperate with other peoples or to safe develop your repository without damage the main branch.

## Create a new branch

Create a new branch from the last commit:

```shell
git branch <new-branch>
```

Another equivalent command (not recommended, see troubleshooting section):

```shell
git checkout -b <new-branch>
```

Create a branch from an older commit (due some need):

```shell
git branch <new-branch-name> <SHA>
```

Where SHA is a code that uniquely identify a commit. That code is easily available on graphical Git interface, such as GitHub Desktop.

Create new local branch that keeps track of changes of a remote branch:

```shell
git checkout -t origin/<branch>
```

Where `-t` expands in `--track`.

## Publish branch

Publish a branch on the remote repository:

```shell
git push -u origin <local-branch>
```

## Switch between branch

The correct command to switch from a branch to the other is:

```shell
git switch <destination-branch>
```

Another equivalent command (not recommended, see troubleshooting section):

```shell
git checkout <destination-branch>
```

## Delete a branch

```shell
git branch -d <branch>
```

## Rename a branch

Rename the current working branch:

```shell
git branch -m <new-branch>
```

Rename a branch from any location:

```shell
git branch <old-branch> <new-branch>
```

Rename a remote branch:

```shell
git push origin --delete <old-branch>
git push -u origin <new-branch>
```
