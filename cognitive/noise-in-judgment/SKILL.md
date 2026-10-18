---
name: noise-in-judgment
description: A judgment-consistency skill based on "Noise" (Kahneman, Sibony, Sunstein). Separate bias from noise, run a noise audit to quantify disagreement, then apply decision hygiene (independent judgment, aggregation, ranking, guidelines) to reduce variance. Includes a multi-run consistency-check protocol for agents. Use when the user says "why is the answer different every time", "which conclusion should I trust", "how do I make scoring consistent", "how do I audit decision quality", "is this much difference between two judgments normal"; not for pure fact lookup, single-answer computation, or personal taste.
---

# Noise × Judgment Consistency · Treating Random Inconsistency as a First-Class Problem

**The core claim of *Noise*:** **judgment error = bias + noise**. Bias is a systematic offset (the star problem for decades); noise is random scatter (the long-ignored invisible problem). Their contributions to total error are **interchangeable** — **total error (MSE) = bias² + noise²**. Noise has a unique advantage: **it can be measured without knowing the correct answer** (you can measure the spread of the bullet holes without seeing the bullseye). So the order of treatment is: measure noise first (a noise audit), then prevent it with process (decision hygiene).

## When to use

- The same question, asked of different people / at different times / of different agents, produces clearly different conclusions, and the user asks "which should I trust" or "why are they different"
- An organizational process needs to make evaluation, scoring, review, and grading "more consistent, fairer"
- The user suspects their own judgment is "good sometimes, bad sometimes" and wants less random fluctuation
- The quality of a judgment system / process needs to be audited (rather than auditing an individual)
- In an agent pipeline, LLM output is unstable across runs and this affects downstream work
- The user asks "what is the difference between bias and noise", "how do I run a noise audit", "what is decision hygiene"

**Lightweight mode**: when the only questions are "why are two conclusions different", "which should I trust", "how much difference is normal", output "a one-sentence diagnosis (bias/noise) + a table of where the disagreement comes from + one action" — no need to run the full pipeline.

**Not for**: computation or retrieval with a single correct answer (just compute it; no judgment protocol needed); personal taste and preference (disagreement is legitimate); task overload, attention allocation, multitasking conflicts → use `bandwidth-and-deep-work`; treatment of specific biases (anchoring, framing, overconfidence) → use `thinking-fast-and-slow`; purely conceptual explanation → explain the concept directly without forcing the pipeline.

## Three iron rules

### Rule 1: Bias and noise are two different diseases; diagnose and treat them separately

Bias = the average deviation of a set of judgments; noise = the dispersion among the judgments. Looking only at the average hides noise; shouting only "eliminate bias" does not treat noise. The error equation supplies the equivalence: **MSE = bias² + noise²** — reducing one unit of noise contributes as much to total error as reducing one unit of bias (*Noise*, Chapter 5).

> Evidence anchor: the insurance underwriting audit — executives expected about 10% disagreement; the measured median difference was 55% (underwriting pricing) / 43% (claims assessment); the median expectation among 828 executives for the disagreement of expert judgments was also 10%. The scale of noise is systematically underestimated by a factor of 4–5 (figures relayed from the book by a strategy+business review).

### Rule 2: Noise can be measured without ground truth — audit first, don't debate

Bias often cannot be measured because the "correct answer" is unavailable; noise only needs "judgments that ought to be identical". A noise audit = have judges who ought to be interchangeable judge the same set of cases independently, and quantify the disagreement. **Disagreement is itself data** (corollary: if two people give different judgments on the same case, at most one of them is right).

### Rule 3: Reducing noise relies on decision hygiene, not on "being smarter or trying harder"

Decision hygiene = measures that target no specific bias but prevent unknown errors through process — analogous to handwashing: you do not know which pathogen you blocked. Core moves: independent judgment → aggregation; structured decomposition; ranking beats scoring; unified scales; sequencing information; rule-ify what can be rule-ified. ⛔ Reject empty phrases such as "be calm", "be objective", "think it through" — accept only executable process changes.

## Step 0 · Gather information (no fabrication)

An audit depends on real judgment data. Before starting you must clarify:

- What is the judgment task (pricing / scoring / diagnosis / grading / forecasting?), and is it **predictive** (there is an objective outcome) or **evaluative** (a value trade-off)?
- Who is judging (person / agent / model), how many, are they interchangeable?
- Are there historical cases that can be reused (8–16 homogeneous cases suffice for a small pilot)
- Is there a ground truth or an after-the-fact outcome (this determines whether bias is measurable)
- What does the current process look like (order of discussion, scale, whether scoring is independent)

⛔ Ask for missing information item by item, or explicitly label it "the following are assumed values". **Fabricating disagreement numbers is forbidden** — with no data, design the audit rather than invent a number.

## Core workflow: the noise audit (six steps, adapted from Appendix A of *Noise*)

| Step | Action | Key requirement |
|---|---|---|
| 1 | Define the team and the unit of judgment | Members make the same kind of judgment and should be interchangeable; the team must be credible |
| 2 | Construct the case set | Domain experts write 8–16 cases close to real work; each case requires a **single numeric answer** (price / probability / score) |
| 3 | The leader commits first | Beforehand, write down the **expected disagreement** and an acceptable ceiling, and commit to acting on the result |
| 4 | Run it independently, quietly, anonymously | Do not call it an "audit" (to avoid alarming people); same time window, independent answers, no comparison, anonymous |
| 5 | Measure dispersion, not the average | Compute the median pairwise relative deviation (\|a−b\|/mean) and similar disagreement metrics; **decompose** level noise (differences in people's averages) vs. pattern noise (differences in how people respond to cases) |
| 6 | Feed back and fix the system | Compare expected vs. measured; locate the noise source (scale? process? judge?) → change rules/tools/training → schedule a re-audit |

**Noise decomposition**: system noise² = level noise² + pattern noise²; pattern noise = stable pattern noise + occasion noise. Pattern noise is usually **the largest** part — the main problem is not "one person is systematically harsher" but "each person reacts differently to different kinds of cases".

## Diagnosis → prescription decision map

| Diagnostic finding | Do this first |
|---|---|
| Large disagreement but nobody admits it (illusion of agreement) | A1 build a homogeneous case set (+ A2 don't call it an audit) + A3 have the leader write their expectation first; use the measured gap to break the illusion |
| Level noise dominates (one overall harsher, one overall looser) | B3 unified scale / reference-frame training; B6 outside-view base rate |
| Pattern noise dominates (different reactions to case types) | B2 structured decomposition; B5 ranking instead of scoring |
| High occasion noise (the same person is inconsistent at different times) | B1 independent repeated judgment + aggregation; B4 information sequencing; review important judgments overnight |
| A verifiable, recurring prediction task | B7 replace intuition with a reasonable rule / simple model |
| A single major decision (acquisition / strategy) | B8 decision observer + premortem; counterfactual thinking |
| A decision made only after group discussion | B1 independent first, aggregate later; discussion first is forbidden |
| Agent output inconsistent across runs | C1–C10 consistency-check protocol (below) |
| Noise is clear but the fix is costly | Return to the "optimal noise" trade-off (see boundaries); prefer smarter rules over giving up |

## Prescription library

### A. Measurement (the noise audit)

1. **A1 Homogeneous case set**: cases must be mutually comparable, with answers on the same scale; 8–16 is enough for a small pilot.
2. **A2 Don't call an audit an audit**: internally call it a "process rehearsal / consistency calibration" to prevent defensive answers.
3. **A3 Expectation before measurement**: have the leader write down the expected disagreement and commit to acting — "I thought it was 10%, it was actually 55%" is the strongest persuasive weapon.
4. **A4 Independence is a hard requirement**: same time window, independent, anonymous; any circulation or discussion contaminates the measurement.
5. **A5 Report the disagreement triad**: median pairwise relative deviation (the noise score), range / coefficient of variation, and the level-vs-pattern decomposition — **never report the mean**.
6. **A6 Schedule re-audits**: institutions drift (after the US sentencing guidelines changed from mandatory to advisory in 2005, sentencing disparity doubled; study cited in the book, underlying source pending verification) — noise reduction is a one-time intervention plus periodic re-auditing.

### B. Decision hygiene (prescriptions from the book)

1. **B1 Independent first, aggregate later**: before discussion, each person writes their judgment independently; aggregation (mean / median / majority vote) beats discussion-based consensus; statistical groups > interacting groups (information cascades and group polarization amplify noise).
2. **B2 Mediating assessments protocol (MAP)**: define the mediating dimensions → collect evidence and score each dimension independently → "score-discuss-score" per dimension → **only then** make the overall intuitive judgment. Treat options like candidates and evaluation like a structured interview.
3. **B3 Unified scales and anchors**: behaviorally anchored rating scales plus reference-frame training, so everyone uses the same ruler; unanchored scales (e.g. dollar compensation amounts) are a noise hotspot (arbitrary coherence).
4. **B4 Information sequencing**: evidence first, background second, conclusions last — this prevents premature intuition (forensic science uses linear sequential disclosure: scene evidence first, then comparison samples and case facts).
5. **B5 Relative judgment beats absolute judgment**: ranking > scoring; if scoring is required, define anchors and behavioral examples first. For a batch of objects, score then convert to an internal ranking.
6. **B6 Outside view**: first ask "what is the distribution / base rate for this class of cases", place the case back into its reference class, then discuss its specificity.
7. **B7 Rule-ify what can be rule-ified**: for high-frequency verifiable judgments, use the five steps of a "reasonable rule" — pick 6–8 clearly relevant variables → standardize → average into a total score → map score bands to actions. Simple, noise-free, explainable; no complex model needed.
8. **B8 Protection for a single decision**: counterfactual thinking (if we swapped the team / the day / the order, would the conclusion change?) + a decision-observer checklist + a premortem (assume it already failed, work backwards to causes).
9. **B9 Pick judges by cognitive style**: actively open-minded thinking (seeking counter-evidence, willing to update) > confidence and eloquence; a respected expert ≠ a well-calibrated forecaster.
10. **B10 Log the "broken-leg" exceptions**: a human may override a rule with decisive information the model does not have, but the override must be logged and the override rate audited afterwards — intuition-based override is not a free pass.

### C. Agent multi-run output consistency-check protocol (this skill maps the book's concepts onto LLM engineering; it is our translation, not the book's wording)

1. **C1 Occasion-noise audit**: re-run the same task with the same prompt N≥3 times (at a fixed temperature) and quantify the disagreement (categorical → share of each answer; numeric → range / standard deviation / coefficient of variation).
2. **C2 Level-noise audit**: run the same case set across models / temperatures and compare overall tendencies (which one is systematically high / systematically harsh).
3. **C3 Pattern-noise audit**: construct 8–16 homogeneous cases and judge them in a batch to see **which type** of case the model is unstable on (model × case interaction), rather than saying vaguely "it's unstable".
4. **C4 Aggregation protocol**: after independent repeated runs, aggregate — majority vote for categorical, median / trimmed mean for numeric; have sub-agents judge independently and then aggregate; do not let them serially reference the previous answer.
5. **C5 Structured output**: define a rubric first and score each dimension independently, and only then synthesize (the agent edition of MAP); write both the dimension scores and the total into the output.
6. **C6 Ranking instead of scoring**: ranking candidates beats a 1–10 score; if scoring is required, define the anchors (e.g. "5 = meets all criteria with no obvious defect").
7. **C7 Information-sequencing hygiene**: in the prompt, put objective facts first and other people's conclusions / anchors / example answers last; when order sensitivity is suspected, rotate the order to test robustness.
8. **C8 Deterministic rules first**: judgments that can be expressed as code / a formula / a lookup should not use LLM intuition (the agent edition of the reasonable rule); the LLM handles only out-of-rule inputs, and exception records are kept.
9. **C9 Report a distribution, not a point**: key judgments carry their basis — "3 runs: 7.2 / 7.5 / 7.8", "±2 disagreement with another model" — and state the availability of ground truth (objective ignorance).
10. **C10 Audit trail**: archive the raw output of every consistency check so the metrics can be recomputed — "how big the disagreement is" must be reproducible by a third party.

## Agent execution protocol

1. **Consistency red line**: evaluation / scoring / conclusion / forecasting outputs are by default labeled "single sample"; for key judgments that affect downstream work, first decide via C1 whether to re-run and aggregate.
2. **Disagreement is information, not a fault**: report the disagreement and the distribution rather than picking one answer in order to "look stable".
3. **Diagnose before prescribing**: separate bias from noise — average deviation from the target is bias evidence; dispersion across runs is noise evidence; report both.
4. **Structure before intuition**: for complex judgments, build the dimensions first (C5), score each dimension, and only then allow an overall judgment — giving a total score off the top is forbidden.
5. **Preserve independence**: in any multi-agent / multi-step process, make sure the judgments are formed independently and then aggregated; serial transmission of conclusions is an information cascade.
6. **Note the optimal-noise trade-off**: zero noise is not the goal — beyond a point, more consistency costs more decision quality; prefer smarter rules to harsher enforcement.
7. **Re-audit after intervention**: after changing a process, re-run the audit and compare before/after; a change without a re-audit is an unverified change.

## Output templates

### Template 1 · Consistency diagnosis report (for "why are two answers different" requests)

```markdown
**One-line diagnosis**: this is [bias / noise / both]; the main disagreement comes from [level / pattern / occasion] noise.

| Source of disagreement | Evidence | Share (estimated) |
|---|---|---|
| Level noise | ... | ... |
| Pattern noise | ... | ... |
| Occasion noise | ... | ... |

**One action**: ...
```

### Template 2 · Noise audit report (organization / pipeline)

```markdown
| Item | Expected | Measured |
|---|---|---|
| Median pairwise relative deviation | ... | ... |
| Range / CV | ... | ... |
| Level noise | ... | ... |
| Pattern noise | ... | ... |

**Diagnosis**: the dominant source is ...
**Countermeasure**: ...
**Re-audit scheduled**: ...
```

### Template 3 · Agent consistency-check record (protocol C)

```markdown
| Run | Output | Notes |
|---|---|---|
| 1 | ... | ... |
| 2 | ... | ... |
| 3 | ... | ... |

**Dispersion**: ...
**Aggregation**: ...
**Ground truth availability**: available / not available (objective ignorance)
```

## Boundaries and common misuse

| Misuse | Correction |
|---|---|
| Treating "noise" as "random error that cannot be studied" | Noise is measurable and treatable; that is the whole point of the book |
| Treating zero noise as the goal | There is an optimal level of noise; beyond it, further consistency costs decision quality |
| Using a noise audit to evaluate individuals | The audit measures the **system**, not people; used against individuals it creates defensiveness and destroys the data |
| Confusing noise with bias | Average deviation = bias; dispersion across judgments = noise; diagnose separately |
| Reporting only the mean disagreement | The mean hides the structure; report the median pairwise relative deviation, the range, and the level-vs-pattern decomposition |
| Skipping independence | Any circulation or discussion contaminates the measurement entirely |
| Treating ranking as always better | Ranking is better than absolute scoring, but only when the objects are genuinely comparable |
| Using decision hygiene as an excuse to avoid deciding | Hygiene improves the quality of judgment; it does not replace the decision |

---

## Reference files (load on demand, not by default)

- `references/noise-in-judgment-book.md` — full book notes: concept dictionary, evidence anchors, quotations, criticism boundaries
- `references/evidence.md` — validation status of this skill's rules inside this project
- `METHOD.md` — conversion record for this book
- `references/SKILL.zh.md` — the Chinese edition of this skill

---

*Based on the ideas of "Noise: A Flaw in Human Judgment" (Daniel Kahneman, Olivier Sibony, Cass R. Sunstein, 2021). This file is Trustbase Lab content; License: Apache-2.0.*
