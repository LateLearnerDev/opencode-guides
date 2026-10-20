# Monitor layout and workspace assignment

Hyprland monitor settings are in `~/.config/hypr/monitors.lua`. Find your own output names and dimensions with `hyprctl monitors`; names such as `DP-1` are specific to a machine and may differ elsewhere.

## Positioning monitors

Each monitor rule sets an output, display mode, desktop position, and scale. Positions use `x` then `y` coordinates. For example, these rules place a 1920×1080 display below the top edge of a 3440×1440 display so their bottom edges align:

```lua
hl.monitor({ output = "DP-2", mode = "preferred", position = "0x360", scale = omarchy_monitor_scale })
hl.monitor({ output = "DP-1", mode = "preferred", position = "1920x0", scale = omarchy_monitor_scale })
```

Replace `DP-2` and `DP-1` with the output names reported on your system. `preferred` lets each display use its preferred mode. Both rules use `omarchy_monitor_scale` so Omarchy's Display → Scale control continues to apply after a reload.

## Assigning workspaces to monitors

To place a workspace on a particular monitor, add a workspace rule using your workspace number and monitor output name. For example, this assigns workspace 2 to `DP-1`:

```lua
hl.workspace_rule({ workspace = "2", monitor = "DP-1" })
```

Replace `"2"` and `"DP-1"` with the workspace and output you want. After editing, reload Hyprland with `hyprctl reload`. Check for configuration errors with `hyprctl configerrors` if the setting does not apply.

The example uses a shared scale variable, allowing Omarchy's scaling control to affect both monitor rules. In this configuration, the variable is set to 1; choose a value appropriate for your displays if setting it manually.
