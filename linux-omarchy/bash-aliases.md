# Bash aliases

Add aliases to `~/.bashrc` to give frequently used commands shorter names. For example:

```bash
alias lg='lazygit'
alias ld='lazydocker'
```

Load the updated file in the current terminal with:

```bash
source ~/.bashrc
```

After that, `lg` runs `lazygit` and `ld` runs `lazydocker`. The underlying programs still need to be installed and available in `PATH`. These are suggested instructions; no `.bashrc` change was made as part of the original help request.
