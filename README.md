# Agent Foundry — project template

A ready-to-use starting point for building a tool or app with a **multi-vendor team
of AI agents**. Thinking and reviewing run on **Claude**; code-writing runs on
**Antigravity (agy / Gemini)**. Git is the shared workspace.

This template contains only the reusable **team layer** — agent definitions,
skills, rules, the flow command, and docs. No product code. You add that.

## Start a new project

1. **Use this template** on GitHub (or clone it) to create your project repo.
2. Open the folder in Claude Code and **reload** the session so the subagents and
   the `/build-tool` command load.
3. Fill the blanks under "This project" in [CLAUDE.md](CLAUDE.md).
4. Run:
   ```
   /build-tool <your idea>
   ```
   …and Claude drives the whole pipeline: ideation → architecture → design → build
   (Antigravity) → review (Claude) → PR → publish, stopping at the two human gates.

## One-time machine setup (not per project)

- **Antigravity CLI** — `agy --version`, `agy models` (install + `agy install` to add to PATH, then log in).
- **GitHub CLI** — `gh auth status` (install + `gh auth login`).

## What's inside

| Path | What it is |
|---|---|
| `AGENTS.md` | Vendor-neutral rules every agent obeys |
| `CLAUDE.md` | Auto-loaded session context: this project's own notes + an import of the shared rules |
| `.claude/foundry.md` | The shared foundry rules (team, how to run a task, gotchas) — synced |
| `scripts/sync-foundry.sh` | Pulls the latest foundry layer from this template into a project |
| `.claude/agents/` | Claude subagents (architect, qa-reviewer, security-engineer, ux-ui-designer, skill-curator, devops) — auto-load, tool-scoped |
| `.claude/commands/build-tool.md` | The `/build-tool` end-to-end pipeline command |
| `.agents/` | Antigravity skills + agent files for the developer role |
| `agents/` | Human-readable role charters (source of truth for authority) |
| `docs/` | Architecture, operating guide, and the release checklist |

## This template is the single source of truth

The foundry layer — `AGENTS.md`, `.claude/foundry.md`, `.claude/agents/`,
`.claude/commands/`, `.agents/`, `agents/`, and the three shared docs — is owned
by **this repo**. Projects get copies; they never edit them.

- **To improve the process:** change it here (branch + PR), merge.
- **To update a project:** in the project, run
  ```
  bash scripts/sync-foundry.sh
  ```
  It copies the latest foundry files in, records the template commit in
  `.foundry-version`, and never touches the project's own files (including its
  `CLAUDE.md` notes). Review the diff and commit it on a branch.

GitHub templates are a one-time copy, so without the sync script a project would
never see later improvements.

## Working rules (learned on the first real project)

- The orchestrating session **never writes product code** — every change goes to
  the developer through a task contract.
- The designer keeps `design/` current; QA fails reviews with stale specs.
- **Run it and look** in the browser preview before review.
- Publishing goes through the `devops` subagent and
  [docs/release-checklist.md](docs/release-checklist.md), with your approval.

## The rule that protects quality

The reviewer must be a **different vendor than the author**. The developer is
Gemini, so QA and Security stay on Claude. Never let one vendor write and review the
same code.
