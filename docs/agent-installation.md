# Agent Installation Notes

This repository is an Agent Skills package: a folder with `SKILL.md` plus optional supporting files. Different agent products discover those folders from different places.

The skill also needs local shell access to `remindctl`, because Apple Reminders data is read from the Mac running the agent.

## OpenAI Codex

Codex reads user skills from:

```bash
~/.agents/skills
```

Install:

```bash
git clone https://github.com/yomete/apple-reminders-skill.git ~/.agents/skills/apple-reminders
```

Codex can also discover repository skills under `.agents/skills` from the current working directory up to the repository root.

Source: [OpenAI Codex Agent Skills](https://developers.openai.com/codex/skills/)

## Claude Code

Claude Code reads personal skills from:

```bash
~/.claude/skills/<skill-name>/SKILL.md
```

Install:

```bash
git clone https://github.com/yomete/apple-reminders-skill.git ~/.claude/skills/apple-reminders
```

Claude Code also supports project skills under `.claude/skills/<skill-name>/SKILL.md`.

Source: [Claude Code skills](https://code.claude.com/docs/en/skills)

## Claude

Claude supports Agent Skills as modular capability packages. For Claude surfaces that support uploading or attaching skills, use this repository as the skill folder and keep `SKILL.md` at the root.

If a Claude surface only supports plain instructions, paste the contents of `SKILL.md` into the relevant project, custom instruction, or agent configuration and make sure the runtime can execute `remindctl`.

Source: [Claude Agent Skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)

## Cursor

Cursor supports Agent Skills and can discover skills from:

```bash
.cursor/skills/
.agents/skills/
```

For a shared user-level install that also works with other harnesses:

```bash
git clone https://github.com/yomete/apple-reminders-skill.git ~/.agents/skills/apple-reminders
```

For a repository-local install:

```bash
git clone https://github.com/yomete/apple-reminders-skill.git .cursor/skills/apple-reminders
```

Cursor also supports `AGENTS.md` and `.cursor/rules` for persistent instructions, but this repository is best used as a skill because it describes a task-specific workflow that should load on demand.

Sources: [Cursor Agent Skills](https://cursor.com/docs/skills), [Cursor Rules and AGENTS.md](https://cursor.com/docs/rules)

## pi

pi implements the Agent Skills standard and loads skills from several locations, including:

```bash
~/.pi/agent/skills/
~/.agents/skills/
.pi/skills/
.agents/skills/
```

Install:

```bash
git clone https://github.com/yomete/apple-reminders-skill.git ~/.agents/skills/apple-reminders
```

pi can also load skills with `--skill <path>` or through its `skills` settings array.

Source: [pi skills documentation](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/skills.md)

## Generic Agent Harness

For any other harness:

1. Put this repository in the harness's skill directory, or point the harness at this folder.
2. Ensure it treats `SKILL.md` as the entrypoint.
3. Ensure it loads only the `name` and `description` until the skill is relevant, then reads the full `SKILL.md`.
4. Ensure it can run local shell commands, especially `command -v remindctl`, `remindctl status --json`, and the read-only reminder commands.
5. Keep mutations opt-in: only run `remindctl add`, `edit`, `complete`, or `delete` when the user explicitly asks.

Source: [Agent Skills overview](https://agentskills.io/) and [Agent Skills specification](https://agentskills.io/specification)
