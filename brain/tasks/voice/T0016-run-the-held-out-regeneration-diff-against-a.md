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
