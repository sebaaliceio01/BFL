# BFL Constitution

**Version**: 1.0.0 · Scope: this repository (research prototype, C++17, no dependencies).

Plans and tasks cite principles by ID. Changing a principle bumps the version and says why.

## PRINCIPLE_1 — A claim needs a measurement
No statement about accuracy, speed or generalization goes in a README, paper or PR without a recorded run that supports it. If a result is within noise, say so.

## PRINCIPLE_2 — Every comparison has a floor and a peer
Report the trivial baseline (constant majority-class predictor) and at least one baseline of the same family (e.g. bit-level local search, binarized network). Comparing only against a different family (an MLP) is context, not evidence.

## PRINCIPLE_3 — Reproducible by construction
Fixed seeds, fixed splits shared by all models, recorded environment (compiler, OS, standard library). Results live in `results/run_<date>-<name>/` with `benchmark.csv`, `tests.txt`, `environment.txt`. Never overwrite an old run; add a new one.

## PRINCIPLE_4 — Defaults never change behavior
New options are off by default and a test proves the default path is unchanged. A change that alters existing results is a deliberate, documented exception.

## PRINCIPLE_5 — Negative results are results
Report losses, ties and failed ideas with the same prominence as wins. Keep the intervals that include zero in the table.

## PRINCIPLE_6 — Tests first
Write the failing test, see it fail for the right reason, implement, refactor. Gate: `test_bfl` and `test_greedy` pass with `-Wall -Wextra -Wpedantic` and no warnings.

## PRINCIPLE_7 — C++17 only, no dependencies
No third-party libraries in `src/`, `include/` or `tests/`. Analysis scripts may use the Python standard library.

## PRINCIPLE_8 — Spec-driven for non-trivial work
`sdd-spec` -> `sdd-plan` -> `sdd-tasks` -> `sdd-impl` -> `sdd-review`, with a human approval gate after spec, plan and tasks. Artifacts live in `.specify/specs/<feature>/`.
