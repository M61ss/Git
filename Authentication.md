## Authenticate via CLI

If you try to push some changes to your private GitHub repositories, Git will ask you for credential, but, even if you provide the correct ones, it will fail.
\
It is possible to easily bypass this problem. Run:

```bash
sudo apt install gh
```

Where `gh` is GitHub CLI. It is necessary to authenticate.

Then, run:

```bash
gh auth login
```

Next, follow the instruction on the screen. When requested, I think it is better to choose HTTPS as authentication method.

Now, you can push whatever you want to your private GitHub repositories using regular Git commands.