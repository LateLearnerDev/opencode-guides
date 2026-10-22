# Removing an OpenCode Plugin

To disable a plugin, remove only its entry from the global OpenCode config at `~/.config/opencode/opencode.json`. Preserve unrelated settings and any other entries in the `plugin` array. For example, change:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "plugin-to-remove",
    "another-plugin"
  ]
}
```

to:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "another-plugin"
  ]
}
```

If the removed plugin was the only entry, remove the `plugin` property entirely. Then validate the JSON:

```bash
jq empty ~/.config/opencode/opencode.json
```

OpenCode caches installed plugin packages under `~/.cache/opencode/packages/`. Removing the config entry is sufficient to stop loading the plugin; optionally delete only that plugin's matching package-cache directory to reclaim space:

```bash
rm -r "$HOME/.cache/opencode/packages/<matching-plugin-package-directory>"
```

Replace the placeholder with the exact directory for that plugin, identified in `~/.cache/opencode/packages/`. Do not remove the entire OpenCode cache or unrelated package directories. If the directory contains nested URL-based path segments, use the complete path for the plugin package.

Quit and restart OpenCode after editing its config. The running process keeps plugins already loaded in memory until it exits.
