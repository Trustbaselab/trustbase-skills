---
name: thinking-in-systems
description: A systems-thinking skill based on "Thinking in Systems" (Donella Meadows). Draw stock-and-flow diagrams and feedback loops, diagnose "why fixing it makes it worse" (watching only flows, ignoring delays, treating symptoms, eroding goals), and use the 12 leverage points to locate the level of intervention. Treat workflows and projects as systems. Use when the user says "the change had no effect", "the metric won't move", "where's the leverage point", "is this a vicious cycle", "what do we do about a systemic problem" (at the level of organization / process / metrics); also for analyzing process or organizational dynamics. For focus / task overload use bandwidth-and-deep-work.
---

# Thinking in Systems · An Operating System for Structure and Loops

**In one sentence: the behavior of a system is produced by its structure (stocks, flows, feedback loops, delays, non-linearity), not by any single element or by anyone's intent** — so when "fixing it makes it worse", the first thing to change is our understanding of the structure, not the amount of force applied.

Based on the ideas of *Thinking in Systems* (Donella H. Meadows, 2008).

## When to use

- The user describes a **recurring** problem: the harder we try the worse it gets, the change had no effect, we push one thing down and another pops up
- Analyzing the dynamics of a system / process / organization: why won't this metric move, why does it oscillate, why do the strong get stronger
- Planning an intervention: change the numbers? the rules? the goals? the paradigm?
- Diagnosing metric distortion: all the KPIs are green but the outcome is bad, or the standard has been quietly lowered
- Multiple roles pulling against each other, resource allocation frozen in place, dependence on external firefighting
- The agent needs a system-level view of a workflow, project structure, or team division of labor

**Lightweight mode**: when the only question is "is this a reinforcing or a balancing loop" or "which leverage level is this", output only "a one-sentence conclusion + the loop verdict + the leverage level"; when the user asks "why does fixing it make it worse" but wants only a first hypothesis, output the short form (3 rows of the diagnosis table + 1 verification action, see the output templates). Neither needs the full five-question pipeline.

**Not for / related**: personal focus, task overload, multitasking scheduling → use `bandwidth-and-deep-work` (that skill handles attention bandwidth; this one handles structure); wanting only the definition of a concept → read the concept dictionary in `references/thinking-in-systems-book.md`; pure historical or legal fact questions do not need a system model; **IT system failure / troubleshooting** ("the system crashed", "the system is slow") is technical troubleshooting, not structural diagnosis — just troubleshoot it, don't apply this pipeline.

---

## Three iron rules

### Rule 1: Structure produces behavior — draw the diagram first, then talk about people

A system's behavior patterns come from its structure (stocks, flows, feedback loops, delays, non-linearity), not from any individual's character or intent. Replace the person without changing the structure, and the behavior barely changes.

> Evidence anchor: Meadows Ch1 — of the three components of a system, "the least obvious part of the system, its function or purpose, is often the most crucial determinant of the system's behavior."

**Corollary: the first action when diagnosing any recurring problem is to draw the stock-and-flow and loop diagram, not to find someone to blame.**

### Rule 2: Leverage points are layered — the higher the level, the greater the leverage and the stronger the resistance

There are 12 levels of intervention (low → high): numbers/parameters → buffers → physical structure → delays → balancing loops → reinforcing loops → information flows → rules → self-organization → goals → paradigm → transcending paradigms. The higher the level, the greater the leverage, but the stronger the system's resistance; and by intuition people often push the leverage point in the **opposite** direction.

> Evidence anchor: Meadows 1999, *Leverage Points* (full text at donellameadows.org): *"The higher the leverage point, the more the system will resist changing it."* There is also the Forrester tradition that everyone is pushing the leverage points in the wrong direction (as relayed in the 1999 article).

**Corollary: before prescribing an intervention, you must report where it sits among the 12 levels and warn about the resistance at that level.**

### Rule 3: Watching flows but not stocks, ignoring delays, treating symptoms = three classic misdiagnoses

Stocks have inertia (a stock takes time to change, because flows take time to flow); a balancing loop with a delay necessarily overshoots and oscillates; applying force to a symptom without touching the structure is merely treating the symptom. These three misdiagnoses are the most common structural causes of "fixing it makes it worse".

> Evidence anchor: *"A stock takes time to change, because flows take time to flow."* (Ch1); Meadows's own estimate that "99% of system failures come from wrong or missing information" (*Dancing with Systems*; the author's personal estimate, not empirical evidence).

**Corollary: when you find "fixing it makes it worse", check these three first rather than adding a fourth kind of effort.**

---

## Step 0 · Gather information (no fabrication)

Structural diagnosis depends on real data. Before starting you must have (ask for whatever is missing; ⛔ no fabrication):

1. **Behavioral history**: a time series of the key metrics (at least several periods) — if absent, ask the user for it, or explicitly label "the following are assumed data, for illustration only"
2. **Stock inventory**: what is accumulating in the system? (inventory, debt, user count, technical debt, trust, backlog of tickets…)
3. **Flows and valves**: what is the inflow? what is the outflow? who controls the valves? by what rule?
4. **Information accessibility**: what state can each decision-maker see? what can't they see?
5. **Rules and goals**: explicit rules, incentives, penalties; whether the declared goal matches the goal implied by actual behavior

Ask for each missing item one by one; only once you have the behavioral history can you skip the "event level" and enter the "behavior level".

---

## Core workflow · the five system questions

### Q1 · Stock-and-flow diagram (the bathtub model)

| Item | Content |
|---|---|
| Stock (water level) | What is accumulating? Current level? Shape of the historical curve? |
| Inflow (the tap) | Driven by whom / what rule? Can it change suddenly? |
| Outflow (the drain) | Same. Are inflow and outflow controlled by the same decision point? |
| Inertia | How slowly does the stock respond to a change in flows? (slow response = expectations inevitably missed) |

Output one sentence: "Stock X is determined by inflow Y and outflow Z; the rate at which X can change is limited by inertia to ____."

### Q2 · Loop identification (R/B)

For each trend ask: **does A cause B, and does B also cause A?**

- **Reinforcing loop R**: the more stock, the more inflow (compounding, snowball, vicious/virtuous cycle). Annotate: "what is amplifying it? is there a balancing loop? how strong and how fast is it?"
- **Balancing loop B**: goal-seeking, pulling back toward the target (a thermostat). Annotate: "what is the target value? who set it? is the target visible?"
- **Dominance**: when several loops coexist, which dominates now? Will dominance shift as the stock level changes?

### Q3 · Delays and non-linearity

- **Delays**: perception delay (how long until it is seen), response delay (how long until a decision), delivery delay (how long until it takes effect). Whenever there is oscillation or overshoot, report the delay first.
- **Non-linearity**: are there thresholds, saturation, tipping points — "gradual cause, sudden result"?

### Q4 · Archetype matching (8 traps)

| Symptom (the user's own words) | Archetype | Loop structure |
|---|---|---|
| "Every department works hard but the result doesn't move" | Policy resistance | Multiple B loops with mutually exclusive goals |
| "Everyone uses it, nobody maintains it" | Tragedy of the commons | Private benefit + shared cost, missing feedback |
| "Let's lower the standard a bit this year and make it up next year" | Eroding goals | Standard dragged down by poor performance (R) |
| "If our competitor cuts prices we have to follow" | Escalation | Both sides' goal = beat the other (double R) |
| "Resources always flow to the same people" | Success to the successful | Redistribution by current performance (R) |
| "We can't get away from this external dependency" | Shifting the burden | Symptom relief erodes own capability (R) |
| "All metrics are met, the problem remains" | Rule beating | Surface compliance, substantive distortion |
| "All KPIs green, all users gone" | Goal displacement | The metric became the goal |

**No-hit branch**: when none of the 8 archetypes fits, do not force one — an archetype is a **candidate hypothesis**, not a diagnosis. Write a custom structural diagnosis directly from the stocks/loops/delays described in Q1–3, and state in the diagnosis card "no known archetype matched; the following is a custom loop description (pending verification against behavioral history)".

### Q5 · Leverage-point location

Place the candidate intervention among the 12 levels (12 = numbers/parameters … 1 = transcending paradigms; full list in `references/thinking-in-systems-book.md`) and report: "this intervention sits at level N; expected leverage ____; expected resistance ____; is there a lower-effort position at the same level?"

---

## The "why does fixing it make it worse" diagnosis table (the core error-hunting path)

| Phenomenon | Common misdiagnosis (treating the symptom) | Structural diagnosis | Prescription direction |
|---|---|---|---|
| The goal changed, the force increased, still no effect | Add more force, replace the executor | Only the level-12 parameters were moved, or a loop is missing | Move up to information flows / rules / goals (Q5) |
| It bounces right back after the change, or gets worse | "poor execution" | The balancing loop has a delay → overshoot; or the reinforcing loop is unconstrained | Fix the delay and the timeliness of information first (A2) |
| Each department does its job yet the whole is bad | Blame the coordinator | Sub-goals are mutually exclusive (policy resistance); subsystem optimization ≠ overall optimization | Align on a larger shared goal (B1) |
| Metrics look good, outcomes look bad | Add more metrics | Rule beating + goal displacement | Define outcomes rather than outputs; redesign the rules (B4) |
| The standard gets lower every year | "pragmatic adjustment" | Eroding goals (R loop) | Make the standard absolute; benchmark against the best historical performance (B3) |
| Growing dependence on one outside party | Renew the contract / raise the budget | Shifting the burden (R loop) | Build own capability in parallel (B5) |
| Resources always go to the winners, new things never grow | "let the capable do more" | Success to the successful (R loop) | Leveling mechanisms / caps / correction (B6) |
| A policy appears, a workaround appears the same day | Tighten the penalties | Rule beating | Redesign the rule from the regulated party's point of view (B4) |

---

## Diagnosis → prescription decision map

| Diagnostic finding | Do this first |
|---|---|
| Symptom-level effort, repeated failure | A1 move up a level: find the loop, not the parameter |
| Oscillation / overshoot | A2 quantify the delays; shorten the information delay first |
| Policy resistance across parties | B1 align on a shared higher goal; co-design |
| Eroding goals | B3 set an absolute standard; benchmark the best historical |
| Shifting the burden | B5 build capability in parallel while relieving the symptom |
| Success to the successful | B6 install leveling / caps / correction |
| Rule beating / goal displacement | B4 redefine the outcome metric and redesign the rule |
| A single point intervention proposed | C1 check the leverage level and resistance before acting |

## Prescription library

### A. Structural level (change the structure first, then the force)

1. **A1 Diagnose the loop before the parameter**: any intervention must first name the loop it acts on; a parameter change with no loop diagnosis is blind.
2. **A2 Shorten delays**: the most common cause of oscillation is a long delay in a balancing loop; shorten the perception delay (make the metric visible sooner) or the response delay (make the decision sooner).
3. **A3 Protect stocks**: stocks provide buffering and stability; running a stock to zero to optimize a flow is a classic mistake.
4. **A4 Design the feedback**: whoever makes a decision must see its consequences. Missing or delayed information is the root of most system failure.

### B. Archetype-level (treatment for the 8 traps)

1. **B1 Policy resistance**: bring the parties into a shared goal and co-design; do not defeat them one by one.
2. **B2 Tragedy of the commons**: regulate access, privatize, or provide feedback on the shared resource's state.
3. **B3 Eroding goals**: make the standard absolute; benchmark against the best historical performance; never renegotiate downward.
4. **B4 Rule beating / goal displacement**: redesign the rule from the regulated party's perspective; measure the outcome, not the output.
5. **B5 Shifting the burden**: build own capability in parallel while relieving the symptom; never let the symptomatic solution crowd out capability building.
6. **B6 Success to the successful**: leveling mechanisms, caps, corrections, or a separate track for new entrants.
7. **B7 Escalation**: unilateral disarmament or a rule that bounds the escalation.
8. **B8 Addictive dependency**: withdrawal management plus capability building; never renew the external dependency forever.

### C. Stance level (dance with the system rather than control it)

1. **C1 Report the leverage level and the resistance**: any prescription must state its level among the 12 and the expected resistance.
2. **C2 Stay humble**: a system's behavior is often non-obvious; design an experiment and let the system tell you.
3. **C3 Watch for unintended consequences**: every intervention changes incentives; predict at least one side effect.
4. **C4 Keep learning**: monitor the system after the intervention; correct early.

---

## Agent execution protocol

1. **Do not rush to prescribe**: for any "why doesn't it work" question, first ask for the behavioral history; with no data, explicitly label assumptions.
2. **Always draw the stock-and-flow**: describe the stock, the inflow, the outflow, and the inertia in one sentence before going further.
3. **Report the loop type and dominance**: R or B, and which one dominates now.
4. **Report the delays**: whenever there is oscillation, quantify the delays first.
5. **Match an archetype or declare none**: never force an archetype; state "no known archetype matched" and give a custom description.
6. **Report the leverage level**: every prescription carries its level among the 12 and the expected resistance.
7. **Distinguish technical troubleshooting**: IT failures are troubleshooting, not structural diagnosis.

## Output templates

### Diagnosis card (standard)

```markdown
**One-sentence diagnosis**: ...

| Item | Content |
|---|---|
| Stock | ... |
| Inflow / outflow | ... |
| Loop type (R/B) and dominance | ... |
| Delays | ... |
| Matched archetype | ... (or "no known archetype matched; custom description below") |
| Leverage level | level N (of 12) · expected leverage ... · expected resistance ... |

**Prescription**: ...
**One verification action**: ...
```

### Short form ("why does fixing it make it worse")

```markdown
1. The stock I am watching is ... ; the flow I am pushing is ... ; inertia means the effect will show in ... 
2. The loop responsible is ... (R/B), and it is amplified/constrained by ... 
3. The leverage level of my intended intervention is ... ; a higher-leverage option is ... 
**One verification action**: ...
```

### Custom structural description (no archetype matched)

```markdown
**No known archetype matched. Custom loop description:**
- Stock: ...
- Reinforcing path: A → B → A because ...
- Balancing path: ... with a delay of ...
- Prediction: if we do X, we expect Y within Z periods (pending verification against behavioral history)
```

## Boundaries and common misuse

| Misuse | Correction |
|---|---|
| Treating "system" as a metaphor for "complicated" | A system is a specific structure of stocks, flows, loops, and delays; if you cannot draw it, you have not diagnosed it |
| Using archetypes as conclusions | Archetypes are candidate hypotheses; they must be checked against behavioral history |
| Blaming individuals | Structure produces behavior; change the structure, not the person |
| Applying maximum force at the lowest leverage level | Parameters (level 12) have the least leverage; pushing harder there changes little |
| Ignoring delays | Delays produce overshoot and oscillation; quantify them |
| Optimizing a subsystem | Subsystem optimization can worsen the whole; check the whole system's goal |
| Using this skill for IT troubleshooting | Technical failures are troubleshooting, not structural diagnosis |
| Using this skill for focus / task overload | That is `bandwidth-and-deep-work` |

---

## Reference files (load on demand, not by default)

- `references/thinking-in-systems-book.md` — full book notes: concept dictionary, the 12 leverage points, the 8 archetypes, evidence anchors, quotations, criticism boundaries
- `references/evidence.md` — validation status of this skill's rules inside this project
- `METHOD.md` — conversion record for this book
- `references/SKILL.zh.md` — the Chinese edition of this skill

---

*Based on the ideas of "Thinking in Systems: A Primer" (Donella H. Meadows, 2008). This file is Trustbase Lab content; License: Apache-2.0.*
