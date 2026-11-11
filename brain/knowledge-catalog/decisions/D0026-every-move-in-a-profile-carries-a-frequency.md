---
id: D0026
type: decision
title: "Every move in a profile carries a frequency"
description: "A profile that lists moves without saying how often to use them instructs a writer to deploy every effect it names, every time; so each move gets a rate, and rates are counted across everything the reader sees at once."
timestamp: "2026-11-11"
tags: [voice, profile, format, rhythm]
status: active
serves: ../goals/G0004-structure-sounds-like-the-operator-and-prose-is.md
invariant: "Every move in a profile states how often it is used, and a budget is counted across the whole batch a reader sees rather than within one passage."
constrains: [voice/profile, skills]
---

# Context

The second casual harvest produced a kind of defect the first had not. Three
separate moves were flagged, and **none of them was called wrong**:

| move | instances | verdict |
|---|---|---|
| foreshadowing | opened and closed one passage, opened the next | *"We can foreshadow, however. It's something that should be used sparingly."* |
| a pair of clipped sentences | twice, in consecutive passages | *"We have to be aware of overuse here, especially compared to the last paragraph where we do the same thing."* |
| the asyndetic triplet — "The tool lands, the work doesn't shrink, the team does" | once | *"a kind of punchiness you might want to use sparingly but it is good when it's used correctly"* |

Each is a move the operator owns and endorses. Each was deployed correctly.
The complaint is rate.

Every move in every profile is currently written as a thing to do. Exactly one
carries a budget — *"Reframe once per piece"* — and it was written that way by
accident rather than by policy. A profile in that shape tells a writer to use
every effect it names, every time it could, which is a serviceable description
of over-written prose.

The second finding is sharper and is what makes this a format change rather
than a wording fix: **he counted across passages.** *"Taking P1 and P2 together,
we're foreshadowing way too much."* The six passages were generated
independently, by one agent, in separate files, and no instruction in the
system could have caught it.

# Decision

**Every move in a profile states how often it is used.** The vocabulary is
small on purpose:

| rate | meaning |
|---|---|
| `always` | a rule, not a move — ownership, correctness, the measured absences |
| `often` | the default way he does this thing |
| `sparingly` | an effect. At most once in a piece, and not in consecutive pieces |
| `once per piece` | at most one, and the piece is worse with two |
| `never` | a move he does not make |

A move with no rate is a defect in the profile, not a licence.

**Budgets are counted across everything a reader sees at once**, not within one
passage. Where several pieces are generated for one reader, the writer tracks
the batch.

# Alternatives

- **Leave moves unrated and trust judgement** — rejected on the measurement. A
  generator given a list of effects used three of them twice in six short
  passages, and each use was individually defensible.
- **Give numeric rates per thousand words** — rejected: these are structural
  moves, not countable surface features, and a false precision would invite
  exactly the gaming that
  [D0018](D0018-a-voice-profile-states-its-claims-checkably.md) as amended
  already forbids for markers.
- **Enforce budgets only inside a passage** — rejected: the operator's
  strongest complaint was explicitly cross-passage, and per-passage enforcement
  would have passed all six.

# Consequences

- All three profiles need a rate on every move. Most are `often`; the effects
  are `sparingly`.
- **A batch of generated pieces must be reviewed as a batch** before it reaches
  anyone. This is new work for `/voice-harvest` and for anything that generates
  more than one passage at a time.
- A rate is itself a claim and can be wrong. It should be recorded as observed
  frequency where the corpus supports one, and as a judgement where it does
  not.
- This is the second format category added in two days, after
  [D0025](D0025-output-is-always-correctly-spelled-punctuated-and-capitalised.md)'s
  *observed, not reproduced*. The profile format is accumulating structure
  faster than the spec that describes it, which does not yet exist.
