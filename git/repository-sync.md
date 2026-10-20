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

Create an empty repository on your Git hosting service, then add its clone URL:

```sh
git remote add origin <repository-url>
git branch -M main
git push -u origin main
```

Replace `<repository-url>` with the repository's HTTPS or SSH URL. `origin` is the conventional name for the remote. `-u` sets the upstream so later pushes and pulls can use the current branch by default. On another machine, clone the remote with `git clone <repository-url>`; afterwards use `git pull` to receive updates and `git push` to publish committed changes.

Never commit access tokens, private keys, or credential-bearing URLs. Authentication should use the hosting provider's supported credential manager or SSH setup.
