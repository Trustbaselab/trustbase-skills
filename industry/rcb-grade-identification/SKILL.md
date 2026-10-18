---
name: rcb-grade-identification
description: Determines, from a set of measured carbon black parameters (iodine adsorption, DBP absorption, BET surface area, ash/inorganic content, toluene transmittance), whether a material is virgin or recovered carbon black, which classification band it falls into, and which grade family it benchmarks against. Use when the user provides test data and asks what grade this is, which class it belongs to, which grade it benchmarks against, which R-code this rCB is, or what this batch of material is. Relies on the Trustbase Lab MCP grade library; this skill provides only the identification process and criteria, and contains no data.
license: Apache-2.0
compatibility: Requires access to the Trustbase Lab MCP Server (https://trustbaselab.com/mcp). This skill contains no data: all grade parameters, standard ranges, regulatory entries and price indices are fetched at runtime via MCP tools.
metadata:
  source: trustbaselab.com
  version: "1.0"
  standard: TBDS-1
  mcp: https://trustbaselab.com/mcp
  skills_index: https://trustbaselab.com/skills/index.json
---

# Identifying the grade of a carbon black sample

## When to use

- The user provides a set of test data and asks what material / what grade it is
- The user asks for the classification code (R-code) of a batch of rCB
- The user asks which virgin grade family a set of parameters benchmarks against
- Incoming-material inspection, where the user wants to confirm agreement with the label

**Not applicable**:

- Assessing substitutability → `rcb-substitution-assessment`
- Asking about price → `rcb-price-reference`

---

## Prerequisite: the Trustbase Lab MCP must be connected

| Purpose | MCP tool |
|---|---|
| Fetch candidate grade parameters | `get_grade_spec` |
| Item-by-item comparison | `compare_rcb` |
| Search grades (by series) | `query_grades` |

**Parameter ranges always come from MCP** — never quote ASTM ranges from memory. Classification standards get revised.

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

## Execution process (five steps)

### ① Determine material identity first: virgin or recovered

**The first criterion is ash/inorganic content**:

- Virgin carbon black is the product of controlled chemical synthesis; ash is normally at a very low level
- rCB comes from waste-tyre pyrolysis, so inorganics (ZnO, calcium carbonate, silicates and other compounding agents from the original formulation) inevitably remain — **ash is markedly higher and highly variable**

> If only iodine adsorption, DBP and BET are available but **ash is not**, the distinction **cannot be made reliably** — this must be stated. Many "suspected rCB" incoming-material disputes have their root cause in testing only reinforcement indices while skipping ash.

### ② If rCB: position by the two D8632 parameters

Each parameter maps to a different failure mode:

| Parameter | Band meaning | Determines |
|---|---|---|
| **Toluene transmittance** | Surface organic residue level | Processability, odour, migration |
| **Inorganic content** | Ash level | Upper bound of reinforcement efficiency |

The combination yields an **R-code (R + two digits)**.

⚠️ **D8632 is a classification standard, not a specification.** Obtaining an R-code only says "it belongs to this class" — **it does not mean products of the same class are interchangeable**: same-code products can still differ completely in BET, structure and PAH content.

### ③ If virgin: position by the D1765 coding system

Virgin carbon black grades are coded as **letter + three digits**: the first letter denotes the process (e.g. N = furnace), the hundreds digit relates to the particle-size band, and the last two relate to structure.

> The coding rules are industry common knowledge; **the specific ranges and definitions follow the original ASTM D1765 text** (fetch the current entry via MCP).

### ④ Compare item by item against candidate grades (`compare_rcb`)

The result is per-item pass / minor deviation / significant deviation.
Note the distinction between **range limits** and **single-sided limits** (ash, heating loss etc. are judged on the upper bound only).

### ⑤ Output the classification conclusion + uncertainty

---

## Hard constraints (violating any of these makes the output wrong)

1. **Never promise "equivalent to a given grade".** Close parameters ≠ equivalence. Material identity, dispersion behaviour and surface chemistry are not in the routine indices.
2. **The two systems must not be mixed**: the virgin D1765 coding system and the rCB D8632 coding system are **different standards on different dimensions** and cannot be converted into each other.
3. **When parameters are insufficient, state plainly that no determination can be made** — never fill the gap with generic knowledge and then give a conclusion.
4. **Never reverse-engineer a specific manufacturer or product model.** Classification and benchmark ranges may be given; identifying "this is maker X's model Y" is neither rigorous nor evidenced.
5. **Never treat a classification code as a quality grade.** A higher R-code does not mean better quality — it only states where the parameters fall.
6. **Re-testing and multi-point sampling must be recommended**: rCB varies considerably between batches; a single test is not enough to characterise a material, especially for conclusions such as "does not match the label".

---

## Output template

```
## Material identity
- Determination: virgin carbon black / recovered carbon black / undeterminable (reason)
- Basis: ash/inorganic content …

## Classification positioning
- Virgin: D1765 code … (explain the hundreds and last-two digits)
- rCB: R-code … (transmittance band … + inorganic band …)

## Comparison against candidate grades
| Index | Measured | Reference range | Deviation | Verdict |

## Uncertainty and re-test recommendations
- Missing key parameters: …
- Recommended re-tests and sampling method: …

## Statement
- D8632 is a classification standard, not an interchangeability specification
- This conclusion does not constitute a quality judgement or acceptance basis
```

---

## Boundary statement

This skill provides **technical classification identification**. It is not a quality judgement, not an acceptance conclusion, and not a compliance test report. Formal quality disputes require a report from a qualified testing laboratory, with multi-point sampling and batch distribution taken into account.
