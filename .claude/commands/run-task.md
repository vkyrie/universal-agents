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
4. The pipeline executes: Research + Domain Expert (concurrent) → Critical
   Thinking → Fact-Checking → Debate → Final Decision.
5. Orchestrator packages the result and returns it to the user.

## Stage 1 note

In Stage 1 this command is a specification — the agents and skills it references are defined in this repo, but there is no runtime to execute them automatically.