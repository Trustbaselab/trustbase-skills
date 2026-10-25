# CBAM timeline phases and the language to use in each

> This reference belongs to the `carbon-cbam-cost-calc` skill.
> **It contains no dates on purpose.** All dates are fetched at runtime from
> `get_cbam_timeline` and must be cited with their record id, confidence and `as_of`.
>
> Reason: the CBAM implementation schedule has been revised more than once.
> A date remembered from training data is worse than no date at all.

---

## 1. The five phases to establish

When a user asks "when does this start" or "what do I need to do now",
establish which phase their shipment falls into. The phase determines the
obligation, and the obligations are completely different:

| Phase | What happens | What the importer must do | What it means for a supplier |
|---|---|---|---|
| **Founding** | The regulation is adopted | Nothing yet | Nothing yet |
| **Transitional** | Reporting only | Quarterly embedded-emissions report | May be asked to provide data by the importer |
| **Definitive, pre-certificate-sale** | Reporting continues, certificates not yet purchasable | Continue reporting | Data requests intensify; no payment yet |
| **Certificate sales open** | Certificates become purchasable | Buy certificates covering embedded emissions | Pricing pressure enters the conversation |
| **Annual surrender** | First full annual cycle | Surrender certificates, submit verified declaration | Embedded emissions become a priced input |

**Do not compress this into "CBAM starts in year X".** The phase matters more than the date.

---

## 2. The three date types that are routinely confused

| Date type | What it marks | Common mistake |
|---|---|---|
| **Entry into force** | The regulation legally exists | Being reported as "when payment starts" |
| **Definitive period start** | Reporting obligations become financial obligations | Being reported as "when certificates must be bought" |
| **Certificate sales start** | Certificates can first be purchased | Being reported as "when the first report is due" |
| **First surrender deadline** | First full annual cycle closes | Being reported as "when CBAM starts" |

**These are four different dates.** Users conflate them constantly, and the
conflated answer is what ends up in a board pack.

**Rule: when the user asks "when does CBAM start", ask which of the four
they mean, or give all four with their labels.**

---

## 3. Language to use in each phase

### Transitional period

```
Use: "You have a reporting obligation, not a payment obligation."
Avoid: "CBAM is in effect" (technically true, practically misleading)
```

### Definitive period, pre-certificate-sale

```
Use: "The financial obligation is now defined, but the certificates
      are not yet purchasable. This is the window to get your
      embedded-emissions data verified, not to budget the payment."
Avoid: "You owe CBAM now."
```

### After certificate sales open

```
Use: "Certificates can now be purchased. The cost depends on the
      carbon price at surrender, which is not the price today."
Avoid quoting today's price as "the CBAM cost".
```

---

## 4. The free-allocation question

CBAM's financial impact is not simply "embedded emissions × carbon price",
because the EU ETS free allocation to domestic producers is being phased out
on a schedule, and CBAM is calibrated against that phase-out.

**Practical consequence:** the effective CBAM cost rises over time even if
the carbon price and the embedded emissions stay flat.

**What to tell the user:**

```
The cost is not constant. It rises as free allocation is phased out.
Fetch the current phase from get_cbam_timeline; do not compute the
phase-out trajectory from memory.
```

---

## 5. What this skill will not do

```
❌ Predict future CBAM scope extensions.
   The scope is defined by Annex I and amended by regulation. Any extension
   is a legislative event, not a forecast. Say "the scope may be extended;
   the current list is what applies as of <as_of>".

❌ Give a definitive embedded-emissions value for a specific installation.
   That requires on-site verification under the implementing regulation.

❌ State the free-allocation percentage for a specific year from memory.
   Fetch it, or say it is not covered.
```
