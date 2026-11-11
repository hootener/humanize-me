---
id: T0023
type: task
title: "Build the precise register profile"
description: "The third register, built from a split corpus — voice from a public incident post-mortem, evidence discipline from peer-reviewed papers, academic house style recorded and discarded."
status: Testing
category: enhancement
initiative: voice
blocked_by: []
spec: ../../knowledge-catalog/specs/S0001-the-voice-workshop.md
timestamp: "2026-11-10"
tags: []
---

# What to build

A precise voice profile for the operator — the third register, and the one
[D0014](../../knowledge-catalog/decisions/D0014-registers-are-organized-by-burden-of-proof-not.md)
as amended renamed from `research` because the old name made people picture a
paper.

# Acceptance criteria

- [x] A corpus whose authorship is proven at the level it was actually written
- [x] A profile whose markers were measured rather than reasoned
- [x] House style separated from voice, with the evidence for the separation
- [x] A `gaps:` field stating what the corpus does not cover
- [ ] A harvest run against it

# Out of scope

- The `voice-precise` craft skill, which now exists and is generic per
  [D0027](../../knowledge-catalog/decisions/D0027-three-generic-voice-skills-ship-and-nothing-personal.md).
  This task builds the operator's personal profile, not the shipped skill.

# Log

# Log

## 2026-11-11 — built on a split corpus, because the obvious corpus was wrong

The operator offered peer-reviewed publications — 17 of them, 15 where he is
first or second author. Academic writing is the obvious precise corpus and it
turned out to be the wrong one.

**Measured, his academic prose is not his voice.** Across three papers: first
person 0–5.8 per thousand words, passive construction 11.6–12.7, contractions
1.4–5.1. His own public incident post-mortem — same register, same demand for
evidence, no reviewers — runs **first person 58.7, passive 2.3**. Thirty-five
times the first person and a fifth of the passive, same writer, same warrant.

That is [E0012](../../knowledge-catalog/reference/E0012-unedited-professional-writing-contradicts-three-absolutes-in-the.md)
at maximum strength. Peer review, co-authors and a journal style guide are the
most gatekeeping any of his writing has passed through, and what survives
describes the venue.

**So the profile is split.** Voice from the post-mortem: first person
throughout, active, naming error with the strongest accurate word — *"we
egregiously mishandled"*, *"we tricked ourselves"*. Evidence discipline from the
papers, where it is genuinely strongest: the parenthesis carries the precision
at 13–20 per thousand words, the highest rate of any register he writes in, and
quantities arrive with units and conditions. Academic convention is recorded
with its numbers and marked **observed, not reproduced**, per
[D0025](../../knowledge-catalog/decisions/D0025-output-is-always-correctly-spelled-punctuated-and-capitalised.md).

**Two gathering rules came out of this and are now in `/voice-gather`.**

*Ask which sections they wrote.* He identified about 3,000 words inside a
9,000-word paper where he is third author — a source a byline check alone would
have discarded whole. Only the author can answer that.

*Watch for house style masquerading as voice.* The more gatekept a source, the
less of the author survives in it, and the measurement above is the worked case.

**Thin, and said so.** One post-mortem is the entire voice sample. The everyday
precise writing someone would actually ask an agent for — an internal analysis,
a data memo, an RFC — is absent and recorded as unknown rather than covered.

# Log — 2026-11-11, the harvest

Six passages, eleven rules, two clean. The full result is
[E0013](../../knowledge-catalog/reference/E0013-the-precise-harvest-produced-the-lowest-defect-rate.md);
what follows is what changed in the profile.

The profile went from 1,142 to 1,863 words. Nine of the eleven rules were added
to it. Two of them changed sections that were already there.

**The split was drawn on the wrong axis.** The profile above says write like the
post-mortem and take only evidence discipline from the papers, because
reproducing academic register would produce a journal submission. The second
half of that is right. The first half was too broad: he rewrote a generated
first-person line into an impersonal one and called it "a more professional
precise way to say it". The split is now by what the sentence is doing — first
person for owning an error or a judgment, impersonal for a finding that
generalises — and the papers are the right model for one of those two jobs
rather than for none.

**Two professional moves are effectively `never` here.** The balanced antithesis
and the short aphoristic landing, both rejected as "too flowery" in the same
passage. The short landing has three confirmations in professional. A rule can
survive a register change while its rate does not, which
[D0026](../../knowledge-catalog/decisions/D0026-every-move-in-a-profile-carries-a-frequency.md)
did not allow for;
[D0028](../../knowledge-catalog/decisions/D0028-a-move-s-rate-is-set-per-register-not.md)
now does.

**A new section on order of argument**, holding three of the eleven rules —
method and controls before results, define the term before the finding,
enumerate in parallel before judging. This register's defects are mostly
sequence rather than wording, which none of the previous three harvests showed.

**"Meaning" marks the inference.** The profile already said to distinguish
measured from inferred and gave no construction for doing it. His is *"208 of
those comments were from 2026, meaning they were written by coding agents"* —
number, then what you take it to mean, with the joint visible.

The frontmatter's `verified` line now records the harvest. It still records no
held-out set and no blind trial, both of which remain true.
