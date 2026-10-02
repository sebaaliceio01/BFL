# BFL — agent instructions

C++17 research prototype of Bit Flip Learning (MUX networks trained by bit flips). Read `README.md` and `docs/greedy.md` for the models and `.specify/memory/constitution.md` for the rules this repo follows.

## Build and test
```sh
g++ -std=c++17 -O3 -Wall -Wextra -Wpedantic -Iinclude src/bfl.cpp src/greedy.cpp tests/test_bfl.cpp -o bfl_tests && ./bfl_tests
g++ -std=c++17 -O3 -Wall -Wextra -Wpedantic -Iinclude src/bfl.cpp src/greedy.cpp tests/test_greedy.cpp -o bfl_greedy_tests && ./bfl_greedy_tests
```
No warnings allowed. No third-party dependencies.

## Rules that matter most
- Claims need a recorded run under `results/run_<date>-<name>/`; never overwrite an old run.
- Report a trivial baseline and a same-family baseline next to every model.
- New options are off by default; a test proves defaults are unchanged.
- Code, identifiers and comments in English.

## Workflow
Non-trivial changes use the spec-driven pipeline in `docs/DEVELOPMENT_PIPELINE.md`: `sdd-spec`, `sdd-plan`, `sdd-tasks`, `sdd-impl`, `sdd-review` (or `sdd-feature` to drive all of them). Stop for human approval after spec, plan, tasks and each implementation phase. Skills live in `.agents/skills/`.
