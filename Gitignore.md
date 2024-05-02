# What is .gitignore

`.gitignore` file is a special hidden file very important working on a repository where you are developing a software. It tell to Git what files to ignore from tracking changes.
\
For example, a lot of IDE create folders with temporary or configuration files which is convenient to ignore during tracking operations to keep clean the interface.

## Creating .gitignore

Create a new file and call it `.gitignore`. Then, to ensure that it has effect, add it to the staging area, then commit.

## Modify .gitignore

To modify this file you can use whatever text editor you want. If you use VS Code and you don't want to leave the command-line, you can run this command:

```bash
code .gitignore
```

## Handle staged files

If you add to the `.gitignore` one or more files that you already added to the staging area, Git keeps to track them. To stop it tracking them, you need to remove these files from the staging area. In the `CLI_GIT.md` file is explained how to do that in the **"Remove a file"** section.

## Formatting .gitignore

The format of `.gitignore` is completly arbitrary according with your needs, but exist a lot of templates that you can use as `.gitignore` for your project. Infact, it is common that a project share some charateristics with others. For example, if you are working with Visual Studio, you can download from [this GitHub repository](https://github.com/github/gitignore) a template from Visual Studio's project.
\
After have been downloaded the desired file, copy the content, then past it into your `.gitignore` file.
