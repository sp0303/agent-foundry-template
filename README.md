# Agent Foundry — project template

Start a new tool or app with a ready-made **team of eight AI agents** across two
vendors. The thinking and reviewing run on **Claude**; the code is written by
**Gemini via the Antigravity CLI**. Git is the shared workspace, and you hold the
two approval gates.

This template holds only the reusable **team layer** — agents, skills, rules, the
pipeline command, and docs. No product code; your project adds that.

## Meet the team

| Name | Role | Runs on | Owns |
|---|---|---|---|
| **Jacobin** | Business analyst | Claude | Your idea → scope, user stories, acceptance criteria |
| **Arjun** | Architect | Claude | Stack, ADRs, interface contracts, task contracts |
| **Sparsha** | UX / UI designer | Claude | Flows, screens, states, visual system, accessibility |
| **Vaka** | Developer | Gemini (Antigravity) | Writes the code, one task at a time, with tests |
| **Tara** | QA reviewer | Claude | Reviews against acceptance criteria; can't edit code |
| **Kara** | Security engineer | Claude | Threat model, OWASP, secrets, dependencies |
| **Ira** | Skill curator | Claude | Keeps the agents, skills and this template sharp |
| **Vihaan** | DevOps | Claude | CI, release checklist, deploys, rollback |

Call them by name or role: "Arjun, plan this", "have Tara and Kara review it".

**The rule that protects quality:** the reviewer is always a different vendor from
the author. Vaka (Gemini) writes; Tara and Kara (Claude) review.

## How a build runs

```
You ─ idea ─▶ Jacobin (scope) ─▶ [Gate 1: you approve]
          ─▶ Arjun (plan + task contracts) ─▶ Sparsha (design, if UI)
          ─▶ Vaka builds one slice ─▶ run it and look
          ─▶ Tara + Kara review ─▶ PR ─▶ [Gate 2: you merge]
          ─▶ Vihaan (release checklist) ─▶ publish with your OK
```

Each agent has a written charter, a persona, explicit "always / never" rules, and
a follow-up step. Claude subagents are tool-scoped: Tara and Kara have no
file-writing tools, and Arjun can't edit or run code.

## Start a new project

1. Create your repo from this template:
   ```
   gh repo create <owner>/<name> --template sp0303/agent-foundry-template --private --clone
   ```
   (or click **Use this template** on GitHub).
2. **Open the new folder as a new Claude Code session** — that is what loads the
   agents and the `/build-tool` command.
3. Fill in the "This project" section of [CLAUDE.md](CLAUDE.md).
4. Run:
   ```
   /build-tool <your idea>
   ```

## One-time machine setup

- **Antigravity CLI** — `agy --version`, `agy models` (install, `agy install` to add to PATH, log in).
- **GitHub CLI** — `gh auth status` (install, `gh auth login`).

## This template is the single source of truth

The foundry layer — `AGENTS.md`, `.claude/foundry.md`, `.claude/agents/`,
`.claude/commands/`, `.agents/`, `agents/`, and the shared docs — is owned by
**this repo**. Projects get copies and never edit them.

- **To improve the process:** change it here (branch + PR).
- **To update a project:** run `bash scripts/sync-foundry.sh` in it. The script
  copies the latest foundry files in, records the template commit in
  `.foundry-version`, and never touches the project's own files (including its
  `CLAUDE.md` notes).

GitHub templates are a one-time copy; the sync script is how projects keep up.

## Working rules (learned on the first real project)

- The orchestrating session **never writes product code** — every change goes to
  Vaka through a task contract.
- Sparsha keeps `design/` current; Tara fails reviews with stale specs.
- **Run it and look** in the browser preview before review.
- Publishing goes through Vihaan and
  [docs/release-checklist.md](docs/release-checklist.md), with your approval.

## What's inside

| Path | What it is |
|---|---|
| `AGENTS.md` | Vendor-neutral rules every agent obeys |
| `CLAUDE.md` | Session context: this project's notes + an import of the shared rules |
| `.claude/foundry.md` | The shared foundry rules (team, how to run a task, gotchas) |
| `.claude/agents/` | Claude subagents: Arjun, Sparsha, Tara, Kara, Ira, Vihaan |
| `.claude/commands/build-tool.md` | The `/build-tool` end-to-end pipeline |
| `.agents/` | Antigravity skills and agent files for Vaka |
| `agents/` | Role charters (the source of truth for each role's authority) |
| `docs/` | Architecture, operating guide, release checklist |
| `scripts/sync-foundry.sh` | Pulls the latest foundry layer into a project |
