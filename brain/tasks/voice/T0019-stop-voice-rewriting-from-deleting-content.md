---
id: T0019
type: task
title: "Stop voice rewriting from deleting content"
description: "The craft skill gains a rule that content survives the rewrite, because voice work destroyed every hyperlink in three documents and nothing told it not to."
status: Testing
category: bug
initiative: voice
blocked_by: []
spec: <optional relative link to ../../knowledge-catalog/specs/...>
timestamp: "2026-11-10"
tags: []
---

# What to build

An agent following `voice-professional` finishes a rewrite with everything it
started with: links, numbers, labels, caveats and the instructions a reader is
meant to act on.

[E0010](../../knowledge-catalog/reference/E0010-a-pooled-marker-floor-pushed-output-away-from.md)
measured the loss. A rewrite pass following this skill destroyed **six of six
hyperlinks** across three documents, dropped an italic *Update:* label and lost
a sentence telling readers where to install something, while every number
survived. The arm given no style guidance kept all six links.

Nothing in the skill or the profile said to preserve content, because neither
was written with rewriting in mind. Voice transformation is lossy and the
shipped artifact had no guard.

# Acceptance criteria

- [x] The skill states that content survives the rewrite, and names the classes
      that get lost — links, labels, standalone instructions — rather than
      saying "keep the content"
- [x] It states the tie-break explicitly: where voice and content conflict,
      content wins
- [x] The pre-send check asks whether everything is still there, and asks it
      first
- [x] The rule is craft, not profile — it names no person, per
      [D0013](../../knowledge-catalog/decisions/D0013-the-craft-ships-generic-and-the-voice-is.md)

# Out of scope

- The marker question. Whether markers belong in a generation prompt at all is
  open and bigger than this fix.
- The casual and research registers. They inherit the rule when written.

# Log

# Log

## 2026-11-10 — fixed, and one marker withdrawn alongside

`skills/voice-professional/SKILL.md` gains **Keep what you were given**, which
cites the measurement rather than asserting a principle, names the six classes
that actually get lost, and states the tie-break: *a sentence that sounds
exactly like the writer and omits where to click is worse than a flat sentence
that tells the reader where to click.* The pre-send check is now five questions
and asks "is everything still here?" first.

The mechanism is worth keeping in view: numbers survived and links did not,
because a figure sits inside a clause and is carried along when the clause is
reworded, while a link or a label is a separate object a rewrite drops without
noticing.

**Also withdrawn, outside this task's stated scope and flagged rather than done
quietly:** `contractions_per_1000w_min: 15` in the operator's profile. E0010
measured it as actively harmful — a pooled floor over a tenfold register spread
that forced announcements to 18-38/1k against the writer's real 4-12, losing to
an arm given no instruction at all. It is now annotated genre-dependent and
marked *do not instruct*, with the measurement in the comment. The number was
not replaced, because the per-register values have not been derived and
inventing one would repeat the original error in a new direction.

Leaving a known-harmful instruction in place while collecting defect reports
would have polluted the collection, which is why it was done now rather than
scheduled.

## 2026-11-10 — the premise was wrong; the fix was rewritten, not reverted

The measurement this task was built on **did not happen**. The briefs contained
no URLs, so the profile arm destroyed nothing; the control *fabricated* six
plausible links — `docs.github.com/...`, `github.com/apps/codecov`,
`about.codecov.io/blog/...` — that no source supplied. The installation sentence
the profile was said to have lost is present in its output. The *Update:* label
was never in the brief; the control invented it. All three claims are retracted
in [E0010](../../knowledge-catalog/reference/E0010-a-pooled-marker-floor-pushed-output-away-from.md).

**The shipped skill carried a false measurement for about an hour.** Its
*Keep what you were given* section opened with "This is measured, not
hypothetical" and then cited a deletion that never occurred. That is the worst
kind of error this project can make, because the whole method rests on
[D0001](../../example/knowledge-catalog/decisions/D0001-claims-must-be-checkable.md)
and a confident false claim costs a reader more than silence would.

Corrected rather than reverted, because the inverted finding is real and
sharper. The section is now **"Keep what you were given, and invent nothing"**,
and it leads with the half that *is* measured: six fabricated, correctly-shaped,
entirely invented hyperlinks in three technical posts. Plausible links are
trivial to generate and among the worst things to be wrong about, because a
reader clicks them. The preservation half remains as craft judgement and is
labelled as judgement, not as measurement.

The pre-send check now asks whether everything is still there **and nothing
more**.
