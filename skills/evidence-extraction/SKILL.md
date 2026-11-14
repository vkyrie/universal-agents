---
name: evidence-extraction
description: Pull structured claims and citations out of unstructured text. Converts source material into tagged claims, quotes, dates, numbers, and attributions that downstream stages can verify and reason about.
inputs:
  - source_text: the raw text of a source (article, transcript, document)
  - source_meta: title, author, publication date, URL
  - claim_focus: the questions or claims the calling agent wants extracted
outputs:
  - claims: a list of structured claims with quote, date, number, attribution, and source reference
  - unparseable: passages that could not be structured, with the reason
---

# evidence-extraction

## Purpose

Pull structured claims and citations out of unstructured text. A capability used
by the Researcher and the Fact-Checker — it converts source material into tagged
claims, quotes, dates, numbers, and attributions. It does not judge whether a
claim is true.

## Step-by-step procedure

1. Read the source text and identify the source metadata (title, author,
   publication date, URL).
2. Scan for claims that bear on the `claim_focus` — assertions, figures, dates,
   attributions, and direct quotes.
3. For each claim, record:
   - the claim text, in your own words
   - the supporting direct quote, if any
   - any date, number, or measurement involved
   - who is attributed as the source of the claim
   - a reference back to the source metadata
4. Preserve the original attribution exactly — do not paraphrase an attribution
   into a different person or body.
5. Separate claims the text actually supports from claims it only implies; mark
   the latter as inferred.
6. Return the structured claim list.

## Output format spec

Return a structured list:

```text
Source: <title> — <author>, <date>, <URL>

Claims:
1. Claim: <claim in your own words>
   Quote: <direct quote or none>
   Value: <date / number / measurement, or unknown>
   Attributed to: <name or body>
   Status: stated | inferred
2. ...
```

## Failure modes

- **No extractable claims:** return an empty claims list and note that the source
  contained no material bearing on the focus. Do not invent claims.
- **Contradictory claims within one source:** record both, with the contradiction
  flagged, rather than resolving it — that is the calling agent's job.
- **Unclear attribution:** if a claim's origin is ambiguous, record it as
  `attributed to: unclear` rather than guessing.
- **Unparseable text:** record the passage in `unparseable` with the reason, and
  continue with the rest.