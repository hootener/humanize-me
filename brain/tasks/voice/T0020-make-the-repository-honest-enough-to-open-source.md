---
id: T0020
type: task
title: "Make the repository honest enough to open source"
description: "Before strangers can install this, the README has to say which half has evidence behind it and which half was measured as harmful, and the published work the design rests on has to be cited."
status: Testing
category: enhancement
initiative: voice
blocked_by: []
timestamp: "2026-11-10"
tags: [adoption, documentation, honesty, release]
---

# What to build

A developer who finds this repository on GitHub can tell, without reading the
brain, what has been measured and what has only been designed — and can follow
every scientific claim to its source.

The operator's framing: MIT, work in progress, *"if we used any scientific
writing to justify our approach we should cite it."*

The README as written overclaims. It lists `voice-professional` as "available"
and says nothing about the fact that its heading guidance beat a no-guidance
control 3 of 3 while its prose guidance lost 0 of 6, or that one of its markers
was measured as actively harmful and withdrawn. For a stranger deciding whether
to install, that distinction is the whole truth of the thing.

# Acceptance criteria

- [x] `REFERENCES.md` lists the published work the design rests on, with what
      each paper is load-bearing for rather than a reading list, and the
      verification caveats attached where they exist
- [x] The README states what has been measured and what has not, prominently
      enough that a reader cannot miss it
- [x] The MIT licence and the work-in-progress status are both unmistakable
- [x] No claim in the README is stronger than its evidence

# Out of scope

- The casual and research registers. Their absence is stated, not fixed.
- The profile format spec, which is unsettled and said to be.

# Log

## 2026-11-10 — references written, README being drafted as a trial

[REFERENCES.md](../../../REFERENCES.md) carries fourteen citations grouped by
the decision each one justifies: Baumler et al. (r = 0.244, n = 81,
pre-registered) under [D0018](../../knowledge-catalog/decisions/D0018-a-voice-profile-states-its-claims-checkably.md)
as amended; Verbalized Sampling (α̂ = 0.57 and 0.65, p < 10⁻¹⁴) under
[D0022](../../knowledge-catalog/decisions/D0022-the-preference-signal-is-named-defects-never-blind.md);
Wang et al. (blogs 16–21% against news 95–97%) for why this corpus is the hard
case; Chakravorty and Konen et al. for what was ruled out. It also points at
[E0007](../../knowledge-catalog/reference/E0007-state-of-the-art-for-reproducing-a-specific.md)
for work read and not built on, including everything that could not be verified.

The README itself is being written twice, as a controlled trial — one arm from
a content-only brief with no style guidance, one arm with the craft skill and
the profile including the eleven rules from
[E0011](../../knowledge-catalog/reference/E0011-eight-defect-harvest-passages-produced-nine-rules-where.md).
The operator picks blind. Whichever wins becomes the README, so the trial costs
nothing beyond the second generation.

## 2026-11-12 — gates met, published

`## What Has Been Measured` closes the two open criteria. It states the one
method with a result behind it (the harvest, 75 rules over four rounds), the
two that went the wrong way (preference ranking at chance; the profile losing
0 of 6 on prose and a marker withdrawn for doing measurable harm), and the
thing the README could most easily have hidden: **the shipped craft skill has
no controlled trial at all**, because every trial tested a personal profile
that does not ship.

A pre-publication audit ran over all tracked files. No email addresses, phone
numbers, postal addresses or credentials. No third-party names beyond seven
published-researcher citations. Nothing quoted from the Slack corpus, which is
D0017 holding. Two things were found and removed: a client project named by
path in E0005 and T0015, and a `resource:` in D0011/D0012 pointing at a session
transcript on one machine. `graph.html` was untracked — it embeds the whole
brain as JSON and would duplicate any future redaction.
