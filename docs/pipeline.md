# Pipeline

The workflow spec for the Universal Multi-Agent Intelligence System: stages,
contracts, and handoffs between agents.

## Stage 1 scope

Stage 1 is complete — 7 agents, 9 skills, 4 rules, and 1 command are defined, with MIT LICENSE. Stage 1 deliberately does NOT include: a runtime or execution engine, live tool wiring, a run-state store, memory, an eval harness, CI, a UI, or installable package.

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

- **Agents work independently first, then debate together.** Each agent forms its
  own judgment using only its own role and skills before any outputs are shared.
  Confidence scores are hidden until all agents have voted — see
  `rules/independent-first.md`.
- The final answer is built from the **highest-scoring verified points** —
  points scored 0–8 on evidence strength, source credibility, logical soundness,
  and whether they survived Fact-Checking — not from the most-agreed points.
- **Cross-scoring + mandatory reveal round + Anti-Sycophancy Guard + Devil's
  Advocate.** Every point is scored; confidence scores revealed simultaneously
  only after all votes; unanimous verdicts must be challenged; debate capped at
  2 rounds; dissent kept verbatim.
- Research and Domain Expert run **concurrently** off the same brief.
- Critical Thinking consumes both of their outputs.
- Fact-Checking and Debate are **sequential** after Critical Thinking.
- Final Decision closes the loop.
- Orchestrator is the only stateful owner. It may **re-dispatch** a stage if a
  later stage invalidates it (e.g. Fact-Checking debunks a load-bearing claim,
  so Critical Thinking re-runs on the remainder).

## Agent contracts

Each agent file (defined in this repo) defines:

- `name`, `description`, `triggers`, `model`, `tools` (frontmatter)
- Role summary
- Input contract — what it receives from the previous stage
- Output contract — what it hands back
- Operating instructions
- Handoff protocol — how it signals done or failure
- Escalation rules — when to kick back to Orchestrator

## Skill contracts

Each skill file (defined in this repo) defines:

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