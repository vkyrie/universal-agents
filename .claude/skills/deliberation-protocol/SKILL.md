---
name: deliberation-protocol
description: Run a structured debate round with assigned sides. Requires each side to state its strongest case, engage the other side's best point, and produce a written rebuttal, so the round produces a record rather than a shouting match.
inputs:
  - question: the contention to debate
  - evidence: the verified findings and arguments available to both sides
  - sides: which positions to assign (pro/con, or named positions)
  - rules: constraints such as time, depth, or required engagement
outputs:
  - record: the opening statements, rebuttals, and cross-examination for each side
  - closed_points: contentions the evidence settles during the round
  - open_points: contentions still unresolved after the round
---

# deliberation-protocol

## Purpose

Run a structured debate round with assigned sides. A capability used by the
Orchestrator and the Debater. It produces a written record of the round — it does
not decide who wins.

## Step-by-step procedure

1. State the question precisely, including what is and is not in scope.
2. Assign sides. Each side gets the same evidence set; no side gets an advantage.
3. Each side writes an opening statement: its position, the evidence it rests on,
   and its single strongest argument.
4. Each side writes a rebuttal that engages the other side's strongest point
   specifically — not a restatement of its own case.
5. Each side may ask one cross-examination question of the other, and the other
   must answer on the record.
6. Record everything verbatim or near-verbatim, with attributions to sides.
7. Identify points where the evidence clearly settles the question — mark these
   `closed`, since no reasonable argument remains.
8. Identify points still unresolved — mark these `open`, and note what would
   settle them.
9. Return the record, closed points, and open points. Do not declare a winner.

## Output format spec

Return a structured record:

```text
Question: <the contention>
Evidence available: <summary of the verified findings>

Opening statements:
- Pro: <statement>
- Con: <statement>

Rebuttals:
- Pro: <engages Con's strongest point>
- Con: <engages Pro's strongest point>

Cross-examination:
- Pro asks Con: <question>
  Con: <answer>
- Con asks Pro: <question>
  Pro: <answer>

Closed points: <contentions settled by the evidence>
Open points: <contentions still unresolved, and what would settle them>
```

## Failure modes

- **Uneven evidence:** if one side has materially more evidence, say so and let
  the record reflect it, rather than pretending the sides are symmetric.
- **No engagement:** if a side refuses to engage the other's strongest point,
  record that as a failure of the round and flag it — do not paper over it.
- **Evidence settles everything:** if the question is already closed by the
  evidence, say so and return an empty round with the reason, rather than
  staging a contest that cannot be won.
- **Too thin to run:** if the evidence is too sparse for a meaningful round, say
  so and return the contentions as unresolved rather than staging a fake contest.