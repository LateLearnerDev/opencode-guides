# Backing Up and Automatically Restoring tmux-resurrect

`tmux-resurrect` keeps its current saved environment in a save directory; a new save replaces the current saved state. Keep dated copies of that directory if you want protection from an accidental save. Common default paths vary by plugin version; check `@resurrect-dir` and the actual save directory before copying. The current setup on this machine uses `~/.local/share/tmux/resurrect`.

Create a snapshot before a risky save (replace the source path if your setup uses a different save directory):

```sh
cp -a ~/.local/share/tmux/resurrect "$HOME/.local/share/tmux/resurrect-backup-$(date +%Y%m%d-%H%M%S)"
```

`cp -a` preserves file metadata, and the timestamp gives each backup a unique name. Replace the source and destination base paths if your setup uses a different location. To recover, stop tmux, copy the chosen backup's contents back into the configured resurrect save directory, and then start tmux and restore.

## Restore automatically at startup

The `tmux-continuum` plugin can automatically restore the last saved environment, so you do not need to press the restore binding when tmux starts. With TPM, add it after resurrect in `~/.tmux.conf`:

```tmux
set -g @plugin 'tmux-plugins/tmux-resurrect'
set -g @plugin 'tmux-plugins/tmux-continuum'
set -g @continuum-restore 'on'
```

Install/update plugins with the TPM install binding (usually `prefix` + `I`), or reload tmux configuration. Automatic restore uses the latest save; it does not preserve older saves by itself, so keep dated backups separately. Check the plugin documentation for current defaults and behavior.
