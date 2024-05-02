# Git configuration

You can configure your Git default settings with 3 different scopes:

- `--system`: all users and their repositories using that machine inherit specified settings;
- `--global`: all repositories of the current user inherit specified settings. If there were already set different settings at system level, please note that global level has priority on those.
- `--local`: the current working repository get specified settings. Local level has priority on system and global levels.

Most used mid-user Git configuration is:

```bash
git config --global user.name "yourusername"
git config --global user.email youremail@gmail.com
git config --global core.editor "code --wait"
```

Where `core.editor` is used to set the default editor. This case I am using Visual Studio Code. For use an editor this way, you have to added it to PATH when you installed that or you should add it before run this command.

**What is `"code --wait"`?**
\
`code` is the command to give to the shell to normally run VS Code (if you added it to PATH). In this case you need to specify the option `--wait` because you have to tell to the shell to wait until you close the new VS Code instance that will be open whenever Git needs an operation of text editing.

## Edit global default settings

After setting up the default Git editor, it is possible to manage more easily Git's settings running this command:

```bash
git config --global -e
```

As you can see trying this command on your machine, when you open a file running a Git command, Git wait the closure of that before starting to work again. This feature is given by the optioin `--wait` as you said a little while ago.

You can verify yourself that Git's settings that appears on the file opened by this command are only those you have already modified at least one time using command line, so this method is useful only if you want to modify or check some settings that, for example, you want to change or you don't remember.

## Handle end of lines

Assuming that CRLF stands for "Carriage Return Line Feed", you can guess what setting `core.autocrlf` refers to.
\
It is very important to set correctly this default setting because it give to Git the ability to translate Windows's carriage return (\n\r) into macOS/Linux's carriage return (\n) and vice versa. Without this option, it can be mistakes when two machines that use different types of carriage return modify the same file. Git fix end of lines consistently with the type of carriage return you specify that your OS supports.

You can set this option running the following command:

```bash
git config --global core.autocrlf true       # for Windows
git config --global core.autocrlf input      # for macOS/Linux
```

## Other configuration options

To know other configuration options available, you can examine the manual page using:

```bash
git config --help
```

Or command-line quick help using:

```bash
git config -h
```