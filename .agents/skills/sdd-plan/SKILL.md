---
name: sdd-plan
description: "Turn an approved spec.md into plan.md: approach, files to change, compatibility with defaults, experiment design and risks. Use after the spec is approved and before writing tasks."
---

# sdd-plan

Needs an approved `spec.md`. Write `.specify/specs/<feature>/plan.md` from `.specify/templates/plan.md`.

1. Read the spec and the constitution; cite principles by ID.
2. Read the code you will change. Name real files and functions.
3. Choose the smallest design that tests the hypothesis.
4. State how defaults stay unchanged and which test proves it (PRINCIPLE_4).
5. Fix the experiment: command, seeds, shared splits, output directory (PRINCIPLE_3).
6. List decisions the user must confirm.

**Gate**: stop. Wait for approval before `sdd-tasks`. Optionally run a consistency check of spec against plan first.
