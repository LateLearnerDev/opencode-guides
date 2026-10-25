# Inspecting Symbolic Links

A symbolic link (symlink) is a filesystem entry that points to another path. Long-format directory listings show the target after `->`, for example:

```text
latest -> backup-20261025.txt
```

The arrow appears where the symlink itself lives. The destination is usually an ordinary file and will not show an arrow just because something links to it. A symlink does not create a second copy: opening and editing the link normally accesses the destination's contents. Removing or replacing the link itself is different from editing the destination.

Use these commands to inspect a link named `latest`:

```bash
readlink latest
```

Prints the path stored in the link. If the target is relative, it is interpreted relative to the directory containing the link.

```bash
realpath latest
```

Prints the resolved absolute path of the target. This is useful for confirming where the link leads; resolution may fail if the target does not exist.

```bash
ls -l latest
```

Shows the link and its target in long format. These commands inspect links; they do not change them.

To check whether a directory path itself is a symlink, inspect the path entry without following it:

```bash
ls -ld ~/.config/tmux
```

The `-d` option lists the directory entry itself rather than its contents. A leading `l` in the permissions indicates a symlink. By contrast, `ls -l ~/.config/tmux/` lists the directory's contents, where a symlinked file will be marked with `->`.

In a configuration managed from another directory, for example, `~/.config/tmux/tmux.conf -> ~/Projects/example/.config/tmux/tmux.conf`, the link is under `~/.config/tmux/` and the project file is its destination. Listings of the project destination show a regular file; they do not indicate that another path links to it. Terminal emulators such as Foot do not determine this—the `ls` command or shell alias controls the listing format.
