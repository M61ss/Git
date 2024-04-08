# Troubleshooting

### Why some commands are marked as "not recommended"?

It is also often used the `Git checkout` command to do many different actions between branches, so it is easy to get confused using that. However, you must remember these instructions because a lot of graphical Git integration use `checkout` keyword referring, for example, to the branch switch operation.

### How much big has to be a commit?

The answer is not easy to define, but please do not be so psychopath to make a commit for every 3 lines that you change in your file. At the same way it is fool to commit once a year, potentially after changing 1 milion lines of code.
\
It is a good practice commit when is meaningful to do that. For example, if you are working on a website, it is logical to commit after building the intestation, then another commit can be about the body, another about webpage animations, etc.

If you would to define a rule, you could say that is useful to commit when you reached a state of the project that you want to record.
\
Working this way it is useful to have the possibility to go back to a previous software version for many reasons. For example, you reached an impasse and have been apported too much changes to use simply CTRL+Z (command+z), so you want to return to a stable version of the software.

### Why should I keep some file unstaged while I am committing?

It is very important to do commits with a logical sense. So, if you work on more block of code that each one has a distinct function into the software you are working on, it is strongly recommended to commit severaly changes applied on each block. The only way to do this is to add to the commit files of the block ready to commit, so to keep others **unstaged**, then do the first commit.

### It is necessary to type the entire commit's SHA?

No.
\
It is uneasy to type the entire SHA of a commit, so it is possible to type fewer characters as long as we don't have another commit that match with them.

### How can I get Git interface prettier?

First of all, consider to use a GUI Git implementations, such as GitHub Desktop, Visual Studio Code or Visual Studio Git integration, etc. (a lot of IDE or editors integrate Git).
\
However, if you want to get command-line Git prettier you can install, on Windows, posh-git or, on Mac, Zhs with Git plugin (posh-git at 58% Coverage... maybe unstable? Be careful).
