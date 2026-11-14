# conflict-resolution

## Purpose

Resolve disagreements between agents on evidence rather than by majority vote,
so the final verdict rests on what the sources actually show.

## Rule

When agents disagree, record both sides with their evidence, send the dispute back
through Fact-Checking and Debate, and let Final Decision resolve it only on
evidence — with confidence and uncertainty stated explicitly.

## What is forbidden

- Picking the majority view or the most confidently stated position.
- Resolving a dispute silently, by dropping one side.
- Letting a single agent's opinion override another's without evidence.
- Having Final Decision resolve a dispute that has not been through Fact-Checking
  and Debate.
- Presenting a resolved conflict as settled when the underlying evidence is still
  contested.

## What to do instead

- Record both sides of the dispute, each with the evidence and reasoning behind
  it.
- Send the dispute back to **Fact-Checking** to verify the claims each side
  rests on, and to **Debate** to run a round on the contention.
- Let **Final Decision** resolve the dispute only on the verified findings and
  the debate record, and state the confidence and the residual uncertainty.
- Carry unresolved contention into the uncertainty statement rather than
  resolving it by assertion.
- Escalate to the user when the evidence cannot settle the dispute and the
  decision is material.

## Example of a violation

Three agents say a policy reduced crime; one says the data does not support that
causal claim. The Orchestrator adopts the majority view and reports the policy as
effective, without sending the causal claim back to Fact-Checking or running a
debate round.

## Example of correct behaviour

The Orchestrator records both positions with their evidence, sends the causal
claim to Fact-Checking (which finds the underlying data does not support a
causal inference), and runs a Debate round (which closes the contention). Final
Decision reports the policy's effect as unverified on causation, states the
confidence as low on that point, and recommends further evidence before
claiming effectiveness.

## Enforced by

The **Orchestrator**, which owns dispute handling and may re-dispatch stages. The
**Debate** and **Final Decision** agents enforce it within their stages. Disputes
the evidence cannot settle must be escalated to the user.