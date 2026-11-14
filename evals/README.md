# Eval Harness (Markdown Specification)

This directory contains evaluation specifications for the Universal Multi-Agent Intelligence System. Since Stage 1 has no runtime, evals are **manual specifications** — they describe how a human would run the pipeline on a test question and judge the output.

## What an Eval Is

An eval is a test case with:
- A **question** to run through the full pipeline.
- An **expected verdict** (direction and key points).
- An **expected confidence level** (HIGH, MODERATE, LOW).
- **Fail criteria** — specific conditions that would make the eval fail.

## How to Run an Eval (Manual)

1. Take the `question` from the eval file.
2. Run the full 7-agent pipeline manually (Orchestrator → Researcher → Domain Expert → Critical Thinking → Fact-Checker → Debater → Final Decision), following the process in `CONTRIBUTING.md`.
3. Record the **actual verdict**, **actual confidence**, and the **full evidence chain** with source URLs.
4. Compare the actual output to the expected values in the eval file.
5. Apply the pass/fail rules below.

## Pass/Fail Rules

The eval **FAILS** if any of the following is true:

| Rule | Description |
|------|-------------|
| **Wrong direction** | The verdict direction contradicts the expected verdict (e.g., expected "No from Moon" but got "Yes from Moon"). |
| **Confidence too high** | Confidence is HIGH when the expected is MODERATE or LOW, OR confidence is MODERATE when expected is LOW. Confidence can be lower than expected (conservative is OK). |
| **CONFIRMED without URL** | Any claim labelled **CONFIRMED** lacks a retrievable URL to the primary source. |
| **Invented source** | Any source, statistic, or citation in the output cannot be retrieved or does not exist. |
| **Missing uncertainty** | The verdict does not include an explicit uncertainty statement listing unresolved points. |

The eval **PASSES** only if none of the above failures occur.

## Eval Files

| File | Question | Expected Verdict Direction | Expected Confidence |
|------|----------|----------------------------|---------------------|
| `01-great-wall.md` | Is the Great Wall visible from space with the naked eye? | No from Moon, barely from LEO | MODERATE |
| `02-small-shop-online.md` | Should a small shop in Pakistan start selling online? | Yes, lean test first on Daraz/Instagram/WhatsApp with COD | MODERATE |
| `03-ev-pakistan-2030.md` | Should Pakistan make 30% of new vehicle sales electric by 2030? | No as blanket target for cars; phased yes for 2/3-wheelers | MODERATE |

## Adding a New Eval

1. Create a new file `evals/NN-descriptive-name.md` using the template below.
2. Update this README with a new row in the table above.
3. Do not commit code — evals are markdown specifications only.

### Template

```markdown
# Eval: [Short Name]

## Question
> [The exact question to run through the pipeline]

## Expected Verdict
[The expected direction and key points of the verdict]

## Expected Confidence
[HIGH | MODERATE | LOW]

## What Would Fail This Eval
- Wrong direction: [specific verdict direction that would be wrong]
- Confidence too high: [HIGH when expected MODERATE/LOW, etc.]
- CONFIRMED without URL: any CONFIRMED claim without a retrievable primary source URL
- Invented source: any source that cannot be retrieved
- Missing uncertainty: verdict lacks explicit uncertainty statement
```