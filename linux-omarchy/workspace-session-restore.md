# Restoring a Fixed Workspace Session at Login

Use a small user script and Hyprland's startup hook to reopen a chosen set of applications on fixed workspaces. This is a launch recipe, not a process snapshot: applications must use their own profile/session persistence to restore internal state.

## Configuration

In `~/.config/hypr/autostart.lua`, add:

```lua
o.launch_on_start("bash ~/.config/omarchy/session-restore.sh")
```

Create `~/.config/omarchy/session-restore.sh` and edit the workspace/command pairs for the apps you want:

```bash
#!/usr/bin/env bash

# Wait briefly for Hyprland IPC; don't block or disrupt login if it isn't ready.
for ((attempt = 0; attempt < 30; attempt++)); do
  if hyprctl -j monitors >/dev/null 2>&1; then
    break
  fi
  sleep 1
done

if ((attempt == 30)); then
  exit 0
fi

# Run at most once per Hyprland instance, including across config reloads.
marker="${XDG_RUNTIME_DIR:-/tmp}/omarchy-session-restore-${HYPRLAND_INSTANCE_SIGNATURE:-unknown}"
if ! mkdir "$marker" 2>/dev/null; then
  exit 0
fi

launch_on_workspace() {
  local workspace="$1"
  local command="$2"

  hyprctl eval "hl.dispatch(hl.dsp.exec_cmd(\"[workspace ${workspace} silent] ${command}\"))" >/dev/null 2>&1 || true
  sleep 1
}

# Example assignments; replace these apps and workspace numbers as needed.
launch_on_workspace 1 "omarchy launch browser"
launch_on_workspace 2 "foot --working-directory=$HOME -e opencode --auto"
launch_on_workspace 3 "chatgpt"
launch_on_workspace 6 "foot --app-id=org.omarchy.btop -e btop"
launch_on_workspace "special:scratchpad" "foot --app-id=omarchy-scratchpad --title=omarchy:nvim --working-directory=$HOME -e bash -lc 'tmux attach || tmux new -s Work'"
```

The example restores a browser, an OpenCode terminal, ChatGPT, btop, and a tmux-backed Neovim scratchpad. The `silent` workspace target places windows without switching the visible workspace. The scratchpad uses a dedicated Foot app ID and `special:scratchpad`, so it remains separate from normal terminals.

Make the script executable and validate it:

```bash
chmod +x ~/.config/omarchy/session-restore.sh
bash -n ~/.config/omarchy/session-restore.sh
hyprctl reload
hyprctl configerrors
```

The marker directory prevents another launch when Hyprland reloads its config during the same compositor session; it lives under the runtime directory and is unique to the Hyprland instance. The shell check validates script syntax; `hyprctl configerrors` should report no Hyprland configuration errors. Login again to verify the full startup sequence. Edit the command/workspace pairs in the script when the preferred session changes. This does not restore unsaved process memory; tmux and each application can only resume state that they persist themselves.
