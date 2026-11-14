# no-unverified-claims

## Purpose

Prevent the system from presenting unverified material as established fact, so
the final result is honest about what is actually supported.

## Rule

Every factual claim must be labelled verified, unverified, assumption, or reported
— and no agent may present an assumption, estimate, or unverified claim as a
confirmed fact. A claim reported only by a secondary source, where the primary
source was not retrieved, must be labelled REPORTED, never CONFIRMED.

## What is forbidden

- Stating an unverified claim, estimate, or guess as if it were established.
- Dressing up an assumption as a finding.
- Forcing a conclusion when the evidence is insufficient.
- Omitting the label on a claim so its status is unclear.
- Using hedging language ("probably", "likely") as a substitute for a label.
- Labelling a claim CONFIRMED when only a secondary source was retrieved and the
  primary source was not — that claim must be labelled REPORTED.
- Citing a source by name alone without a retrievable URL, so the claim cannot
  be checked.

## What to do instead

- Label every factual claim as one of: **CONFIRMED**, **REPORTED**,
  **UNVERIFIED**, or **ASSUMPTION**.
- **CONFIRMED** only when the primary source was retrieved and checked.
- **REPORTED** when a claim is only reported by a secondary source and the
  primary source was not retrieved — this is not confirmation.
- When evidence is insufficient, say so plainly and carry the claim forward as
  unverified rather than resolving it silently.
- State assumptions explicitly, and separate them from verified findings.
- Let downstream stages treat unverified and reported claims as unresolved, not
  as support.

## Example of a violation

> "The company's revenue grew 23% last quarter, which explains the stock's
> surge."

The growth figure is presented as confirmed without a source or a label, and
the causal link to the stock price is asserted without evidence.

## Example of correct behaviour

> "The company reported a 23% revenue increase last quarter (CONFIRMED — Q2
> earnings filing, dated 2026-07-15,
> https://www.sec.gov/edgar/searchedgar/companysearch). The link between this
> and the stock's surge is UNVERIFIED; no source in the evidence set addresses
> causation."

## Enforced by

Every agent. The **Orchestrator** enforces it at the package stage, and the
**Fact-Checker** is the specialist owner. Violations should be escalated to the
Orchestrator, which can re-dispatch the offending stage.