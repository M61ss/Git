## Authenticate via GitHub CLI

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

## Autenticate via SSH

Alternatively, you can create a key pair and use it to authenticate to GitHub. This procedure is **particularly useful when working on remote servers**, like HPC clusters. Follow these steps:

1. Generate a new SSH key pair on the cluster (skip this step if you already have one you want to use):

    ```bash
    ssh-keygen -t ed25519 -C "your-email@example.com" -f ~/.ssh/id_ed25519_github
    ```

    You can press Enter to leave the passphrase empty, or set one if you prefer extra security.

2. Add the key to the SSH agent (if available):

    ```bash
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_ed25519_github
    ```

    You may need to add those lines to your `.bashrc` in order to not repeat that operation for every login (if you set a passphrase for your key, you will need to insert that at every login).

3. Copy the public key:

    ```bash
    cat ~/.ssh/id_ed25519_github.pub
    ```

4. Add the key to your GitHub account: go to **Settings → SSH and GPG keys → New SSH key**, and paste the content you just copied. Alternatively, it is possible to add the key to the single repository: go to **Settings → Deploy keys → Add deploy key**.

5. If you used a custom file name for the key, configure `~/.ssh/config` so that Git knows which key to use for GitHub:
    
    ```txt
    Host github.com
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_ed25519_github
    ```

6. Clone your repo using: 

    ```bash
    git clone git@github.com:your-username/your-repo.git
    ```

    If you already cloned your repo, you can switch its remote from HTTPS to SSH:

    ```bash
    git remote set-url origin git@github.com:your-username/your-repo.git
    ```

7. Test the connection and push:

    ```bash
    ssh -T git@github.com
    git push
    ```

    Note: if the device you are working on does not have direct internet access (which is common on HPC clusters), you may need to run the push from the login node instead.
