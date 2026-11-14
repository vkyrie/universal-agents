---
name: consensus-and-report
description: Merge verified findings, debate record, and unresolved items into one coherent verdict with confidence and uncertainty, using only the highest-scoring verified points, and listing rejected points with reasons. Do not emit a verdict from unverified claims.
inputs:
  - verified_findings: the Fact-Checker's confirmed, corrected, and debunked claims
  - debate_record: the Debater's arguments, scored points, closed points, open contentions
  - unresolved: items that could not be verified or settled
  - confidence_bar: the minimum confidence required for a confident verdict
outputs:
  - verdict_document: a merged, coherent verdict with confidence, uncertainty, and recommended action
  - evidence_chain: the path from evidence to conclusion, inspectable
  - open_items: what remains unresolved and what would settle it
---

# consensus-and-report

## Purpose

Merge multi-agent outputs — verified findings, the debate record, and unresolved
items — into a single coherent verdict document. A capability used by the Final
Decision agent. It assembles and reconciles; it does not invent evidence, run
debate, or resolve what remains open. It emits a verdict only from the
highest-scoring verified points.

## Step-by-step procedure

1. Take the verified findings, debate record, unresolved items, and the
   confidence bar.
2. Build the evidence chain: for each load-bearing claim, trace it back to its
   verified source, and note where the chain depends on an unresolved item.
3. Reconcile the debate record with the verified findings:
   - If the debate closed a contention, mark it closed in the verdict.
   - If a contention remains open, carry it into the uncertainty statement.
4. Merge corrected and debunked claims into the picture so the verdict reflects
   what the Fact-Checking actually found, not the original claims.
5. Filter points by Best-Point score: only points that scored highest across
   evidence strength, source credibility, logical soundness, and whether they
   survived Fact-Checking are eligible for the final verdict. Points with no
   retrievable source, DEBUNKED by Fact-Checking, or that failed
   cross-examination are excluded.
6. Assess confidence against the bar:
   - High: load-bearing claims verified, debate closed, no material open items.
   - Moderate: some contentions remain open or the evidence is partially thin.
   - Low: load-bearing claims unverified, evidence thin, or contested.
7. Write the uncertainty statement: what is unresolved, what is contested, and
   what would change the verdict if resolved.
8. Recommend an action that follows from the verdict, with conditions —
   including what would raise or lower confidence.
9. Return the verdict document, evidence chain, and open items. Do not declare
   a winner of the debate; do not resolve open items on your own.

## Output format spec

Return a structured document:

```text
Verdict: <clear statement of what the evidence supports>

Confidence: <high | moderate | low> — <reason>

Uncertainty:
- Unresolved: <items that could not be verified or settled>
- Contested: <points where the debate did not close>
- What would change it: <what evidence would raise or lower confidence>

Recommended action: <action, with conditions and caveats>

Evidence chain:
- <claim> → supported by <source> → <verification status>
- ...

Open items: <what remains unresolved and what would settle each>
```

## Failure modes

- **Cannot reach the confidence bar:** state the best verdict honestly and say
  it does not meet the bar — do not dress it up as confident.
- **Everything is unresolved:** return a verdict that says the evidence cannot
  support a confident conclusion, and recommend against acting on it.
- **Conflicting verified findings:** if the Fact-Checker's record is internally
  inconsistent, carry the conflict into the uncertainty statement rather than
  silently picking one side.
- **Empty inputs:** if any input is missing or empty, say so and build the
  verdict from what exists, marking the missing input as a gap.
- **Scope of the merge:** this skill merges; it does not create. Never invent a
  claim, source, or argument that was not produced by an earlier stage.
- **Unverified claims leak:** if an unverified or REPORTED claim is used as a
  load-bearing premise, flag it and exclude it from the verdict — load-bearing
  claims must rest only on CONFIRMED points with retrievable sources; REPORTED
  points may appear only as non-load-bearing, labelled REPORTED.