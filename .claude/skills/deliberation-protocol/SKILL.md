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
9. **Run a mandatory reveal round.** All confidence scores are revealed
   simultaneously only after every agent has voted. No score is shown before
   voting is complete.
10. **Apply the Anti-Sycophancy Guard.** An agent must not change its answer
    only because most agents agree. If it changes position, it must cite the
    specific evidence or reasoning that caused the change. Agreement without
    evidence is not a reason to change.
11. **Apply the Devil's Advocate rule.** A unanimous verdict must be challenged
    before finalizing. Assign one side to argue the strongest counter-case
    regardless of its own position. If the challenge survives, the verdict is
    reopened; if it fails, the challenge is recorded as closed.
12. **Cap the debate at 2 rounds.** After 2 rounds, stop. Unresolved points are
    carried forward as `open` — they are not resolved by running more rounds.
13. Score every point raised in the round using Best-Point Scoring, and record
    each score.
14. Return the record, closed points, open points, and the scored points. Do not
    declare a winner.
9. Score every point raised in the round using Best-Point Scoring, and record
   each score.
10. Return the record, closed points, open points, and the scored points. Do not
    declare a winner.

## Best-Point Scoring

Score every point raised in the round on four criteria, 0–2 each, for a total of
0–8. The highest-scoring points win — not the most-agreed points.

| Criterion | 2 | 1 | 0 |
|-----------|---|---|---|
| Evidence strength | Strong, specific, directly supports the point | Weak, indirect, or only suggestive | No evidence at all |
| Source credibility | Primary source retrieved and checked (CONFIRMED) | Secondary source only (REPORTED) or weak source | No retrievable source |
| Logical soundness | No logical flaws; survives cross-examination | Minor flaw or unstated assumption | Circular, contradicted, or fails cross-examination |
| Survived Fact-Checking | Verified by Fact-Checking (CONFIRMED) | Not checked, or REPORTED/UNVERIFIABLE | DEBUNKED or contradicted |

**Scoring rules:**
- A point with **no retrievable source** cannot score above 2 total — it is
  capped at 0 on Source credibility and 0 on Survived Fact-Checking, so its
  total score is capped at 2.
- A point that is **DEBUNKED** or contradicted by Fact-Checking scores 0 on
  Survived Fact-Checking and cannot win.
- **Ties** are broken by evidence strength, then source credibility.
- The winning points are those with the highest total scores. Record every
  point with its score, and state which points were rejected and why.

## Anti-Sycophancy Guard

An agent must not change its answer only because most agents agree. Majority
agreement is not evidence.

- **Trigger:** an agent's position differs from the majority and the pressure to
  converge is present.
- **Required action:** the agent must either (a) hold its position, citing its
  evidence, or (b) change it, citing the specific evidence or reasoning that
  caused the change.
- **Forbidden:** changing a position because "everyone else thinks so," because
  the majority is large, or because disagreeing seems costly.
- **Record:** every position change must be logged with the reason. A change
  with no cited evidence is a violation and the original position stands.

## Devil's Advocate Rule

A unanimous verdict must be challenged before finalizing. Consensus is not the
same as correctness.

- **Trigger:** all agents agree on a verdict.
- **Required action:** assign one side to argue the strongest counter-case
  regardless of its own position. That side must produce the best possible
  argument against the verdict, using the same evidence set.
- **If the challenge survives:** the verdict is reopened and the round continues
  within the 2-round cap.
- **If the challenge fails:** it is recorded as `closed` with the reason, and the
  verdict stands.
- **Record:** the challenge, the counter-case, and the outcome must appear in the
  debate record. A unanimous verdict with no recorded challenge is invalid.

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

Scored points:
1. <point text> | Evidence: <0-2> | Source: <0-2> | Logic: <0-2> | Fact-checked: <0-2> | Total: <0-8>
2. ...

Winning points: <highest-scoring points>
Rejected points: <points that did not win, with reason>
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