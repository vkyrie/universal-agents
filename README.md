# Universal Multi-Agent Intelligence System

A GitHub-style repository of **agents** and **skills** that work together as a
multi-stage reasoning pipeline. Inspired by ECC's agent/skill/command layout.

## What this is

A specification-first system. A user gives a task, and a chain of specialized
agents reasons through it — decomposing, researching, stress-testing, verifying,
debating, and finally deciding — rather than one model answering in a single pass.

## Layout

```
universal-agents/
├── README.md
├── CLAUDE.md
├── .gitignore
├── .claude-plugin/plugin.json
├── .claude/                 # Claude Code native layout (loadable)
│   ├── agents/              # agent definitions, loadable by Claude Code
│   ├── skills/              # skills, loadable by Claude Code
│   ├── commands/            # slash commands, loadable by Claude Code
│   └── rules/               # standing constraints, loadable by Claude Code
├── agents/                  # SOURCE OF TRUTH for agent definitions
├── skills/                  # SOURCE OF TRUTH for skill definitions
├── commands/                # SOURCE OF TRUTH for command definitions
├── rules/                   # standing constraints the whole system obeys
└── docs/
    └── pipeline.md          # the workflow spec: stages, contracts, handoffs
```

## Source of truth

**Top-level `agents/`, `skills/`, and `commands/` are the source of truth.**

`.claude/agents/`, `.claude/skills/`, `.claude/commands/`, and `.claude/rules/`
are the Claude Code native layout — the same content, mirrored so the repo is
loadable directly by Claude Code without any install step. When they differ, the
top-level folders win; the `.claude/` copies should be regenerated from them.

`.claude-plugin/plugin.json` declares the plugin so the package is recognized.

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

- **Independent first, then debate.** Every agent works independently without seeing other agents' conclusions or confidence scores; confidence hidden until all vote.
- **Cross-scoring + reveal round + Anti-Sycophancy Guard + Devil's Advocate.** Points scored 0–8 (evidence strength, source credibility, logical soundness, survived Fact-Checking); no retrievable URL = max 2; unanimous verdicts challenged; debate capped at 2 rounds; dissent kept verbatim.
- **Best-scoring points win.** The final answer is built only from the highest-scoring verified points, not from vote counts or majority agreement.
- Research and Domain Expert run concurrently off the same brief.
- Critical Thinking consumes both.
- Fact-Checking and Debate follow sequentially.
- Final Decision closes the loop.
- Orchestrator is the only stateful owner and can re-dispatch a stage if a later
  stage invalidates it (e.g. Fact-Checking debunks a load-bearing claim, so
  Critical Thinking re-runs on the remainder).

## Stage 1 scope

Stage 1 is complete — 7 agents, 9 skills, 4 rules, and 1 command are defined, with MIT LICENSE. No runtime, no live tool wiring, no memory/persistence, no UI.

## Usage

To run a task once the agents and skills exist:

```text
/universal-agents run "<your task>"
```

See [docs/examples/](docs/examples/) for three full pipeline runs:
- [01-great-wall-visible-from-space.md](docs/examples/01-great-wall-visible-from-space.md)
- [02-small-shop-selling-online.md](docs/examples/02-small-shop-selling-online.md)
- [03-python-vs-javascript-beginner.md](docs/examples/03-python-vs-javascript-beginner.md)

## License

MIT — see LICENSE.

## Community

- [CHANGELOG.md](CHANGELOG.md) — version history
- [CONTRIBUTING.md](CONTRIBUTING.md) — how to contribute