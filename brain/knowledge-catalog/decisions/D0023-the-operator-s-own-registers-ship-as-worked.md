---
id: D0023
type: decision
title: "The operator's own registers ship as worked examples, never as loaded defaults"
description: "Three registers tuned on the operator ship in the repository so an adopter can read a filled-in profile and copy it if they want, but nothing is resolved or loaded from them automatically."
timestamp: "2026-11-10"
tags: [voice, profile, adoption, examples]
status: active
serves: ../goals/G0005-someone-can-produce-their-own-voice-registers-by.md
invariant: "No profile shipped in this repository is ever loaded automatically; a profile takes effect only where a user has put it."
constrains: [voice/profile, skills, examples]
---

# Context

The workshop needs something to show. A format described in prose and never
exhibited is the hardest kind of thing to fill in, and this project has three
registers' worth of profile material already built — one of them tuned through
two rounds of defect harvesting against the operator's own writing.

The operator proposed shipping them: *"the default voice profiles we ship could
honestly just be mine."*

The force against shipping them **as defaults** is
[D0015](D0015-a-voice-profile-is-optional-and-the-skills.md), which promises a
profile is optional and that the skills do the generic job without one. A
default profile that loads breaks that promise in a specific and unpleasant way:
every adopter's agent would write in one particular person's voice until they
noticed and replaced it. For them, that is worse than generic — generic prose is
nobody's, and this would be somebody else's.

The operator's own resolution: *"the default profile is just the one we generate
on our own output."* Nothing is pre-loaded. What ships is the artifact the
process produced, there to take or leave.

# Decision

The operator's three registers ship in the repository as **worked examples**.
They live somewhere a reader will find them, they are plainly labelled as one
person's voice, and **nothing loads them**.

Profile resolution is unchanged from
[D0019](D0019-humanize-me-ships-as-a-claude-code-plugin.md): project first, then
user scope, then nothing. A shipped example participates in none of it. It takes
effect only where a user has copied it to a path that resolves.

They are shipped for three reasons, in order: to show what a filled-in profile
looks like; to be copied by someone who likes the output and does not want to
run the process; and to let the workshop be read before it is run.

# Alternatives

- **Ship them as loaded defaults** — rejected on
  [D0015](D0015-a-voice-profile-is-optional-and-the-skills.md). An adopter who
  installs and writes a paragraph should get generic craft, not a stranger's
  voice. Being nobody is a safe default; being someone else is not.
- **Ship no examples** — rejected: a format with no instance is the thing people
  fail to fill in, and this project has spent a day learning that an abstract
  description underperforms a concrete one.
- **Ship a synthetic example profile for an invented person** — rejected: it
  would describe a voice no corpus produced, and every value in it would be a
  claim with nothing behind it, which is the failure
  [D0001](../../example/knowledge-catalog/decisions/D0001-claims-must-be-checkable.md)
  names.

# Consequences

- The examples carry the measurement history with them. The professional
  register's profile records what has been checked, what was withdrawn, and
  what is unstable — a reader copying it inherits an honest artifact rather than
  a confident one.
- Two of the three do not exist yet. Casual and research are unwritten, and
  shipping one register as an example while claiming three is the kind of
  overclaim this repository is trying not to make.
- A shipped example is a privacy surface. These are derived from the operator's
  published writing and his sent mail; nothing quoting unpublished
  correspondence may appear in a file that ships, under
  [D0017](D0017-writing-reached-through-mcp-is-distilled-in-flight.md).
