# independent-first

## Purpose

Ensure every agent forms its own independent judgment before any group deliberation, so the debate tests genuine reasoning rather than cascading agreement.

## Rule

Every agent must first work independently on the task using only its own role and skills, without seeing other agents' outputs, conclusions, or confidence scores. All confidence scores are hidden until every agent has voted. Only after all agents have completed independent work and voted may they debate together.

## What is forbidden

- An agent reading another agent's output, conclusion, or confidence score before completing its own independent analysis.
- Copying or adopting another agent's conclusion before doing independent work.
- Anchoring on the first answer shared in the debate.
- Agreeing with the majority without evidence — sycophancy is forbidden.
- The Orchestrator sharing interim outputs between agents before the independent phase ends.
- Skipping the independent phase to "save time" or because the answer seems obvious.
- Revealing any confidence score before all agents have voted.

## What to do instead

- The Orchestrator runs the independent phase first: each agent receives the task and its role-specific inputs, produces its output and a hidden confidence score, and hands both to the Orchestrator without seeing peers' work.
- Confidence scores remain hidden until every agent has voted. Only then are they revealed simultaneously.
- Only after all independent outputs and hidden votes are collected does the Orchestrator open the debate phase, sharing all outputs simultaneously.
- Agents may then challenge, refine, or adopt points from peers — but the record must show which points originated independently and which were influenced by debate.
- An agent must not change its answer only because most agents agree. If it changes its position, it must cite the specific evidence or reasoning that caused the change.

## Example of a violation

The Orchestrator sends the Researcher's findings to the Domain Expert before the Domain Expert has formed its own plausibility read. The Domain Expert simply echoes the Researcher's source list rather than applying domain priors independently.

## Example of correct behaviour

The Orchestrator gives the Researcher and Domain Expert the same brief simultaneously. Each produces its output without seeing the other's. The Orchestrator then shares both with Critical Thinking, which independently identifies assumptions. Only then does the debate phase begin, with all independent outputs on the table.

## Enforced by

The **Orchestrator** controls the phase gate — it must not release any agent's output to another agent until the independent phase is complete. The **Debater** enforces it by recording the independent origin of each point.