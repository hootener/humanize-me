---
id: E0015
type: evidence
title: "Classical readability formulas rank agent prose above the human writing it is trying to sound like"
description: "Flesch Reading Ease scores the operator's published prose 45.0 and 34.7 against 54-59 for agent output; shipping against the formula would optimise away from the target, and the no-guidance control scores best of all."
timestamp: "2026-11-12"
tags: [readability, metrics, measurement, findings, method]
status: active
---

Measured before adopting reader burden as the project's shipping metric,
because the obvious way to measure "readability" is a classical formula and
those formulas had not been checked against this corpus.

# Result

Flesch Reading Ease — higher is nominally easier. Flesch-Kincaid grade — lower
is nominally easier. Headings, lists, tables, code spans and URLs stripped.

| text | words | words/sentence | FRE | grade |
|---|---|---|---|---|
| **His published prose**, train set | 6,421 | 19.3 | **45.0** | 11.8 |
| **His published prose**, held out | 3,059 | 25.3 | **34.7** | 14.7 |
| Agent passages, with profile and craft | 809 | 20.7 | 58.6 | 10.2 |
| Agent document, no guidance at all | 763 | 14.7 | 54.1 | 9.4 |
| Agent document, written with `voice-draft` | 1,060 | 14.3 | 56.7 | **8.9** |

**Every agent text scores more readable than every human text**, by 10 to 24
FRE points. The target of the whole project is the worst-scoring row in the
table. The best-scoring row is a document written with no guidance at all.

# Why this happens

Both formulas are driven by words per sentence and syllables per word. Short
clipped sentences and short words score well. The README's own defect list says
agent prose "comes out short and clipped" — so the formulas are rewarding the
exact failure mode the project exists to correct.

A metric that moves the wrong way when the defect is present is not a weak
metric. It is an inverted one.

# This is the same finding as E0010, in a second domain

[E0010](E0010-a-pooled-marker-floor-pushed-output-away-from.md) found that a
marker written as a target pushed output away from the writer, and that an arm
given no guidance landed closer to him than the profile did. The same shape
appears here: a number that is informative as a description becomes harmful as
an objective, and the unguided arm wins on the number.

Twice now, in unrelated measurements, and it is the reason
`markers: # diagnostics, not a gate and not a target` is in every profile
`voice-draft` writes.

# Limits

**Genre is confounded.** The two agent documents are reference files with
tables; his texts are essays and announcements. The cleanest comparison is the
generated passages against his prose, same register, and that gap is still 14
to 24 FRE points in the same direction.

**Syllable counting is heuristic** — a vowel-group count with one silent-`e`
correction, not a dictionary. It is applied identically to every row, so it
biases the absolute numbers rather than the ordering.

**Formulas were never validated for this.** Flesch-Kincaid was fitted to US
Navy training manuals and predicts decoding difficulty for a reader learning to
read. It was never evidence about whether experienced adults find prose
tiring, which is the claim this project actually makes.

# Citations

- `flesch.py` and the corpus it ran over, session scratchpad, 2026-11-12
- [E0010](E0010-a-pooled-marker-floor-pushed-output-away-from.md) — the same finding in the marker domain
- [E0014](E0014-voice-draft-changed-every-drafting-behaviour-it-claims.md) — source of the two agent documents
