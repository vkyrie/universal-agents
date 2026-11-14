---
name: academic-search
description: Retrieve scholarly and primary-source material. Searches academic databases, citations, and primary-source repositories for a topic.
inputs:
  - query: a search query or list of queries
  - field: academic discipline or subfield, if known
  - date_range: preferred publication date range
  - primary_only: whether to prefer primary sources over secondary
outputs:
  - candidates: a list of scholarly/primary sources with title, authors, venue, date, and identifier (DOI, URL)
  - coverage_note: what was searched and what returned nothing
---

# academic-search

## Purpose

Retrieve scholarly and primary-source material. A capability used by the
Researcher — it finds material, it does not evaluate it.

## Step-by-step procedure

1. Take the query and, if a field is known, phrase it using that field's
   terminology and conventions.
2. Search academic databases and citation indexes, plus primary-source
   repositories where relevant.
3. Collect each source's title, authors, venue, publication date, and any
   persistent identifier (DOI, ISBN, URL).
4. Prefer primary sources when `primary_only` is set — accounts, datasets,
   original documents, direct reports — over secondary summaries.
5. De-duplicate sources that describe the same work.
6. Record which databases were searched and what returned nothing.
7. Return the candidate list without credibility assessment — that is
   `source-credibility`'s job.

## Output format spec

Return a structured list:

```text
Query: <query>
Field: <field or unknown>
Coverage: <what was searched>

Candidates:
1. Title: <title>
   Authors: <authors>
   Venue: <journal, conference, or repository>
   Date: <date or unknown>
   ID: <DOI / ISBN / URL or unknown>
   Type: primary | secondary
```

## Failure modes

- **No results:** return an empty candidate list with the coverage note and
  flag that the academic query space is exhausted. Do not fabricate sources.
- **No access to a database:** record it in the coverage note and continue with
  the sources that are reachable.
- **Ambiguous field:** if the discipline is unclear, search broadly and let the
  calling agent narrow the results.
- **Tool unavailable:** report the failure to the calling agent with the query
  that failed, so it can be retried or the coverage note updated.