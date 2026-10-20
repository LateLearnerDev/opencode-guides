# Creating and synchronizing a guide repository

## Initialize a local repository

From the folder to track, initialize Git and make the first commit:

```sh
git init
git add .
git commit -m "Initial guides"
```

`git init` creates local repository metadata. `git add .` stages files in the current folder. `git commit` saves the staged snapshot with a descriptive message.

## Connect a remote and sync

You can create the remote repository in GitHub's website, or use the GitHub CLI (`gh`). From the local repository folder, for example:

```sh
gh repo create opencode-guides --private --source=. --remote=origin --push
```

This creates a private GitHub repository named `opencode-guides`, uses the current directory as the local source, adds it as remote `origin`, and pushes the current branch. Use `--public` instead of `--private` only if you want the guide files visible to everyone. The `gh` CLI must be installed and authenticated first.

Alternatively, create an empty repository on the hosting website, then add its clone URL:

```sh
git remote add origin <repository-url>
git branch -M main
git push -u origin main
```

Replace `<repository-url>` with the repository's HTTPS or SSH URL. `origin` is the conventional name for the remote. `-u` sets the upstream so later pushes and pulls can use the current branch by default. On another machine, clone the remote with `git clone <repository-url>`; afterwards use `git pull` to receive updates and `git push` to publish committed changes.

Never commit access tokens, private keys, or credential-bearing URLs. Authentication should use the hosting provider's supported credential manager or SSH setup.
