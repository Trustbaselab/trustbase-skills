---
name: factfulness
description: A data-thinking skill based on "Factfulness" (Hans Rosling et al.). Audit every statistic against four provenance items (source / year / definition / baseline), diagnose the ten dramatic instincts, and output a level-plus-trend dual view and a danger-by-exposure fact-check card. Use when the user says "is the world getting worse", "is this number trustworthy", "cite a statistic for me", "stop fear-mongering", "let the data speak", "do we have to decide right now"; also for any output involving data citation, trend judgment, risk communication, or urgency-driven decisions.
---

# Factfulness · An Operating System for Citing Data

**The core claim of *Factfulness*:** our judgments about the world are systematically worse than random. In a 2017 study across 14 countries, the average score on 12 global-fact questions was **2.2 out of 12**, while random guessing would score **4 out of 12**, and 15% of respondents got every question wrong. That cannot be ignorance — it is a **systematically overdramatic worldview**, shaped by **ten dramatic instincts plus the media's appetite for bad news**.

**This skill translates the book's central rule — "look at the world through data, not through emotion and bias" — into concrete data-acquisition and citation discipline for an agent.**

## When to use

- The user asks "is the world getting worse", "is X finished / collapsing" — a level-plus-trend audit is needed
- The user asks you to cite or verify a statistic, a trend, or a market judgment
- The output touches risk, disaster, or panic themes (including self-restraint against fear-mongering)
- The context contains urgency cues such as "must right now / immediately / or it's too late"
- The user frames a binary judgment ("poor vs rich", "developed vs undeveloped")
- An attribution discussion ("it's all because of X", "we owe everything to Y")
- The agent itself is about to cite data or cases from training memory

**Lightweight mode**: when only one or two numbers are being verified, or the only question is "is this number trustworthy", output **a one-sentence conclusion plus one fact-check card (containing the level-plus-trend columns)** — do not run the full pipeline.

**Not for**: purely conceptual explanation (you may explain it without forcing the whole pipeline); task overload / multitasking / focus scheduling → use `bandwidth-and-deep-work`; academic history discussions (read `references/factfulness-book.md` directly).

---

## Three iron rules

### Rule 1: Any cited statistic must carry the four provenance items

Every statistic must be accompanied by: **source (who measured it) + year (which year's data) + definition (what exactly is being measured) + baseline (compared to what: per capita? ratio? chance level?)**. Missing any one item means **unverified** — label it "pending verification" and ⛔ **never fill it in so that it looks verified**.

> Evidence anchor: the Gapminder Misconception Study 2017 — about 12,000 people in 14 countries answered 12 global-fact questions; the average was 2.2/12, below the 4/12 expected from random guessing, and 15% got everything wrong. Getting everything wrong cannot be ignorance; it can only be a **systematically wrong worldview**. The book's official site also maintains an errata page with 30+ published corrections (including p.37, where an income threshold was corrected from $64 to $32) — if even the authors must publish errata, an agent certainly has no exemption.

### Rule 2: Report level and trend separately

"the current level is still bad" and "the direction is improving" can both be true. Reporting only the level is negativity; reporting only the trend is whitewashing. **Write both columns.**

> Evidence anchor: the book's 13-question set — extreme poverty has nearly halved in the last 20 years; global life expectancy is 70; the primary-school completion rate for girls in low-income countries is 63.2%; deaths from natural disasters have fallen by more than half over the last century. Most people get these wrong (only 7% get the girls' question right), because **a bad level obscures an improving trend**.

### Rule 3: Fear and urgency are signals, not instructions

A feeling of fear ≠ the size of a risk; "must be now" does not automatically mean "genuinely urgent". **Risk = danger × exposure.** When you receive a fear or urgency signal, slow down first: ask for the data, compute the risk, break the decision into small steps — then decide whether a large action is warranted.

> Evidence anchor: the book's official fear-instinct page defines **Risk = danger × exposure** verbatim. The book lists only five genuinely urgent global risks (global pandemic, financial collapse, world war, climate change, extreme poverty — wording per chapter 10, pending verification). Tigers, giant pandas, and black rhinos are all no more endangered than in 1996 (IUCN) — **the object of fear is often not where the risk is.**

---

## Step 0 · Gather information (no fabrication)

Before acting you must have (ask for whatever is missing, or explicitly declare "the following are assumed values"):

- The data or trend to be cited, plus the user's specific domain and time range
- The number's source, year, and definition (who measured it, when, under what definition)
- The comparison baseline (total or per capita? compared against what baseline?)

⛔ **Any number that comes from memory is treated as "a remembered value, unverified"; before citing it, retrieve it or label it.**

---

## Core workflow: four pre-citation questions → instinct diagnosis

### Step 1 · The four provenance items (for every number)

| Question | What to do if missing |
|---|---|
| Who measured it? | Label "source pending verification", or replace it with a traceable number |
| Which year? | Label "year pending verification"; if older than 3 years, look up the latest value first |
| What is the definition? | Label "definition pending verification"; if several definitions conflict, present them side by side (e.g. life expectancy: IHME 72.48 vs UN Population Division 71.9, rounded to 70 in the book) |
| Compared to what? | Add the baseline: per capita / ratio / 80-20 / chance level / historical baseline |

### Step 2 · Level + trend, two columns

"Current level X" + "direction of change Y" + "data as of Z" — all three present, or it is not a complete factual statement.

### Step 3 · Ten instinct diagnostics (self-check the output draft item by item)

| # | Instinct | Self-check question | Trigger signal → prescription |
|---|---|---|---|
| 1 | Gap instinct | Have I split the world into two halves? | Binary labels "developed/developing", "rich/poor" → B1 |
| 2 | Negativity instinct | Have I reported only the bad news? | Saying only "it's bad" without the trend → B2 |
| 3 | Straight-line instinct | Am I extrapolating in a straight line? | "At this rate it will…" → B3 |
| 4 | Fear instinct | Am I amplifying fear? | Disaster/crime/terror themes → B4 |
| 5 | Size instinct | Are the numbers put in proportion? | Large numbers with no baseline → B5 |
| 6 | Generalization instinct | Am I generalizing from one example? | "Over there it's like this" style generalization → B6 |
| 7 | Destiny instinct | Am I assuming the status quo is permanent? | "They've always been like that" → B7 |
| 8 | Single-perspective instinct | Do I have only one hammer? | A single explanation or a single metric → B8 |
| 9 | Blame instinct | Am I looking for a villain or a hero? | "It's all X's fault" → B9 |
| 10 | Urgency instinct | Am I (or the user) in a hurry? | "Must right now" → B10 |

### Step 4 · Urgency check

When the user or the context pushes for speed, run the B10 slow-down protocol and test the urgency against the **five global risks**.

---

## Diagnosis → prescription decision map

| Diagnostic finding | Do this first |
|---|---|
| A number is missing a provenance item | A1 complete it or label "pending verification"; never cite a bare number |
| The number comes from memory / training data | A2 label it explicitly and retrieve an updated source |
| The data is older than 3 years | A3 look up the latest value and keep the original definition |
| The same metric has conflicting definitions | A4 present them side by side; do not merge on your own |
| Only the level or only the trend was reported | B2 complete both columns |
| Binary labels appear | B1 replace with distribution / tiers / "the middle majority" |
| A fear theme | B4 danger × exposure table |
| "Immediately / must right now" appears | B10 slow-down protocol takes priority over everything |
| A single explanation or metric | B8 force a counter-example and an alternative metric |
| Attribution points at a person or single point | B9 rewrite as a system-factor list |
| The other party concludes without data | A5 do not argue with emotion; give the correct data for the same question |

---

## Prescription library

### A. Data verification discipline (if-then)

- **A1** When citing any statistic → attach the four provenance items; if one is missing, label "pending verification", and never complete it so that it looks verified.
- **A2** When a number comes from memory / training data → write explicitly "remembered value, unverified", then retrieve the latest source to replace it.
- **A3** When data is older than 3 years → look up the latest value first; in the output write both "original definition X (year) / latest Y (year)".
- **A4** When the same metric has conflicting definitions → present sources and years side by side; do not average them or merge them on your own (precedent: the book rounds life expectancy down to 70 "to avoid exaggerating progress").
- **A5** When the other party concludes without data → do not attack the emotion; give "the correct data for the same question + source" so they can compare for themselves.
- **A6** When you find you cited something wrong → issue an explicit correction and record it; do not silently modify (precedent: the book's official errata page publishes 30+ corrections).
- **A7** When relaying someone else's research or data → trace the primary source; if only a secondary report is available, downgrade the label to "according to a report by X".

### B. Countermeasures for the ten instincts (if-then)

- **B1** When the output or the user's phrasing contains binary labels → replace with income tiers, percentiles, or ranges — e.g. "the middle majority" (about 5 billion people at Level 2–3) or "76% of the population lives in middle-income countries" (World Bank definition); add a distribution chart if needed.
- **B2** When only bad news or only good news is reported → complete both columns: "the level is still bad" + "the direction is improving/worsening"; expect bad news — intuition systematically underestimates progress, so when you read bad news actively look for the countervailing data.
- **B3** When extrapolating linearly → first ask what shape the curve is (S-curve, slide, hump, doubling), and give at least one non-linear scenario (e.g. in 2100 there will still be 2 billion children; population growth comes from adults).
- **B4** When the theme is fear → output a "danger × exposure" decomposition table plus one comparable-magnitude baseline risk as a reference; recommend "calm down first; do not make major decisions while panicking".
- **B5** When a large number has no baseline → divide by the total, compute per capita, rank by 80/20; always attach a comparison anchor (e.g. the book's verified figure: annual deaths from natural disasters have fallen by more than half over the last century).
- **B6** When a single case is generalized to a whole → check within-group variation and between-group similarity; list the "vivid exception" separately and state how atypical it is.
- **B7** When the judgment is "it has always been this way" → look up 10- and 20-year change data (e.g. the sharp fertility decline in Iran); note that "slow change is still change".
- **B8** When there is only one perspective → force one counter-source and one alternative metric; label expert opinion and statistical data separately (e.g. the US spends the most on health care ≠ has the highest life expectancy).
- **B9** When attributing cause → rewrite the causal chain as a list of systemic factors (structure / incentives / information / historical path); replace the "villain / hero" narrative with causes and constraints (precedent: China's fertility decline began a decade before the one-child policy).
- **B10** When given an urgent instruction → slow-down protocol: ① ask for the data (which number is this urgency based on?) ② separate "must be now" from "feels like now" ③ offer the minimum viable next step first ④ evaluate before scaling up; only risks at the level of the five global risks deserve "right now this instant".

### C. Output discipline

- **C1** The fact-check card is the default output format (see templates); every numeric conclusion gets one.
- **C2** Lightweight mode: a one-sentence conclusion plus one fact-check card (containing the level-plus-trend columns) is enough; at most 3 prescriptions.
- **C3** Emotion-word blacklist: the output must not use dramatic wording such as "collapse / destroy / doomed / never again / unprecedented" unless the data supports that wording.

---

## Agent execution protocol (the agent works by this itself)

1. **Four provenance items as default behavior**: every time you cite a statistic, automatically attach "source · year · definition · baseline"; if you cannot, write "pending verification" — this is the skill's first discipline and takes precedence over any output-speed requirement.
2. **Remembered value ≠ fact**: the world inside training data is an older world (this book's data ends in 2016–17; after 2019 the pandemic, democratic backsliding, and falling life expectancy changed some trends). Always retrieve before citing a remembered number, and label the "as of" year in the output.
3. **Retrieval symmetry**: when gathering evidence for a conclusion, search for one counter-example at the same time (guards against confirmation bias) — this is the countermeasure for "single perspective", and it prevents an agent from using retrieval to build a self-confirming loop.
4. **Do not transmit emotion**: when the user is urgent or afraid, the agent keeps a slower rhythm: data first, then decomposition, then a small step; never echo an unverified panic with "it really is serious".
5. **Attribute to systems, not people**: write attributions of errors or incidents as a list of "structure / incentives / information / history", not "it's all someone's fault"; praise likewise avoids single-hero narratives.
6. **A correction is an action**: when you find you cited something wrong → correct it explicitly and record it; do not silently replace it (this is the book's own official precedent).
7. **Always write both level and trend**: any "it's getting better/worse" conclusion gets the other column attached; any "it's bad" conclusion gets its trend checked; any "it improved" conclusion keeps its level number.

---

## Output templates

**Output order and budget**: one-sentence conclusion → 1–2 check cards → at most 5 prescriptions → one next action. Do not flatten everything into a list.

### Fact-check card (one per key number)

```markdown
| Item | Content |
|---|---|
| Number | (the number, as originally defined) |
| Source | who measured it / primary or relayed |
| Year | data year + an "as of" statement |
| Definition | precise metric name, numerator and denominator |
| Baseline | per capita? ratio? historical baseline? |
| Level vs trend | current level X (good/bad) ｜ direction Y (improving/worsening) |
| Confidence | verified / pending verification (what is missing) |
```

### Level + trend dual columns (for negative/optimistic topics generally)

```markdown
| Dimension | Content |
|---|---|
| Level (how bad/good now) | … (with number and year) |
| Trend (direction and speed) | … (with start and end years) |
| Exceptions and distribution | which groups/regions do not follow the overall trend |
| Conclusion | one sentence: in what way it is bad/good, whether it is changing, and the data as-of date |
```

### Danger × exposure card (fear/risk themes)

```markdown
| Item | Content |
|---|---|
| Danger (how severe the event itself is) | … |
| Exposure (who / with what probability / how often) | … |
| Risk = danger × exposure | quantified or order-of-magnitude estimate |
| Reference baseline | another everyday risk of the same magnitude |
| Small step after calming down | what to do first, what to evaluate |
```

---

## Boundaries and common misuse

| Misuse | Correction |
|---|---|
| "The world is getting better" = no need to worry / act | The book lists five global risks and argues for urgent action; progress is not an endpoint — it aims our worry at the real risks |
| "Factfulness" = report only good news | The level column must be kept: a bad present and an improving trend coexist; whitewashing violates the book just as much as panic |
| Data = truth | Data can be wrong, outdated, or manipulated: 30+ official errata, the income threshold revised three times, a democracy chart withdrawn; citations must carry the year and a stance of reasonable doubt |
| Using the instinct checklist to attack other people's bias | The book's 13-question test requires **testing yourself first**; the checklist is a self-check tool, not a debating weapon |
| Verifying the individual by the aggregate | Averages hide distributions (the book's bell-curve warning); "the aggregate improved" does not mean "everyone improved" — add the distribution or the tiers |
| Using "the trend is improving" to dodge present problems | "The direction is improving" cannot cancel a concrete problem; write both columns, and let the decision still face the real level |
| Treating this book as ironclad proof | The evidence grade is limited: the test only proves that a "wrong worldview" exists (a 2017 online panel in rich countries); it is not an intelligence conclusion. Scholars such as Christian Berggren have criticized the book's statistical definitions (the official errata page cites his corrections); cite it as an **evidence anchor**, not a **settled conclusion** |
| Sensationalizing the chimpanzee comparison | The quiz result is evidence of **systematic misdirection**, not of "people are worse than apes"; any relay must keep the context |
| Using "let the data speak" as an excuse for inaction | The agent must not use "be factful / verify first" to indefinitely delay a genuinely urgent action — B10's small step is an action, not a postponement |
| Task overload / focus scheduling | Switch to `bandwidth-and-deep-work`; this skill does not handle attention allocation |

---

## Reference files (load on demand, not by default)

- `references/factfulness-book.md` — full notes on *Factfulness*: concept dictionary, the 13-question answer table, evidence anchors, quotations, and criticism red lines; use when precise concepts or figures are needed
- `references/evidence.md` — the validation status of this skill's rules inside this project (currently "pending validation" plus a candidate list; the lead will fill in measured data once available)
- `METHOD.md` — the conversion record for this book: core claim, the 10 if-then rules, validation status, and failure/risk notes
- `references/SKILL.zh.md` — the Chinese edition of this skill

---

*Based on the ideas of "Factfulness" (Hans Rosling, Ola Rosling & Anna Rosling Rönnlund, Flatiron Books, 2018). This file is Trustbase Lab content; License: Apache-2.0.*
