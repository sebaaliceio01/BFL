---
name: sdd-feature
description: "Drive a feature end to end through spec, plan, tasks, implementation and review with an approval gate between phases. Use when the user describes a new feature or asks to continue the pipeline."
---

# sdd-feature

Orchestrates the other skills. It writes no content itself.

1. New feature: pick a short kebab-case name, create `.specify/specs/<name>/`, run `sdd-spec`.
2. No argument and an active feature: look at which of `spec.md`, `plan.md`, `tasks.md` exist and continue from the first missing or unapproved one.
3. Order: `sdd-spec` -> `sdd-plan` -> `sdd-tasks` -> `sdd-impl` -> `sdd-review`.
4. **Stop for approval after spec, plan and tasks, and after every implementation phase.** Never advance on your own.
5. If a later phase finds a problem in an earlier artifact, go back and amend it, then re-confirm.

Trivial fixes (typos, comments) skip the pipeline.
