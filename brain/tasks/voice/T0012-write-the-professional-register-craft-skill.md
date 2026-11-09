---
id: T0012
type: task
title: "Write the professional register craft skill"
description: "The first register skill, craft only and profile-free, so the library does something useful before any corpus exists and the profile format has real gaps to be designed against."
status: Testing
category: enhancement
initiative: voice
blocked_by: []
timestamp: "2026-11-09"
tags: [voice, registers, craft]
---

# What to build

An agent asked to write something at professional warrant — a message that
stakes the writer's judgment and owes the reader the reasoning behind it —
produces prose that reads as a person's considered position rather than as an
assistant's summary. With no profile present and nothing known about who is
writing.

The substance is the craft: what agent prose does wrong specifically at this
register, and what a claim resting on stated judgment has to carry.
[D0014](../../knowledge-catalog/decisions/D0014-registers-are-organized-by-burden-of-proof-not.md)
sets the axis — the failure to fix is uniform unearned confidence, hedging what
should be owned and asserting what should be qualified — not formality.

This is deliberately the first register written. It is the one where the
failure is worst, and writing it is how the profile format gets designed
against real gaps rather than imagined ones: whatever the skill cannot say
without knowing the writer is, by definition, what the profile has to carry.

# Acceptance criteria

- [x] The skill produces usable prose with no profile present, and says which
      mode it is in, per
      [D0015](../../knowledge-catalog/decisions/D0015-a-voice-profile-is-optional-and-the-skills.md)
- [x] It states what a claim at this register rests on before it states any
      style preference, per
      [D0014](../../knowledge-catalog/decisions/D0014-registers-are-organized-by-burden-of-proof-not.md)
- [x] It selects on what the claims require, never on the medium the prose will
      be sent through
- [x] It names no particular person and asserts nothing about the operator, per
      [D0013](../../knowledge-catalog/decisions/D0013-the-craft-ships-generic-and-the-voice-is.md)
- [x] It declares a human reader, per
      [D0011](../../knowledge-catalog/decisions/D0011-only-prose-with-a-human-reader-is-in.md)
- [x] It resolves a profile project-first then user-scope, and proceeds on a
      miss, per
      [D0019](../../knowledge-catalog/decisions/D0019-humanize-me-ships-as-a-claude-code-plugin.md)
- [x] The gaps it could not fill without knowing the writer are written down,
      as the input to the profile format spec

# Out of scope

- The casual and research registers. Written after this one settles the shape.
- The profile format itself. This task produces the requirements for it, not
  the format.
- The generator and the marker checker.

# Log

## 2026-11-09 — written

`skills/voice-professional/SKILL.md`, 146 lines, craft only and profile-free.

It opens on what a claim at this register rests on — the writer's judgment,
stated as judgment and owned — before any style guidance, per
[D0014](../../knowledge-catalog/decisions/D0014-registers-are-organized-by-burden-of-proof-not.md),
and its selection section routes on what the claims require with an explicit
note that medium and register are independent. Profile resolution is
project-then-user per
[D0019](../../knowledge-catalog/decisions/D0019-humanize-me-ships-as-a-claude-code-plugin.md),
a miss is declared rather than silent per
[D0015](../../knowledge-catalog/decisions/D0015-a-voice-profile-is-optional-and-the-skills.md),
and the description names a human reader and excludes agent-facing text per
[D0011](../../knowledge-catalog/decisions/D0011-only-prose-with-a-human-reader-is-in.md).

Twelve named failures, all one failure underneath — confidence that floats free
of warrant — then seven positive moves and a three-question check.

The gaps it could not fill without knowing the writer are
[E0004](../../knowledge-catalog/reference/E0004-what-the-professional-craft-skill-could-not-say.md).
Two findings there bear on decisions already on record: the countable half of a
profile is the minority of the value, which cautions against reading
[D0018](../../knowledge-catalog/decisions/D0018-a-voice-profile-states-its-claims-checkably.md)
as "countably" rather than "checkably"; and the skill's own conflict rule —
warrant beats profile — is too blunt for hedging *level*, where it would
flatten every user toward one setting. Neither is resolved here.

Left for `/spec-review`: whether this skill is any good is a judgment about
prose, and nothing in it has been exercised against a real writing request yet.
