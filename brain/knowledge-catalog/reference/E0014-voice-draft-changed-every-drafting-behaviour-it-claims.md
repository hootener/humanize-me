---
id: E0014
type: evidence
title: "voice-draft changed every drafting behaviour it claims to, against a control that was better than predicted"
description: "Two fresh agents, one corpus, pre-registered rubric: the control turned its own measurements into targets and recorded no provenance, while the skilled arm passed all seven mechanical checks — but the test cannot separate the skill from careful instruction in general."
timestamp: "2026-11-11"
tags: [voice, profile, skills, experiment, findings, method]
status: active
---

The first test of
[D0029](../decisions/D0029-the-profile-file-format-is-a-contract-with.md)'s
claim that a drafting agent not told about
[E0010](E0010-a-pooled-marker-floor-pushed-output-away-from.md) will write
markers as floors.

# Design

Same corpus to both arms: five published pieces, 6,469 words, one author,
spanning a technical announcement, an argumentative essay and an interview —
the genre range that produces this writer's real 4.0 to 37.7 contraction
spread. Both arms were fresh agents barred from `~/.claude/voice/profile/`
(where a profile for the same person already exists), from `brain/`, and from
the web.

- **Control**: "build a voice profile from this corpus", no further guidance.
- **Treatment**: identical, plus `voice-draft`.

**The rubric, the prediction and the scoring script were written to disk before
either arm ran.** The prediction recorded in advance was that treatment would
pass P1–P3 and control would fail P1 and P2.

# Result

| check | control | treatment |
|---|---|---|
| P1 markers as observed ranges, not floors or targets | **fail** | pass |
| P2 derived per register, not pooled | **partial** | pass |
| P3 denominator and date recorded | **fail** | pass |
| S1 specific `gaps:` | **fail** | pass |
| S2 observed-not-reproduced section | **fail** | pass |
| S3 moves carry rates | partial | pass |
| S4 markers labelled diagnostic | **fail** | pass |
| frontmatter contract the voice skills can load | **none** | complete |

**The control was better than predicted.** It measured rather than guessed —
sentence-length distribution, dash and colon rates, the length of every
paragraph-final sentence — quoted the corpus for every rule, and found the
two-register split on its own: 36 contractions per thousand words in the essays
against 4 in the product documentation. That split is the thing E0010 is about,
and it was discovered without being told to look. So **"derive per register,
never pool" does not describe a failure every competent agent makes**, and the
pre-registered partial null is recorded as such.

**It then did the exact thing the skill exists to prevent.** Its section is
titled `## 2. Measured targets`, under a column headed **Target**, and the
contraction row reads:

> `| Contractions | ~23 per 1,000 words | essay register: 36/1k. Use them everywhere |`

Having measured 36 and 4, it published a pooled target of ~23 — a figure that
describes neither genre — and instructed the writing agent to use contractions
everywhere. The split survives as a note; the pooled target is what an agent
reading at write time would try to hit. This is E0010 reproduced from scratch by
an agent that had the right measurement in hand.

The control also recorded no measurement date, no `gaps:`, nothing marked as
observed-but-not-to-be-copied, and **no frontmatter at all**, so none of the
three voice skills could load it as a contract.

The treatment arm wrote 22 bracketed ranges with per-file evidence in comments,
split the corpus into two sub-modes rather than averaging them, put the
product-documentation register under "Observed, and deliberately not reproduced"
as house style rather than voice, counted all 20 of the corpus's real headings
as a population, carried no `never` because the corpus is edited-only, and set

> `verified: Nothing. This is a fresh draft and no generated output has been
> checked against this person's judgement.`

Two apparent floor phrasings in the treatment arm were false positives of the
scorer — "not a target" and a move rate of "at least once per piece" — caught
because the script prints the matching lines rather than only a count.

# What this does not show

**It cannot separate the skill from careful instruction in general.** The
treatment arm was told to follow a skill; the control was told nothing. Some of
the gap is plausibly "an agent given detailed instructions follows them". A
control given generic rigour guidance — *measure carefully, record provenance,
state what you are unsure of* — would isolate the specific content. That control
was not run and should be.

**It does not show the resulting profile produces better prose.** This measures
drafting behaviour only. Whether a `voice-draft` profile beats a hand-built one
at the thing profiles are for needs generated passages and a harvest.

**n = 1.** One corpus, one register, one pair of agents, one run.

**The same person wrote the skill, the rubric and the scorer.** Pre-registration
limits the experimenter's freedom here; it does not remove it.

# Citations

- `draft-test/RUBRIC.md` — rubric, prediction and null condition, written before either arm ran
- `draft-test/score.py` — scorer, written before any output existed
- `draft-test/control-profile.md` (1,799 w), `draft-test/treatment-profile.md` (1,592 w)
- [E0010](E0010-a-pooled-marker-floor-pushed-output-away-from.md) — the harm this tests for
