---
id: D0013
type: decision
title: "The craft ships generic and the voice is a generated profile"
description: "The library ships register skills that hold the craft for everyone; a generator reads the operator's writing and emits only a profile those skills read at write time."
timestamp: "2026-11-09"
tags: [voice, architecture, profile]
status: active
serves: ../goals/G0003-an-agent-writes-human-facing-prose-in-the.md
invariant: "A register skill holds no fact about any particular person, and a profile holds no craft instruction."
constrains: [skills, voice/profile]
---

# Context

The library has to combine two things that change on completely different
schedules. The craft — what agent prose does wrong, and what a claim at a given
pitch has to rest on — is the same for every user and improves as the project
learns. The operator's voice is theirs, improves only when they feed it more of
their writing, and is worth hand-editing.

The tempting shape is one generator that writes three finished skills, each
holding craft and voice together. It reads well and needs nothing resolved at
write time.

The force against it is the update path. Craft baked into a generated artifact
reaches an existing user only if they regenerate, which means every
improvement the project makes is an improvement most users never see. It also
puts the generator on the hook for restating the craft correctly on every run,
where getting it wrong is silent.

# Decision

The two halves ship separately and meet at write time.

The library ships the register skills. They hold the craft, name no person, and
are identical in every install. A generator reads the operator's writing and
emits **only** a profile — a description of how that person writes. The skills
read the profile when they write.

Neither half may take on the other's job: a shipped skill that knows something
about a particular person has leaked, and a profile that instructs on craft is
duplicating what already ships.

# Alternatives

- **The generator writes three self-contained skills** — rejected: craft
  improvements then reach nobody who already installed, and the generator has
  to get the craft right on every run with no way to tell when it did not.
- **One skill holding all three registers, plus a profile** — rejected on
  loading rather than on principle: a register is picked before writing starts,
  so the other two are dead weight in context. Revisit if the registers turn
  out to share more than they differ.

# Consequences

- A register skill is reviewable as craft on its own, with no corpus in hand.
- The profile format is an interface between the two halves, so changing it
  breaks installed skills and is a versioned change rather than a tidy-up.
- The library does something useful before any profile exists, which is what
  [D0015](D0015-a-voice-profile-is-optional-and-the-skills.md) turns into a
  requirement.
- Where the profile is *found* is a separate question, settled by
  [D0019](D0019-humanize-me-ships-as-a-claude-code-plugin.md).
