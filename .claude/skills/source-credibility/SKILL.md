---
name: source-credibility
description: Rate the authority, recency, and recourse of a source. Produces a credibility assessment that other agents use as one input among several — never as the final word on a claim.
inputs:
  - source: URL, title, author, publication date, and type
  - claim: the claim the source is being used to support
outputs:
  - assessment: authority, recency, recourse, and overall credibility rating
  - caveats: limitations and reasons the rating should not be taken alone
---

# source-credibility

## Purpose

Rate the authority, recency, and recourse of a source. A capability used by the
Domain Expert and the Fact-Checker. It supplies a credibility signal — it does
not by itself confirm or reject a claim.

## Step-by-step procedure

1. Identify the source type: peer-reviewed journal, official publication,
   news outlet, academic book, blog, forum post, social media, etc.
2. Assess **authority**: the author's or publisher's credentials, institutional
   affiliation, track record, and whether the outlet has a reputation for
   correction.
3. Assess **recency**: the publication date relative to the claim's subject
   matter — recent enough for the field, or superseded?
4. Assess **recourse**: whether the source can be checked — a citable,
   retrievable, persistent source scores higher than an ephemeral one.
5. Check for known credibility problems: retracted papers, documented
   misinformation history, conflict of interest, or an outlet with a known
   track record.
6. Produce a rating and a short justification, and record the limitations.

## Output format spec

Return a structured assessment:

```text
Source: <title> — <author>, <date>, <URL>
Type: <source type>

Assessment:
  Authority: <high | moderate | low> — <reason>
  Recency: <adequate | dated | superseded> — <reason>
  Recourse: <verifiable | partially | poor> — <reason>
  Overall: <high | moderate | low> — <reason>

Caveats: <what this rating should not be used to conclude>
```

## Failure modes

- **Unknown source:** if the author or outlet cannot be identified, mark authority
  as `low — unknown` and say so plainly rather than guessing.
- **Self-published or anonymous source:** mark recourse as `poor` and record it;
  do not treat it as equivalent to a credentialed outlet.
- **Retracted or debunked source:** flag it explicitly and mark overall `low`,
  and recommend the calling agent not rely on it.
- **Rating cannot settle the claim:** always state that credibility is one input
  among several — a credible source can still be wrong, and a weak one can
  occasionally be right.