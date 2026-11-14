# Contributing to Universal Multi-Agent Intelligence System

Thank you for your interest in contributing! This document explains how to propose changes, add new components, and run the pipeline.

## How to Propose a New Agent, Skill, or Rule

1. **Open an issue first.** Describe the problem the new component solves, its scope, and how it fits the pipeline. Do not open a PR without a prior issue.
2. **One change per PR.** Each PR should add or change exactly one agent, skill, or rule. Do not bundle multiple new components in one PR.
3. **Follow the existing patterns.** Copy the structure of an existing agent/skill/rule file. All components must have:
   - YAML frontmatter with required fields
   - The six sections for agents (role summary, input contract, output contract, operating instructions, handoff protocol, escalation rules)
   - The four sections for skills (purpose, step-by-step procedure, output format spec, failure modes)
   - The seven parts for rules: purpose, rule in one sentence, what is forbidden, what to do instead, violation example, correct-behaviour example, enforcing agent
4. **Mirror the change.** If you add or change a file in the top-level `agents/`, `skills/`, `commands/`, or `rules/` folder, you must also copy it byte-identically to the corresponding `.claude/` subfolder. The top-level folders are the source of truth.

## Repository Rules

These rules are enforced by the system and must be followed by all contributors:

### Source of Truth
- Top-level `agents/`, `skills/`, `commands/`, `rules/` are the **source of truth**.
- `.claude/agents/`, `.claude/skills/`, `.claude/commands/`, `.claude/rules/` are **mirrors** — they must be byte-identical to the source.
- When they differ, the top-level folders win; the `.claude/` copies should be regenerated from them.

### Citation Discipline
- Every externally researched factual claim must carry a source, an excerpt where possible, and a **retrievable URL**.
- A source name alone is not a citation. If the URL cannot be retrieved, mark the claim **unverified** and state that the URL is missing.
- No invented sources, statistics, or citations. If a source cannot be found for a claim, mark the claim **unverified**.

### Verification Labels
- Use **CONFIRMED** only when the primary source was retrieved and checked.
- Use **REPORTED** when a claim is only reported by a secondary source and the primary source was not retrieved.
- Use **UNVERIFIABLE** when no adequate source exists or the URL could not be retrieved.
- Use **DEBUNKED** when the source contradicts the claim.

### Security
- No secrets, API keys, passwords, or tokens in any file.
- `.env` and `runs/` are gitignored. Do not commit them.

### Stage 1 Scope
- This repository is **Stage 1 only**: agent/skill/rule definitions, specifications, and documentation.
- **No runtime, no live tool wiring, no run-state store, no memory, no UI, no installable package.**
- Do not add code that executes the pipeline. The command `/universal-agents run` is a specification only.

## How to Run the Pipeline Manually on a Test Task

Since there is no runtime, the pipeline is executed manually by a human following the agent sequence:

1. **Orchestrator** — receive the task, restate it, set the confidence bar, dispatch Researcher and Domain Expert concurrently.
2. **Researcher** — use `web-research`, `academic-search`, `evidence-extraction` to gather raw findings and sources.
3. **Domain Expert** — use `source-credibility` to judge plausibility and flag domain issues.
4. **Critical Thinking** — use `bias-and-framing`, `counterfactual-analysis` to surface assumptions, gaps, alternatives.
5. **Fact-Checker** — use `evidence-extraction`, `source-credibility` to label each claim CONFIRMED/REPORTED/UNVERIFIABLE/DEBUNKED.
6. **Debater** — use `deliberation-protocol`, `argument-graph` to run independent-first debate with Best-Point Scoring (0-8), Anti-Sycophancy Guard, Devil's Advocate, 2-round cap.
7. **Final Decision** — use `consensus-and-report` to build the verdict from highest-scoring verified points, list rejected points with reasons, state confidence and uncertainty.

Document the full output in a new file under `docs/examples/` following the format of the existing examples.

## How to Add an Example in docs/examples/

1. Create a new file: `docs/examples/NN-descriptive-name.md` (next number in sequence).
2. Follow the exact format of existing examples (see `docs/examples/01-great-wall-visible-from-space.md`):
   - Task block
   - Orchestrator Brief
   - Research Findings (with sources table, claims table with status labels)
   - Domain Expert Read
   - Critical Thinking Challenges
   - Fact-Checking Labels
   - Debate Pro/Con
   - Final Decision Verdict (with verdict, confidence, uncertainty, recommended action)
3. Every claim must have a retrievable URL or be marked UNVERIFIABLE. No invented sources.
4. Update `docs/examples/README.md` with a new row in the table.
5. Update the main `README.md` examples section if the link list has changed.

## License

This project is licensed under the **MIT License** — see `LICENSE` for details.

Copyright (c) 2026 Vkyrie

By contributing, you agree that your contributions will be licensed under the same MIT License.