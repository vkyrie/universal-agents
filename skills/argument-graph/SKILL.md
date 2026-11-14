---
name: argument-graph
description: Model claims, premises, objections, and dependencies as a graph. Makes the reasoning chain explicit and inspectable so it can be checked, challenged, or re-traced.
inputs:
  - material: the claims, evidence, and arguments to model
  - goal: what question the graph should answer or what conclusion it should support
outputs:
  - graph: nodes (claims, premises, objections, evidence) and edges (supports, contradicts, depends_on, undermines)
  - summary: the main paths from evidence to conclusion, and where the chain is weak
---

# argument-graph

## Purpose

Model claims, premises, objections, and dependencies as a graph. A capability
used by all agents — it makes the reasoning chain explicit and inspectable. It
does not judge the truth of anything; it only lays out how the pieces relate.

## Step-by-step procedure

1. Take the material and the goal, and identify the conclusion being advanced.
2. Break the conclusion into its constituent claims — each a node.
3. For each claim, identify the premises and evidence supporting it, and draw
   `supports` edges.
4. Identify objections and counter-claims, and draw `contradicts` or `undermines`
   edges.
5. Identify dependencies: where a claim rests on another claim rather than on
   direct evidence, draw a `depends_on` edge.
6. Trace the paths from evidence to conclusion. Mark any path that lacks
   evidence at some point as weak.
7. Return the graph and a summary of the main paths and the weak points.

## Output format spec

Return a structured graph:

```text
Goal: <the question or conclusion>

Nodes:
1. id: <n1> | type: claim | text: <...>
2. id: <n2> | type: premise | text: <...>
3. id: <n3> | type: evidence | text: <...>
4. id: <n4> | type: objection | text: <...>

Edges:
1. <n1> depends_on <n2>
2. <n2> supported_by <n3>
3. <n4> contradicts <n1>

Paths to conclusion:
- <n3> → <n2> → <n1> → conclusion
Weak points: <nodes or edges with no direct support>
```

## Failure modes

- **Circular reasoning:** if the material contains a loop, record it as a cycle
  and flag it — do not silently flatten it.
- **Unconnected components:** if part of the material does not connect to the
  conclusion, record it as a separate component and say so.
- **No conclusion identifiable:** ask the calling agent for the conclusion rather
  than guessing which claim is the main one.
- **Too large to model fully:** model the load-bearing portion and flag the rest
  as out of scope, rather than producing a shallow graph.