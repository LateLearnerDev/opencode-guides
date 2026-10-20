# Managing tmux plugins with TPM

The **Tmux Plugin Manager (TPM)** installs and loads plugins declared in the tmux configuration. Keep plugin declarations in `~/.config/tmux/tmux.conf` (or the config file you actually load) and initialize TPM after those declarations:

```tmux
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-resurrect'

# Keep TPM initialization at the end of the config
run '~/.tmux/plugins/tpm/tpm'
```

TPM is the manager; `tmux-resurrect` saves and restores tmux sessions, windows, panes, and (optionally) running programs. The plugin list above reflects the available configuration on this machine; add or remove plugin declarations to suit your setup. Install TPM itself by following its upstream installation instructions, then install declared plugins from inside tmux with the TPM prefix followed by `I` (uppercase i). Use prefix + `U` to update plugins.

After changing plugin declarations, reload the tmux config (for example, `tmux source-file ~/.config/tmux/tmux.conf`) and run the install binding. Plugin-specific options can be added as `set -g @resurrect-* ...` settings before TPM initialization.
