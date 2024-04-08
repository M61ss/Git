# Git branches

Git branches are very important to cooperate with other peoples or to safe develop your repository without damage the main branch.

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

Where `-t` expands in `--track`.

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