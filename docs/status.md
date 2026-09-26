# Status — what is real right now

**This file is the only place in the repo that states what is live, deployed, or verified.** Every other document links here instead of repeating it. A status claim anywhere else is a bug; `scripts/check-status-claims.sh` fails CI on one.

`PLAN.md` says what we _intend_ to build and ticks off work as it lands. This file says what actually _exists_ — environments, infra, verified facts — with the date each was last checked. Keep it a table; if a row needs a paragraph, it needs an ADR or a ticket instead.

Dates below are the date each row was last checked — set them to today's date on the first commit in a new repo, then keep them honest.

## Environments

| Environment | State       | URL | Deployed SHA | Last verified |
| ----------- | ----------- | --- | ------------ | ------------- |
| staging     | not created | —   | —            | —             |
| prod        | not created | —   | —            | —             |

## Infrastructure

| Resource    | State      | Notes         | Last verified |
| ----------- | ---------- | ------------- | ------------- |
| GitHub repo | local only | no remote yet | YYYY-MM-DD    |

## Application

| Area            | State          | Last verified |
| --------------- | -------------- | ------------- |
| Product plan    | not written    | YYYY-MM-DD    |
| App             | not scaffolded | YYYY-MM-DD    |
| CI (PR checks)  | not created    | YYYY-MM-DD    |
| Deploy pipeline | not created    | YYYY-MM-DD    |
