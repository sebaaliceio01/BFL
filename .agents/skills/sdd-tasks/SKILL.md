---
name: sdd-tasks
description: "Generate tasks.md from an approved spec and plan: TDD-ordered tasks with IDs T001, T002, parallel [P] and test [TEST] markers, and a gate per phase. Use after the plan is approved."
---

# sdd-tasks

Needs approved `spec.md` and `plan.md`. Write `.specify/specs/<feature>/tasks.md` from `.specify/templates/tasks.md`.

- IDs `T001`, `T002`, ... Mark `[P]` if parallelizable, `[TEST]` for tests.
- A test task always precedes the code it covers (PRINCIPLE_6).
- Group into phases, each ending in a gate: warning-free build and passing tests.
- Last phase: run the experiment into `results/run_<date>-<name>/` and update `results/README.md`.
- Every task names the file it touches.

**Gate**: stop and wait for approval before `sdd-impl`.
