# Trustbase Skills

> **Agent Skills that connect AI to verifiable industry facts.**
> Skills that don't just tell an agent *what to do* — they tell it *where the data comes from, whether it's right, and who is accountable.*

[![skills.sh](https://skills.sh/b/Trustbaselab/trustbase-skills)](https://skills.sh/Trustbaselab/trustbase-skills)
[![License: Apache-2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/skills-14-green.svg)](#skill-catalog)
[![Verifiable facts](https://img.shields.io/badge/verifiable_facts-520+-orange.svg)](https://trustbaselab.com/database)
[![MCP tools](https://img.shields.io/badge/MCP_tools-59-purple.svg)](https://trustbaselab.com/mcp)

```bash
npx skills add Trustbaselab/trustbase-skills
```

---

## Why this repo is different

**Most skill repositories teach an agent *how to do things*.**
**We do one more thing: every skill here is backed by a source that can be verified.**

| Typical skill repo | ⭐ This repo |
|---|---|
| Teaches you to write docs / design UI | Teaches an agent to **retrieve trustworthy facts in a vertical** |
| Where did the data come from? — unknown | **520+ verifiable facts, each with ID, confidence, source, as-of date** |
| Who is accountable for errors? — nobody | **Correction-notice mechanism: callers are told when a record is corrected** |
| Can I check it? — no | **Every record is re-checkable at `/record/<id>/`** |

**Our real asset is not the skill text. It's the combination of *skill + verifiable source*.**
**→ Anyone can write a skill. The verifiable fact layer cannot be copied.**

---

## Two layers

```
trustbase-skills/
├── cognitive/     ⭐ Cognitive layer  — makes the agent *think better* (methodology)
└── industry/      Industry layer     — lets the agent *retrieve reliable facts* (data)
```

### ⭐ `cognitive/` — THE STAR PROJECT

**Classic books, translated into executable rules for AI agents — and validated inside our own project.**

**⭐ An eight-layer cognition operating system:**

```
① Input layer       factfulness              How to read data correctly
② Processing        thinking-fast-and-slow   How not to be fooled by intuition
③ Quality           noise-in-judgment        How to keep judgments consistent
④ Global            thinking-in-systems      How to see systems and feedback
⑤ Bandwidth         bandwidth-and-deep-work  How to work under limited resources
⑥ Execution         (same)                   How to produce depth
⑦ Epistemics        knowledge-illusion       How to know what you actually know
⑧ Trust             trust-formation          How trust is built and verified
        +
⭐ Meta layer       book-to-skill            The method itself, packaged as a skill
```

| Skill | Based on | Core |
|---|---|---|
| **`factfulness`** | *Factfulness* | Four-part data provenance audit + ten instinct diagnostics |
| **`thinking-fast-and-slow`** | *Thinking, Fast and Slow* | Detect System-1 patterns in AI output, force a System-2 review |
| **`noise-in-judgment`** | *Noise* | Separate bias from noise; reduce variance with decision hygiene |
| **`thinking-in-systems`** | *Thinking in Systems* | Stock-and-flow diagrams, feedback loops, 12 leverage points |
| **`bandwidth-and-deep-work`** | *Scarcity* + *Deep Work* | ⭐ **In this project: per-round tokens 141K → 5.6K (−96%)** |
| **`knowledge-illusion`** | *The Knowledge Illusion* | Distinguish "remembered / verified / retrieved"; never pass community knowledge off as own understanding |
| **`trust-formation`** | *Who Can You Trust?* | Turn trust from a claim into something verifiable |
| ⭐ **`book-to-skill`** | **—** | ⭐ **The method for turning a book into a skill, packaged as a skill itself** |

**⭐ Every cognitive skill ships three things:**
- `SKILL.md` — the rules the agent reads
- `references/` — the book's ideas (written by us, **no verbatim excerpts**) + **`evidence.md` (validation data from this project)**
- `METHOD.md` — **how this specific book was converted** (reusable for the next one)

**→ What we produce is not "reading notes". It is **validated behavioral rules + real data**.**

**See [`cognitive/README.md`](cognitive/README.md).**

### `industry/` — INDUSTRY LAYER

| Skill | What it does |
|---|---|
| `rcb-export-compliance` | rCB export compliance check (CBAM / REACH / recycled content / certification chain) |
| `rcb-grade-identification` | Identify a carbon black grade from lab parameters (ASTM D1765 / R-code) |
| `rcb-price-reference` | rCB price reference range and spread vs virgin carbon black |
| `rcb-substitution-assessment` | Whether rCB can substitute a virgin grade, substitution ceiling, what must be tested |
| `carbon-black-weekly` | Produce the *Carbon Black Weekly* industry report (Chinese-language publication) |
| `ai-industry-daily` | Produce the *AI Observer* daily column (Chinese-language publication) |

**⭐ The four `rcb-*` skills are bilingual** (`SKILL.md` in English + `references/SKILL.zh.md` in Chinese).
**⭐ The two content skills are Chinese-only by design** (they target Chinese-language publications).

---

## Data source

**All industry skills depend on the Trustbase Lab MCP server:**

```
https://trustbaselab.com/mcp
```

- **Protocol**: MCP `2026-07-28`
- **Tools**: **59**
- **Extensions**: `io.modelcontextprotocol/skills` · `io.modelcontextprotocol/ui`
- **Records**: **520+ cross-domain benchmarks · 2,738 records total**
- **Standard**: **TBDS-1** (data standard)
- ⭐ **Every fact carries**: stable ID · confidence grade A/B/C · `source_url` · `as_of` · a verification URL

**⭐ Registry**: `com.trustbaselab/rcb-data` (MCP Registry)

---

## Install

### Skills CLI (any supported agent)

```bash
npx skills add Trustbaselab/trustbase-skills              # all skills
npx skills add Trustbaselab/trustbase-skills@factfulness  # one skill
```

### DSH (DeepSeek Harness)

```bash
git clone https://github.com/Trustbaselab/trustbase-skills.git
cp -r trustbase-skills/industry/*  ~/.dsh/skills/
cp -r trustbase-skills/cognitive/* ~/.dsh/skills/
```

### Claude Code / Claude Desktop

```bash
/plugin marketplace add Trustbaselab/trustbase-skills
```

### Any other agent

**A skill is a directory containing `SKILL.md`. Any agent that supports the Agent Skills spec can use it directly:**
- **Spec**: [agentskills.io](https://agentskills.io)
- **Required**: `SKILL.md` (YAML frontmatter: `name` · `description`)
- **Optional**: `references/` · `scripts/` · `assets/`

---

## Skill catalog

### cognitive/ (8)

| Skill | Triggers on | Not for |
|---|---|---|
| **`factfulness`** | "Is the world getting worse" · "Is this number trustworthy" · "Cite a source for me" · "Stop fear-mongering" | Pure fact lookup with no judgment |
| **`thinking-fast-and-slow`** | "Is this AI conclusion reliable" · "That answer felt too smooth / too confident" · "Review this AI output" | Task overload (use `bandwidth-and-deep-work`) |
| **`noise-in-judgment`** | "Why does the answer change every time" · "Which conclusion should I trust" · "How do I make scoring consistent" | Single-answer computation · pure personal taste |
| **`thinking-in-systems`** | "Why does fixing it make it worse" · "The change had no effect" · "Where's the leverage point" | Individual focus problems (use `bandwidth-and-deep-work`) |
| **`bandwidth-and-deep-work`** | "Too much to do" · "Always interrupted" · "Can't focus" · "How should I prioritize" | Pure academic discussion |
| **`knowledge-illusion`** | "How do you know" · "Why are you so sure" · "Don't pretend to know" · "Explain the mechanism" | Data provenance (use `factfulness`) |
| **`trust-formation`** | "Why should anyone trust this" · "How do we prove we're credible" · "Is this source trustworthy" | Organizational management / brand marketing |
| ⭐ **`book-to-skill`** | "Turn this book into a skill" · "Make a skill about X" · "How do I package this knowledge" | Wanting plain reading notes / a book review |

### industry/ (6)

| Skill | Triggers on |
|---|---|
| **`rcb-export-compliance`** | "Can rCB be exported to the EU" · "What certification is needed" · "What happens if PAH is too high" |
| **`rcb-grade-identification`** | "What grade is this" · "Which grade does it match" · "What R-code is this rCB" |
| **`rcb-price-reference`** | "What's the rough price of rCB" · "Is this quote reasonable" · "How much cheaper than virgin" |
| **`rcb-substitution-assessment`** | "Can rCB replace N550/N330" · "What substitution ratio" · "What's the ceiling" |
| **`carbon-black-weekly`** | "Write Carbon Black Weekly" · "Chart the carbon black trend" |
| **`ai-industry-daily`** | "Tell me something about AI today" · "Compare Chinese models" |

---

## Integrity & anti-counterfeit

**⭐ Every `SKILL.md` carries a sha256; it can be cross-checked against the official page:**

```
https://trustbaselab.com/skills/
```

**Verify a download:**

```bash
sha256sum -c SHA256SUMS
```

**⚠️ Anti-counterfeit**: the only official distribution channels are **this repository** and **`https://trustbaselab.com/skills/`**.
**For any other source, check the sha256 first.**

---

## Contributing

**⭐ We ship templates and a spec:**

- [`template/BOOK-SELECTION-SCORE.md`](template/BOOK-SELECTION-SCORE.md) — book scoring rubric
- [`template/SKILL-TEMPLATE.md`](template/SKILL-TEMPLATE.md) — skill template
- [`template/EVIDENCE-TEMPLATE.md`](template/EVIDENCE-TEMPLATE.md) — evidence template
- [`template/BOOK-TO-SKILL-CHECKLIST.md`](template/BOOK-TO-SKILL-CHECKLIST.md) — delivery checklist

**⭐ Before submitting, make sure:**
1. `name` ≤64 chars, lowercase, hyphens, **equal to the directory name**
2. `description` ≤1024 chars, **with explicit trigger conditions and an out-of-scope boundary**
3. **A `references/` directory exists**
4. **⛔ No verbatim excerpts** — cite the source, write our own understanding
5. ⭐ **Every quoted idea carries a provenance status**: `verified (page)`, `secondhand`, or `from memory — pending verification`

---

## License

**Apache-2.0** — see [LICENSE](LICENSE).

**On citing book ideas**: the cognitive skills are based on the **ideas** of published books, with sources noted inside each file.
**We do not reproduce or translate excerpts of the original works.**
Our contribution is the layer that **turns ideas into executable rules for agents**.

**Engineering data** (e.g. token counts and before/after comparisons in `evidence.md`) is **Trustbase Lab project content**.

---

## Disclaimer

**Skills are provided for use at your own risk.**

**Industry skills (`industry/`) provide checking procedures and decision rules only — they contain no regulation values.**
**For actual values, retrieve them from the MCP data source and cross-check the original source.**

**This repository does not provide investment, legal, or customs-declaration advice.**

---

## Links

- **Data platform**: https://trustbaselab.com
- **MCP endpoint**: https://trustbaselab.com/mcp
- **Usage board**: https://trustbaselab.com/usage/
- **Corrections**: https://trustbaselab.com/corrections/
- **Skills page**: https://trustbaselab.com/skills/
- **Agent Skills spec**: https://agentskills.io
