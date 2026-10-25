# CBAM scope and the transmission path to carbon black

> This reference belongs to the `carbon-cbam-cost-calc` skill.
> It contains no data — all coverage lists and dates are fetched at runtime from
> `get_cbam_timeline` and `compare_carbon_prices`.

---

## 1. What CBAM actually covers

CBAM (the EU Carbon Border Adjustment Mechanism, established by Regulation (EU) 2023/956) currently covers **six product categories**:

| Category | Typical CN chapters |
|---|---|
| Cement | 2523 |
| Iron and steel | 72, plus selected 73 items |
| Aluminium | 76 |
| Fertilisers | 28, 31 |
| Electricity | 2716 |
| Hydrogen | 2804 10 |

**Anything not on this list is outside the current scope.** That includes:

```
carbon black (HS 280300 / CN 2803)
tyres
rubber goods
most downstream manufactured products
```

**This is the single most common error in this domain** — both directions:

- Some sellers overclaim: "CBAM regulates carbon black, so buy our low-carbon rCB."
- Some sellers underclaim: "CBAM has nothing to do with us."

Both are wrong. The right answer is a two-part statement.

---

## 2. The two-part statement (use this wording)

```
Part 1 — Scope:
  Carbon black is not in CBAM's current covered list
  (cement, iron & steel, aluminium, fertilisers, electricity, hydrogen).
  So no CBAM certificate is payable on carbon black itself.

Part 2 — Transmission:
  But carbon black's downstream customers — tyre makers, rubber goods
  manufacturers, automotive OEMs — are subject to CSRD, ESPR / DPP,
  Euro 7 and ISCC PLUS. Those instruments DO require carbon-footprint
  data from their suppliers. So the pressure is real; it is customer-driven,
  not CBAM-driven.
```

**Why both parts are necessary:**

| Only saying "not covered" | Only saying "it affects you" |
|---|---|
| The customer concludes there is no action needed, then gets blindsided when a tyre-maker asks for a PCF declaration | The customer thinks the seller is exaggerating to sell something, and discounts the whole message |

---

## 3. The transmission instruments, one by one

| Instrument | Who it binds | What it asks the supplier for |
|---|---|---|
| **CSRD** (Corporate Sustainability Reporting Directive) | Large EU companies, including tyre and automotive | Scope 3 upstream emissions, supplier-level data |
| **ESPR / DPP** (Ecodesign for Sustainable Products Regulation / Digital Product Passport) | Product-level; phased by product group | Material composition, recycled content, carbon footprint per product |
| **Euro 7** | Vehicle type approval | Tyre abrasion limits; indirectly drives material choices |
| **ISCC PLUS** | Voluntary but commercially required by many EU customers | Mass-balance chain of custody for recycled / bio feedstock |

**Key point for the conversation:** these instruments ask for **data**, not **payment**. The customer's request for a carbon footprint is not a tax — it is a procurement condition. Confusing the two leads to the wrong investment decision.

---

## 4. How to handle "but my customer says CBAM applies"

This happens frequently, and it is usually a communication problem, not a regulatory one.

**Recommended response:**

```
Ask the customer for the exact CN code they are importing under,
and for the specific CBAM obligation they are referring to.

Two outcomes:
  · If the CN code is in the six covered categories → CBAM does apply,
    to that product, and the conversation is about embedded emissions.
  · If the CN code is 2803 (carbon black) or a downstream rubber/tyre code
    → CBAM does not apply to that product. What the customer actually needs
    is a product carbon footprint for their own CSRD / DPP reporting.
```

**Never argue with the customer's compliance team.** Ask for the CN code. That resolves it in one step.

---

## 5. Where this site has coverage and where it does not

| Question | Coverage |
|---|---|
| CBAM timeline (founding → transitional → definitive → certificate sales → surrender) | Covered — `get_cbam_timeline` |
| Carbon prices by market and basis | Covered — `compare_carbon_prices` |
| Carbon accounting standards (ISO 14064 / 14067 / 14068) | Covered — `get_carbon_standards` |
| CBAM cost arithmetic | Covered — `calculate_cbam_cost` |
| **Product-level CN code classification** | **Not covered** — must be confirmed with a customs broker |
| **Verified embedded emissions for a specific installation** | **Not covered** — requires on-site verification |
| **Free allocation schedule details** | **Partially covered** — check `get_cbam_timeline` with `as_of` |

State the gaps plainly. Do not fill them with general knowledge presented as database content.
