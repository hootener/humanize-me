---
id: E0005
type: evidence
title: "Markers are genre-sensitive and the checker must read paragraph prose"
description: "Measurements from building the first real profile and applying it to two client documents: the marker scheme needs a genre scope and a defined text population, and first-person ownership did more than every marker combined."
timestamp: "2026-11-09"
tags: [voice, profile, markers, verification, findings]
status: active
---

Findings from the first end-to-end run of the design: a professional profile
built from seven published pieces by the operator, then applied to two
client-facing feature walkthroughs in an unrelated project.

Numbers below are measured, not estimated. The corpus was 8,771 prose words:
5 training samples (5,685 words) and 2 held out (2,302 words), per
[D0018](../decisions/D0018-a-voice-profile-states-its-claims-checkably.md).

# The checker has to define its text population

The first marker run on the rewritten paperwork document reported a median
sentence of 12.0 words against a profile range of 15–22, and a short-sentence
share of 38% against a 15% floor. Both were partly artefacts: the measurement
swept up figure captions, UI labels and headings as "sentences". "Paperwork is
the new entry." is a caption, not prose.

Re-measuring over paragraph-length blocks only — matching how the profile's own
markers were derived — moved the median to 12.5. So the artefact was real but
small, and the failure survived it.

**A marker is meaningless without a stated population.** The profile's ranges
were computed over paragraph prose; a checker that measures all visible text
will fail documents that are merely caption-heavy. This has to be part of the
marker format, not a convention in whoever writes the checker.

# Markers are genre-sensitive, and the profile knows it

Final measurements, same profile, same markers, two documents:

| | paperwork | map |
|---|---|---|
| prose words | 639 | 906 |
| sentence median (target 15–22) | **13 — fail** | 17 — pass |
| short share (floor 0.15) | 0.33 | 0.21 |
| semicolons /1k (max 0.2) | 0.0 | 0.0 |
| exclamations /1k (max 0.0) | 0.0 | 0.0 |
| parentheticals /1k (2–6) | 4.69 | 2.21 |
| contractions /1k (min 15) | 34.4 | 21.0 |

Seven of eight pass on the paperwork document and eight of eight on the map.
The single failure is the sentence median, and it tracks genre rather than
voice: the paperwork document is mostly numbered UI instructions, which are
intrinsically short, while the map document carries more argument.

The fix was available and was **declined**. Reaching 15 would have meant
padding instructions with subordinate clauses — a better number and a worse
document, which is the exact failure
[E0004](E0004-what-the-professional-craft-skill-could-not-say.md) predicted
when it found the countable half of a profile to be the minority of its value.

The profile already carries the explanation in its own `gaps:` field: every
source was a published blog post or interview, so there is no instructional or
correspondence writing in the corpus at all. **A marker range inherits the
genre of the corpus it was measured on**, and the format needs somewhere to say
so — either a genre scope per marker, or a marker set per genre.

# What actually changed the documents

Ranked by effect on the prose, not by measurability:

1. **First-person ownership.** Both originals contained zero instances of "I".
   Every judgment was unattributed — "Those are the next steps", "it can be
   turned off". The rewrites own them: "I set the consent date two weeks out on
   purpose", "It's the piece I'm least sure about". This is the largest change
   and no marker measures it.
2. **Specific limitations.** The paperwork original admitted "Those are the
   next steps" and nothing more. The rewrite says what you will and will not
   know, and adds a third limitation the original omitted entirely: nothing
   reads the uploaded document, so a stale W-9 sends as cheerfully as a current
   one. The map original was already strong here — "in one measured case by
   about seven miles" is the operator's own voice arriving unassisted.
3. **Contractions.** 0 before, 34.4 and 21.0 per 1,000 words after. Mechanical,
   measurable, and the single cheapest change.
4. **Closing on a position.** Both originals ended on "Reply to the email this
   came with". Both now end on what the operator most wants back from the
   review, and why.
5. **Semicolons removed.** Three in the map document, none in the corpus.

Items 3 and 5 are countable. Items 1, 2 and 4 are not, and they are the ones a
reader would notice.

# Corpus gaps worth recording

- **Two of nine sources were unreachable.** Both Medium posts returned 403 to
  every fetch attempt. They were the operator's laid-back-audience pieces, so
  the loss falls on the casual register rather than this one — but it means a
  corpus cannot be assumed fetchable, and the generator will need a path for
  writing the operator supplies directly.
- **Dash style is unsettled in the corpus itself.** The 2026 post uses `--`
  31 times and the em-dash never; the 2024 post inverts it exactly. Recorded in
  the profile as unstable rather than asserted as a habit. A generator reading
  this corpus naively would have produced a confident false marker.
- **The corpus skews old on bullets.** The 2021 sample is 50% bullet lines at a
  23-word median; the 2024 and 2026 samples run 15–16 words with far fewer.
  The profile weights recent work and says so, which is a judgment a script
  would not have made.

# Not yet done

The held-out regeneration diff has not run. Two samples (2,302 words) were
reserved for it and remain unread by the profile. Until it runs, this profile
is verified by markers only, and its own `verified:` field says exactly that.

# Citations

- `~/.claude/voice/profile/professional.md`, built 2026-11-09
- `smart-labor-management/brain/plans/subcontractor-paperwork/handoff.html` and
  `smart-labor-management/brain/plans/subcontractors/map-handoff.html`,
  rewritten 2026-11-09; originals preserved as `.bak` beside each, that project
  being outside version control
- [T0015](../../tasks/voice/T0015-build-the-professional-profile-from-real-samples-and.md)
