---
id: E0016
type: evidence
title: "No automated proxy earned screening status, and pooling both hid a signal and manufactured one"
description: "Nine metrics against 18 already-judged passages: the pre-registered bar was not met by any of them, repetition was the only consistent lead, the readability formulas flipped sign between registers, and the single significant pooled result was a register artifact."
timestamp: "2026-11-12"
tags: [readability, metrics, measurement, findings, method, negative-result]
status: active
---

Run to answer one question from
[D0031](../decisions/D0031-the-shipping-metric-is-reader-burden-measured-as.md):
on passages a person has already judged, does any automated metric track the
number of defects he named? A metric that did would be a cheap screen with
evidence behind it.

**It did not. The pre-registered bar was not met by any metric**, and this is
recorded as the negative result the pre-registration said it would be.

# Design

18 generated passages, 2,420 words, with per-passage defect counts from three
harvests already run: precise (0,3,3,3,2,0), casual round 1 (6,5,5,5,4,3),
casual round 2 (3,5,4,5,4,4). Outcome: defects per 100 words. Statistic:
Spearman rho, reported per harvest and pooled.

**The bar, the metrics and three predictions were written to disk before a
single metric was computed.** The bar: `|rho| >= 0.5 in a consistent direction
across all three harvests`.

# Result

| metric | precise | casual r1 | casual r2 | pooled | p (pooled) |
|---|---|---|---|---|---|
| `repeated_4grams` | +0.45 | +0.60 | +0.85 | +0.39 | 0.113 |
| `syllables_per_word` | −0.17 | −0.17 | −0.14 | **−0.54** | **0.021** |
| `words_per_sentence` | −0.72 | +0.47 | −0.20 | +0.37 | 0.133 |
| `flesch_reading_ease` | +0.17 | −0.41 | +0.31 | −0.27 | 0.269 |
| `mean_paragraph_words` | −0.32 | −0.36 | −0.38 | −0.34 | 0.163 |
| `type_token_ratio` | +0.26 | 0.00 | −0.37 | +0.36 | 0.138 |
| `repeated_sentence_openings` | +0.40 | n/a | n/a | −0.16 | 0.667 |

p from a 200,000-shuffle permutation test. **At n = 6, two-tailed p < 0.05
needs |rho| >= 0.886**, so no within-harvest number here is significant,
including the 0.85.

# Predictions, scored

1. *Flesch shows |rho| < 0.4 pooled.* **Correct** — −0.27.
2. *Repetition metrics show rho > 0.4 pooled.* **Wrong.** `repeated_4grams`
   reached 0.39, just under, and `repeated_sentence_openings` was −0.16.
3. *Bare demonstratives show rho > 0.3.* **Wrong** — −0.30, the wrong sign,
   and undefined in both casual harvests.

One of three. Pre-registration earned its place again.

# The formulas are not merely useless here — they are unstable

`flesch_reading_ease` correlates +0.17, −0.41 and +0.31 across the three
harvests. `words_per_sentence` runs −0.72, +0.47, −0.20. These are not weak
relationships, they are **relationships that point in opposite directions
depending on the register**. [E0015](E0015-classical-readability-formulas-rank-agent-prose-above-the.md)
showed the formulas rank agent prose above human prose; this adds that their
direction is not even fixed within this project's own output.

# Pooling hid one signal and manufactured another, in the same dataset

This is the finding worth keeping.

**`repeated_4grams` was deflated by pooling.** Within each harvest it is +0.45,
+0.60, +0.85 — every value above the pooled 0.39, all three the same sign, and
strengthening. Pooling three registers dragged the best candidate below its own
worst subgroup.

**`syllables_per_word` was inflated by pooling.** Within each harvest it is
−0.17, −0.17, −0.14, which is nothing. Pooled it is −0.54 at p = 0.021, the
only nominally significant result in the table. The correlation lives entirely
*between* harvests: precise passages have longer words and fewer defects than
casual ones. It is a register difference wearing a correlation's clothes, and
it would not survive correcting for the seven metrics tested
(Bonferroni: 0.05/7 = 0.007).

A reader given only the pooled column would discard the one real lead and adopt
the one artifact. That is the third time this project has been bitten by
pooling across registers, after
[E0010](E0010-a-pooled-marker-floor-pushed-output-away-from.md) and
[D0028](../decisions/D0028-a-move-s-rate-is-set-per-register-not.md).

# What follows

- **D0031 is unchanged.** No automated metric is good enough to screen with.
  Every one of them stays a guard-rail reported beside a result, never an
  objective.
- **Repetition is the one lead worth a powered run.** Consistent sign across
  three independent harvests, rising each time, and it is the metric that moves
  the *right* way where the formulas move backwards. It needs roughly 30
  passages per register to be testable rather than suggestive.
- **Report metrics per register, never pooled**, and this table is the standing
  demonstration of why.

# Limits

n = 18, and n = 6 within each harvest; nothing here is significant and the
within-harvest rho values are the weakest kind of evidence. Defect counts
reflect how much one judge chose to say on a given day, and the profile
improved between casual rounds, so the outcome variable is not clean. One
judge, one writer, passages of 120-180 words where every metric is noisy.

# Citations

- `proxy-cal/PREREGISTRATION.md` — bar, metrics and predictions, written before any was computed
- `proxy-cal/calibrate.py`, `proxy-cal/metrics.json` — the run and its per-passage output
- `compare/PRECISE-FEEDBACK.json`, `CASUAL-FEEDBACK.json`, `CASUAL-FEEDBACK-2.json` — the judged defects
- [E0015](E0015-classical-readability-formulas-rank-agent-prose-above-the.md) — the formulas on this corpus
