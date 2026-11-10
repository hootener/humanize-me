---
id: E0010
type: evidence
title: "A pooled marker floor pushed output away from the operator's real register"
description: "Why the no-guidance control beat the profile 0/6 on prose: a contraction floor averaged across registers that differ tenfold forced generated announcements 2-9x above the operator's true rate. A second finding claimed here was wrong and is retracted below."
timestamp: "2026-11-10"
tags: [voice, markers, genre, findings, regression]
status: active
---

Diagnosis of the prose result in
[E0009](E0009-the-profile-works-on-headings-and-not-on.md), where the arm given
no style guidance at all outranked the shipped profile in **6 of 6** prose
trials. Measured on the full generated documents, not the judged excerpts.

# Finding 1 — the marker floor was harmful as an instruction

The operator's contraction rate varies almost tenfold across his own corpus,
and it tracks register rather than noise:

| piece | kind | contr/1k |
|---|---|---|
| evals-before-agents | argumentative essay | 37.7 |
| codecov-is-now-fair-source | opinion | 21.2 |
| turingpost answers | interview | 18.5 |
| impact-analysis-open-beta | short announcement | 18.3 |
| 32-hour work week | reflection | 13.5 |
| enterprise 4.5.0 release | announcement | 12.0 |
| runtime insights | announcement | 6.4 |
| introducing the new uploader | technical announcement | **4.0** |

The profile carries `contractions_per_1000w_min: 15`, a **floor** derived from
the pooled corpus mean of roughly 25/1k.

All three test pieces are technical announcements or a post-mortem, where his
own rate is **4–12**. Measured on the generated documents:

| piece | control | profile | his genre rate |
|---|---|---|---|
| granular components | 1.8 | 21.2 | ~4–12 |
| github integration | 5.9 | 38.2 | ~4–12 |
| pypi post-mortem | 1.2 | 18.0 | ~4–12 |

**The control, given no instruction, was closer to his real register rate than
the profile was.** The profile's floor forced output two to nine times above
how he actually writes this genre, and a floor cannot be satisfied by going
lower, so the instruction had no way to be right here.

This is stronger than [E0005](E0005-markers-are-genre-sensitive-and-the-checker-must.md),
which found marker ranges genre-bound and therefore prone to **false failures**.
A marker is also an instruction, and as an instruction a pooled value does not
merely fail to help — it actively moves generated text away from the target it
was derived from. A mean over a tenfold spread describes none of the registers
it averages.

# Finding 2 — RETRACTED, and inverted

**This section originally claimed the profile arm destroyed every hyperlink in
all three documents — six of six — and additionally dropped an italic *Update:*
label and a sentence of installation instructions. All three claims were wrong,
and the truth runs the other way.**

What was actually the case, checked the same day:

| claimed | measured |
|---|---|
| the profile destroyed 6 of 6 hyperlinks | **The briefs contained no URLs at all.** The control *fabricated* six — `docs.github.com/...`, `github.com/apps/codecov`, `about.codecov.io/blog/...` — none of them supplied by anything. The profile arm correctly produced none. |
| the profile lost the installation sentence | It is present: *"Installation and configuration both happen over on GitHub."* |
| the profile dropped an *Update:* label | The brief mandates *a short note with no heading above all the sections* and its content, but specifies no label. The note is present in both arms; the control added the word *Update:* in italics, which no source supplied. The framing was given; the label was invented. |

So the profile arm was **faithful to its source** and the control
**hallucinated**. Six plausible, correctly-shaped, entirely invented links in a
technical post is a serious defect, and it belonged to the arm this evidence
node was praising.

**How the error was made.** The link count came from counting `](http` in each
arm and treating the difference as deletion, without once checking whether the
briefs contained any URLs to delete. The two supporting claims came from reading
a `difflib.SequenceMatcher` sentence alignment as semantic correspondence — the
matcher paired non-corresponding sentences across the two documents, and those
pairings were read as "A has this, B dropped it".

This is the **second tool-manufactured finding in one day**, after the heading
count in [T0016](../../tasks/voice/T0016-run-the-held-out-regeneration-diff-against-a.md)
that turned out to be a parser classifying YAML as headings. Both were
confident, specific, plausible and false. The pattern is now a recurring failure
mode of this project's method: a measurement tool is written quickly, is never
checked against a case whose answer is already known, and the first thing it
produces is believed.

**What survives.** Finding 1 — the contraction floor — stands and was arrived at
differently: by measuring the operator's own corpus per piece, where the answer
was checkable against eight documents whose rates could be inspected
individually. The difference between the two findings is not care taken; it is
that one was computed against a known baseline and the other against nothing.

# A flaw in the comparison, recorded because it cuts against the result

The rendering used for the blind trials stripped bold, italic and code markup
but **not** link syntax, so the control's excerpts displayed raw
`[file a suggestion](https://…)` on screen while the profile's — having no
links left — displayed clean prose. That disadvantaged the control in the very
trials it won. The effect survives the flaw; the flaw should be fixed before the
next run.

# Consequences

- A marker expressed as a floor or a minimum is the dangerous shape, because it
  can only push in one direction. Ranges derived per register are the minimum
  fix; whether markers belong in the prompt at all is now open.
- The craft skill carries a rule covering **both** directions — invent nothing
  you were not given, and keep what you were. Only the first half is measured;
  the second is craft judgement and is stated as such. An earlier version of
  that section cited the retracted deletion finding as a measurement and had to
  be corrected in the shipped artifact.
- It explains the 0/6 without appeal to taste: for this genre the profile made
  the text *less* like the operator, by a measurable amount, on the one marker
  that differed most between the arms.
- [D0018](../decisions/D0018-a-voice-profile-states-its-claims-checkably.md)'s
  amendment said markers may not gate anything. This says more: a pooled marker
  may not be **instructed** either.

# A third writer repeated the invention, and called it preservation

A later run on the same briefs, using the corrected skill, reported that it had
**preserved** "the italic *Update:* label opening the post-mortem". The brief
contains no such label. That writer invented it exactly as the control had, and
then described the invention as fidelity.

Worth recording because it is the failure mode the corrected skill section
exists to catch, appearing in a writer that had just read the section. A
plausible, conventional, well-formed addition does not feel like an invention
from the inside — it feels like doing the job properly. "Keep what you were
given" is not self-enforcing, because the writer's sense of what it *was* given
has already absorbed what it added.
