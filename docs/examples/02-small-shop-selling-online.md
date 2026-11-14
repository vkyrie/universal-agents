# Example 2: Should a small shop start selling online?

## Task
> Should a small shop start selling online? Give a final verdict with pros, cons, risks, and uncertainty.

---

## Orchestrator Brief
**Agents selected:** Researcher, Domain Expert, Critical Thinking, Fact-Checker, Debater, Final Decision.
**Confidence bar:** MODERATE. This is a business decision with context-dependent variables.
**Scope:** Small independent retail shop (1–5 locations), considering an e-commerce channel. No specific industry or geography assumed.

---

## Research Findings
**Sources retrieved:**

| ID | Source | Type | Retrievable URL |
|----|--------|------|-----------------|
| S1 | U.S. Census Bureau, "E-Commerce Retail Sales" (quarterly) | Official statistics | https://www.census.gov/retail/index.html |
| S2 | Shopify, "Future of Commerce 2024" (annual report) | Industry report | https://www.shopify.com/research/future-of-commerce |
| S3 | National Retail Federation, "Retail's Digital Transformation" | Industry association | https://nrf.com/resources/retail-library |
| S4 | McKinsey Global Institute, "The future of retail" | Consulting analysis | https://www.mckinsey.com/industries/retail |

**Claims extracted:**

| Claim | Source | Quote/Value | Status |
|-------|--------|-------------|--------|
| C1: U.S. e-commerce share of retail sales reached ~15.6% in Q4 2023. | S1 (Census) | "E-commerce sales in Q4 2023 accounted for 15.6% of total retail sales." | REPORTED (Census page retrieved; specific quarterly table not deep-linked) |
| C2: Global e-commerce sales projected to reach $6.3 trillion by 2024. | S2 (Shopify) | "Global e-commerce sales expected to hit $6.3 trillion in 2024." | REPORTED (Shopify report retrieved; methodology page not retrieved) |
| C3: 76% of consumers say they shop online for convenience. | S2 (Shopify) | "76% of respondents cite convenience as a top reason for online shopping." | REPORTED (survey methodology not retrieved) |
| C4: Small businesses with online channels grow revenue 2x faster than offline-only. | S3 (NRF) | "Omnichannel retailers saw 2x revenue growth vs. single-channel." | REPORTED (NRF report retrieved; underlying data not retrieved) |
| C5: Average customer acquisition cost (CAC) for small e-commerce: $30–$50. | S4 (McKinsey) | "CAC for DTC brands ranges $30–$50 depending on channel." | REPORTED (McKinsey article retrieved; underlying study not retrieved) |
| C6: Average cart abandonment rate: ~70%. | S1 (Census) / industry benchmark | "Cart abandonment averages ~70% across sectors." | REPORTED (widely cited benchmark; no single primary source retrieved) |
| C7: Returns rate for online apparel: 20–30%. | S3 (NRF) | "Online apparel returns average 20–30%." | REPORTED (NRF retrieved; primary data not retrieved) |
| C8: Shopify Basic plan: $39/mo + 2.9% + 30¢ per transaction (US). | S2 (Shopify) | Pricing page shows $39/mo base. | CONFIRMED (pricing page retrieved and verified at https://www.shopify.com/pricing) |
| C9: WooCommerce core is free; hosting $10–$30/mo; payment fees ~2.9% + 30¢. | S2 (Shopify) / general knowledge | — | REPORTED (pricing components from public pages; no single primary source for full stack) |
| C10: 30% of small businesses fail within 2 years; online adds complexity. | S1 (Census) / SBA data | "About 30% of small businesses fail within 2 years (SBA)." | REPORTED (SBA statistic widely cited; original SBA table not retrieved) |

**Coverage note:** All sources are industry reports or official statistics pages — no primary survey microdata or proprietary small-business financials retrieved. All numeric claims are REPORTED except C8 (platform pricing, directly verified).

---

## Domain Expert Read
**Domain:** Small business strategy, e-commerce operations, retail economics.

**Plausibility assessment:**
- **Market trend (C1–C4):** Directionally correct — e-commerce share has grown steadily for 15+ years. The "2x growth" claim (C4) is plausible for omnichannel vs. single-channel but likely confounds selection bias (businesses that go online may already be better-run). **Flagged as correlation, not causation.**
- **Costs (C5, C8, C9):** CAC $30–$50 (C5) is plausible for paid social but highly variable by niche; $300–$1000/mo total operating cost (platform + ads + fulfillment) is a reasonable floor for a small shop. **C8 CONFIRMED; C9 REPORTED.**
- **Operations (C6, C7):** 70% cart abandonment (C6) and 20–30% returns (C7) are standard industry benchmarks. Apparel/footwear returns skew high; hard goods lower. **Plausible as averages.**
- **Risk (C10):** 30% 2-year failure rate is a general SBA statistic, not specific to e-commerce. **Not directly applicable** — the relevant risk is incremental failure from online investment, which is unquantified.

**Open questions:**
- What is the shop's current margin structure? (Online fees of ~3–5% + shipping can erase thin margins.)
- Does the shop have fulfillment capacity? (Packing/shipping time is a hidden cost.)
- What is the competitive landscape? (Local vs. national; niche vs. commodity.)
- No source retrieved on incremental profitability for *small independent* shops specifically — most data is for DTC brands or omnichannel chains.

---

## Critical Thinking Challenges
| ID | Assumption / Gap / Alternative | Severity |
|----|--------------------------------|----------|
| A1 | **"Small shop" is one thing.** A boutique with 80% margins differs from a convenience store with 15%. The verdict is meaningless without margin/volume context. | CRITICAL |
| A2 | **Correlation ≠ causation (C4).** Omnichannel retailers growing 2x may be better businesses to start with. No RCT or quasi-experiment retrieved. | HIGH |
| A3 | **Average CAC (C5) is not your CAC.** Small shops lack brand, creative, and data for efficient ads. Their CAC is often 3–5x benchmarks. | HIGH |
| A4 | **Hidden costs unquantified.** Fulfillment labor, returns processing, customer service, chargebacks, platform lock-in, SEO/ads management time. No source retrieved. | HIGH |
| A5 | **Channel cannibalization.** Online sales may just shift in-store buyers to a lower-margin channel (shipping eats margin). No source retrieved. | MODERATE |
| A6 | **Platform risk.** Policy changes, fee increases, account suspension. No source retrieved. | MODERATE |
| A7 | **Alternative: marketplace first.** Selling on Etsy/Amazon/Google Shopping before own site lowers fixed cost but increases take-rate. Not explored. | LOW |

---

## Fact-Checking Labels
| Claim | Label | Reason |
|-------|-------|--------|
| C1 | REPORTED | Census page retrieved; specific Q4 2023 table not deep-linked. |
| C2 | REPORTED | Shopify report retrieved; methodology not retrieved. |
| C3 | REPORTED | Survey methodology not retrieved. |
| C4 | REPORTED | NRF report retrieved; underlying data not retrieved; correlation not causation. |
| C5 | REPORTED | McKinsey article retrieved; underlying study not retrieved; range too wide to be actionable. |
| C6 | REPORTED | Benchmark widely cited; no single primary source retrieved. |
| C7 | REPORTED | NRF retrieved; primary data not retrieved. |
| C8 | **CONFIRMED** | Shopify pricing page retrieved and verified at https://www.shopify.com/pricing |
| C9 | REPORTED | Components from public pages; no single primary source for full stack. |
| C10 | REPORTED | SBA statistic widely cited; original table not retrieved; not e-commerce specific. |

---

## Debate Pro/Con

**Question:** Should a small shop start selling online?

**Pro:**
- **Market access:** E-commerce share growing (C1 REPORTED, C2 REPORTED) — online is where customer growth is.
- **Omnichannel advantage:** Multi-channel retailers grow faster (C4 REPORTED) — even if correlational, the capability is becoming table stakes.
- **Customer expectation:** 76% shop online for convenience (C3 REPORTED) — not having a channel loses buyers.
- **Low barrier to start:** Shopify $39/mo (C8 CONFIRMED); WooCommerce free core. Can test with minimal fixed cost.
- **Data ownership:** Own site = customer data, email list, retargeting — not possible on marketplace-only.
- **Scalability:** Once systems work, marginal cost of additional sales is low vs. opening a second physical location.

**Con:**
- **Margin erosion:** 3–5% platform/payment fees + shipping + returns (C7 20–30%) + CAC (C5 REPORTED $30–50) often exceed in-store margin for small shops.
- **Hidden labor:** Packing, shipping, customer service, returns processing = 10–20 hrs/wk for a small shop. No source retrieved — but operational reality.
- **Cannibalization risk:** Existing in-store customers may shift online, same revenue at lower margin.
- **Competitive intensity:** Competing with Amazon, big-box, and well-funded DTC brands on ads/SEO. CAC for small shops often 3–5x benchmarks (A3).
- **Platform dependency:** Fee hikes, policy changes, account suspension can kill the channel overnight. (A6)
- **Failure rate context:** 30% 2-year failure (C10 REPORTED) — adding fixed cost + complexity to a fragile business is risky.

**Closed points:**
- Platform pricing (C8 CONFIRMED) is known and low enough to test.
- Market trend (C1, C2) is real and sustained.

**Open points:**
- **Your margins** — unknown, decisive.
- **Your fulfillment capacity** — unknown, decisive.
- **Incremental profitability for *your* SKU mix** — no source retrieved.
- **Cannibalization vs. incrementality** — no source retrieved for small independents.

---

## Final Decision Verdict

**Verdict: Yes, with conditions — but the conditions are the agent's test rules, not evidence from sources.**

**Proceed IF (agent's test rules — not sourced evidence):**
1. **Gross margin sufficient to absorb online costs** — platform fees (~3–5%), shipping, returns, CAC. No source retrieved for a universal minimum margin threshold; the agent's test rule of ≥50% is a heuristic, not a cited number.
2. **Average order value supports unit economics** — must exceed per-order costs (fees + shipping + CAC). No source retrieved for a universal AOV threshold; the agent's test rule of ≥$50 is a heuristic, not a cited number.
3. **Fulfillment capacity exists** (can pack/ship 10–20 orders/day without hiring) — or budget for 3PL. No source retrieved for a universal order-volume threshold.
4. **Start on marketplace (Etsy/Amazon/Google Shopping) first** — test demand at 15–45% take-rate before committing to own-site fixed costs. Agent's test rule; no source retrieved for these specific marketplace take-rates or test duration.
5. **Set a 90-day test budget** ($2,000–$5,000 for ads + platform) and a kill criterion (e.g., CAC > $75 or ROAS < 2.0). Agent's test rule; no source retrieved for these specific numbers.

**Do NOT proceed if:**
- The shop cannot absorb online costs at current margins (agent's judgment).
- The shop has no fulfillment capacity and no budget for 3PL.
- The shop is already cash-flow negative — adding fixed cost increases failure risk (C10 REPORTED).

**Confidence: MODERATE.**
- High confidence on the *conditions* — they follow from unit economics that are mathematically sound.
- Moderate confidence on the *market data* — all trend claims are REPORTED, no primary sources retrieved, and correlation/causation is unresolved (A2).
- **Major uncertainty:** The shop's specific numbers (margin, AOV, fulfillment) are not in evidence. The verdict is a framework, not a yes/no for any specific shop. The specific thresholds (≥50% margin, ≥$50 AOV, 90-day test, etc.) are the agent's test rules, not evidence from sources.

**Uncertainty:**
- No primary data on incremental profitability for small independents.
- CAC benchmarks (C5) are for funded DTC brands, not owner-operated shops.
- Returns rate (C7) varies wildly by category — apparel 30%, electronics 10%, books 5%.
- Platform fee changes (Shopify raised prices 2023, 2024) — future costs unknown.
- Cannibalization vs. incrementality unquantified.

**Recommended action:** Run the 5-condition checklist above as the agent's test rules. If all pass, launch a 90-day marketplace test with a strict budget and kill criteria. Do not build a custom site or commit to annual platform contracts until the test validates unit economics. All specific thresholds are the agent's test rules, not sourced evidence.