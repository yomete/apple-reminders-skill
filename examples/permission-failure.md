# Permission Failure Behavior

When `remindctl status --json` reports that Reminders access is not authorized, run:

```bash
remindctl doctor --for-agent
```

Then report both command outputs to the user. Do not summarize reminders, and do not say reminders were checked.

Good failure response shape:

```text
Apple Reminders access is unavailable.

`remindctl status --json`:
...

`remindctl doctor --for-agent`:
...

Fix: grant Reminders access to the terminal or app running Codex, or your active AI agent harness, in macOS Privacy & Security settings, then retry.
```
