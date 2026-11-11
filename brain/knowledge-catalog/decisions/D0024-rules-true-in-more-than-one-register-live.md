---
id: D0024
type: decision
title: "Rules true in more than one register live in a shared profile"
description: "A rule confirmed in two registers moves to common.md beside the register profiles, because the alternative is rediscovering it once per register at the cost of a review round each time."
timestamp: "2026-11-11"
tags: [voice, profile, architecture, registers]
status: active
serves: ../goals/G0004-structure-sounds-like-the-operator-and-prose-is.md
invariant: "A rule confirmed in two or more registers lives in common.md and is not duplicated into a register profile; where the two disagree the register profile wins."
constrains: [voice/profile, skills]
---

# Context

[D0021](D0021-a-profile-is-derived-per-text-population-not.md) established that a
profile is derived per text population. Nothing said what happens when a rule
turns out to hold across *registers*, and the answer was being arrived at the
expensive way.

Two defect harvests produced three rules independently in both the professional
and casual registers:

- **the head noun is never implicit** — five confirmations, three professional
  and two casual, one of them flagged by the operator himself as recurring
- **a vague abstraction gets replaced by a precise phrase**
- **no trailing weak phrase** — and the casual instance *settled* an ambiguity
  the professional profile had recorded and could not resolve, because his two
  professional examples disagreed on whether the rule was about prepositions
  specifically

Four more hold across every register measured: no semicolons, no em-dashes, a
short landing that compresses rather than coins, and reported speech in quote
marks.

Each was found by showing the operator generated prose and having him name the
defect. **Finding the same rule a second time costs a review round** — his
attention, which [D0022](D0022-the-preference-signal-is-named-defects-never-blind.md)
already identifies as the scarce resource. The research register is unwritten,
and without a shared file it would rediscover all seven.

A shared layer was in the first design sketched for this project, as
`voice/profile/common.md`, and was never built because nothing had yet earned a
place in it.

# Decision

A rule confirmed in **two or more registers** lives in
`voice/profile/common.md`, beside the register profiles and resolved from the
same place.

A register skill loads its register profile **and** `common.md`, and applies
both. **Where they disagree the register profile wins** — it is the more
specific, and the shared file is a generalisation drawn from it.

A rule is not promoted on a guess that it generalises. It moves when it has been
named in a second register, by the person, about their own writing.

# Alternatives

- **Duplicate the rule in each register profile** — rejected: three copies drift,
  and the copy that gets corrected is whichever register was last harvested. The
  trailing-weak-phrase rule is the case in point: the professional profile
  recorded an unresolved ambiguity, and the casual finding settled it. With
  duplicates, one file would now be right and the other still wrong.
- **Put cross-register rules in the craft skill** — rejected on
  [D0013](D0013-the-craft-ships-generic-and-the-voice-is.md). The skill ships
  generic and may hold no fact about any person. "This writer never leaves a
  head noun implicit" is a fact about a person.
- **Promote anything that looks general** — rejected: the casual register's
  lowercase message starts look like they might generalise and emphatically do
  not. Two registers, named by the person, is the bar.

# Consequences

- The register-loading instruction in every register skill changes, and a skill
  that loads only its register profile is now incomplete.
- `common.md` is a third file an adopter has to understand. The cost is real and
  is paid once; the alternative is paid per register per rule.
- A rule promoted from a register profile should be removed from it rather than
  left in both, or the drift this decision exists to prevent arrives anyway.
- The research register, when built, starts with seven rules already in hand
  instead of rediscovering them over three review rounds.
- **`/voice-harvest` gains a step**: after encoding a rule, check whether it has
  now been named in a second register, and promote it if so.
