# CLAUDE.md

This repo is the **Universal Multi-Agent Intelligence System** — a specification
of a multi-stage reasoning pipeline made of agents and skills.

## Layout

- `agents/` — agent definitions (source of truth)
- `skills/` — skill definitions (source of truth)
- `commands/` — slash command definitions (source of truth)
- `rules/` — standing constraints the whole system obeys
- `docs/pipeline.md` — the workflow spec: stages, contracts, handoffs
- `.claude/` — Claude Code native layout, mirrored from the top-level folders
- `.claude-plugin/plugin.json` — plugin declaration

## Source of truth

Top-level `agents/`, `skills/`, `commands/`, and `rules/` are the source of
truth. `.claude/agents/`, `.claude/skills/`, `.claude/commands/`, and
`.claude/rules/` mirror them so the repo loads directly in Claude Code. Keep the
`.claude/` copies in sync with the top-level ones.

## Pipeline

User task → Orchestrator (decompose, own the run) → Research + Domain Expert
(concurrent) → Critical Thinking → Fact-Checking → Debate → Final Decision →
Orchestrator (package result).

Orchestrator is the only stateful owner and may re-dispatch a stage if a later
stage invalidates it.

## Stage 1

Structure only. No agent or skill content, no runtime, no run-state store.
See `docs/pipeline.md`.