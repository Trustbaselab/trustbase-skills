---
name: thinking-fast-and-slow
description: An AI judgment-quality skill based on "Thinking, Fast and Slow" (Daniel Kahneman). Detect System-1 patterns in agent/LLM output (anchoring, availability, representativeness, framing, loss aversion, overconfidence, planning fallacy), and force a System-2 review and calibration. Use when the user says "is this AI conclusion reliable", "review this AI output", "that answer felt too smooth / too confident", "why does changing the wording change the answer", "don't jump to conclusions", "is this attribution right", "is this schedule estimate reasonable"; also for agent self-review, estimation, and retrospectives. For task overload use bandwidth-and-deep-work.
---

# The AI System-1 Trap · A System-1/System-2 Review Protocol

**Kahneman's framework:** **System 1** is fast, automatic, associative, pattern-matching, and aims at *coherence*; **System 2** is slow, effortful, and responsible for review — but by default it is **lazy** and simply adopts System 1's conclusions. Transplant those two into an AI workflow: the default output path of an LLM/agent (next-token associative generation) is **functionally ≈ System 1** — fluent, coherent, confident, and not necessarily correct. All this skill does is **turn System 2 into a process**, not a slogan.

> Function-analogy disclaimer: AI has no biological cognitive resources. "AI's System 1/System 2" is an **analogy used to design a review process**, not a neuroscience claim (see the boundaries table).

## When to use

- Reviewing AI/agent output: the user asks "is this conclusion reliable", "is this a hallucination", "that answer felt too smooth"
- Answers that move with the question: swapping framing (gain/loss), word order, or supplying a "reference value" makes the answer drift
- Making estimates and plans: schedule, cost, success probability, risk probability — especially when only the inside view is available
- Attribution and retrospectives: turning a success or failure into a causal story; "this failed because of X"
- Before an irreversible decision: dropping a database, changing an architecture, a large investment, a release — needs calibrated output and red-team review
- Agent self-check: its own intermediate conclusions in a multi-step task, judgments after retrieval, advice given to the user

**Lightweight mode**: for a single question "is this conclusion reliable" → output only "a one-sentence conclusion + a list of System-1 suspicions (≤4)" — no need to run the full pipeline.

**Not for**: wanting only a conceptual explanation (you may explain without forcing the pipeline); task overload / multitasking / focus scheduling → use `bandwidth-and-deep-work`; "the answer is different every time / conclusions are inconsistent" (random variance rather than systematic bias) → use `noise-in-judgment`; data provenance and fact-checking (whether the number itself is right) → use `factfulness` (division of labor: provenance/facts belong to `factfulness`; bias review of judgments and estimates belongs here); when real experimental data is needed, this skill supplies only the judgment process and concepts, not data.

---

## Three iron rules

### Rule 1: Fluency ≠ correctness; coherence ≠ evidence

System 1's output objective is coherence, and cognitive fluency is misread as a signal of correctness. An AI's fluency, good formatting, and confident tone are the machine version of cognitive ease — **"it makes sense" and "there is evidence" must be scored separately**.

> Evidence anchor: Chapter 5 (cognitive ease) and Part III (confidence comes from the quality of the story, not from evidence): *"The confidence that individuals have in their beliefs depends mostly on the quality of the story they can tell about what they see, even if they see little."*

**Corollary: when reviewing AI output, lower the confidence first and then look at the content — the degree of confidence itself carries no information about the amount of evidence.**

### Rule 2: A bias is a "phenomenon with trigger conditions", not an adjective

Anchoring, availability, representativeness, framing, loss aversion, overconfidence, planning fallacy — each has **specific trigger conditions** in the book. Shouting "that's a bias" without a trigger condition says nothing; having the trigger condition and not checking for it is walking around naked.

> Evidence anchor: Tversky & Kahneman (1974, *Science* 185:1124) — the heuristics-and-biases list; in the book Ch.9 substitution, Ch.11 anchoring, Ch.12 availability, Ch.14/15 representativeness, Ch.34 framing, Ch.23/24 planning fallacy.

**Corollary: check the trigger-condition table first (see the core workflow), item by item; generic suspicion is forbidden.**

### Rule 3: Knowing about a bias does not immunize you against it — prescriptions must be process

Kahneman himself wrote the "law of small numbers" paper and, 40 years later, still fell into a small-sample study in Chapter 4 (publicly acknowledged in 2017). So this skill's prescriptions are **all external structure**: independent baselines, base rates, premortems, red teams, falsifiability. Empty phrases such as "be more vigilant" or "be objective" are not accepted.

> Evidence anchor: Kahneman in 2017, responding to Schimmack: *"What the blog gets absolutely right is that I placed too much faith in underpowered studies."* (On the replication crisis see the boundaries table.)

---

## Step 0 · Gather information (no fabrication)

Before starting you must have (ask for whatever is missing item by item, or explicitly label it as an "assumed value"):

- The **verbatim text** of the conclusion under review, plus the context / data / source it claims to rely on (if absent → require it first; otherwise you can only review **structure**, not **facts**)
- Background needed for the trigger conditions: precedent numbers / reference values, the list of materials actually retrieved, two framings of the question, historical records for similar tasks
- What decision the conclusion will affect (this determines review intensity: the bigger the impact, the fuller the process)

⛔ **Fabricating "what mistake it might have made" is forbidden: for facts with no trigger condition, write "no trigger condition observed".**

---

## Core workflow · System-1 diagnosis → bias list → forced review

### Q1 · Is this a System-1 or a System-2 product? (grade with four questions)

| Question | "System 1" signal | "System 2" signal |
|---|---|---|
| Generation process | One-shot draft, no intermediate steps, no trace of retrieval/computation | Traces of decomposition, retrieval, verification, self-checking |
| Confidence-to-evidence ratio | Assertive wording but no source / no number / no verifiable step | Gives confidence, uncertainty, rejected alternative explanations |
| Consistency | Answer drifts after changing framing or wording | Conclusion stable across framings |
| Cost sensitivity | Long essays for trivial tasks | Effort matched to the size of the decision |

> **Unobservable cell**: if any cell cannot be observed (typical: reviewing an external AI output forwarded by the user, with no process trace and no framing-swap test) → record that cell as "unknown", count the whole as **a System-1 suspicion**, but the conclusion must explicitly state "insufficient evidence; structural review only".

### Q2 · Bias trigger-condition checklist (tick item by item; a hit gets flagged)

| # | Bias | Trigger condition (per the book) | Stage | Typical manifestation in an AI setting |
|---|---|---|---|---|
| 1 | Anchoring | A concrete number, draft, or precedent appeared before the judgment | General | A "reference budget" from the user, the first draft, or the first number in a list drags later estimates |
| 2 | Availability | The judgment relies on what is easiest to recall / most recently retrieved | General | Concluding after only the last 3 documents; rare events overestimated because retrieval hits are frequent |
| 3 | Representativeness | Replacing probability with "does it look like the prototype", ignoring base rates | General | "this code looks like a bug" replacing "this module's historical bug rate"; labeling an individual case |
| 4 | Framing | The same choice is stated as a loss and as a gain | General | Flipping "10% failure rate" to "90% success rate" reverses the recommendation; cost-cutting vs. protecting revenue yield inconsistent conclusions |
| 5 | Loss aversion | Status quo / past investment vs. change / abandonment | General | Over-conservative about "abandoning the current plan"; sunk-cost-driven "let's invest a bit more" |
| 6 | Overconfidence | The output rests on a coherent narrative rather than evidence | General | High confidence with zero confidence interval; treating "a common claim in the training distribution" as fact |
| 7 | Planning fallacy | Discussing only task details, not the historical distribution of similar tasks | Ex-ante (estimating/planning) | Schedule/cost estimated directly, no base rate, no buffer (linked to bandwidth's ×1.5–2) |
| 8 | Hindsight / outcome bias | Judging decision quality from the outcome | Ex-post (results already exist) | A retrospective writes "bad luck" as "bad decision"; success presented as inevitable |
| 9 | Regression-to-the-mean misread | Attributing a single extreme result immediately | Ex-post (an extreme result just appeared) | Claiming "the process broke / the strategy works" after one spike or crash |
| 10 | WYSIATI | Building a story only from the information activated in context | General | Giving a complete coherent conclusion despite missing key context; not volunteering "what's still missing" |

> Stage note: ex-ante = planning/estimating before results exist; ex-post = retrospective attribution after results exist. Items that do not fit the current situation are skipped directly (e.g. when reviewing a plan that has not been executed, do not check #8/#9); **a skip is not a miss** — note "skipped by stage" in the report.

### Q3 · Forced System-2 review (choose by hits; see the prescription library)

0 hits → routine review is enough; 1–2 hits → the corresponding prescriptions; ≥3 hits or an irreversible decision → the full process (outside view + red team + premortem + calibrated output).

---

## Diagnosis → prescription decision map

| Diagnostic finding | Do this first |
|---|---|
| Confident wording + no source/number | C1 evidence-tier rewrite (separate fact / inference / guess) |
| An anchor is present (user-supplied number/draft/precedent) | A1 independent baseline first, then process the given value |
| Retrieval scope is suspect (only recent materials) | A2 complete the retrieval and explicitly list "what was not checked" |
| A single-case narrative replaces statistics | A3 base rate first: report the distribution before the case |
| Advice under a loss frame | A4 rewrite in both frames and disclose the preference gap |
| An estimate/plan has only the inside view | A5 reference-class forecasting + ×1.5–2 + premortem |
| Retrospective attribution turned into a causal story | A6 hindsight check: could the same story explain the opposite outcome? |
| An extreme metric plus immediate attribution | A7 regression check: compare against the historical distribution |
| High confidence + no verification path | A8 calibrated output: confidence + falsifiable steps |
| Irreversible decision / ≥3 hits | B1 red-team review (make the output falsify itself) |

---

## Prescription library

### A. Executable by one person / one agent

- **A1 Independent baseline first (anti-anchoring)**: before processing any input that contains a number, write down your own independent estimate range and its rationale, then look at the other party's number/draft. IF the user says "reference budget is 500k" THEN first write "per the distribution of similar projects: median X, range Y", then compare against 500k.
- **A2 Retrieval completeness self-check (anti-availability)**: list two columns — "what I actually retrieved/read" and "what I have not checked yet"; the unchecked part may not support the conclusion. IF the conclusion relies on the last 3 materials THEN complete the retrieval of historical files before concluding.
- **A3 Base rate first (anti-representativeness)**: first answer "what is the overall distribution for this class of situations", then answer "what about this specific case". IF there is no base-rate data THEN say explicitly "base rate unknown; the following judgment is representativeness-driven; confidence lowered".
- **A4 Dual-frame rewrite (anti-framing / anti-loss-aversion)**: write the recommendation once in a gain frame and once in a loss frame; if the two versions disagree, disclose the disagreement as the first risk to the user. IF the recommendation involves abandoning the status quo or admitting a loss THEN explicitly flag "is the sunk cost influencing this recommendation?".
- **A5 Reference-class forecasting (anti-planning-fallacy)**: for time/cost estimates, first take the historical distribution of similar tasks (start from the median), then multiply by ×1.5–2 (linked to the estimation factor in `bandwidth-and-deep-work`), and write "what the most optimistic assumption is". IF there is no historical data THEN use a premortem to generate risk items instead.
- **A6 Hindsight check (anti-narrative-fallacy)**: for any "because X, therefore Y" attribution, first ask "if the outcome had been the opposite, would this story still hold?" If it would → downgrade the attribution to "one possible narrative".
- **A7 Regression check (anti-noise-attribution)**: when a single extreme result appears, first compare against the metric's historical distribution and volatility; if it falls within normal fluctuation → record the observation first, do not change the process.
- **A8 Calibrated output (anti-overconfidence)**: every important conclusion must carry ① confidence (high/medium/low + reason) ② key uncertainties ③ falsifiable verification steps ④ rejected alternative explanations (for the **conclusion already proposed**; when source text is missing write "none available — missing source text, cannot evaluate"; do not guess at possible errors). IF these four cannot be assembled THEN declare "this conclusion does not meet the calibration standard".

### B. Structural level (for decisions that matter)

- **B1 Red-team review**: make the output falsify itself — "Please list the 3 necessary assumptions that make this conclusion hold, then write one scenario that overturns each; then re-evaluate the conclusion." Where necessary, use an independent agent / fresh context to review, so the same context does not self-certify.
- **B2 Premortem** (Ch.24, Klein): before finalizing a plan, write "one year from now this plan has failed — how does the failure history read?" — force the failure paths out, then build the risk list.
- **B3 Outside-view panel**: for irreversible decisions (dropping a database, changing an architecture, a large investment) → pull in at least a distribution of comparable historical cases plus one red team, then conclude.

### C. Expression discipline

- **C1 Evidence-tier rewrite**: rewrite every conclusion in three tiers: **fact** (has a source / is verifiable), **inference** (derived from facts, with assumptions labeled), **guess** (no basis, labeled as a guess). The user may act only on the highest tier available.

---

## Agent execution protocol (the agent works by this itself)

1. **By default, distrust "the feeling of fluency"**: after writing a passage you consider fluent and confident, treat it as a System-1 product; run the trigger-condition checklist before delivering.
2. **Numbers in, baseline out**: when an input contains a number (budget, reference value, draft), first record that number as an **external anchor**, then supply an independent baseline.
3. **Leave a retrieval trace**: before concluding you must be able to list "what was checked / what was not"; the unchecked part may not enter the conclusion.
4. **Estimates go through the outside view**: every schedule/cost/success-probability estimate first gives the historical distribution for similar work, or explicitly says "no base rate", then gives the number; default ×1.5–2 buffer (linked to the slack principle in `bandwidth-and-deep-work`).
5. **Downgrade attributions**: in retrospectives and failure analyses, write causal narratives as "one possible narrative + alternative explanation + question that would verify it"; do not write definitive statements.
6. **Calibrated output is the default**: key advice to the user by default carries confidence and falsifiable steps; if the four items (Rule 3 / prescription A8) cannot be produced, say so.
7. **Close a round with the peak-end rule**: put the most important judgment at the end; close with four lines — "conclusion / evidence grade / risk / next step" (mutually compatible with the shutdown ritual in `bandwidth-and-deep-work`).

---

## Output templates

**Output order and budget**: one-sentence conclusion → list of System-1 suspicions → review prescriptions and results → calibrated conclusion. Total length should match the size of the question; in lightweight mode ≤4 suspicions.

### Review report (standard)

```markdown
**Conclusion (one sentence)**: ...

**System-1 suspicions**:
| Bias | Trigger condition | Hit in this case | Evidence |
|---|---|---|---|
| Anchoring | ... | yes/no | ... |
(only list hits, at most all 10)

**Review performed**: prescription IDs + what was done + how the conclusion changed
(e.g. "A3 base rate: this module's historical bug rate is 2%; confidence lowered accordingly")

**Calibrated conclusion**:
- Confidence: high/medium/low (reason)
- Key uncertainties: ...
- Verification steps: ...
- Rejected alternative explanations: ... (write "none available — missing source text, cannot evaluate" when there is no source text; do not guess at possible errors)
```

### Estimation template (schedule / cost / success probability)

```markdown
| Item | Inside-view estimate | Reference-class baseline (historical distribution) | Adopted value (with ×1.5–2) |
|---|---|---|---|
| ... | ... | ... | ... |

**Premortem**: if this fails in one year, the failure history reads — (3–5 items)
**Action**: buffer X, trigger condition Y (escalate when it appears), review point Z
```

### Structural-review mode (no source text; structure only; the legitimate exit from the Step-0 gate)

```markdown
**Conclusion**: only the structure can be reviewed at present — "fluent/confident" by itself carries no evidence (Rule 1); whether the conclusion is wrong cannot be judged before the source text is available.

**Observable structural signals** (≤4): fluency signal, confidence-to-evidence ratio, visibility of the generation process, frame stability (mark unknown items honestly as "unknown").

**Performed**: C1 evidence-tier rewrite (all available information classified as fact / inference / guess); A8 calibrated output cannot assemble four items → declare "this conclusion does not meet the calibration standard".

**Next step**: please provide — ① the verbatim conclusion under review ② the context/data/source it claims to rely on ③ what decision it affects.
```

---

## Boundaries and common misuse

| Misuse | Correction |
|---|---|
| Citing this book as scientific law | Evidence tiers: prospect theory has been retested in 19 countries (Ruggeri et al. 2020); anchoring is robust (Yoon et al. 2019); but Schimmack (2020) estimated via z-curve that the average power of studies cited in the book is only 46%, with reproducibility 12–46%. Always cite in the "evidence anchor" register |
| Using "priming" to explain or design prompt behavior | ⛔ Chapter 4 is a replication-crisis hotspot (R-Index = 14); the author publicly withdrew the chapter's strong conclusions in 2017 ("too much faith in underpowered studies"). Do not claim that "subtle wording reliably changes behavior" |
| Explaining behavior with "ego depletion / willpower battery" | Ego depletion has not replicated at scale (Hagger 2016; Vohs 2021). To discuss cognitive resources, use the bandwidth metaphor (`bandwidth-and-deep-work`), not a "battery" |
| Parroting "the hot hand is an illusion" | After Miller & Sanjurjo (2018) the hot hand is real — the claim that "people are seeing patterns that aren't there" does not hold. For pattern judgments, check for statistical bias rather than defaulting to denial |
| Treating loss aversion as an iron law | Gal & Rucker (2018) raised systematic challenges and the field has not settled; phrase it as "≈1.5–2.5×, disputed" |
| Treating System 1 / System 2 as brain regions | The author explicitly says it is a fictional two-character metaphor; for AI it is a functional analogy, not a claim about capacity or neuroscience |
| "AI has no System 1" so this skill does not apply | The analogy is about **the cognitive character of the output path** (associative generation vs. explicit review), and is used to design a review process — that is the whole of this skill |
| Using "bias" as a disclaimer ("it's anchoring, so it's not my fault") | A bias is a mechanism explanation, not an excuse; a trigger-condition hit must be paired with its prescription, not a label and a delivery |
| Knowing about biases = immunized | The author's own Chapter 4 is the counter-example; prescriptions accept only external process (checklists, base rates, premortems, red teams), never "be more vigilant" |
| Using this skill for task overload / focus scheduling | That is the domain of `bandwidth-and-deep-work`. The link between the two: time pressure and multitasking amplify System-1 thinking (System 2 is lazy), so run the bandwidth diagnosis first, then this skill's review |

---

## Reference files (load on demand, not by default)

- `references/thinking-fast-and-slow-book.md` — full book notes: concept dictionary (original meaning + common misreading), evidence anchors, quotations, criticism boundaries
- `references/evidence.md` — validation status of this skill's rules inside this project (currently: pending validation + candidate applications and measurement plan)
- `METHOD.md` — conversion record for this book (why it fits / core claim, the 10 core rules, validation status, failure and risk notes)
- `references/SKILL.zh.md` — the Chinese edition of this skill

---

*This skill is based on the ideas of "Thinking, Fast and Slow" (Daniel Kahneman, 2011, Farrar, Straus and Giroux), translating the book's concepts into AI/agent behavioral rules; original passages appear only as short quotations. The rule design, agent protocol, and templates in this file are Trustbase Lab content; License: Apache-2.0.*
