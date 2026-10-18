---
name: trust-formation
description: A trust-building skill based on "Who Can You Trust?" (Rachel Botsman). Translate trust from a claim into something verifiable (trust ≠ confidence, institutional trust → distributed trust, the trust leap, the four elements competence / reliability / integrity / transparency), and output a statement framework directly usable for a website's "why you can trust us" section. Use when the user says "why should anyone trust this", "how do we prove we're credible", "how do we make people believe us", "is this platform trustworthy", "institutions aren't trusted anymore, what now", "how do we write a trust endorsement"; not for pure organizational management or pure brand marketing; for data provenance use factfulness.
---

# Trust Cannot Be Claimed — Only Verified

Based on the ideas of *Who Can You Trust?* (Rachel Botsman, 2017).

## When to use

- "Why should anyone trust this" · "how do we prove we're credible" · "how do we make people believe us" · "how do we write a trust endorsement" · "how do we prove we're trustworthy"
- "Is this source/platform/tool trustworthy" · "institutions aren't trusted anymore, what now" · "you can't trust anybody"
- Before designing trust signals (ratings / certifications / badges / endorsement copy), run a four-element audit first
- **Lightweight mode**: if simply asked "is X trustworthy" → go straight to Step 0 and output the "trust check card" (template 2), without the full pipeline

**Not for**:
- Data provenance / year / definition checks → use `factfulness`
- AI conclusions that are overconfident, or bias review → use `thinking-fast-and-slow`
- "How do you know you actually understand this" calibration → use `knowledge-illusion`
- Attention / multitasking / scheduling problems → use `bandwidth-and-deep-work`
- Internal organizational management and culture building (the part this book does not address) → do not apply this skill

## Three iron rules

### Rule 1: Trust ≠ confidence — trust faces the unknown and cannot be obtained by claiming it

**Trust** is a confident relationship with the unknown, requiring vulnerability and choice; **confidence** comes from past predictability. So the sentence "we are trustworthy" is itself untrustworthy — only testable statements can build trust.

**Do**: write every trust assertion as "fact + verification entry point" (e.g. "59 tools, see the tools list").
**Don't**: write "trustworthy", "authoritative", "industry-leading" or similar self-evaluations — a hit means rewrite.

### Rule 2: Trust is shifting from institutions to verifiability — "you are a big institution" no longer produces trust

The Edelman 2017 report described a "global trust collapse" in institutional trust; Botsman's conclusion is that people no longer trust you because you are a big institution, but because you can be verified. In the era of distributed trust, the currency of trust is a **re-checkable record**.

**Do**: translate "who we are" into "what you can check, and how".
**Don't**: substitute job titles, scale, years, or a client list for verifiable facts (those are signals, not evidence).

### Rule 3: A "why you can trust us" section must contain only testable statements — four questions + four elements

Every external statement must be able to answer the project S-1 four questions: **who guarantees it · is it first-hand · what confidence level · can it be re-checked**; and must map onto the four-element framework: **competence (can you do it) / reliability (do you do it every time) / integrity (do you stand with me when interests conflict) / transparency (can I verify it)**. The book's precise source for the four elements is **pending verification**; when using it, do not claim "the book's exact wording" — only claim "a translation based on the book's ideas".

**Do**: statement format "X units of Y, see Z" (X is a number, Y is the definition, Z is the verification entry point).
**Don't**: "we are very transparent", "we are trustworthy" — whether something is transparent or trustworthy is the other party's verification conclusion, not our self-description.

## Step 0 · Gather information (ask for what is missing; fabrication forbidden)

Before writing any trust statement, confirm these 5 items; if one is missing, ask:

1. **The number being asserted**: exact value + definition (e.g. 59 = the number of upstream MCP tools, measured 2026-10-18)
2. **As-of date**: a number without an as-of date is unreliable
3. **Source**: the guarantor + an openable URL (not just "according to authoritative sources"); an internal measurement document may only serve as a definition footnote — the external "verification entry point" must be a public path the user can click
4. **Confidence level**: A = official filing / announcement · B = company statement / authoritative media · C = unverified (do not put it in a statement without a level)
5. **Verification entry point**: a path the reader/customer can click to check (record/<id>/, /usage/, /corrections/, etc.)

## Core workflow: trust-statement audit

```
① Gather the 5 items from Step 0 (missing → ask)
② Four-element self-check: place each statement under competence / reliability / integrity / transparency
③ Four-question filter: who guarantees it? is it first-hand? what confidence level? can it be re-checked?
   — any question unanswerable → downgrade to "unverified" or delete
④ Self-praise word scan: trustworthy / authoritative / leading / top / exclusive / first / most professional / most reliable …
   a hit → rewrite as "fact + entry point"
⑤ Output the "why you can trust us" statement framework (template 1) or the "trust check card" (template 2)
```

## Diagnosis → prescription decision map

| Diagnostic finding | Do this first |
|---|---|
| The copy is all adjectives, no numbers | Delete the adjectives → each assertion gets a number + definition + as-of date (prescription A1) |
| There are numbers but no sources | Add the guarantor + an openable URL (prescription A2) |
| There is a source but no level | Assign an A/B/C level and label it (prescription B1) |
| There is a data gap but it is being smoothed over | Change it to "we do not have this data" + a gap description (prescription C1) |
| Something said earlier is now outdated or wrong | Correct it proactively and leave a trace; never silently revise (prescription C2) |
| A "transparency" promise with no accountability clause | Add "who can check, check what, what happens if it's wrong" (prescription D1) |
| The user is in a "you can't trust anybody" mood | First distinguish trust / confidence / risk, then explain the shift in trust (prescription E1) |
| Need to evaluate an external platform or source | Use the trust-stack layered check (prescription E2) |

## Prescription library (if-then rules)

**A. Competence — "can you do it?"**
- A1 When you want to write "we are capable" → write "N tools/records/domains, see <entry point>", and state the measurement date and definition.
- A2 When the number comes from internal statistics → attach the measurement method (who counted it, when, how), otherwise downgrade to "pending verification".
- A3 When a capability claim exceeds the current facts (e.g. "covering the whole industry" but only 6 domains) → narrow the claim to the actual coverage; write the boundary, not the vision.
- Counter-example: writing "comprehensive capability" with no verification entry point → the reader can only choose to believe or not believe; the statement fails.

**B. Reliability — "do you do it every time?"**
- B1 When giving any number → it must carry a confidence level (A/B/C) and an as-of date; if either is missing, do not publish it.
- B2 When the other party cannot verify your claim → lower the certainty of the wording (use "according to…" rather than "it is…").
- B3 When using a sampled percentage (e.g. "89% are grade A") → you must state the sample size and sampling scope ("89 of 100 sampled benchmarks"), never "all of them are grade A".
- Counter-example: treating one performance as standing evidence → reliability evidence is a time series, not a single point.

**C. Integrity — "do you stand with me when interests conflict?"**
- C1 When the data is insufficient → write "we do not have this data" and explain the gap; do not substitute similar data.
- C2 When you find you previously gave something wrong → correct it proactively, explain why, and leave a trace (corresponding to the /corrections/ correction archive); never silently modify.
- C3 When there is a conflict of interest or a positional background → disclose it proactively (e.g. the commercial background of the data publisher); do not pretend to be neutral.
- Counter-example: hiding gaps, filling "unavailable" with "—" without explanation → short-term persuasive gain, long-term destruction of trust.

**D. Transparency — "can I verify it?"**
- D1 When writing a "transparency" promise → it must carry an accountability clause: who can check, check what, what happens if it is wrong; "public" without "checkable + accountable" = performative transparency — delete it.
- D2 When giving a verification entry point → use a stable ID + a re-check URL + a snapshot (to guard against link rot / page edits); do not paste a bare link.
- D3 When publishing an "all passed" type result → write the test method and the count ("193 re-check URLs, 193 returned 200, verified in 11 seconds"); do not write the four characters "all passed".
- Counter-example: showing data with no verification entry point → showing ≠ transparency (per a CIPD 2018 report, Botsman argued transparency is not the answer to building trust; original wording pending verification).

**E. Trust mechanics (trust shift / trust leap)**
- E1 When the user asserts "nobody can be trusted" → first distinguish trust (faces the unknown, requires vulnerability) / confidence (based on predictability) / risk (probabilizable), then explain the shift in where trust flows (institutions → distributed); do not argue "institutions are still fine".
- E2 When evaluating an external platform or source → use the trust-stack layers: ① do I trust the idea (is the model valuable) ② do I trust the platform (can the system govern both sides) ③ do I trust the person/algorithm on the other side (are the signals verifiable); look for signals layer by layer; a missing layer is a risk point.
- E3 When designing trust signals (ratings / badges / certification copy) → keep only signals a third party can re-check; delete the rest.
- Counter-example: treating a "trust leap" as a risk the user should bear → the designer's job is to reduce the leap's risk, not to celebrate the user's bravery.

## Agent execution protocol (the agent works by this itself)

1. Any factual assertion in the output → attach a re-checkable path (record ID + source URL + as_of), otherwise label it "unverified".
2. Before writing copy or a reply → run the self-praise word blacklist (trustworthy / authoritative / leading / top / exclusive / first / most professional / most reliable); a hit is rewritten as "fact + entry point".
3. When asked for numbers where "roughly is fine" → do not pass an estimate off as a measurement; write "approximately" or "pending verification".
4. When you find a previous output of yours was wrong → issue a correction and explain why; do not silently rewrite.
5. When asked to "prove we are credible" → output template 1 (the four-element statement framework), with a verification entry point in each cell; no adjectives.
6. When citing trust surveys (Edelman etc.) → label the definitional and methodological controversies, and phrase it as "that survey shows", never as "the fact is".
7. For data provenance → check the `factfulness` four items first; for overconfident conclusions → review with `thinking-fast-and-slow` first; do not re-expand those inside this skill.

## Output templates

### Template 1 · the "why you can trust us" statement framework (website copy structure)

```markdown
# Why you can trust us

> We don't ask you to believe us. Every number you can click and verify.

⚠️ Before filling this in, re-measure or take a fresh export; the numbers below are as of 2026-10-18 and must not be copied from stale values.

| Dimension | Fact (verifiable, with confidence · as-of) | How you verify it |
|---|---|---|
| Competence | 59 MCP tools · 2,738 records · 6 domains (MCP overview export 2026-10-18T13:40:13; grade-A source) | Open /database and count yourself |
| Reliability | Of 100 sampled benchmarks, 89 are grade A (grade-B source: platform self-measurement, 2026-10-18); every record carries a stable ID / as_of / source_url | Sample a record and open record/<id>/ to check |
| Integrity | The fact pack honestly discloses 8 data gaps (grade-B source: project document, 2026-10-18); the corrections page keeps a trace | Look at data_gaps in facts.json · /corrections/ |
| Transparency | 193 re-check URLs were tested: 193/193 returned 200 (11 seconds; a post-launch per-URL re-test is still pending) · /usage/ publishes usage metrics | Click "re-check" on any fact |

## Verification entry points
- Record re-check: https://trustbaselab.com/record/<id>/
- Usage metrics: /usage/ · Correction archive: /corrections/ · Data overview: /database
```

Constraint: numbers must come from a measured or checkable source and carry an as-of date; when writing copy for an external site, replace product facts with the corresponding verifiable statements; if any cell cannot be answered → leave it blank with "pending verification", never fill it with an adjective.

### Template 2 · trust check card (lightweight mode)

```markdown
| Subject | Trust-stack layer | Signal | Verifiable | Verdict |
|---|---|---|---|---|
| <platform/source> | Idea | … | yes/no | pass / risk point |
|  | Platform | … | yes/no |  |
|  | Person/algorithm on the other side | … | yes/no |  |

One-sentence conclusion: <by layer: layers with sufficient verifiable signals are more trustworthy; a layer missing signals = a trust-leap risk point>
Statement discipline: <N self-praise words removed; M verification entry points added; list of pending-verification items>
```

### Output order and length budget
Give the conclusion first (1–2 sentences) → then the framework/check card → finally "pending items + next step". Full pipeline ≤ 800 words; lightweight mode ≤ 300 words.

## Boundaries and common misuse

| Misuse | Correction |
|---|---|
| Using "trust" as a synonym for "high confidence" | Trust faces the unknown and requires vulnerability; confidence is a source grading — two different mechanisms. Confusing them is the number-one error this book names |
| Writing "we are trustworthy / authoritative" | Violates the red line and the book's argument: trust cannot be claimed. Write only "verifiable facts + how to verify" |
| Quoting the four elements as if they were the book's exact wording | The precise source of the four-element framework is **pending verification**; phrase it as "a translation based on the book's ideas" |
| Transparency = trust | Per a CIPD 2018 report, the author argues transparency must be paired with accountability to be verifiable transparency, otherwise it is performance (original wording pending verification) |
| "Distributed trust is inherently more reliable" | Ratings can be gamed, identities faked, algorithms biased; distributed trust has a dark side too |
| Citing Edelman figures without stating the definition | The sample includes an "informed public" subset, single-question measurement, and the publisher is a PR firm; phrase it as "that survey shows" and flag the methodological controversy |
| Treating a "trust leap" as a risk the user should bear | The designer's job is to reduce the leap's risk (signals / guarantees / escrow), not to celebrate the user's bravery |
| Using the phrase "trust layer" in external copy | Project S-1 decision: externally do not use "trust layer"; use "who guarantees it · is it first-hand · what confidence level · can it be re-checked" |
| Writing the evidence status as "verified" | This skill's validation status is **pending verification** (see evidence.md); the product facts are a factual mapping, not causal validation |

## Reference files (load on demand, not by default)

- `references/trust-formation-book.md` — full book notes: concept dictionary, evidence anchors, quotations, criticism (including the underlying reference to Fukuyama's *Trust*)
- `references/evidence.md` — validation status (pending verification) + candidate applications + data provenance
- `METHOD.md` — conversion record for this book
- `references/SKILL.zh.md` — the Chinese edition of this skill

---

*Based on: Who Can You Trust? by Rachel Botsman (2017). We license our translation, not the original.*
*License: Apache-2.0*
