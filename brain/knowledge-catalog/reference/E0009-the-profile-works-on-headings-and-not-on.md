---
id: E0009
type: evidence
title: "The profile works on headings and not on prose"
description: "Nine blind trials: the profile beat the no-guidance control 3/3 on headings and 0/6 on prose excerpts, a dissociation at Fisher p = 0.012 that the pooled result completely hides."
timestamp: "2026-11-10"
tags: [voice, verification, experiment, findings, headings]
status: active
amends: [E0008-the-profile-did-not-beat-the-control-and.md]
---

Three more trials on the PyPI post-mortem, judged the same way as the six in
[E0008](E0008-the-profile-did-not-beat-the-control-and.md), bringing the run to
nine. The pooled numbers stayed flat. Split by text population they are not.

# The result

**Headings (n = 3)**

| arm | mean rank | ranks |
|---|---|---|
| profile | **1.33** | 2, 1, 1 |
| the operator's own text | 1.67 | 1, 2, 2 |
| control | 3.00 | 3, 3, 3 |

**Prose excerpts (n = 6)**

| arm | mean rank | ranks |
|---|---|---|
| control | **1.33** | 1, 1, 1, 2, 2, 1 |
| profile | 2.33 | 2, 2, 2, 3, 3, 2 |
| the operator's own text | 2.33 | 3, 3, 3, 1, 1, 3 |

**The profile beat the control 3/3 on headings and 0/6 on prose.** Fisher exact,
two-sided, **p = 0.0119**. On headings the control placed last in every trial.
Twice in three headings trials the operator picked the *profile* output as his
own writing.

Pooled, all of this vanishes: profile above control 3/9 (p = 0.508), own writing
identified 3/9 against a chance rate of exactly 3/9. Two effects of opposite
sign cancelling to nothing. **A pooled mean over text populations was the wrong
summary**, which is [D0021](../decisions/D0021-a-profile-is-derived-per-text-population-not.md)
arriving in the analysis after arriving in the profile and in the tooling.

# What it is honestly worth

**This is a post-hoc subgroup analysis.** The split was looked for after the
pooled result came back flat. With n = 9 and two subgroups, p = 0.012 is
reachable from noise without much effort. It generates a hypothesis; it does not
confirm one. Any confirmation has to come from trials designed around headings
in advance.

What raises it above a fishing expedition is that it is the **third independent
appearance of the same thing**, and the first two were not looked for:

- [E0006](E0006-the-operator-rejected-a-profile-that-passed-every.md) — the
  operator's rejection of a generated document arrived as a complaint about a
  heading, unprompted.
- [E0008](E0008-the-profile-did-not-beat-the-control-and.md) — headings were the
  only population where he ranked his own writing in the top two.
- Here — the profile's entire measurable effect sits in headings.

# Why this shape is plausible

The profile's heading section is **enumerable and population-specific**: three
named shapes, a prohibition on withholding the subject, Title Case, derived
directly from the corpus. That is the kind of instruction that transfers intact
through a prompt.

Its prose guidance is rhythm, hedging mechanism and landing sentences — and at
90-word excerpt scale the profile arm ranked **below a control that received no
style guidance at all**, in every single trial. Either the guidance does not
transfer, or following it actively degrades the prose. This run cannot separate
those two.

# The finding that did not move

Across all nine trials the operator **ranked his own published prose last in 4
of 6 prose trials**, and identified it at exactly chance overall. He prefers
generated prose to his own. Whatever is being measured when he ranks prose, it
is not authorship — which is
[E0007](E0007-state-of-the-art-for-reproducing-a-specific.md)'s r = 0.244
reproduced on a sample of one, and the reason
[D0018](../decisions/D0018-a-voice-profile-states-its-claims-checkably.md) is
amended rather than merely annotated.

# Consequences

- Blind operator judgment is a usable instrument **for headings** and is not one
  for prose excerpts. It discriminated in one population and sat at chance in
  the other.
- [D0013](../decisions/D0013-the-craft-ships-generic-and-the-voice-is.md) is
  now **partially supported rather than unsupported**: a generated description
  demonstrably works, for the population where the description is enumerable.
  Its invariant concerns separation of concerns, not efficacy, so it is not
  amended — but the shape of its artifact is now an empirical question with one
  data point on each side.
- [T0017](../../tasks/voice/T0017-experiment-population-matched-exemplar-retrieval-versus-a-described.md)
  gains a sharp prediction to test rather than a vague hope: if descriptions
  carry enumerable rules and exemplars carry what cannot be enumerated, then
  verbatim passages should beat the profile **on prose and not on headings** —
  the exact inverse of this result.
- No decision is taken here about shrinking the profile's prose guidance.
  One post-hoc subgroup at n = 9 does not justify cutting a section of the
  shipped artifact, and T0017 is the experiment that would.

# Citations

- Nine trial responses and two sealed keys, 2026-11-10, each recorded before
  unsealing
- [T0016](../../tasks/voice/T0016-run-the-held-out-regeneration-diff-against-a.md)
