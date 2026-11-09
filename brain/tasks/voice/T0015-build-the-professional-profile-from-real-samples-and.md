---
id: T0015
type: task
title: "Build the professional profile from real samples and apply it"
description: "The operator's own professional voice profile, built from published writing and applied to two live client documents, as the first end-to-end exercise of the design."
status: Testing
category: enhancement
initiative: voice
blocked_by: []
timestamp: "2026-11-09"
tags: [voice, profile, dogfood]
---

# What to build

A professional voice profile for the operator, at user scope, built from their
own published writing — and then used on real documents so the profile-reading
path is exercised rather than asserted.

This is the dogfood [D0012](../../knowledge-catalog/decisions/D0012-make-it-adoptable-first-then-dogfood-it-as.md)
asked for, one step early: it runs without the generator, because
[D0019](../../knowledge-catalog/decisions/D0019-humanize-me-ships-as-a-claude-code-plugin.md)
resolves a profile from a file and does not care whether a script or a person
wrote it. Hand-writing the first one is also the only way to find out what the
format needs, which is what the format spec is waiting on.

# Acceptance criteria

- [x] A corpus is gathered from the operator's published writing, with each
      sample's register declared rather than inferred
- [x] Samples are held back from the build, and the profile records which,
      per [D0018](../../knowledge-catalog/decisions/D0018-a-voice-profile-states-its-claims-checkably.md)
- [x] `~/.claude/voice/profile/professional.md` exists with machine-readable
      markers and prose sections, and its `verified:` field states honestly
      what has and has not been checked
- [x] The profile asserts no marker that the corpus contradicts, and records
      what the corpus leaves unsettled
- [x] The profile is applied to at least one real document, and the result is
      measured against the markers
- [x] The findings are written down as evidence, including the failures

# Out of scope

- The generator. This profile is hand-written on purpose.
- The casual and research profiles. The two laid-back samples the operator
  offered were unreachable, so the casual corpus is short two pieces.
- The held-out regeneration diff. Reserved samples exist and the check has not
  run; see [E0005](../../knowledge-catalog/reference/E0005-markers-are-genre-sensitive-and-the-checker-must.md).

# Log

## 2026-11-09 — built and applied

**Corpus.** Nine sources offered, seven fetched. 8,771 prose words after
stripping site chrome: 5 training samples (5,685 words) and 2 held out
(2,302 words). The two Medium posts returned 403 to every attempt, including
through a second fetcher. One source was an interview, so only the operator's
answers were taken — the interviewer's questions and the publication's section
headings were excluded by hand, line by line.

**Profile.** `~/.claude/voice/profile/professional.md`, 1,300 words. Eight
countable markers in frontmatter, then prose for the moves, the hedging level
(per [D0020](../../knowledge-catalog/decisions/D0020-craft-governs-ownership-and-falsifiability-a-profile-governs.md)),
how a judgment gets owned, diction, measured absences, and an explicitly
*unstable* section for what the corpus contradicts itself on.

The hedging entry is the one [D0020](../../knowledge-catalog/decisions/D0020-craft-governs-ownership-and-falsifiability-a-profile-governs.md)
made necessary, and the corpus had a clear answer: this writer hedges by
narrowing scope, not by softening verbs. Modal mush is nearly absent;
"Generally speaking", "for our purposes" and "maybe a third of the time" are
everywhere. A craft rule that counted hedges would have stripped exactly the
hedges that carry the information.

**Applied** to two client-facing walkthroughs in `smart-labor-management`. The
map document passes 8 of 8 markers; the paperwork document passes 7 of 8.

**The one failure is recorded, not fixed.** Sentence median 13 against a 15–22
range, because that document is mostly numbered UI instructions and the profile
was measured on blog prose. Reaching 15 meant padding instructions with
subordinate clauses. Declined, and written up as
[E0005](../../knowledge-catalog/reference/E0005-markers-are-genre-sensitive-and-the-checker-must.md).

**That project is not under version control.** Checked before cleaning up, so
the `.bak` files beside each document are the only copies of the originals and
were deliberately left in place.

## 2026-11-09 — what this hands to the format spec

Three requirements the format does not currently have, all from
[E0005](../../knowledge-catalog/reference/E0005-markers-are-genre-sensitive-and-the-checker-must.md):

- a marker needs a **text population** (paragraph prose, not all visible text),
  or caption-heavy documents fail spuriously
- a marker needs a **genre scope**, because a range inherits the genre of the
  corpus it was measured on
- a profile needs an **unstable** section, for habits the corpus contradicts
  itself on — asserting one would have produced a confident false marker

## 2026-11-09 — operator review: rejected, and why

Shown both documents in a browser beside their originals, the operator rejected
the result: *"i think it sounds like you doing an impression of me."*

The map document had passed 8 of 8 markers. That is the finding
([E0006](../../knowledge-catalog/reference/E0006-the-operator-rejected-a-profile-that-passed-every.md)):
a full marker pass is not evidence that a profile works.

Two causes, neither measurable:

- **Headings were never a measured population.** The profile described paragraph
  moves and nothing else, so paragraph moves were applied to a heading. The
  corpus had the answer all along — the operator's headings take three plain
  shapes and never withhold their subject, and their proposed fix "Why we built
  a map" nearly matches "Why did Codecov build Impact Analysis?" already in the
  training set. Now [D0021](../../knowledge-catalog/decisions/D0021-a-profile-is-derived-per-text-population-not.md).
- **Landing sentences coined instead of compressed.** The profile named the
  rhythm correctly and reproduced it wrongly: four inventions arrived at the
  landing position carrying claims the paragraphs had not made. The rule is now
  "compress, never coin".

Fixed in the profile and in both documents. Both still pass their markers, the
map at 8 of 8 and the paperwork at 7 of 8 on the genre-bound median.

This is the evidence that moves the held-out regeneration diff from nice-to-have
to the next thing worth doing: it is the only check in the design that could
have caught either cause, and it still has not run.
