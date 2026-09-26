# agentic-template

A starting point for a project built with coding agents. It carries the **way of working** — the dev flow, the lanes, the doc structure, the gates, the git rules — and nothing about any product, domain, or stack. Those get decided per project, by the flow itself.

Extracted from `home-manager` and `fish-tank-manager`, which were built this way.

## What's in it

| Path                             | What it is                                                                                   |
| -------------------------------- | -------------------------------------------------------------------------------------------- |
| `AGENTS.md`                      | The agent entry point — dev flow, who does the work, conventions, commit discipline          |
| `CLAUDE.md`                      | One line: `@AGENTS.md`, so Claude Code reads the same file                                   |
| `docs/agents/workflow.md`        | The nine steps, the three lanes, gate message wording, worktree rules, which skill does what |
| `docs/agents/issue-tracker.md`   | How tickets are written and tracked as local markdown                                        |
| `docs/conventions/git.md`        | Conventional Commits, branch-per-feature, PR + squash merge                                  |
| `docs/adr/`                      | `_template.md` plus ADR-0001, which establishes recording decisions at all                   |
| `docs/status.md`                 | The single status surface — what is actually live                                            |
| `scripts/context-check.mjs`      | Hook that measures live context every prompt and says when to hand off (200k threshold)      |
| `scripts/check-status-claims.sh` | CI gate: fails if a status claim appears outside `docs/status.md`                            |
| `.claude/settings.json`          | Registers the context-check hook                                                             |
| `.githooks/pre-commit`           | Prettier check on staged files                                                               |

Deliberately **not** included: `PRD.md`, `PLAN.md`, `CONTEXT.md`, `docs/design/hld.md`, `docs/design/lld.md`. They are written per project by the dev flow, and `AGENTS.md`'s directory map marks them `(to write)`. An empty stub claiming to describe a product is worse than a missing file.

## Using this template

```sh
cp -R agentic-template <new-project> && cd <new-project>
rm -rf .git && git init
git config core.hooksPath .githooks        # enable the prettier pre-commit hook
```

Then, in order:

1. **Edit `AGENTS.md`** — replace the title and the first two paragraphs with what the project is. Leave everything from _Where to look_ down alone; it is the process, not the product.
2. **Set the dates** — `docs/status.md` and `docs/adr/0001-*.md` both carry `YYYY-MM-DD` placeholders.
3. **Plan the product** — run the flow: `/grill-with-docs` → `/to-spec`. That is what writes `PRD.md`, `PLAN.md`, `CONTEXT.md`, and the design docs. Ask for a stack recommendation rather than assuming the last project's; record the choice as an ADR if it reverses a default.
4. **Delete this README** (or replace it with a real one for the project). It is instructions for starting, not documentation of the thing you built.
5. **First commit** goes on `main` — the one exception to the worktree rule, per `docs/conventions/git.md`. Everything after that gets its own worktree.

## Prerequisites

- Node (for `scripts/context-check.mjs` and its tests: `node --test 'scripts/**/*.test.mjs'`)
- `npx prettier` available — the pre-commit hook calls it
- Claude Code, with the whole `mattpocock/skills` set installed — it is the flow's spine: `npx skills add mattpocock/skills`
- `ponytail` as a user-level plugin; `naive-user` once there is a UI — see `docs/agents/workflow.md` → Skills

## The one rule worth reading first

Nothing is committed unless the user asks. The agent edits, reports what changed, and stops. Four moments need a human answer: the spec, the tickets, the commit, the merge. Everything else is the agent proving its work before asking. Full version: `docs/agents/workflow.md` → At a glance.
