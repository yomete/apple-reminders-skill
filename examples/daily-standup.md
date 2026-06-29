# Daily Standup Prompt

```text
Good morning! Give me a daily standup briefing.

Use $apple-reminders to read:
1. Incomplete reminders that are due today or overdue.
2. Incomplete reminders without due dates (unscheduled tasks).

Summarize what I need to focus on today, grouped by:
- Due today/overdue (highest priority)
- Unscheduled tasks (no due date)

Keep it concise and actionable.

If Apple Reminders access is unavailable, report the exact `remindctl status --json` and `remindctl doctor --for-agent` result and say what permission needs fixing. Do not claim reminders were checked if access failed.
```
