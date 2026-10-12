# qa-kit

Claude Code plugin (v0.1.0) with a code-review subagent and a PR-summary command.

## What it adds

| Type | Name | Purpose |
|------|------|---------|
| Command | `/qa-kit:summarize-changes` | Lists each file changed on the current branch with a one-line description. Output is short enough to paste into a PR description. |
| Agent | `qa-kit:code-reviewer` | Read-only reviewer (tools: `Read`, `Grep`, `Glob`; model: `sonnet`). Checks recent changes for bugs, missing error handling, and unclear names. Returns a list grouped by severity (high/medium/low), with the file and a one-sentence fix per item. |

## Install

Load it for a single session from a local checkout:

```
claude --plugin-dir /path/to/claude-assemble-and-ship
```

## Usage

### Summarize a branch

```
/qa-kit:summarize-changes
```

Run it on the branch you are about to open a PR for. Paste the output into the PR description.

### Review code

Claude delegates to the reviewer automatically after you write or edit code. You can also invoke it explicitly:

```
Use the qa-kit:code-reviewer agent to review my latest changes
```

Or pick it via `/agents`.

## Layout

```
.claude-plugin/plugin.json      manifest
agents/code-reviewer.md         subagent
commands/summarize-changes.md   slash command
```
