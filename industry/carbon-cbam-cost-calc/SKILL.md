---
name: carbon-cbam-cost-calc
description: Estimates a CBAM certificate cost for a given product and explains why a given commodity is or is not inside CBAM scope. Use when the user asks how much CBAM will cost, what the carbon border adjustment means for their export, whether a specific product (e.g. carbon black, tyres, rubber goods) is covered by CBAM, when CBAM obligations start, or how CBAM cost compares across carbon prices. Relies on the Trustbase Lab MCP Server for the CBAM timeline, carbon prices and the cost calculator; this skill provides only the decision process and constraints, and contains no data.
license: Apache-2.0
compatibility: Requires access to the Trustbase Lab MCP Server (https://trustbaselab.com/mcp). This skill contains no data: CBAM timeline entries, carbon prices and cost arithmetic are fetched at runtime via MCP tools.
metadata:
  source: trustbaselab.com
  version: "1.0"
  standard: TBDS-1
  mcp: https://trustbaselab.com/mcp
  skills_index: https://trustbaselab.com/skills/index.json
---

# CBAM cost estimation and scope check

## When to use

Triggered when the user shows any of the following intents:

- Asks how much CBAM will cost for a shipment, or asks for a carbon border cost estimate
- Asks whether a specific product is covered by CBAM (steel / aluminium / cement / fertiliser / electricity / hydrogen / **or a product they assume is covered**)
- Asks when CBAM obligations start, what the transitional period is, when certificates must be surrendered
- Asks how CBAM cost changes with different carbon prices

**Not applicable (use another skill)**:

- Asking about rCB prices or indices → `rcb-price-reference`
- Assessing whether rCB can substitute a virgin grade → `rcb-substitution-assessment`
- Checking non-CBAM export requirements (ISCC, REACH, PAH, EUDR) → `rcb-export-compliance`

---

## ⚠️ Scope first, cost second — the most common error in this domain

**Carbon black (including rCB) is NOT in the current CBAM scope.**

CBAM's current coverage is six product categories: **cement, iron & steel, aluminium, fertilisers, electricity, hydrogen**. Everything else — including carbon black, tyres, rubber goods, most downstream manufactured products — is outside the current Annex I list.

**Therefore, the correct answer to "does carbon black need to pay CBAM?" is: no, not under the current scope.**

But that is not the end of the story, and saying only "no" is unhelpful. The real transmission path is:

```
CBAM does not directly regulate carbon black
        ↓
but carbon black's downstream customers (tyres, rubber goods, automotive)
are subject to CSRD / ESPR / DPP / Euro 7 / ISCC PLUS
        ↓
those customers therefore demand carbon-footprint data from their suppliers
        ↓
the supplier pressure is real, but it is customer-driven, not CBAM-driven
```

**Never say "CBAM covers carbon black". Never say "CBAM does not affect you at all" either.** Both are wrong. Say the scope, then say the transmission path.

---

## Prerequisite: the Trustbase Lab MCP must be connected

**This skill contains no data whatsoever.** All timeline entries, prices and arithmetic come from MCP:

| Purpose | MCP tool |
|---|---|
| CBAM timeline (founding regulation → transitional → definitive → certificate sales → first surrender) | `get_cbam_timeline` |
| Current carbon price snapshots by market and basis | `compare_carbon_prices` |
| Carbon market overview | `get_carbon_market_overview` |
| Cost arithmetic (embedded emissions × price) | `calculate_cbam_cost` |
| Carbon accounting standards (ISO 14064 / 14067 / 14068) | `get_carbon_standards` |

If MCP is unavailable: **tell the user plainly that the CBAM timeline and carbon prices cannot be fetched, and do not quote dates or prices from memory.** CBAM implementation dates have been revised more than once; memory-quoted dates are unreliable.

---

## Citation rules (Trustbase standard language · TBDS-1)

Every factual judgment in this skill that is drawn from the Trustbase database **must carry all three of the following**:

| Element | Where it comes from | Example |
|---|---|---|
| **Record ID** | The `id` field of the tool response | `tbm-021` · `rcb-pol-004` |
| **Confidence** | The record's `sourced.confidence` | **A** = verified against government documents / official announcements · **B** = company self-reporting / authoritative media · **C** = pending verification / questionable |
| **Retrievable address** | `https://trustbaselab.com/record/<record ID>/` | https://trustbaselab.com/record/tbm-021/ |

Hard rules:

1. **A citation MUST retain both the confidence level and `as_of`** (TBDS-1 §8.2).
2. **C-grade records MUST be marked "pending verification"**; **B-grade records MUST state the nature of the source**.
3. **Where this site has no coverage, the gap MUST be stated plainly** — never fill it with generic knowledge.
4. Values always come from real-time MCP tool responses, **never hard-coded from memory**.
5. Full standard text: https://trustbaselab.com/standard (TBDS-1 v0.1 · CC BY 4.0).

---

## Execution process (four steps, no step may be skipped)

### ① Identify the product and confirm CBAM scope

Ask (or infer) which product the user is talking about. Then check it against the CBAM coverage list fetched from `get_cbam_timeline`.

| Outcome | What to say |
|---|---|
| In the six covered categories | Proceed to ②. Note the 50-tonne single-mass threshold (hydrogen and electricity excepted) if relevant. |
| **Not** in the six covered categories | Say so plainly, then explain the **transmission path** (see the scope-first section above). Do not stop at "no". |
| Ambiguous / mixed consignment | Say the classification depends on the CN code, and recommend confirming the CN code with the customs broker. Do not guess. |

### ② Establish the timeline position

Call `get_cbam_timeline`. Determine which phase the user's shipment falls into:

| Phase | What it means for the user |
|---|---|
| Transitional period | Quarterly reporting obligation, **no certificate purchase** |
| Definitive period, before certificate sales start | Reporting continues; certificates not yet purchasable |
| After certificate sales start | Certificates must be bought and surrendered on the annual schedule |

**Never state these dates from memory.** They come from `get_cbam_timeline`, with `as_of`.

### ③ Get a carbon price and compute

Call `compare_carbon_prices` to obtain the current price snapshot. **Present the price as a dated snapshot with its market and basis — never as a single "the carbon price is X" statement.**

Then call `calculate_cbam_cost` with the user's own emission intensity and quantity. If the user does not have an emission intensity, **say plainly that it is the missing input and cannot be estimated from this database** — do not invent a default intensity.

### ④ State what is not covered

Always close with the limits: this is an arithmetic estimate, not a customs declaration. Free allocation phase-out, the actual CN code, the embedded-emissions verification methodology, and any future scope extension all change the answer.

---

## Hard constraints (violating any of these makes the output wrong)

1. **Never say carbon black is in CBAM scope. Never say CBAM is irrelevant to a carbon black producer.** Scope and transmission path are two different statements and both must be made.
2. **Never state CBAM dates from memory.** Always fetch `get_cbam_timeline`. The implementation schedule has been revised repeatedly.
3. **Never present a carbon price as a fixed number.** Always give market + basis + date of the snapshot.
4. **Never invent an emission intensity.** If the user has none, say it is the missing input.
5. **Never claim this output is a customs declaration or a compliance certificate.** It is an arithmetic estimate.
6. **Where this site has no coverage, state the gap plainly.**

---

## Output template

```
## 1. Scope check
(product / whether in CBAM's six covered categories / record id + confidence + as_of)

## 2. If outside scope: the transmission path
(who actually pushes the carbon-footprint requirement, and through which instrument)

## 3. Timeline position
(phase / what obligation applies now / record id + as_of)

## 4. Cost estimate (only if in scope and inputs provided)
- Emission intensity: (source: user-provided)
- Quantity: (source: user-provided)
- Carbon price snapshot: (market / basis / date, from compare_carbon_prices)
- Estimated cost: (from calculate_cbam_cost)

## 5. Limits of this estimate
(free allocation phase-out / CN code confirmation / verification methodology / possible scope extension)

## 6. Data sources and confidence
(mark source and A/B grade for each item)
```

---

## Boundary statement (must be reflected in the conclusion)

This skill provides a **scope check and an arithmetic estimate**. It is not a customs declaration, not a compliance opinion, and not legal advice. The final CBAM obligation depends on the CN code, the verified embedded emissions, the prevailing certificate price at surrender, and the free-allocation schedule in force at that time.

CBAM's scope may be extended in future. Any statement about scope in this skill reflects the database's `as_of` date, not a prediction.

---

## References

- `references/scope-and-transmission.md` — the six covered categories, the transmission instruments (CSRD / ESPR / DPP / Euro 7 / ISCC PLUS), and how to explain the difference to a customer
- `references/timeline-phases.md` — what obligation applies in each phase, and the language to use
