---
name: sdd-spec
description: "Write or refine a feature spec in .specify/specs/<feature>/spec.md: the problem, a falsifiable hypothesis, metric, baselines and success criteria. Use at the start of any non-trivial change, before planning or coding."
---

# sdd-spec

Create `.specify/specs/<feature>/spec.md` from `.specify/templates/spec.md`.

1. Read `.specify/memory/constitution.md`. If the request touches a principle, name it.
2. Ask the user only for what you cannot infer. Mark the rest `[NEEDS CLARIFICATION]`.
3. The spec says **what and why**, not how: no file names, no algorithms.
4. The hypothesis must be falsifiable and the success/failure criteria written **before** any run (PRINCIPLE_1, PRINCIPLE_2).
5. Name the baselines: trivial floor and one same-family peer.

**Gate**: stop. Show the spec and wait for explicit approval before `sdd-plan`.
