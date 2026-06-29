# Apple Reminders Agent Skill

A small [Agent Skills](https://agentskills.io/) package for reading and triaging local Apple Reminders through the `remindctl` CLI.

The skill is intentionally narrow:

- check `remindctl` availability and Reminders authorization first
- read Reminders through JSON output
- summarize due, overdue, upcoming, open, or unscheduled reminders
- default to read-only behavior
- mutate reminders only when the user explicitly asks
- report exact permission diagnostics instead of pretending access worked

## Install

Install it in any Agent Skills-compatible harness by placing this repository where that harness discovers skill folders.

Common locations:

```bash
# OpenAI Codex, Cursor, pi, and other harnesses that read the shared Agent Skills folder
git clone https://github.com/yomete/apple-reminders-skill.git ~/.agents/skills/apple-reminders

# Claude Code
git clone https://github.com/yomete/apple-reminders-skill.git ~/.claude/skills/apple-reminders
```

Then restart or reload your agent if it does not pick up the new skill automatically.

See [agent installation notes](docs/agent-installation.md) for Claude, Claude Code, Cursor, Codex, pi, and generic harnesses.

## Dependency

This skill expects `remindctl` to be installed and available on `PATH`.

Check locally:

```bash
command -v remindctl
remindctl status --json
```

If Reminders access is not authorized, run:

```bash
remindctl doctor --for-agent
```

The active agent harness should report the exact `status` and `doctor` output so you know which macOS permission needs fixing.

## Example prompts

```text
Good morning. Give me a daily standup briefing from Apple Reminders.
```

```text
Show me incomplete reminders that are overdue or due today.
```

```text
Find open reminders without due dates and group them by list.
```

```text
Complete the reminder with id E6265F26-E929-4861-92F8-15F8A2C16B3B.
```

## Safety

The skill tells the active agent harness to prefer read-only commands. Creation, edits, completion, and deletion should only happen when the user explicitly requests them.

When a reminder must be changed, the agent should use stable reminder IDs from JSON output instead of numeric indexes.

## License

MIT
