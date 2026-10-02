# Spec-driven development pipeline

A small, tool-agnostic pipeline for non-trivial changes. It works the same in Claude Code and Codex because the skills are plain `SKILL.md` files (the open agent-skills format) in one place, `.agents/skills/`.

```
sdd-spec -> sdd-plan -> sdd-tasks -> sdd-impl -> sdd-review
   |           |            |           |
 approve     approve      approve     approve each phase
```

Each step writes one file under `.specify/specs/<feature>/` and **stops for human approval**. Rules live in `.specify/memory/constitution.md` and plans cite them by ID (`PRINCIPLE_4`).

## Layout

| Path | Purpose |
|---|---|
| `AGENTS.md` | Project instructions read by the agent (build, rules, workflow). `CLAUDE.md` just imports it. |
| `.specify/memory/constitution.md` | The versioned rules (measure claims, baselines, reproducibility, defaults unchanged, ...). |
| `.specify/templates/` | `spec.md`, `plan.md`, `tasks.md` templates. |
| `.specify/specs/<feature>/` | Artifacts of one feature. |
| `.agents/skills/sdd-*/SKILL.md` | The six skills. `.claude/skills` is a symlink to this folder. |

## How to use it

Claude Code: type `/sdd-feature "what you want"`, or run the steps one by one (`/sdd-spec`, `/sdd-plan`, ...).
Codex: mention the skill with `$` (for example `$sdd-feature`), or describe the task and let Codex pick the skill from its description.

A typical session:

1. `sdd-feature "try learnable topology"` creates `.specify/specs/learnable-topology/` and runs `sdd-spec`. Answer its questions; it writes `spec.md` with a falsifiable hypothesis, the metric, baselines and success criteria **decided before any run**.
2. Read `spec.md`, say "approved" (or ask for changes). `sdd-plan` writes `plan.md`: real files to touch, how defaults stay unchanged, the exact experiment command.
3. Approve. `sdd-tasks` writes `tasks.md`: `T001 [TEST] ...`, tests before code, a build-and-test gate per phase.
4. Approve. `sdd-impl` does one phase at a time with failing-test-first, then waits.
5. `sdd-review` checks the change against the spec and the constitution before the PR.

Trivial fixes (typos, comments) skip the pipeline.

## Using it in Codex

Nothing to convert for the skills: Codex reads `SKILL.md` (frontmatter `name` + `description`) from `.agents/skills/` in the repo. `AGENTS.md` carries the project rules. Keep both tools in sync by editing only `.agents/skills/` and `AGENTS.md`.

Two things to know:

- Codex's custom prompts (`~/.codex/prompts/*.md`, `/prompts:name`) are deprecated in favor of skills, so do not port the skills as prompts.
- Codex may start a skill on its own when your request matches the `description`. Keep descriptions specific, and add `agents/openai.yaml` with `allow_implicit_invocation: false` to a skill if you want it to run only when named.

### Porting an existing Claude-only pipeline

If you have skills under `.claude/skills/<name>/SKILL.md`, move them to `.agents/skills/<name>/` and symlink `.claude/skills` to it. Then check each one for what does not carry over:

| Claude Code feature | In Codex |
|---|---|
| `SKILL.md` with `name` and `description` | Same file works |
| Extra frontmatter (`allowed-tools`, `$ARGUMENTS`, ...) | Not portable. Write the intent in plain text in the body |
| Slash call `/skill-name` | `$skill-name` or implicit invocation |
| `.claude/agents/*.md` subagents | No file-for-file equivalent. Fold the role into the skill text |
| Hooks in `settings.json` | Not portable. Express the rule as a gate in the skill (for example "run the tests before continuing") |
| `CLAUDE.md` | `AGENTS.md` (this repo keeps one file and `CLAUDE.md` imports it with `@AGENTS.md`) |

Company-specific parts (infrastructure, tenancy headers, internal tooling references) should be removed, not ported, when the repo is public.

Codex docs used for this page: custom prompts and agent skills at developers.openai.com/codex. Check them if the format has changed.
