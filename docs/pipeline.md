# Pipeline

The workflow spec for the Universal Multi-Agent Intelligence System: stages,
contracts, and handoffs between agents.

## Stage 1 scope

Stage 1 is **structure only**:

- Repo layout, agent/skill/command/rules folders, README, CLAUDE.md, .gitignore.
- This document: the pipeline spec.

Stage 1 deliberately does **not** include:

- Agent definitions or skill content (the 7 agents and 9 skills are planned, not written).
- A runtime or execution engine — agents are specifications, not programs.
- Live tool wiring (no search API, no browser, no actual retrieval).
- A run-state store, memory, or persistence layer.
- An eval harness, CI, or benchmark suite.
- A UI, installable package, or distribution scripts.
- The `status` command — there is no run-state store to inspect yet.

## The pipeline

```
user task
   │
   ▼
Orchestrator ──► decomposes, sets the confidence bar, owns the run
   │
   ├──► Research ──────► raw findings + source list
   ├──► Domain Expert ──► plausibility read on those findings
   │         │
   ▼         ▼
Critical Thinking ─► assumptions, gaps, alternatives
   │
   ▼
Fact-Checking ─► verified claims, corrections, debunked items
   │
   ▼
Debate ─► pro/con rounds, strongest-argument record
   │
   ▼
Final Decision ─► verdict, confidence, uncertainty, recommendation
   │
   ▼
Orchestrator ─► packages and returns
```

## Execution rules

- Research and Domain Expert run **concurrently** off the same brief.
- Critical Thinking consumes both of their outputs.
- Fact-Checking and Debate are **sequential** after Critical Thinking.
- Final Decision closes the loop.
- Orchestrator is the only stateful owner. It may **re-dispatch** a stage if a
  later stage invalidates it (e.g. Fact-Checking debunks a load-bearing claim,
  so Critical Thinking re-runs on the remainder).

## Agent contracts

Each agent file (planned for Stage 2) defines:

- `name`, `description`, `triggers`, `model`, `tools` (frontmatter)
- Role summary
- Input contract — what it receives from the previous stage
- Output contract — what it hands back
- Operating instructions
- Handoff protocol — how it signals done or failure
- Escalation rules — when to kick back to Orchestrator

## Skill contracts

Each skill file (planned for Stage 2) defines:

- `name`, `description`, `inputs`, `outputs` (frontmatter)
- Purpose
- Step-by-step procedure
- Output format spec
- Failure modes — what to do when the capability cannot deliver

## Rules

Standing constraints the whole system obeys:

- `rules/no-unverified-claims.md` — label every claim verified, unverified, or
  assumption; never present unverified material as confirmed fact.
- `rules/citation-discipline.md` — every externally researched claim carries a
  source and, where possible, an excerpt; no invented sources or citations.
- `rules/conflict-resolution.md` — disagreements are recorded with evidence,
  sent back through Fact-Checking and Debate, and resolved by Final Decision on
  evidence only, with confidence and uncertainty stated.

## Commands

- `commands/run-task.md` — the entry point: `universal-agents run "<task>"`.
  Hands the task to Orchestrator and runs the pipeline.