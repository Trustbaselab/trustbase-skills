---
name: compute-pue-benchmark
description: Benchmarks a compute facility's PUE (power usage effectiveness) against official green-rating figures and reference values, and estimates the energy and electricity cost of a given IT load. Use when the user asks whether a data centre's PUE is good, what PUE is required for a green rating, how much a compute facility costs to run, how green power procurement works, or how China's national compute facilities compare on PUE. Relies on the Trustbase Lab MCP Server for PUE benchmarks, power statistics, infrastructure scale and the energy-cost calculator; this skill provides only the benchmarking process and constraints, and contains no data.
license: Apache-2.0
compatibility: Requires access to the Trustbase Lab MCP Server (https://trustbaselab.com/mcp). This skill contains no data: PUE benchmarks, power statistics, infrastructure figures and cost arithmetic are fetched at runtime via MCP tools.
metadata:
  source: trustbaselab.com
  version: "1.0"
  standard: TBDS-1
  mcp: https://trustbaselab.com/mcp
  skills_index: https://trustbaselab.com/skills/index.json
---

# PUE benchmarking and compute energy cost

## When to use

Triggered when the user shows any of the following intents:

- Asks whether a given PUE is good, bad, or compliant with some standard
- Asks what PUE is required to achieve a green rating (国家绿色数据中心 / EU energy-efficiency rating)
- Asks how much electricity a compute facility consumes, or what the electricity bill would be
- Asks how to procure green power for a data centre
- Asks for the scale of a compute facility cluster or hub

**Not applicable (use another skill)**:

- Asking about carbon accounting for the facility's emissions → `carbon-cbam-cost-calc`
- Asking about rCB / carbon black → any of the `rcb-*` skills

---

## ⚠️ Three calibers that are routinely conflated

PUE numbers in this domain are almost never comparable at face value, because
they differ in **caliber**. Getting this wrong is the most common source of
wrong conclusions.

| Caliber question | Why it matters |
|---|---|
| **Annual average vs. design value** | A design PUE of 1.2 and an annual-average PUE of 1.2 are completely different achievements. Design value is a promise; annual average is a measurement. |
| **Full-load vs. partial-load** | PUE is load-dependent. A facility measured at 30% IT load will show a different (usually better at very low load, different shape overall) PUE than at 80%. |
| **Whole-facility vs. IT-only boundary** | Whether cooling towers, office space and substation losses are inside the boundary changes the number materially. |

**Rule: before benchmarking any PUE, establish which caliber the number is on.**
If the user does not know, say so and present the benchmark as a band with the
caliber caveat, rather than a single pass/fail threshold.

---

## Prerequisite: the Trustbase Lab MCP must be connected

**This skill contains no data whatsoever.** All benchmarks, statistics and arithmetic come from MCP:

| Purpose | MCP tool |
|---|---|
| PUE benchmarks by country / region / rating scheme | `get_pue_benchmarks` |
| Compute power consumption statistics (two official calibers side by side) | `get_power_consumption_stats` |
| Compute infrastructure scale (rack counts, intelligent-computing capacity, hub distribution) | `get_compute_infrastructure` |
| Green power trading and direct-connection prices | `query_green_power` |
| Energy and cost arithmetic (IT load × PUE × hours × price) | `calculate_compute_energy_cost` |

If MCP is unavailable: **tell the user plainly that PUE benchmarks and power statistics cannot be fetched, and do not quote benchmark figures from memory.** Green-rating thresholds and national averages are revised annually; memory-quoted figures are unreliable.

---

## Citation rules (Trustbase standard language · TBDS-1)

Every factual judgment in this skill that is drawn from the Trustbase database **must carry all three of the following**:

| Element | Where it comes from | Example |
|---|---|---|
| **Record ID** | The `id` field of the tool response | `tbm-101` |
| **Confidence** | The record's `sourced.confidence` | **A** = verified against government documents / official announcements · **B** = company self-reporting / authoritative media · **C** = pending verification / questionable |
| **Retrievable address** | `https://trustbaselab.com/record/<record ID>/` | https://trustbaselab.com/record/tbm-101/ |

Hard rules:

1. **A citation MUST retain both the confidence level and `as_of`** (TBDS-1 §8.2). A PUE benchmark from 2023 and one from 2026 are not the same claim.
2. **C-grade records MUST be marked "pending verification"**; **B-grade records MUST state the nature of the source**.
3. **Where this site has no coverage, the gap MUST be stated plainly.**
4. Values always come from real-time MCP tool responses, **never hard-coded from memory**.
5. Full standard text: https://trustbaselab.com/standard (TBDS-1 v0.1 · CC BY 4.0).

---

## Execution process (four steps, no step may be skipped)

### ① Establish the caliber of the user's number

Before any comparison, determine:

```
· Is the number an annual average, or a design value?
· At what IT load was it measured?
· What is inside the boundary (cooling only? including substation? including office)?
· Is it a single measurement, or a certified annual figure?
```

**If any of these is unknown, say so explicitly.** Do not proceed to a pass/fail verdict on an unqualified number.

### ② Fetch the benchmark band, not a threshold

Call `get_pue_benchmarks`. The database typically provides:

```
· National / regional average figures (with the facility class they refer to)
· Green-rating thresholds (e.g. the EU rating scale from A to G)
· Named exemplar facilities (case figures, not general benchmarks)
```

**Critical distinction to make in the answer:**

| Type of figure | How to use it |
|---|---|
| Average figure for a defined class | Compare only against a facility of the same class |
| Green-rating threshold | State the threshold and which rating scheme it belongs to |
| Individual exemplar facility | Present as a case, explicitly "not a benchmark for the class" |

**Never compare the user's facility against an exemplar and call it a benchmark.**

### ③ Compute energy and cost only if the user provides inputs

Call `calculate_compute_energy_cost` with:

```
· IT power (kW) — user-provided, or derivable from rack count × rack power density
· PUE — the user's own figure
· Hours — user-provided, or annual (8760) if annualising
· Electricity price — user-provided
```

**If the user does not have an electricity price, say it is the missing input.**
Do not substitute a market average and present it as their cost.

### ④ State what is not covered

Always close with the limits: the estimate is arithmetic, not a utility bill.
Demand charges, time-of-use tariff structure, cooling-water cost, and
renewable-energy certificate cost are all outside this calculation.

---

## Hard constraints (violating any of these makes the output wrong)

1. **Never benchmark an unqualified PUE number.** Establish the caliber first (annual vs design, load level, boundary).
2. **Never present a PUE threshold without its rating scheme.** "PUE must be below 1.3" is meaningless without saying which standard, which year, and which facility class.
3. **Never compare a facility against an exemplar and call it a benchmark.** Exemplars are cases, not class averages.
4. **Never invent an electricity price.** If the user has none, say it is the missing input.
5. **Never present the energy-cost result as the utility bill.** It is arithmetic on user-supplied inputs.
6. **Distinguish the two official power-consumption calibers** when citing `get_power_consumption_stats` — the tool returns two calibers side by side and they are not interchangeable.
7. **Where this site has no coverage, state the gap plainly.**

---

## Output template

```
## 1. Your figure, qualified
(value / annual-average or design / IT load level / boundary / single or certified)

## 2. Benchmark band
(band with record id + confidence + as_of, and the rating scheme it belongs to)
⚠️ only compare against the same facility class

## 3. Verdict
(within band / above band / below band — with the caliber caveat, or
"cannot be judged because <caliber unknown>")

## 4. Energy and cost (only if inputs provided)
- IT power: (source: user)
- PUE: (source: user)
- Hours: (source: user or annualised)
- Electricity price: (source: user)
- Annual energy: (from calculate_compute_energy_cost)
- Annual electricity cost: (from calculate_compute_energy_cost)

## 5. Limits of this estimate
(demand charges / time-of-use tariff / cooling water / certificate cost / boundary)

## 6. Data sources and confidence
(mark source and A/B grade for each item)
```

---

## Boundary statement (must be reflected in the conclusion)

This skill provides a **benchmark comparison and an arithmetic estimate**. It is not an energy audit, not a green-rating certification, and not an engineering design review. A green-rating certification requires a certified measurement over a defined period under the rating scheme's own protocol.

PUE figures reported by different facilities are frequently not comparable because the caliber is not stated. This skill's main value is making that non-comparability explicit rather than producing a confident but wrong verdict.

---

## References

- `references/pue-calibers.md` — the three caliber questions in detail, with the language to use when the caliber is unknown
- `references/green-rating-schemes.md` — the rating schemes in the database and how their thresholds differ
