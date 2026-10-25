# PUE calibers — the three questions that must be answered before any comparison

> This reference belongs to the `compute-pue-benchmark` skill.
> It contains no data — all benchmarks are fetched at runtime from `get_pue_benchmarks`.

---

## Why this reference exists

PUE is one of the most-reported and least-comparable metrics in the data-centre
industry. Two facilities can both report "PUE 1.25" and be describing completely
different things. Most bad PUE advice comes from comparing numbers that were
never on the same basis.

**This skill's main value is not producing a verdict — it is making the
non-comparability explicit.**

---

## Question 1: Annual average, or design value?

| Type | What it is | How it is used | Reliability |
|---|---|---|---|
| **Design PUE** | The figure promised at design time for full load under design conditions | Specification, procurement, contract | A promise. Frequently not achieved in operation. |
| **Measured annual average** | The actual figure over a full year of operation | Reporting, rating, benchmarking | A measurement. The only figure that should be called "the facility's PUE". |
| **Point-in-time measurement** | A snapshot, often at a favourable season or load | Marketing | Not a benchmark. |

**Language to use:**

```
When the user gives a design PUE:
  "That is a design figure. The comparable benchmark is the measured
   annual average, which is usually higher. Do you have the annual figure?"

When the user gives a measured annual PUE:
  "Good — that is comparable. Which load band did it cover?"
```

---

## Question 2: At what IT load?

PUE is strongly load-dependent. The relationship is not monotonic:

```
At very low IT load    → PUE is very high (fixed overheads dominate)
At mid load            → PUE improves
Near full load         → PUE is usually at its best, but cooling may degrade
                          if the design was sized for a different load point
```

**Practical consequence:** a facility measured at 30% load and one measured at
80% load are not comparable, even if both report "annual average".

**Language to use:**

```
"At what average IT load was that measured? PUE at 30% load and PUE at
 80% load are different numbers for the same facility."
```

**If the load is unknown:** present the benchmark as a band and say the
comparison cannot be tightened without the load figure.

---

## Question 3: What is inside the boundary?

| Boundary choice | What is included | Effect on the number |
|---|---|---|
| **IT-only** (strict) | Cooling, UPS losses, lighting serving IT | Highest PUE |
| **Whole-facility** | Above + office, canteen, external lighting | Lower PUE (denominator unchanged, numerator larger — wait, actually higher) |
| **Including substation losses** | Above + transformer losses | Higher PUE |

The direction depends on exactly which loads are added, which is precisely why
the boundary must be stated. Two facilities with identical physical plants can
differ by 0.05–0.15 in reported PUE purely from boundary choice.

**Language to use:**

```
"What is inside the boundary — cooling only, or also office and
 substation losses? That alone can move the number by 0.1."
```

---

## How to handle an unknown caliber

This is the most common situation. Do not refuse to answer — but do not produce
a confident verdict either.

**Recommended structure:**

```
## Your figure
PUE 1.35 (caliber not stated)

## What the benchmark band says
[band from get_pue_benchmarks, with record id + confidence + as_of]

## Verdict
Cannot be judged definitively — the caliber is not stated.
  · If this is a design value at full load → likely within band
  · If this is an annual average at mid load → likely above band
  · To judge, I need: annual-average or design, average IT load, boundary

## What would change the answer
[the three caliber questions]
```

**This is more useful than a confident wrong verdict, and it teaches the user
to ask the right question next time.**

---

## What never to do

```
❌ Compare a design PUE against an annual-average benchmark and call it good/bad
❌ Compare against an exemplar facility (a named case) and call it a class benchmark
❌ Quote a threshold without its rating scheme and year
❌ State a national average from memory — these are revised annually
❌ Conclude "compliant" or "non-compliant" without knowing the applicable scheme
```
