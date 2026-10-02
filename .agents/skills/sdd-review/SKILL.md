---
name: sdd-review
description: "Review the current change against spec, plan, tasks and the constitution: acceptance criteria covered by tests, defaults unchanged, claims backed by recorded runs, caveats stated. Use before merging or opening a PR."
---

# sdd-review

Read the diff, the feature's `spec.md`/`plan.md`/`tasks.md` and the constitution. Report findings by severity (blocker, should fix, nit), each with file and line.

Check:
1. Every success criterion in the spec has a test or a recorded run.
2. Defaults unchanged, with a test (PRINCIPLE_4).
3. Every number in docs comes from a file under `results/` (PRINCIPLE_1).
4. Trivial baseline and a same-family peer are reported (PRINCIPLE_2).
5. Intervals that include zero are not described as wins (PRINCIPLE_5).
6. Environment recorded and no old run overwritten (PRINCIPLE_3).
7. Warning-free build, no new dependency (PRINCIPLE_6, PRINCIPLE_7).

Do not edit code during review.
