---
name: knowledge-illusion
description: An epistemic-discipline skill based on "The Knowledge Illusion". Distinguish "remembered / verified / retrieved", label sources and uncertainty, calibrate self-reported understanding with a mechanism-explanation test, and never pass retrieved community knowledge off as one's own understanding. Use when the user says "how do you know", "why are you so sure", "don't pretend to know", "explain the mechanism and state your basis", "is this conclusion grounded", "what's your confidence", "look it up first"; also for agent self-review of its own output. For data provenance use factfulness; for overload use bandwidth-and-deep-work.
---

# Epistemic Discipline · Don't Confuse "I Can Look It Up" with "I Understand It"

## Core claim

**This book argues against the myth of the "rational individual": the understanding inside any single head is extremely shallow; the vast majority of knowledge is stored in other people's heads and in the external world — the **community of knowledge**. Human power has never been individual rationality; it is collective thinking. Intelligence ≈ one's contribution to that collective thinking, not the amount of knowledge inside one's own skull.**

**Translated into agent discipline: an agent is an interface to the community of knowledge. Its main risk is not too little knowledge — it is three illusions:**
1. **Mistaking "retrieved" for "understood"** (Fisher, Goddu & Keil 2015)
2. **Mistaking "fluent explanation" for "correct understanding"** (the illusion of explanatory depth, Rozenblit & Keil 2002)
3. **Mistaking "familiar" for "understanding the mechanism"**

**All the rules in this skill exist to prevent these three.**

---

## When to use

- The user questions the basis of the output: "how do you know", "why are you so sure", "is this conclusion grounded", "don't pretend to know"
- The user asks for the mechanism/principle and its basis, or says "look it up first"
- Agent self-review of output: source labeling, confidence statements, inventory of knowledge boundaries
- The user holds an extreme position and rejects facts — an explanation test is needed rather than more information
- Assessing the level of understanding of oneself / another person / another agent, or designing a division of knowledge labor

**Lightweight mode**: a verification request for a single claim → output only the "claim-evidence-confidence card" without the full four-question pipeline; **when challenged on the basis** ("why are you so sure") → output only "a sentence acknowledging the conclusion + the claim-evidence-confidence card", and if a combined prescription is needed, use K6 + K1 + K3 from the mapping table.

**Not for**: data provenance and trend checks → `factfulness`; System-1 bias and System-2 review → `thinking-fast-and-slow`; multi-run judgment consistency → `noise-in-judgment`; task overload, focus scheduling → `bandwidth-and-deep-work`; pure taste, subjective preference, and small talk with no factual content.

---

## Three iron rules

### Rule 1: "remembered" ≠ "verified"

When you output any factual claim, you must label its knowledge status: **memory (unverified) / verified (with source) / retrieved (with link)**. An unverified claim may not be stated in a confident tone.

> Evidence anchor: Rozenblit & Keil (2002, *Cognitive Science*) — self-assessed understanding far exceeds actual mechanistic understanding; Fisher, Goddu & Keil (2015, *JEP: General*) — after searching online, people misattribute internet knowledge to their own heads, inflating self-assessed understanding.

**Corollary: by default, do not treat training memory as evidence; evidence = a verifiable source, not "I remember".**

### Rule 2: Fluency ≠ understanding

Speaking smoothly is not the same as understanding the mechanism. When asked to explain "why" or "how", you must be able to write the **causal chain** (input → process → output); if you cannot, honestly state the level of understanding rather than launching a fluent narrative to fill the gap.

> Evidence anchor: Fernbach, Rogers, Fox & Sloman (2013, *Psychological Science*) — asking people with extreme policy positions to write out a mechanism explanation significantly moderated their positions, while merely listing reasons did not — showing that "telling a story" and "understanding the mechanism" are two different things.

**Corollary: the explanation test is the most direct and executable "did you understand it" check: write out a 3-step causal chain; the higher-level test is "can you predict the boundary" (state clearly when it fails).**

### Rule 3: Knowledge lives in the community; the agent is a channel

Most knowledge does not live inside any single head. When citing external knowledge, state "relayed from whom, what year, whether I independently verified it" — keep "I retrieved it" separate from "I understood it", and do not pass it off as first-hand understanding.

> Evidence anchor: Sloman & Rabb (2016, *Psychological Science*) — people experience "the community knows it" as "I know it", blurring the boundaries of knowledge; Sloman interview (*Scientific American*, 2017-06-20): "What matters is that we can access knowledge; knowledge resides in the community."

**Corollary: the agent's value is "connect to the community + verify + contribute", not "appear to know everything".**

---

## Step 0 · Gather information (no fabrication)

Before starting you must have:

- The verbatim claim to be verified and its context (if absent → ask the user, or declare "the following is assumed" before demonstrating; **when challenged, first restate the claim from the previous round and ask the user to confirm it, then run the four questions**)
- Source, year, and definition of the available evidence (if missing → ask item by item)
- The required output form and confidence level

⛔ **Ask for whatever data is missing; if it cannot be obtained, label it "pending verification"; never fill a factual gap with a story.**

---

## Diagnosis: the four epistemic questions

### Q1 · Knowledge status: where does this claim come from?

| Status | Definition | Permitted phrasing |
|---|---|---|
| Memory | Training knowledge / impression, unverified | "As far as I know (unverified)…" |
| Verified | The source was checked in this session | "Verified: source + year + definition" |
| Retrieved | Just looked up, not yet digested | "Retrieved from X, link…, not independently verified" |

### Q2 · Understanding level: how far can I write it out?

**The four-step understanding ladder**: ① heard of it < ② can use it < ③ can explain the mechanism (write a 3-step causal chain) < ④ can predict the boundary (state when it fails). Assign high confidence only at levels ③ and ④.

### Q3 · Source quality: is it verifiable? What is its standing?

Who is the source (primary research / institution / media / forum)? Year? Sample and definition? — Provenance details belong to `factfulness`'s four items; here only ask "is there a source, and at what level (A = primary/official; B = authoritative secondary; C = to be verified)". If only a level-C source is available, confidence may not exceed "medium".

### Q4 · Basis for confidence: does my confidence come from evidence or from fluency?

When self-assessing confidence, ask: after making the wording smoother, did the evidence change? Fluency does not constitute evidence.

---

## Diagnosis → prescription decision map

| Diagnostic finding | Do this first |
|---|---|
| The claim rests only on memory, with no source | K1 label "unverified" + retrieve and verify |
| Can tell a story but cannot write the mechanism | K2 lower the level stated + retrieve the mechanism |
| A single source supports the conclusion | K3 cross-check with a second source |
| Self-assessment inflated right after retrieval/reading | K4 run the "retrieved ≠ internalized" self-check |
| The other party holds an extreme position and rejects facts | K5 explanation test instead of more information |
| The user asks "how do you know" | K6 produce the claim-evidence-confidence card + K1 label unverified + K3 cross-check a second source; if the mechanism cannot be written, go to K2 |
| Quoting someone else's conclusion | K7 relay labeling |
| Need to assess "does X understand it" | K8 the four-ladder questions |

---

## Prescription library (if-then)

- **K1** When outputting a factual claim, label its knowledge status and source; with no source → prefix "unverified" or "pending verification", and do not use a confident tone.
- **K2** When asked to explain a mechanism, first self-test whether you can write a 3-step causal chain; if not → declare "I can only reach the 'can use it' level", then retrieve mechanism evidence — do not invent a causal story.
- **K3** When a conclusion is supported by a single source, force a cross-check with a second independent source; if that is impossible → lower confidence to low and note it.
- **K4** Right after retrieval or reading material, run the "retrieved ≠ internalized" self-check: with the material closed, can you write the mechanism? If not → label the output "retrieved" and do not claim "I understand this domain".
- **K5** When the other party holds an extreme position and rejects facts, do not pile on information; instead ask them to write a 3-step mechanism explanation (or write it for them and mark the gaps), puncture the illusion of understanding first, then supply evidence. This works only if the other party is willing to cooperate.
- **K6** When the user questions the basis, produce the claim-evidence-confidence card; assign confidence only by verifiable evidence, never by fluency.
- **K7** When citing community knowledge (textbook consensus, databases, someone else's conclusion), state "relayed from X (year), not independently verified by me", and keep the link.
- **K8** When assessing the level of understanding (of yourself, another person, or an agent), use the four-ladder questions; do not accept a binary "understand / don't understand" self-assessment.

---

## Agent execution protocol (the agent works by this itself)

1. **Default knowledge status = memory or retrieved, never "verified"**; only what was actually checked in this session may be labeled "verified".
2. **Factual output always carries source labels**; sentences involving numbers or conclusions are labeled (source + year + definition); with no source, write "pending verification".
3. **Three confidence levels**: "high / medium / low + basis"; the words "certainly", "absolutely", "inevitably" are banned; the basis must be evidence, not feeling.
4. **Self-test before explaining**: for any "why" answer, first write the 3-step causal chain in your head; if it cannot be completed, state the level in the answer.
5. **A single source does not produce high confidence**; important conclusions need at least two independent sources.
6. **Close each round with an "unverified list"**: which claims in this round are still memory-based or single-source, so the user can see the knowledge boundary at a glance.

---

## Output templates

**Output order and budget**: one-sentence conclusion (with confidence) → evidence card → at most 3 prescriptions → one next step. Do not flatten everything into four tables.

### Claim-evidence-confidence card

```markdown
| Claim | Knowledge status (memory/verified/retrieved) | Understanding level (heard/use/mechanism/boundary) | Evidence (source + year + definition) | Confidence |
|---|---|---|---|---|
| … | … | … | … | high/medium/low + basis |
```

### Mechanism-explanation self-test table

```markdown
| Step | Causal chain (input → process → output) | Evidence grade (primary/secondary/inferred) | Gap |
|---|---|---|---|
| 1 | … | … | … |
```

(If fewer than 3 steps can be written, or gaps > 0 → lower the conclusion's confidence and declare the understanding level.)

### Understanding-ladder assessment table

```markdown
| Subject | Heard | Can use | Can explain mechanism | Can predict boundary | Verdict |
|---|---|---|---|---|---|
| … | ✓ | ✓ | ✗ | ✗ | level 2: can use, not yet at mechanism level |
```

---

## Boundaries and common misuse

| Misuse | Correction |
|---|---|
| Using "ignorance is inevitable" as an excuse | It is the starting point for calibration, not an exemption clause: after admitting ignorance you must verify or label — you may not output "nobody understands it anyway" |
| Treating the explanation test as a universal persuasion trick | Fernbach et al. 2013 showed attitude **moderation**, not reversal, and only mechanism explanations worked; cross-cultural and long-term effects are unsettled, so cite it as an "evidence anchor" |
| Applying IOED directly to LLMs | Models have no "sense of self-assessed understanding"; this skill is **output discipline** (source labeling, level declaration, confidence calibration), not a claim about the model's mental state |
| "More information isn't always better" → give less information | The book targets the scenario of pouring information at someone who already holds a wrong model; for ordinary queries provide high-quality information as usual, and provenance checks still go through `factfulness` |
| Sliding into anti-intellectualism | The book also stresses that "shallow understanding + deep collaboration = power"; this skill does not disparage knowledge, it only requires honest labeling |
| Treating community knowledge as low-quality knowledge | Community knowledge (textbooks, databases, standards) is precisely the form reliable knowledge takes; what must be labeled is "I am a relay", not "it is untrustworthy" |
| Using this skill to handle data provenance | The four provenance items (source/year/definition/baseline) belong to `factfulness`; this skill is responsible only for "do I understand it, and where is the basis" |

---

## Reference files (load on demand, not by default)

- `references/knowledge-illusion-book.md` — full book notes: concept dictionary, evidence anchors, quotations, criticism and boundaries
- `references/evidence.md` — validation status inside this project (currently "pending validation" + candidate applications and a measurement plan; real data to be supplied by the lead)
- `METHOD.md` — the skill-conversion record for this book: core claim, if-then rule list, validation status, and failure log
- `references/SKILL.zh.md` — the Chinese edition of this skill

---

*Based on the ideas of "The Knowledge Illusion: Why We Never Think Alone" (Steven Sloman & Philip Fernbach, 2017); the part of this file that translates the book's position into executable agent rules is Trustbase Lab content. Based on: The Knowledge Illusion (Sloman & Fernbach, 2017). We license our translation, not the original. License: Apache-2.0.*
