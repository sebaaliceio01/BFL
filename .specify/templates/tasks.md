# Tasks: <feature>

Format: `T001 [P] [TEST] description (file)` — `[P]` can run in parallel, `[TEST]` writes a test. Tests come before the code they cover.

## Phase 1 — <name>
- [ ] T001 [TEST] ...
- [ ] T002 ...

**Gate**: build with `-Wall -Wextra -Wpedantic`, run `test_bfl` and `test_greedy`.

## Phase N — Experiment and report
- [ ] T0NN Run the experiment into `results/run_<date>-<name>/`
- [ ] T0NN Update `results/README.md` with the table, intervals and caveats
