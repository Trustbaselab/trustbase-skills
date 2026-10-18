# ⭐ Cognitive Skills — Classic Books, Turned Into Executable Rules for Agents

> **This layer is not "reading notes".**
> **It is: validated behavioral rules + real data.**

---

## Why we do this

**An AI's training objective is *average* — it is a compression of everything.**
**A book with a soul is one specific person, in one specific situation, making one specific judgment.**

**⭐ So what a book gives an AI is not "knowledge" (the AI already has knowledge) — it is **stance and criteria for judgment**.**
**And that is exactly what AI lacks most.**

### Our thesis

> **AI cannot write a book with a soul — because it pursues the *general*, while a book is *specific*.**
> **But AI needs these books in order to become stronger and better.**

**→ So turning books into rules an agent can execute is a worthwhile thing to do in this era.**

---

# ⭐⭐ The eight-layer cognition operating system

**These are not 8 isolated skills. They form one continuous chain:**

```
① Input layer       factfulness              How to read data correctly
        ↓
② Processing        thinking-fast-and-slow   How not to be fooled by intuition
        ↓
③ Quality           noise-in-judgment        How to keep judgments consistent
        ↓
④ Global            thinking-in-systems      How to see systems and feedback
        ↓
⑤ Bandwidth         bandwidth-and-deep-work  How to work under limited resources
        ↓
⑥ Execution         (same skill)             How to produce depth
        ↓
⑦ Epistemics        knowledge-illusion       How to know what you actually know
        ↓
⑧ Trust             trust-formation          How trust is built and verified
        ↑
⭐ Meta layer       book-to-skill            The method itself, packaged as a skill
```

**⭐ Together, the eight layers form a complete "AI cognition operating system".**

---

# 1. ⭐ What every skill ships

```
<skill-name>/
├── SKILL.md                 ← the rules the agent reads
├── references/
│   ├── <book>-book.md       ← the book's ideas (written by us, no verbatim excerpts)
│   └── evidence.md          ← ⭐ validation data from this project
└── METHOD.md                ← ⭐ how this specific book was converted
```

| File | Purpose | Key |
|---|---|---|
| **`SKILL.md`** | **Trigger conditions · rules · counter-examples** | **if-then form, not slogans like "be focused"** |
| **`references/*.md`** | **the book's ideas** | **our own understanding; ⛔ no verbatim excerpts** |
| ⭐ **`references/evidence.md`** | **validation data from this project** | **⭐ the dividing line: others summarize books, we validate in our own project** |
| ⭐ **`METHOD.md`** | **the conversion method** | **⭐ makes the next book faster** |

---

# 2. ⭐⭐ The eight skills

## ① `factfulness` — Input layer

| Item | Content |
|---|---|
| **Based on** | ***Factfulness*** (Hans Rosling et al.) |
| **Core claim** | **Human judgments about the world are systematically biased; data must correct intuition** |
| **What it does** | **Four-part data provenance audit (source / year / definition / baseline) → ten instinct diagnostics → "level + trend" dual-column output** |
| ⭐ **Triggers** | "Is the world getting worse" · "Is this number trustworthy" · "Cite a source for me" · "Stop fear-mongering" |
| ⭐ **Why it matters to us** | **Directly aligned with our business — we do verifiable data; this teaches how to use it** |

## ② `thinking-fast-and-slow` — Processing layer

| Item | Content |
|---|---|
| **Based on** | ***Thinking, Fast and Slow*** (Daniel Kahneman) |
| **Core claim** | **Two systems: fast (intuition) and slow (reasoning); the fast system errs systematically** |
| **What it does** | **Detect System-1 patterns in agent/LLM output → force a System-2 review and calibration** |
| ⭐ **Triggers** | "Is this AI conclusion reliable" · "That answer felt too smooth / too confident" · "Review this AI output" |
| ⭐ **Concepts** | **anchoring · availability · representativeness · framing · loss aversion · overconfidence · planning fallacy** |

## ③ `noise-in-judgment` — Quality layer

| Item | Content |
|---|---|
| **Based on** | ***Noise*** (Kahneman, Sibony, Sunstein) |
| **Core claim** | **Inconsistency (noise) is more hidden — and more common — than bias** |
| **What it does** | **Separate bias from noise → noise audit to quantify disagreement → decision hygiene (independent judgment, aggregation, ranking, structured guides)** |
| ⭐ **Triggers** | "Why does the answer change every time" · "Which conclusion should I trust" · "How do I make scoring consistent" |
| ⭐ **Concepts** | **level noise · pattern noise · occasion noise · decision hygiene** |

## ④ `thinking-in-systems` — Global layer

| Item | Content |
|---|---|
| **Based on** | ***Thinking in Systems*** (Donella Meadows) |
| **Core claim** | **System behavior is produced by structure, not by individual intent** |
| **What it does** | **Stock-and-flow diagrams + feedback loops → structural diagnosis (watching only flows / ignoring delays / treating symptoms / eroding goals) → 12 leverage points** |
| ⭐ **Triggers** | "Why does fixing it make it worse" · "The change had no effect" · "Where's the leverage point" |
| ⭐ **Concepts** | **reinforcing loops · balancing loops · stocks and flows · delays · leverage points · system traps** |

## ⑤⑥ `bandwidth-and-deep-work` — Bandwidth + Execution layer

| Item | Content |
|---|---|
| **Based on** | ***Scarcity*** (Mullainathan & Shafir) + ***Deep Work*** (Cal Newport) |
| **Core claim** | **Bandwidth is limited; when occupied, cognition degrades; only by blocking distraction can depth be produced** |
| **What it does** | **Bandwidth audit + tunneling check → deep/shallow layering + deep-block scheduling → plus agent-side context-management and batching protocols** |
| ⭐ **Triggers** | "Too much to do" · "Always interrupted" · "Can't focus" · "How should I prioritize" |
| ⭐ **Validated in this project** | **Per-round tokens 141K → 5.6K (−96%) · pending items 67 → 2 · status lookup 2–3 min → 5 s** |
| ⭐ **Concepts** | **bandwidth tax · tunneling · slack · scarcity trap · focus dividend · attention residue · shutdown ritual** |

## ⑦ `knowledge-illusion` — Epistemics layer

| Item | Content |
|---|---|
| **Based on** | ***The Knowledge Illusion*** (Sloman & Fernbach) |
| **Core claim** | **People believe they understand the world far more deeply than they do; what they actually know is *who knows*** |
| **What it does** | **Distinguish "remembered / verified / retrieved"; label source and uncertainty; calibrate self-assessed understanding with a mechanism-explanation test** |
| ⭐ **Triggers** | "How do you know" · "Why are you so sure" · "Don't pretend to know" · "Explain the mechanism" |
| ⭐ **Why it matters to AI** | **AI is the extreme case: it "knows" a lot and is also the most unaware of its own boundaries** |

## ⑧ `trust-formation` — Trust layer

| Item | Content |
|---|---|
| **Based on** | ***Who Can You Trust?*** (Rachel Botsman) |
| **Core claim** | **Trust cannot be obtained by claiming it — only by being verifiable** |
| **What it does** | **Turn every trust claim into "fact + verification entry point"; audit against four elements (competence / reliability / integrity / transparency)** |
| ⭐ **Triggers** | "Why should anyone trust this" · "How do we prove we're credible" · "Is this source trustworthy" |
| ⭐ **Why it matters to us** | ⭐ **This is our business. This skill is our brand's explanation document.** |

## ⭐ Meta: `book-to-skill` — The method as a skill

| Item | Content |
|---|---|
| **Based on** | **—** (it is a synthesis of the seven conversions above) |
| **Core claim** | **Its capability is general; its standard is specialized** |
| **What it does** | **Seven-step SOP: score the book → read for the core claim → separate "wisdom" from "rules" → translate into if-then rules → validate in a real scenario → write SKILL.md / evidence.md / METHOD.md → check against the delivery checklist** |
| ⭐ **Why it's the meta layer** | ⭐ **It packages "the method of packaging knowledge" as a skill** |

---

# 3. ⭐⭐ The conversion method (`METHOD.md` · six steps)

| # | Step | Hard requirement |
|---|---|---|
| **1** | **Read for the core claim** | **Not a summary — what is the author arguing, and against whom?** |
| **2** | ⭐ **Separate "wisdom" from "rules"** | **Only what can become an if-then rule counts; "be objective" is not a rule** |
| **3** | ⭐ **Translate into agent rules** | **if-then form** ("when X, do Y"); ⛔ **no slogans** |
| **4** | ⭐⭐ **Validate in a real scenario** | **Must have a real application with before/after data** |
| **5** | ⭐ **Record the validation data** | **Before/after · reproducible · provenance stated** |
| **6** | **Write `SKILL.md`** | **Triggers / rules / counter-examples / source status / copyright boundary** |

### ⭐ Copyright boundary

| ✅ Allowed | ⛔ Not allowed |
|---|---|
| **Summarize ideas and write our own understanding** | **Quote long passages** |
| **Attribute: "based on the ideas of <book>"** | **Claim the ideas are our original theory** |
| **License our own written part** | **Include the book's text / PDF** |

### ⭐⭐ Provenance boundary (rule 2b of `book-to-skill`)

**Every citation must carry a provenance status:**

| Status | How to write | How it may be used |
|---|---|---|
| **Verified** | "《Book》p.XX: …" | ✅ May be cited as "proposed in the book" |
| **Secondhand** | "According to <source> reporting <book>: …" | ⚠️ Label as secondhand |
| **From memory** | "Our understanding is: … (provenance pending verification)" | ⛔ **May not be presented as "the book says"** |

---

# 4. ⭐ Honesty boundary (our convention)

**Every `evidence.md` must state:**

1. **Data provenance** (what was measured, what was estimated)
2. **Attribution limits** — ⭐ **"the change came first, the concept attribution came after; this is not a controlled experiment"**
3. **Citation phrasing** — **"a validation case in this project", not "causal proof"**
4. **Open items** — **if it is in progress, say "in progress"**

**⭐⭐ The principle:**
> **We do not claim causality.**
> **We say "we applied this method, and the data moved like this" — not "this method caused the change".**
> **→ That is what "verifiable" means at the methodology level.**

**⭐⭐ Rule:**
> **Rather omit one piece of evidence than overstate it by a millimeter.**

---

# 5. ⭐ Next-generation candidates (not urgent)

| Book | Layer it fills | Status |
|---|---|---|
| **_The Signal and the Noise_** | Forecasting | ⏳ Candidate |
| **_Superforecasting_** | Forecasting | ⏳ Candidate |
| **_The Box_** (containerization) | Standards | ⏳ Candidate |
| **_Antifragile_** | Robustness | ⏳ Candidate |

**⭐⭐ Our judgment:**
> **Eight skills already form a complete chain (input → processing → quality → global → bandwidth → execution → epistemics → trust).**
> **More books without validation data would just be "stacked reading notes".**
> **⭐ And our differentiation is precisely **validation** — not **quantity**.**

**→ So: first make these eight thorough, put them to use, and gather external feedback. Then consider the next batch.**

---

*Based on the **ideas** of published books; sources are noted inside each skill. This layer's contribution is «**translating ideas into executable rules for agents**».*
*License: Apache-2.0*
