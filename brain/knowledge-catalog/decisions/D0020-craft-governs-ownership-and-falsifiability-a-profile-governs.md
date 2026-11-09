---
id: D0020
type: decision
title: "Craft governs ownership and falsifiability; a profile governs how much"
description: "A craft rule may require that a judgment has a holder and a confidence that could be wrong; it may never legislate the quantity of hedging, which is voice and belongs to the profile."
timestamp: "2026-11-09"
tags: [voice, craft, profile, registers]
status: active
serves: ../goals/G0003-an-agent-writes-human-facing-prose-in-the.md
invariant: "A craft rule constrains ownership and falsifiability only; hedge quantity and wording belong to the profile."
constrains: [skills, voice/profile]
---

# Context

[D0013](D0013-the-craft-ships-generic-and-the-voice-is.md) draws the line
between the two halves of the library: a shipped skill holds craft and knows
nothing about any person, a profile holds the person and no craft. It does not
say where the line falls on a rule that straddles, and hedging straddles.

The first register skill resolved it the blunt way. It sorted every rule into
warrant or taste, filed hedging under warrant, and declared that warrant wins
where the two conflict. Recorded at the time as a gap in
[E0004](../reference/E0004-what-the-professional-craft-skill-could-not-say.md).

Four sentences carrying the same judgment at the same real confidence show why
that fails:

| | |
|---|---|
| A | "It may be worth considering whether the migration should be split." |
| B | "Split the migration." |
| C | "I'd split the migration." |
| D | "I'd probably split the migration, though I haven't looked at the foreign keys." |

A is a genuine failure. Nobody holds it, nothing in it could turn out wrong,
and a reader who has to act cannot. B, C and D all own the judgment and differ
only in how much they hedge — which is voice. D hedges most and is arguably the
best of the four, because its hedge carries information: it says which part is
soft.

The skill as written cannot tell D from A, because it states the prohibition
against hedging as a surface quantity. Combined with "warrant wins", a profile
correctly recording that someone writes like D loses to the craft, and every
user converges on B or C regardless of how they actually write. The library
would flatten the voices it exists to preserve.

# Decision

A craft rule may require two things of a claim and no more:

1. **Every judgment has a holder.** Yours, or someone you name.
2. **Every confidence is something you could be wrong about.**

Hedge quantity and hedge wording are voice. The profile governs them, and no
craft rule overrides a profile on either.

A hedge that names what the writer is unsure of, or states a likelihood that
could turn out false, satisfies the craft rule **at any quantity**. "It may be
worth considering" fails it at quantity one.

This replaces hedge-counting wherever a register skill does it. The stacked
hedge is caught by the same rule and for the honest reason: "this might
possibly be somewhat slower" is not wrong because it carries three qualifiers,
it is wrong because after them no claim remains that could be false.

# Alternatives

- **Keep "warrant wins" and let the profile state a personal hedging floor** —
  the shape [E0004](../reference/E0004-what-the-professional-craft-skill-could-not-say.md)
  proposed when it raised this. Rejected: it patches the symptom and leaves the
  craft rule wrong. A floor is also the wrong instrument, since the problem is
  not that the craft sets the level too low but that it has an opinion about
  the level at all.
- **Drop the hedging rules from the craft entirely** — rejected: A is a real
  failure and the most common one in agent prose. Removing the rule to fix its
  overreach would give up the thing the register exists to fix.
- **Let the profile win every conflict** — rejected: it makes the craft
  advisory, and a profile is generated from a corpus that may itself contain
  unowned judgments. The craft is what stops a profile teaching a bad habit
  back.

# Consequences

- The professional register skill is rewritten on this rule, which is
  [T0013](../../tasks/voice/T0013-restate-the-hedging-rules-as-ownership-and-falsifiability.md).
  The casual and research registers inherit it before they are written.
- The rule is testable in a way hedge-counting was not: a passage fails if a
  judgment has no holder or a confidence could not be wrong. That is closer to
  something [D0018](D0018-a-voice-profile-states-its-claims-checkably.md)'s
  marker vocabulary can carry than "hedges too much" ever was.
- Banned-opener lists stay legitimate — "It may be worth considering" earns its
  place by failing the rule, not by being a hedge.
- A profile may record a writer who hedges heavily, and the skills must honour
  it. A reader who finds that prose over-qualified is disagreeing with the
  writer's voice, which is not a defect this library is obliged to fix.
- It sharpens [D0013](D0013-the-craft-ships-generic-and-the-voice-is.md) rather
  than contradicting it: the craft/profile boundary now has a stated test for
  rules that straddle it.
