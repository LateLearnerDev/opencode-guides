# Configuring Omarchy idle screensaver and lock timers

Omarchy's shell idle timers are set in `~/.config/omarchy/shell.json`, under `idle`. Values are seconds from the start of user inactivity:

```json
"idle": {
  "screensaver": 600,
  "lock": 900
}
```

Here the screensaver starts after 10 minutes and the session locks after 15 minutes. Replace these values with the desired delays in seconds. Keep both keys inside the existing top-level JSON object; do not replace unrelated shell/bar settings.

The Omarchy shell hot-reloads `shell.json` when saved, so a restart is normally unnecessary. If the new timers do not take effect, use `omarchy restart shell`.
