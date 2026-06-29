# Apple Reminders Skill

A small skill for Codex or any compatible AI agent harness to read and triage local Apple Reminders through the `remindctl` CLI.

The skill is intentionally narrow:

- check `remindctl` availability and Reminders authorization first
- read Reminders through JSON output
- summarize due, overdue, upcoming, open, or unscheduled reminders
- default to read-only behavior
- mutate reminders only when the user explicitly asks
- report exact permission diagnostics instead of pretending access worked

## Install

For Codex, clone this repository into your skills directory:

```bash
git clone https://github.com/yomete/apple-reminders-skill.git ~/.codex/skills/apple-reminders
```

Restart Codex or reload skills if needed.

For another AI agent or harness, use `SKILL.md` as the instruction file and make sure the harness can run `remindctl` locally.

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

Codex or the active agent harness should report the exact `status` and `doctor` output so you know which macOS permission needs fixing.

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

The skill tells Codex or the active agent harness to prefer read-only commands. Creation, edits, completion, and deletion should only happen when the user explicitly requests them.

When a reminder must be changed, the agent should use stable reminder IDs from JSON output instead of numeric indexes.

## License

MIT
