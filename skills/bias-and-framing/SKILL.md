---
name: bias-and-framing
description: Detect loaded language, strawmen, selection bias, and framing effects in claims and sources. Flags reasoning distortions without making a judgment about the underlying topic.
inputs:
  - material: the claims, arguments, or source passages to examine
  - context: the question being asked and who is advancing the claim
outputs:
  - findings: detected biases and framing effects, each with the specific text and the type of distortion
  - clean_passages: material that showed no detectable distortion
---

# bias-and-framing

## Purpose

Detect loaded language, strawmen, selection bias, and framing effects in claims
and sources. A capability used by the Critical Thinking agent. It flags reasoning
distortions — it does not take a side or decide who is right.

## Step-by-step procedure

1. Read the material with the question and the claimant in mind.
2. Look for **loaded language**: emotionally charged words, weasel wording, or
   terms that presuppose the conclusion.
3. Look for **strawmen**: whether an opposing position is engaged in its strongest
   form or a weakened caricature.
4. Look for **selection bias**: evidence chosen to support a view while
   contrary evidence is ignored, and whether the ignored material is material.
5. Look for **framing effects**: how the question is posed, what is included or
   excluded from the premise, and whether reframing would change the apparent
   answer.
6. For each finding, quote the specific text and classify the distortion.
7. Note passages that show no detectable distortion, so the calling agent knows
   what is clean.

## Output format spec

Return a structured list:

```text
Context: <the question and who is advancing the claim>

Findings:
1. Text: "<the exact passage>"
   Type: loaded language | strawman | selection bias | framing effect
   Detail: <what the distortion is and why it matters>
2. ...

Clean passages: <material with no detectable distortion>
```

## Failure modes

- **No distortion found:** return an empty findings list and say so plainly —
  absence of a finding is a finding.
- **Thin material:** if the passage is too short to assess, say so and flag the
  claim as low-confidence for this check.
- **Over-flagging:** avoid calling every disagreement a bias. A challenge to a
  claim is not automatically a framing effect — mark it as such only when the
  text shows the specific distortion.
- **Subject-matter judgment:** this skill flags form, not substance. Do not
  label a claim as biased simply because you think it is wrong.