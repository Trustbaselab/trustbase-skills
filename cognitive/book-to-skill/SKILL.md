---
name: book-to-skill
description: Turn a book with real intellectual substance into executable, verifiable behavioral rules for an AI agent (a skill). Seven-step SOP - score the book, read for the core claim, separate wisdom from rules, translate into if-then rules, validate in a real scenario, write SKILL.md / evidence.md / METHOD.md, then check against the delivery checklist. Ships three quality gates and four honesty boundaries, plus all templates. Use when the user says "turn this book into a skill", "make a skill about X", "how do I package this knowledge for an agent", "capture this book's wisdom", "book to skill", "how do I make this methodology executable". Not for: wanting plain reading notes or a summary, writing a book review, or knowledge organization not intended to become executable agent rules.
---

# Book to Skill: Turning a Book into Executable Behavioral Rules for an Agent

> **This is not reading notes.**
> **It is: turning a book's judgment into rules an agent can execute, and validating them in a real scenario.**

---

## When to use

- "Turn this book into a skill", "make a skill about X"
- "How do I package this knowledge so an agent can use it"
- "Capture this book's wisdom so AI can use it too"
- "book to skill", "how do I make this methodology executable"

**Not for**:
- Wanting reading notes / a summary - just summarize; no need for the full pipeline
- Writing a book review - use ordinary writing
- Knowledge organization not intended to become executable agent rules - use ordinary knowledge management

---

## Core claim (get this straight before starting)

**An AI's training objective is average - it is a compression of everything.**
**A book with a soul is one specific person, in one specific situation, making one specific judgment.**

**> So what a book gives an AI is not "knowledge" (the AI already has knowledge) - it is stance and criteria for judgment.**
**And that is exactly what AI lacks most.**

**X Therefore: not every good book is suitable for conversion.**
**Some books are excellent but cannot be translated into agent rules.**

---

## Three iron rules

### Rule 1: Score the book before starting

**Before starting you must score the book with `references/BOOK-SELECTION-SCORE.md`; only proceed if the weighted total is >= 4.0.**

| Dimension | Weight | Key question |
|---|---|---|
| **1 Has a stance** | 20% | **Who is the author arguing against?** Cannot answer -> 0 |
| **2 Translatable into if-then** | 30% | **Can it become "when X, do Y"?** All values, no rules -> 0 |
| **3 Aligned with the project's domain** | 25% | **Does it relate to the problem the project is solving?** |
| **4 Validatable** | 25% | **Can we prove it works with real data?** |

**X Red flags mean abandon**: "A brief history of X" type, pure academic monograph, self-help/motivational, strongly political, **a book written by AI**.

**Do**: fill in the scoring sheet and keep the record (avoids re-litigating later)
**Don't**: skip scoring and start writing - 90% of the subsequent time will be wasted

### Rule 2: Separate "wisdom" from "rules"

| Category | Characteristic | Handling |
|---|---|---|
| **Wisdom** | Nod while reading, forgotten after | **X Do not put it in SKILL.md** (or only in references) |
| **Rule** | **Can become "when X, do Y"** | **Must go into SKILL.md** |

**Test: can this sentence be translated into if-then?**
**No -> it is wisdom, not a rule.**

**X The most common mistake: treating "be objective", "be focused", "think systemically" as rules - these are slogans an agent cannot execute.**

**Do**: "When the user gives a single data point, find a comparison baseline first, then conclude"
**Don't**: "Look at the data objectively"

### Rule 2b: Every citation must carry a provenance status

**This is the `knowledge-illusion` rule: distinguish "remembered / verified / retrieved".**

| Status | How to write | How it may be used |
|---|---|---|
| **Verified** | "Book p.XX: ..." | **May be cited as "proposed in the book"** |
| **Secondhand** | "According to source reporting book: ..." | Label as secondhand |
| **From memory** | "Our understanding is: ... (provenance pending verification)" | **May not be presented as "the book says"** |
| **Not found** | "This skill does not adopt this argument from the book" | Discard |

**Rule:**
**X Writing "someone proposed X in book" is forbidden unless you have a page number or the original text.**
**Without it -> write "our understanding is (provenance pending verification)".**

**Why this matters most:**
**Our project is called "verifiable data".**
**If our own skills are dishonest about provenance, we do not deserve to do verifiable data.**
**And: if `evidence.md` contains unlabeled "memory passed off as fact", the entire body of evidence becomes untrustworthy.**

**Checklist at delivery:**
- [ ] Every "proposed in the book" has a page number or original text
- [ ] Everything without a page number is labeled "pending verification"
- [ ] Task documents (e.g. project material) and the skill carry consistent labels

**Do**: "Our understanding is that trust has four elements (provenance pending verification; to be filled in from the book)"
**Don't**: "Botsman proposes in Who Can You Trust? that trust has four elements" (no page number, yet written as "proposes")

### Rule 3: No validation means not done

**Every rule must have a real scenario + before/after data.**

| Not accepted | Accepted |
|---|---|
| "It should work in theory" | "We used it in project X, A -> B" |
| "It improved substantially" | "565.6KB -> 26.8KB (-95%)" |
| "Failure rate dropped to 5%" (not done) | "Failure rate 20% -> target 5% (in progress)" |

**Four honesty boundaries (write them into `evidence.md`; non-negotiable):**
1. **Data provenance** (what was measured, what was estimated)
2. **Attribution limits** - **"the change came first, the concept attribution came after; this is not a controlled experiment"**
3. **Citation phrasing** - **"a validation case in this project", not "causal proof"**
4. **Open items** - **if it is in progress, say "in progress"**

**Rule: rather omit one piece of evidence than overstate it by a millimeter.**

---

## The seven-step SOP

```
1 Score      -> references/BOOK-SELECTION-SCORE.md (>=4.0 to continue)
2 Read       -> find the core claim (who is the author arguing against, and about what)
3 Separate   -> wisdom vs rules (only what can become if-then counts as a rule)
4 Translate  -> write if-then rules + counter-examples ("what happens if you don't")
5 Validate   -> use it once in a real scenario + record before/after data
6 Write      -> SKILL.md + references/<book>-book.md + references/evidence.md + METHOD.md
7 Check      -> references/BOOK-TO-SKILL-CHECKLIST.md item by item + score (>=4.5 to deliver)
```

**Every step has a corresponding file - do not rely on memory, rely on the checklist.**

---

## Output format (deliverables)

**Every skill must produce four things:**

```
<skill-name>/
|-- SKILL.md                     <- the rules the agent reads
|-- references/
|   |-- <book>-book.md           <- the book's ideas (written by us, no verbatim excerpts)
|   `-- evidence.md              <- validation data (four-part structure + four honesty boundaries)
`-- METHOD.md                    <- the specific conversion record for this book
```

### Frontmatter hard requirements

```yaml
---
name: <kebab-case, = directory name, <=64 chars, lowercase letters/digits/hyphens only>
description: <one sentence on what it does> + <all trigger conditions> + <out-of-scope boundary> (<=1024 chars)
---
```

### SKILL.md structure

```markdown
# <Title>

## When to use
- concrete trigger 1
- concrete trigger 2
**Not for**: ...

## Core claim
<who the author is arguing against, and about what>

## Three iron rules
### Rule 1: <rule name>
<what the rule is and why it holds>
**Do**: ...
**Don't**: ...

## Output format
<short and checkable>

## References
- `references/<book>-book.md`
- `references/evidence.md`
```

### evidence.md four-part structure (every piece of evidence)

| Part | Content |
|---|---|
| **Problem** | What the situation was before the change (**must include numbers**) |
| **Which concept from the book** | Which concept was used (be specific) |
| **Concrete action** | What was done (**reproducible**) |
| **Quantified result (before -> after)** | **Must have before/after numbers** |

---

## Three quality gates

| Gate | Timing | Criterion |
|---|---|---|
| **Gate 1 - Book selection** | Before starting | **Score >= 4.0** |
| **Gate 2 - Content** | After writing SKILL.md | **Rules are if-then + have counter-examples** |
| **Gate 3 - Delivery** | Before submitting | **Checklist fully passed + score >= 4.5** |

**Failing any gate -> do not proceed to the next step.**

---

## Copyright boundary (legal risk; must comply)

| Allowed | Not allowed |
|---|---|
| Summarize ideas and write our own understanding | Quote long passages |
| Attribute: "based on the ideas of book" | Claim the ideas are our original theory |
| Publish our own written part under our license | Include the book's text / PDF |
| **Translate into agent rules** (this is the contribution) | Translate passages of the book (translation rights) |

**Every SKILL.md must end with:**
```
*Based on: <book>. We license our translation, not the original.*
```

---

## Common mistakes (record them once hit)

| # | Mistake | Consequence | Fix |
|---|---|---|---|
| **1** | `name` != directory name | CLI can't install it | Rename the directory |
| **2** | `description` has no out-of-scope boundary | False triggering | Add a "not for" section |
| **3** | Rules are slogans, not if-then | The agent does not know what to execute | Change to "when X, do Y" |
| **4** | Evidence says only "improved substantially" | Unverifiable = no value | Replace with concrete numbers |
| **5** | No "attribution limits" | Becomes a false claim | Add "this is not a controlled experiment" |
| **6** | Unfinished work written as "achieved" | Credibility collapses | Change to "in progress" |
| **7** | Long verbatim quotations | Legal risk | Rewrite in our own words |
| **8** | Missing `METHOD.md` | The next book cannot reuse it | Add it |

---

## Skills this project has already produced (this is the validation of this skill)

| # | Book | Skill | Status |
|---|---|---|---|
| **1** | *Factfulness* | `factfulness` | OK |
| **2** | *Thinking, Fast and Slow* | `thinking-fast-and-slow` | OK |
| **3** | *Noise* | `noise-in-judgment` | OK |
| **4** | *Thinking in Systems* | `thinking-in-systems` | OK |
| **5** | *Scarcity* + *Deep Work* | `bandwidth-and-deep-work` | OK |
| **6** | *The Knowledge Illusion* | `knowledge-illusion` | OK |
| **7** | *Who Can You Trust?* | `trust-formation` | OK |

**-> This is the best validation of this skill: it has already produced seven shipped skills.**

---

## References

- `references/BOOK-SELECTION-SCORE.md` - book scoring rubric
- `references/SKILL-TEMPLATE.md` - SKILL.md template
- `references/EVIDENCE-TEMPLATE.md` - evidence.md template
- `references/BOOK-TO-SKILL-CHECKLIST.md` - delivery checklist + scorecard
- `references/SKILL.zh.md` - the Chinese edition of this skill

---

*This skill practices what it preaches: it was built by its own method.*
*Trustbase Lab - Apache-2.0*
