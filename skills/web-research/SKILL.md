---
name: web-research
description: Execute broad web searches and return candidate sources. Gathers a wide net of web material for a topic without pre-filtering on credibility.
inputs:
  - query: a search query or list of queries
  - scope: domains, languages, or date ranges to prefer
  - max_results: desired number of candidate sources
outputs:
  - candidates: a list of candidate sources with URL, title, snippet, and date
  - coverage_note: what was searched and what returned nothing
---

# web-research

## Purpose

Execute broad web searches and return candidate sources. This skill is a
capability used by the Researcher — it gathers material, it does not judge it.

## Step-by-step procedure

1. Take the query and expand it into several phrasings if the topic is narrow or
   ambiguous.
2. Run searches across general web sources, preferring the scope constraints
   (domains, languages, date ranges) if given.
3. Collect candidate sources: URL, title, snippet from the result, and any
   publication date visible.
4. De-duplicate sources that point to the same content.
5. Record which queries ran and what they returned, including queries that
   returned nothing.
6. Return the candidate list without ranking or credibility assessment — that is
   `source-credibility`'s job.

## Output format spec

Return a structured list:

```text
Query: <query>
Coverage: <what was searched>

Candidates:
1. URL: <url>
   Title: <title>
   Snippet: <snippet>
   Date: <date or unknown>
   Type: news | blog | official | forum | other
```

## Failure modes

- **No results:** return an empty candidate list with the coverage note, and
  flag that the query space is exhausted. Do not fabricate sources.
- **Paywalled or inaccessible:** record the URL as inaccessible and continue;
  do not block on it.
- **Ambiguous topic:** if the query is too vague to search meaningfully, ask the
  calling agent for a more specific query rather than guessing.
- **Search tool unavailable:** report the failure to the calling agent with the
  query that failed, so it can be retried or the coverage note updated.