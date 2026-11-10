---
id: E0010
type: evidence
title: "A pooled marker floor pushed output away from the operator's real register"
description: "Why the no-guidance control beat the profile 0/6 on prose: a contraction floor averaged across registers that differ tenfold forced generated announcements 2-9x above the operator's true rate, and the profile arm destroyed every hyperlink in all three documents."
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

# Finding 2 — the profile arm destroyed every hyperlink

| | control | profile |
|---|---|---|
| words | 2,751 | 2,813 |
| **hyperlinks** | **6** | **0** |
| numeric tokens | 29 | 29 |

Six of six links gone, across three documents. Also lost: an italic *Update:*
label opening the post-mortem, and a sentence telling readers where
installation and configuration happen.

Numbers survived and links did not, which points at the mechanism: the profile
arm **rewrites sentences** to meet voice targets, and markup does not survive a
rewrite while a figure embedded in a clause does. Nothing in
`voice-professional/SKILL.md` or in the profile instructs the writer to preserve
content through the rewrite, because neither was written with rewriting in mind.

**Voice transformation is a lossy operation and nothing in the shipped artifact
guards against the loss.**

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
- The craft skill needs a content-preservation rule, or voice work will keep
  silently deleting links, labels and whole sentences. This is a defect in what
  ships today.
- It explains the 0/6 without appeal to taste: for this genre the profile made
  the text *less* like the operator, by a measurable amount, on the one marker
  that differed most between the arms.
- [D0018](../decisions/D0018-a-voice-profile-states-its-claims-checkably.md)'s
  amendment said markers may not gate anything. This says more: a pooled marker
  may not be **instructed** either.
