---
name: apple-reminders
description: Read and summarize local Apple Reminders through the `remindctl` CLI. Use when the user asks for Reminders triage, daily standup briefings, due or overdue reminders, unscheduled tasks, reminder search, or reminder edits/completion/deletion on macOS.
---

# Apple Reminders

Use `remindctl` for structured access to the same reminders shown in Reminders.app. Prefer JSON output and read-only commands unless the user explicitly asks to create, edit, complete, or delete reminders.

## First Checks

1. Run `command -v remindctl`.
2. If missing, report that `remindctl` must be installed before this skill can read local Apple Reminders.
3. Run `remindctl status --json` before assuming access.
4. If access is not authorized, run `remindctl doctor --for-agent` and report the exact blocker. Do not pretend the Reminders data was checked.

## Reading Reminders

Use JSON for agent work:

```bash
remindctl today --json
remindctl overdue --json
remindctl upcoming --json
remindctl open --json
remindctl search "query" --json
remindctl list --json
```

For a daily standup or task triage:

1. Read incomplete reminders due today with `remindctl today --json`.
2. Read incomplete overdue reminders with `remindctl overdue --json`.
3. Read open incomplete reminders with `remindctl open --json` and select reminders without due dates for unscheduled tasks.
4. Group due today and overdue reminders before unscheduled tasks.
5. Keep the summary concise and actionable.

Prefer stable reminder IDs from JSON or search output over numeric indexes when referring to items.

## Mutations

Only mutate reminders when the user explicitly asks. Before mutating, state the exact reminders and action. Use `--no-input` and stable IDs when possible.

```bash
remindctl add "Task title" --due tomorrow --no-input
remindctl edit <id> --title "New title" --no-input
remindctl complete <id> --no-input
remindctl delete <id> --force --no-input
```

## Limits

`remindctl` uses Apple's public EventKit APIs. Do not claim support for native Reminders sections, tags, smart lists, file/image attachments, or Apple's private Urgent toggle.
