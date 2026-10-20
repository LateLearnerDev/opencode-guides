# Linux and Omarchy change records

Whenever you make, apply, or help the user make a change to Linux, Omarchy, or desktop settings on this machine, keep a user-readable record in this folder:

- Keep reusable guides in `linux-omarchy/`, `git/`, or `nvim-lazyvim/`, according to topic. Each section has a `README.md` index.
- Use stable, topic-based Markdown filenames. Update an existing guide when the topic already exists; create one only for a new topic. Do not put dates or session details in filenames.

Whenever the user asks for Git help or makes/changes Git configuration, record useful, reusable guidance in the relevant `git/` guide—even if you only give advice. Do not log routine Git commands used incidentally during unrelated coding work.

Whenever the user asks how to change or configure Linux, Omarchy, or desktop settings, or you make such a change, record it in the relevant `linux-omarchy/` guide—even if you only give advice. Include system, shell, Omarchy, and desktop configuration; exclude application/game settings that do not change Linux or desktop configuration.

Whenever the user asks how to configure Neovim/LazyVim, its plugins, or settings, or you make such a change, record reusable guidance in the relevant `nvim-lazyvim/` guide—even if you only give advice. Do not capture unrelated general editor usage questions.

Write these as quick, reusable user guides—not session transcripts. Keep them concise and easy to scan:

1. State what changed and why, identify the relevant config path, and show the exact final config lines needed to understand or reproduce the setting. Explain important values briefly.
2. If a terminal command is the relevant way to make or apply the setting, show the exact command and a short plain-language explanation of its purpose and any non-obvious options. Do not include unrelated inspection commands, repeated reloads, or routine validation output.
3. Mention important reload/restart steps, validation, and caveats briefly. Do not claim success if it was not verified.
4. Keep each guide focused on the setting, not the history of how the user or agent arrived at it.
5. Write guides so they make sense on another machine: use task-oriented headings (for example, “Assigning Workspaces to Monitors”), explain the general approach, and clearly identify machine-specific names, values, or paths as examples to replace with the reader's own. Do not make a one-off setting the guide's whole framing.

The guide collection is a Git repository intended to be synchronized to other machines. Do not place credentials, private URLs, or machine-specific secrets in it. Use `git/README.md`, `linux-omarchy/README.md`, and `nvim-lazyvim/README.md` as the section indexes.

Never put passwords, tokens, private keys, or other secrets in records. Redact sensitive values and say that they were redacted; do not reproduce unrelated configuration. If a change cannot safely be recorded verbatim, explain why and provide a safe redacted representation.

For changes made directly by the user outside the agent, do not invent exact diffs or commands: record only what is known and label missing details as unavailable. Follow any more specific repository or skill instructions as well; this file does not authorize a system change or override safety/confirmation requirements.
