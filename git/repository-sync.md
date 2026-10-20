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

## Set up on another machine

After the remote exists and the first push has completed, clone it on the other machine:

```sh
git clone <repository-url> "$HOME/Documents/opencode-guides"
mkdir -p "$HOME/.config/opencode"
ln -s "$HOME/Documents/opencode-guides/AGENTS.md" "$HOME/.config/opencode/AGENTS.md"
```

`git clone` downloads the repository. `mkdir -p` creates the OpenCode config directory if needed. `ln -s` makes OpenCode's global instruction path point to the tracked file. If the target `~/.config/opencode/AGENTS.md` already exists, inspect it before linking rather than overwriting it. On later visits, run `git pull` inside the clone to receive updates.

Never commit access tokens, private keys, or credential-bearing URLs. Authentication should use the hosting provider's supported credential manager or SSH setup.

## Fix GitHub HTTPS authentication failures

GitHub no longer accepts account passwords for Git operations over HTTPS. An error such as `Invalid username or token` can also occur when the remote uses HTTPS but your GitHub CLI (`gh`) is configured for SSH. Check the remote and the CLI's selected protocol:

```sh
git remote -v
gh config get git_protocol
```

If `gh` reports `ssh`, change the remote to the matching SSH form, replacing the owner and repository with yours:

```sh
git remote set-url origin git@github.com:OWNER/REPOSITORY.git
git ls-remote origin HEAD
```

`git ls-remote` verifies that authentication and repository access work without changing local files. If you prefer HTTPS, authenticate `gh` for HTTPS with `gh auth login --hostname github.com --git-protocol https`, then run `gh auth setup-git` to configure Git to use the GitHub CLI credential helper. Keep tokens out of remote URLs and config files.
