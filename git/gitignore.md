# Ignoring Files and Folders with Git

Use a `.gitignore` file to keep generated files, local settings, and other untracked content out of normal Git status and staging workflows. Repository-wide patterns belong in the repository-root `.gitignore`; machine-specific patterns that should not be shared can go in `.git/info/exclude` or a configured global ignore file.

## Ignore a Folder at the Repository Root

Add a root-anchored pattern to `.gitignore`:

```gitignore
/folder-name/
```

The leading `/` limits the match to that folder at the repository root. Without it, Git can match directories with the same name at other levels. Replace `folder-name` with the directory to ignore.

For example, to keep a machine-specific `erazer-laptop/` folder local, use:

```gitignore
/erazer-laptop/
```

## Verify Which Rule Matches

Run `git check-ignore -v` with a path inside the folder:

```sh
git check-ignore -v folder-name/README.md
```

Git prints the ignore file, line number, and pattern responsible for ignoring the path. Use `git check-ignore -v --no-index <path>` when diagnosing a path that is already tracked.

## Ignore Files That Are Already Tracked

`.gitignore` only affects untracked files. To stop tracking an already committed folder while keeping its local files, remove it from the Git index:

```sh
git rm -r --cached folder-name
```

Replace `folder-name` with the tracked directory. Commit the resulting index change so other clones also stop tracking those files. The local working copy remains on disk.
