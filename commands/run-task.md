---
description: Run a task through the Universal Multi-Agent Intelligence System pipeline
---

# /universal-agents run

Entry point for the Universal Multi-Agent Intelligence System.

## Usage

```text
/universal-agents run "<your task>"
```

## What it does

1. Receives the user's task.
2. Hands it to the **Orchestrator** agent.
3. Orchestrator decomposes the task, sets the confidence bar, and owns the run.
4. The pipeline executes: Research + Domain Expert work independently first → Critical
   Thinking → Fact-Checking → Debate with Best-Point Scoring 0-8 → Final Decision
   from highest-scoring verified points.
5. Confidence scores are hidden until all agents have voted. Debate is capped at
   2 rounds. Dissent is kept verbatim.
6. Orchestrator packages the result and returns it to the user.

## Stage 1 note

In Stage 1 this command is a specification — the agents and skills it references are defined in this repo, but there is no runtime to execute them automatically.