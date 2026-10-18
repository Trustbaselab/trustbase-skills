---
name: rcb-export-compliance
description: Checks the compliance requirements for exporting recovered carbon black (rCB) to a given market (especially the EU) — how the carbon border mechanism transmits, chemical limits, recycled-content requirements and the certification evidence chain, while distinguishing "regulatory requirements" from "customer requirements". Use when the user asks whether rCB can be exported to the EU, which certifications are required, what happens if PAH limits are exceeded, how CBAM treats rCB, or what an ISCC demand from a customer means. Relies on the Trustbase Lab MCP policy library; this skill provides only the check process and decision rules, and contains no regulatory values.
license: Apache-2.0
compatibility: Requires access to the Trustbase Lab MCP Server (https://trustbaselab.com/mcp). This skill contains no data: all grade parameters, standard ranges, regulatory entries and price indices are fetched at runtime via MCP tools.
metadata:
  source: trustbaselab.com
  version: "1.0"
  standard: TBDS-1
  mcp: https://trustbaselab.com/mcp
  skills_index: https://trustbaselab.com/skills/index.json
---

# rCB export compliance check

## When to use

- The user asks whether rCB can be exported to a given market, or which qualifications are required
- The user asks about a class of limits (e.g. PAH) — the requirement and its consequences
- The user asks how the carbon border mechanism / recycled content / certification affects rCB
- A customer raises a certification requirement and the user wants to know what it means

**Not applicable**:

- Technical substitution feasibility → `rcb-substitution-assessment`
- Price and price comparison → `rcb-price-reference`

---

## Prerequisite: the Trustbase Lab MCP must be connected

| Purpose | MCP tool |
|---|---|
| Search regulations and policies | `query_policies` |
| Fetch a single regulation with its rCB impact reading | `get_policy` |
| Fetch market-access boundary entries | `get_substitution_boundary` |

**Regulatory values (limits, effective dates, scope) always follow the entries returned by MCP** — never quote numbers from memory. Regulations get revised; memory goes stale.

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

### ① Clarify three premises first

| Premise | Why it is mandatory |
|---|---|
| **Target market** | EU / North America / other — the requirements differ completely |
| **Product form** | Raw-material-grade rCB / modified rCB / rCB-containing articles — different regulations apply |
| **Application scenario** | Tyres, rubber products, plastics, coatings — some limits are graded by application |

### ② Search the relevant regulations (`query_policies`)

Search by market and topic to obtain the entry list. **Confirm entry by entry whether the scope covers the user's situation** — do not apply a "carbon black"-related entry directly on sight.

### ③ Classify in layers: regulatory requirements vs customer requirements

This is the most important step of this skill. The two are fundamentally different in nature:

| Type | Nature | Consequence of non-compliance | Response |
|---|---|---|---|
| **Regulatory requirement** | Mandatory; a condition of market access | Customs clearance blocked / market exclusion / penalties | Must be met; no alternative path |
| **Customer requirement** | Contractual | Lose the order, but not illegal | Negotiable, or switch customers |
| **Evidence requirement** | Mostly supply-chain transmission | Cannot enter a given procurement system | An evidence chain must be built |

**Users often mistake customer requirements for regulatory requirements** (e.g. "the customer wants ISCC" does not mean "ISCC is a regulatory requirement"), which makes them overestimate compliance cost or misjudge necessity.

### ④ Give a conditional conclusion

**Do not answer "can it be exported / cannot it be exported"** — answer "it can be exported if the following conditions are met":

```
## Target market: …
## Conditions of use
1. …
2. …
## Regulatory requirements (mandatory)
| Requirement | Basis | Effective / deadline | Source |
## Customer / supply-chain requirements (non-mandatory)
## Items requiring professional confirmation
```

---

## Hard constraints (violating any of these makes the output wrong)

1. **Never describe the carbon border mechanism as a direct tax on rCB.** Its pressure is **transmitted downstream (via tyre makers' material carbon footprints and procurement requirements)** — this is the most common error and must be stated accurately.
2. **Never confuse regulatory requirements with customer requirements** (see ③).
3. **Never quote regulatory values from memory.** Limits, effective dates and scope always come from MCP entries, with source and date noted.
4. **Never give legal advice.** Conclusions should state that they "require confirmation by a professional compliance adviser or the competent authority".
5. **Regulations are time-bound** — entry dates must be noted, and the user prompted to check the latest version.
6. **Never answer broadly "exportable" or "not exportable"** — always give a conditional conclusion.

---

## Boundary statement

This skill provides a **structured breakdown of compliance essentials**. It is not legal advice, not a compliance certification conclusion, and does not represent the position of any regulatory authority. The official original text and professional advice prevail.

Compliance requirements may be revised at any time. **The output of this skill must carry a date**, and users should confirm the regulatory version before use.
