---
name: counterfactual-analysis
description: Test alternative hypotheses and what-if scenarios. Explores what would have to be true for different explanations to hold, and checks the evidence against them.
inputs:
  - current_reasoning: the claims, evidence, and conclusion currently on the table
  - evidence_set: the verified or candidate findings available
outputs:
  - alternatives: a list of alternative hypotheses, each with what would have to be true and how the evidence bears on it
  - settled: alternatives the evidence rules out, with the reason
  - open: alternatives the evidence neither supports nor rules out
---

# counterfactual-analysis

## Purpose

Test alternative hypotheses and what-if scenarios. A capability used by the
Critical Thinking agent. It explores what would have to be true for a different
explanation to hold, and checks the evidence against each. It does not pick a
winner — it maps the possibility space.

## Step-by-step procedure

1. Take the current reasoning and the evidence set.
2. Generate alternative hypotheses: different causes, different mechanisms,
   different timelines, different scopes, or the possibility that the apparent
   link is coincidental.
3. For each alternative, state what would have to be true for it to hold.
4. Check the evidence against each alternative:
   - Does the evidence support it, contradict it, or say nothing about it?
   - What would the evidence look like if it were true?
5. Mark alternatives the evidence clearly rules out as `settled`, with the
   reason.
6. Mark alternatives the evidence neither supports nor rules out as `open`,
   and say what evidence would settle them.
7. Return the alternatives, their status, and the reasoning.

## Output format spec

Return a structured list:

```text
Current conclusion: <the claim being tested>

Alternatives:
1. Hypothesis: <the alternative explanation>
   What must be true: <premises it rests on>
   Evidence bearing: <supports | contradicts | silent>
   Reason: <what the evidence shows>
   Status: settled | open
2. ...

Open alternatives: <what would settle each>
```

## Failure modes

- **No alternatives generated:** if the reasoning is so thin that no alternative
  is worth testing, say so and report the current reasoning as unchallenged —
  do not invent hypotheses to fill the gap.
- **Evidence silent on everything:** if the evidence says nothing about any
  alternative, mark all alternatives as `open` and say the evidence cannot
  discriminate. Do not claim a test was run.
- **Circular alternatives:** an alternative that merely restates the current
  reasoning in different words is not an alternative — discard it and say so.
- **Scope creep:** keep alternatives focused on the question. Do not chase
  every remote possibility; rank by plausibility and materiality.