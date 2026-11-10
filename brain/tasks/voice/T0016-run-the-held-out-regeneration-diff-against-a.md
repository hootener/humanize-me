---
id: T0016
type: task
title: "Run the held-out regeneration diff against a pristine test set"
description: "Regenerate pieces the operator already wrote, from content-only briefs, and compare against the real thing — the only check in the design that could have caught the failure in E0006."
status: In Progress
category: enhancement
initiative: voice
blocked_by: []
timestamp: "2026-11-10"
tags: [voice, verification, experiment]
---

# What to build

A blind comparison that answers one question: does the profile make generated
prose more like the operator's, less like it, or neither?

[D0018](../../knowledge-catalog/decisions/D0018-a-voice-profile-states-its-claims-checkably.md)
designed this check and it has never run.
[E0006](../../knowledge-catalog/reference/E0006-the-operator-rejected-a-profile-that-passed-every.md)
established that markers pass while the operator rejects, and
[E0007](../../knowledge-catalog/reference/E0007-state-of-the-art-for-reproducing-a-specific.md)
found that no published metric predicts an author's own verdict better than
r = 0.244 (n = 81). When every instrument disagrees with the person and with the
other instruments, the test is to regenerate text the operator already wrote.
They wrote the answer key.

# Design

**Pristine test set.** Three Codecov posts by the operator that no one on this
side has read: granular components (705 words), GitHub integration (597), PyPI
post-mortem (1,843). Extracted by script, never printed.
[T0015](T0015-build-the-professional-profile-from-real-samples-and.md) failed
exactly here — "held out of the build" was treated as "unseen", and it was not,
because the extraction was done by eye.

**Content-only briefs**, written by a sub-agent that reads the original. The
brief carries every fact, number and argument and the order they appear in. It
carries **no headings and no phrasings** — headings especially, since heading
style is the thing [E0006](../../knowledge-catalog/reference/E0006-the-operator-rejected-a-profile-that-passed-every.md)
caught us failing, and a brief that leaks them tests nothing.

**Arms.** Generation is done by fresh sub-agents with no exposure to the corpus,
not by the session that built the profile — which cannot un-know the five
training pieces it read, and so cannot write an honest control.

| arm | input |
|---|---|
| A control | brief only |
| B profile | brief + `~/.claude/voice/profile/professional.md` |
| D real | what the operator actually published |

Arm B is production-faithful: the shipped skill reads the profile, never the
corpus. The exemplar arm is deliberately absent and belongs to
[T0017](T0017-experiment-population-matched-exemplar-retrieval-versus-a-described.md).

**Judgment.** The operator, blind and shuffled. Markers computed alongside, as a
diagnostic and explicitly not as the verdict.

# Acceptance criteria

- [ ] Test pieces extracted mechanically and never read by the session
      conducting the comparison
- [ ] Briefs carry no heading and no phrase from the originals
- [ ] Each generated arm produced by an agent with no corpus exposure
- [ ] The operator judges blind, with arm labels withheld until after
- [ ] The result is recorded whichever way it falls, including "the profile made
      no difference"

# Out of scope

- Rebuilding the profile on the expanded corpus. The current profile is the
  baseline under test; changing it and the method together would confound the
  result. The new training material is staged and unused.
- Exemplar retrieval. [T0017](T0017-experiment-population-matched-exemplar-retrieval-versus-a-described.md).
- Any style-embedding metric. [E0007](../../knowledge-catalog/reference/E0007-state-of-the-art-for-reproducing-a-specific.md)
  is clear that it is a drift tripwire, not an acceptance test.

# Log

## 2026-11-10 — run set up, awaiting the operator's judgment

Two pieces under test: granular Components (705 real words) and the GitHub
integration change (597). The PyPI post-mortem is briefed and held in reserve —
1,843 words is a lot to ask someone to judge blind in one sitting.

**The leak check earned its place immediately.** The first granular brief
carried **10 of its 13 headings verbatim**, plus 51 eight-word phrase overlaps.
Had it gone through, the heading question — the one
[E0006](../../knowledge-catalog/reference/E0006-the-operator-rejected-a-profile-that-passed-every.md)
caught us failing — would have been untestable on that piece, and we would have
scored ourselves a pass on the thing we are least able to do. Rewritten: 0
leaked headings on all three. The 12 overlaps that survive in granular are YAML
file paths, which no writer invents.

The check is mechanical and takes a second: candidate headings are lines of
2–12 words under 80 characters with no terminal punctuation; leakage is a
verbatim lowercase substring match; phrase overlap is shared 8-word shingles.
Worth keeping as a tool.

**Arms as run.** Control got the brief alone. The profile arm got
`skills/voice-professional/SKILL.md` plus
`~/.claude/voice/profile/professional.md` — what ships, not the profile alone.
Both generating agents were forbidden the corpus and the originals, and both
confirmed they read nothing outside `briefs/`. Lengths landed within 15% of
target on all four.

**Presentation.** Three versions per piece, shuffled, with markup normalised —
headings, lists and paragraphs rendered identically — so format is not a tell.
The key is on disk and unread by the session running the comparison.

**A confound was claimed and then retracted.** This log first recorded that
both generations produced *14 headings against the operator's 7*, read as the
agents over-sectioning. **That was wrong and is withdrawn.** It was an artefact
of the comparison tool: one heading heuristic was applied to all three versions,
and it classified YAML lines as headings — `name: CommentFeature`, bare
backticks, config comments. The real counts are **4, 4 and 5** on granular and
**2, 2 and 1** on the GitHub piece. Heading counts match closely and there is no
over-sectioning effect.

The cause is worth keeping: the two generated versions are Markdown, where a
heading is unambiguously a `#` line and no guessing is needed, while only the
operator's extracted original requires a heuristic. Applying one rule to both
manufactured a finding out of a parser bug. The fixed tool parses Markdown
structurally and reserves the heuristic for plain text, excluding fenced code,
lowercase `key:` lines, indented lines and bare punctuation.

A measurement tool that has not been checked against a known case will invent
findings, and this one invented a confident, plausible, specific one.

**One known defect carried into the run.** The profile arm chose em-dashes over
`--`, correctly following the profile's `Unstable — do not assert` section. But
the sent-mail sweep on 2026-11-10 found `--` in the operator's own unedited
typing, which suggests it is a real habit and the published em-dashes were
editorial. The evidence was in hand and the profile was not updated before the
run, so any dash tell in arm B belongs to that omission and not to the method.

## 2026-11-10 — first six trials judged; result in E0008

The profile ranked above the no-guidance control in **2 of 6** trials
(two-sided p = 0.688), and the operator identified his own writing in **2 of 6**
— exactly chance. His own published prose carried the worst mean rank of the
three arms. Full numbers and the caveats in
[E0008](../../knowledge-catalog/reference/E0008-the-profile-did-not-beat-the-control-and.md).

The run is not finished. Three more trials are generating from the PyPI
post-mortem brief, which takes headings from n = 2 to 3 and prose from n = 4 to
6. Still underpowered, but the headings-versus-prose split is the most
actionable thing the first six produced and is currently resting on two trials.

Worth recording about the method rather than the result: the sealed-key
discipline held, the operator's rankings were written down before anything was
unsealed, and the two most useful findings — bullet length, one subject per
heading — came from reasons he volunteered rather than from the rankings
themselves. The free-text reason is carrying more information than the ordinal.
