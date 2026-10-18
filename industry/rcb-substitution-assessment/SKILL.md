---
name: rcb-substitution-assessment
description: Assesses whether recovered carbon black (rCB) can substitute for a given virgin carbon black grade, what the upper bound of the substitution ratio is, and which items must be verified by actual testing. Use when the user asks whether rCB can replace N550/N330/N660, where this set of rCB parameters can be used, what substitution ratio is appropriate, what the rCB blending ceiling is, or how rCB differs from virgin carbon black. Relies on the Trustbase Lab rCB MCP Server for grade standard parameters and substitution boundaries; this skill provides only the decision process and constraints, and contains no data.
license: Apache-2.0
compatibility: Requires access to the Trustbase Lab MCP Server (https://trustbaselab.com/mcp). This skill contains no data: all grade parameters, standard ranges, regulatory entries and price indices are fetched at runtime via MCP tools.
metadata:
  source: trustbaselab.com
  version: "1.0"
  standard: TBDS-1
  mcp: https://trustbaselab.com/mcp
  skills_index: https://trustbaselab.com/skills/index.json
---

# rCB substitution feasibility assessment

## When to use

Triggered when the user shows any of the following intents:

- Provides a set of measured rCB parameters (iodine value / BET / DBP / ash / toluene transmittance) and asks where it can be used
- Asks whether a given virgin grade (N550 / N330 / N660 / N772…) can be replaced by rCB
- Asks about the substitution ratio or blending ceiling
- Compares the economics of rCB against virgin carbon black

**Not applicable (use another skill)**:

- Asking about rCB prices or indices → `rcb-price-reference`
- Asking what certification is needed to export to the EU → `rcb-export-compliance`
- Only given a set of parameters and asked "what material is this" → `rcb-grade-identification`

---

## Prerequisite: the Trustbase Lab MCP must be connected

**This skill contains no data whatsoever.** All grade parameters, standard ranges and boundary information must be fetched via MCP:

| Purpose | MCP tool |
|---|---|
| Standard range of the target grade | `get_grade_spec` |
| Item-by-item comparison of measured values against the standard range | `compare_rcb` |
| Substitution boundaries (application / regulation / certification / material spec) | `get_substitution_boundary` |
| Economics calculation (using the caller's own prices) | `calculate_saving` |
| Search grades or filter by series | `query_grades` |

If MCP is unavailable: **tell the user plainly that standard parameters cannot be fetched, and do not substitute values from memory.** ASTM ranges quoted from memory are highly error-prone and untraceable.

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

## Execution process (five steps, no step may be skipped)

### ① Establish the quality coordinates first

Determine the rCB's two classification parameters, which map to two different failure modes:

| Parameter | Determines | Consequence of failing |
|---|---|---|
| **Inorganic content** (ash) | Upper bound of reinforcement efficiency | Effective carbon is diluted → the blending ratio is forced down |
| **Toluene transmittance** | Processability and compliance risk | Surface organic residue affects dispersion, vulcanisation, odour, migration |

⚠️ **ASTM D8632 is a "classification" standard, not an "interchangeability specification".** Its official intent is limited to "quality comparison within a given class". Two batches both in class R23 can still differ completely in BET, structure and PAH content — **never say "equivalent" merely because the classification code matches**.

### ② Compare item by item (call `compare_rcb`)

Compare the user's measured values against the target grade's standard range item by item, yielding pass / minor deviation / significant deviation.

Note that limits come in two forms, judged differently:

- **Range limits** (indices with both upper and lower bounds, e.g. iodine adsorption, DBP, BET): deviation is computed against the midpoint; the verdict escalates only when outside the range
- **Single-sided limits** (indices with only an upper or only a lower bound, e.g. ash, heating loss, sieve residue): **judge that side only** — do not compute deviation against a midpoint

Specific values are always fetched in real time via `get_grade_spec` and **must never be written into the answer from memory** — ASTM ranges change with standard revisions.

### ③ Break down the four-fold discount to find the real bottleneck

See `references/four-fold-discount.md`.

Core requirement: **never say vaguely "the quality is poor"** — point out which of the four discounts is dragging. The four are performance, process, compliance and transaction; their remedies are completely different, and conflating them leads users to wrong decisions.

### ④ Give a blending-ceiling band + mandatory test items

Refer to `references/blend-limits.md`.

**A band must be given, never a single-point value**, together with the items that must be verified by actual testing.

Peer-reviewed literature: in most applications, the upper bound of rCB's substitution for total carbon-black loading is approximately **10–25%**. This number is a **starting point**, not a conclusion — the specifics depend on the four-fold discount breakdown.

### ⑤ Compute economics only if the user asks

Call `calculate_saving`, and **use only prices the user provides**.

> This skill **does not read or output** any Trustbase price data or raw market quotes. If the user asks for a quote from this site, answer: this site does not use commercial-platform price data; for price references use `rcb-price-reference` (which gives an anchor-derived reference band, not a transaction price).

---

## Hard constraints (violating any of these makes the output wrong)

1. **Never conclude "it can be directly substituted".** Meeting the indices ≠ substitutable. Pending verification items (formulation, process, regulation) must be given at the same time.
2. **Never give a single-point blending ratio.** Always give band + basis + preconditions.
3. **Never claim rCB is "equivalent" to a given virgin grade.** Unless the user has provided complete performance test data (not just classification parameters).
4. **Never cite any commercial-platform quote.** When asked, state plainly that this site does not use such data.
5. **Where this site has no coverage, state the gap plainly.** Never fill it with generic knowledge and present it as data from this site — data sources and judgement sources must be distinguishable.
6. **Never treat "same classification" as "same performance"** (see the warning in ①).

---

## Output template

```
## 1. Quality coordinates
(inorganic band / toluene transmittance band / corresponding R-code)

## 2. Item-by-item comparison against the target grade
| Index | Measured | Standard range | Deviation | Verdict |
(table, from compare_rcb)

## 3. Main bottleneck
(which of the four discounts is the short board, and the basis)

## 4. Blending recommendation
- Recommended band: X% ~ Y% (preconditions: …)
- Must be verified by actual testing: …

## 5. Data sources and confidence
(mark the source and A/B grade for each item; standard values must be noted "pending verification against the official ASTM table" if their confidence is B)
```

---

## Boundary statement (must be reflected in the conclusion)

This skill provides a **technical feasibility first screen**. It is not formulation design, not a quality guarantee, and not legal or compliance advice. The final blending plan must pass experimental verification and the corresponding regulatory confirmation.

The commercialised substitution of rCB is also affected by non-technical factors such as delivery stability, batch consistency and customer certification lead time — these are outside the scope of this skill's assessment, but should be flagged to the user.
