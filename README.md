# task-progress

A Codex skill that keeps a task checklist visible and up to date throughout multi-step work.

## Install

Copy the `task-progress` directory into your Codex skills directory, for example `~/.codex/skills/task-progress/`. Restart Codex or start a new session if needed for the skill to be discovered.

## Usage

Invoke `$task-progress` or instruct Codex to use it for tasks involving file changes, multiple commands, or several steps. The skill uses `update_plan` when available and falls back to a Markdown checklist otherwise.

See [SKILL.md](task-progress/SKILL.md) for the complete instructions.

## License

MIT. See [LICENSE](LICENSE).
