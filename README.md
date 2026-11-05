# task-progress

A Codex skill that maintains a live task checklist during multi-step work.

## Install

Copy the `task-progress` directory to your Codex skills directory, for example `~/.codex/skills/task-progress/`. Restart Codex or start a new session if needed.

## Enable the plan tool

If your Codex version supports it and `update_plan` is unavailable, add this to your global `~/.codex/config.toml`:

```toml
[tools.update_plan]
enabled = true
```

If the table already exists, update its `enabled` value instead of adding a second table. Restart Codex and check a new chat. Availability can vary by version and environment.

## View progress

Invoke `$task-progress` or instruct Codex to use it for tasks involving file changes, multiple commands, or several steps. It updates `update_plan` when available and can also show a Markdown checklist in chat.

In the tested Windows desktop version (26.1029.7803.0), the compact “Step X / Y” indicator appears above the input box while the response is running. Hover over it to see the task names and statuses. The indicator disappears when the response finishes. A user confirmed the hover list displayed all three test items. Other versions may behave differently.

For a checklist that stays visible in the chat, ask Codex to display and update it as Markdown. See [SKILL.md](task-progress/SKILL.md) for the complete instructions and [display investigation](docs/display-investigation.md) for details.

## License

MIT. See [LICENSE](LICENSE).
