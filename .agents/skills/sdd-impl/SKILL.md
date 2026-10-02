---
name: sdd-impl
description: "Execute tasks.md phase by phase with strict TDD: failing test first, minimal code to pass, then refactor, running the build and tests as a gate after each phase. Use after tasks are approved."
---

# sdd-impl

Needs approved `tasks.md`. Work one phase at a time.

For each task: write the test, run it and confirm it fails **for the right reason**, write the minimum code, confirm it passes, refactor. Tick the box in `tasks.md`.

After each phase run the gate:
```sh
g++ -std=c++17 -O3 -Wall -Wextra -Wpedantic -Iinclude src/bfl.cpp src/greedy.cpp tests/test_bfl.cpp -o /tmp/t1 && /tmp/t1
g++ -std=c++17 -O3 -Wall -Wextra -Wpedantic -Iinclude src/bfl.cpp src/greedy.cpp tests/test_greedy.cpp -o /tmp/t2 && /tmp/t2
```
Any warning or failure stops the phase. Report it; do not skip or weaken a test.

Never edit an earlier `results/run_*` directory. Experiments go into a new one (PRINCIPLE_3).

**Gate**: after each phase, report what passed and wait for the user before the next phase.
