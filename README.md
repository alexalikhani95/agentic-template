# agentic-template

A starting point for a project built with coding agents. It carries the **way of working** — the doc structure, the git rules, and how `/develop` fits the repo — and nothing about any product, domain, or stack. Those get decided per project, by the flow itself.

## What's in it

| Path                             | What it is                                                                                |
| -------------------------------- | ----------------------------------------------------------------------------------------- |
| `AGENTS.md`                      | The agent entry point — dev flow, who does the work, conventions, commit discipline       |
| `CLAUDE.md`                      | One line: `@AGENTS.md`, so Claude Code reads the same file                                |
| `docs/agents/workflow.md`        | How `/develop` fits this repo, the by-hand flow, worktree rules, which skills and plugins |
| `docs/agents/issue-tracker.md`   | How tickets are written and tracked as local markdown                                     |
| `docs/conventions/git.md`        | Conventional Commits, branch-per-feature, PR + squash merge                               |
| `docs/adr/`                      | `_template.md` plus ADR-0001, which establishes recording decisions at all                |
| `docs/status.md`                 | The single status surface — what is actually live                                         |
| `scripts/context-check.mjs`      | Hook that measures live context every prompt and says when to hand off (200k threshold)   |
| `scripts/check-status-claims.sh` | CI gate: fails if a status claim appears outside `docs/status.md`                         |
| `.claude/settings.json`          | Registers the context-check hook for Claude                                               |
| `.codex/hooks.json`              | Registers the same hook for Codex                                                         |
| `.githooks/pre-commit`           | Prettier check on staged files                                                            |

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
- Claude Code and/or Codex, with the personal skills repo ([alexalikhani95/skills](https://github.com/alexalikhani95/skills)) cloned to `~/.claude/skills` and its `sync.sh` run once — it carries the Matt Pocock skills that are the flow's spine, for both agents
- `ponytail` and `naive-user` installed as plugins in each agent — see `docs/agents/workflow.md` → Skills and plugins

## The one rule worth reading first

Nothing is committed unless the user asks. The agent edits, reports what changed, and stops. The one exception is `/develop`: starting it counts as asking, for its own feature branch, and it stops for a human answer three times: the spec, the tickets, the merge. Everything else is the agent proving its work before asking. Full version: the `develop` skill in the skills repo.
