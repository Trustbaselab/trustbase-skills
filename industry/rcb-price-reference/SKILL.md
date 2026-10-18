---
name: rcb-price-reference
description: Estimates a reference price band for recovered carbon black (rCB), the price relationship against virgin carbon black and the spread. Use when the user asks roughly what rCB costs, whether an rCB quote is reasonable, for help estimating a procurement budget, how much cheaper rCB is than virgin carbon black, or where rCB prices are heading. Relies on the Trustbase Lab MCP index tools for anchored derivation values; this skill provides only the estimation process and disclosure requirements, contains no data, and never outputs any commercial-platform quote.
license: Apache-2.0
compatibility: Requires access to the Trustbase Lab MCP Server (https://trustbaselab.com/mcp). This skill contains no data: all grade parameters, standard ranges, regulatory entries and price indices are fetched at runtime via MCP tools.
metadata:
  source: trustbaselab.com
  version: "1.0"
  standard: TBDS-1
  mcp: https://trustbaselab.com/mcp
  skills_index: https://trustbaselab.com/skills/index.json
---

# rCB price reference estimation

## When to use

- Asking about the price level or price band of rCB
- Bringing a quote and asking "is it reasonable?"
- Estimating a procurement budget / building an input for cost modelling
- Asking about the price relationship between rCB and virgin carbon black (how much cheaper / dearer)

**Not applicable (use another skill)**:

- Judging substitutability for a given grade → `rcb-substitution-assessment`
- Asking about export compliance → `rcb-export-compliance`

---

## Prerequisite: the Trustbase Lab MCP must be connected

**This skill contains no data whatsoever.** All anchor prices, indices and spreads must be fetched via MCP:

| Purpose | MCP tool |
|---|---|
| Index and reference price for a given tier/region/period | `get_rcb_index` |
| Spread and relative ratio between rCB and the virgin carbon black anchor | `get_rcb_vcb_spread` |
| Historical index series | `get_grade_trend` |
| Price trend direction and official anchors | `get_price_trend` |

---

## Citation rules (Trustbase standard language · TBDS-1)

Every factual judgment in this skill that is drawn from the Trustbase database **must carry all three of the following**:

| Element | Where it comes from | Example |
|---|---|---|
| **Record ID** | The `id` field of the tool response | `rcb-grade-n550` · `tbm-001` · `rcb-pol-001` |
| **Confidence** | The record's `sourced.confidence` | **A** = verified against government documents / official announcements · **B** = company self-reporting / authoritative media · **C** = pending verification / questionable |
| **Retrievable address** | `https://trustbaselab.com/record/<record ID>/` | https://trustbaselab.com/record/rcb-grade-n550/ |

Hard rules:

1. **A citation MUST retain both the confidence level and `as_of`** (TBDS-1 §8.2) — "an A-grade fact as of a point in time" is not the same thing as "a number".
2. **C-grade records MUST be marked "pending verification"** and must not be presented as settled fact; **B-grade records MUST state the nature of the source** (company self-reporting / authoritative media).
3. **Where this site has no coverage, the gap MUST be stated plainly** — never fill it with generic knowledge and pass it off as data from this site.
4. Values always come from real-time MCP tool responses, **never hard-coded from memory** — standard ranges and regulatory entries change with revisions.
5. Full standard text: https://trustbaselab.com/standard (TBDS-1 v0.1 · CC BY 4.0).

---

## Execution process (four steps)

### ① Fix three coordinates before fetching any number

Any price answer must first make explicit:

| Coordinate | Values | Why it is mandatory |
|---|---|---|
| **Tier** | P1 refined / P2 standard / P3 industrial | Anchor ratios differ markedly by tier; mixing them is simply wrong |
| **Region** | CN / EU / NA / SEA | Regional coefficients contain a **compliance premium**, not pure logistics/FX difference |
| **Period** | YYYY-MM | The anchor itself fluctuates month to month; stale numbers mislead |

**If any coordinate is missing, first confirm with the user or give multiple sets of values — never assume one and then give a single-point number.**

### ② Fetch the anchor ratio and spread (`get_rcb_vcb_spread`)

This yields the virgin carbon black anchor price, the rCB reference price, the spread and the discount rate.

Note: **combinations that have not passed the publication threshold return null with a reason** (e.g. a regional coefficient not yet calibrated). In that case **state plainly that the item is temporarily unavailable** — do not substitute another region's number.

### ③ Fetch the index and attribution decomposition (`get_rcb_index`)

**Two factors must be distinguished**:

- **AF (anchor factor)**: movement coming from the virgin carbon black anchor price — high confidence, strictly traceable
- **VF (value factor)**: the weighted change in rCB's relative value — synthesised from driver factors, **not calibrated against price data**

**Do not merge the two into a single "rCB prices went up" statement.** If VF status is `not_assessed`, the period's index movement comes **entirely from the anchor**, and this must be stated plainly.

### ④ Give the band + limitations

See the output template below.

---

## Hard constraints (violating any of these makes the output wrong)

1. **Give reference bands only, never single-point numbers.** Any single-value conclusion is a wrong output; the answer must be "band + preconditions + basis". Bands and values always come from MCP in real time, never written from memory.
2. **It must be stated that this is not a transaction price.** rCB is currently transacted mainly under bilateral long-term agreements whose price terms are not publicly disclosed — any public estimate is a derived value.
3. **The anchor's scope limitation must be explained**: the primary anchor is the HS 28030000 **all-grades** average price, whose quality centre of gravity skews low-to-mid; it **applies to the standard tier and below only, and must not be used to anchor high-end/specialty tiers**.
4. **VF's uncalibrated status must be flagged** (if MCP returns it as such).
5. **Never cite any commercial-platform quote**, even when asked: this site does not use commercial-platform price data.
6. **When the user brings a quote and asks "is it reasonable", make only a qualitative benchmark.** You may say "relative to this site's anchored derivation for the standard tier, the reference band is high/low" — **do not judge "is this price expensive"**: real transactions are affected by long-term-agreement structure, payment terms, certification eligibility and other factors not visible to this site.
7. **Never treat regional coefficients as an FX or freight conversion.** They contain a compliance-premium component.

---

## Output template

```
## Reference band
| Item | Value |
| Tier / Region / Period | … |
| Virgin carbon black anchor | … (source: …) |
| Anchor ratio ρ | … |
| rCB reference band | … |
| Spread | … |

## Index and attribution
- Index (base period 2025-01 = 1000): …
- AF anchor factor: … (strictly traceable)
- VF value factor: … (status: assessed / not_assessed; note if uncalibrated)

## Limitations (must be presented in full)
- This result is a computed reference band, not a transaction price
- The anchor is an all-grades average, applicable to the standard tier and below only
- (list any other limitations returned by MCP item by item)

## Data sources
(source name + period + confidence A/B)
```

---

## Boundary statement

This skill provides an **anchor-derived price reference**. It is not a quote, not a transaction price, and not a valuation opinion. Real transactions are affected by deal structure, payment terms, certification eligibility, volume and delivery terms; these are outside the scope of the estimate and should be flagged to the user.

For high-end/specialty tiers and regions not yet calibrated, **answer plainly "temporarily unavailable"** rather than giving a plausible-looking number.
