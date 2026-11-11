---
id: D0028
type: decision
title: "A move's rate is set per register, not per profile"
description: "The same construction can be a signature move in one register and noise in another, so a rate belongs to the move-in-a-register rather than to the move."
timestamp: "2026-11-11"
tags: [voice, profile, format, registers, rhythm]
status: active
serves: ../goals/G0004-structure-sounds-like-the-operator-and-prose-is.md
invariant: "A move's rate is stated for the register it appears in; a rate recorded in one register's profile does not carry to another."
constrains: [voice/profile, skills]
---

# Context

[D0026](D0026-every-move-in-a-profile-carries-a-frequency.md) gave every move a
frequency because a profile listing moves without rates instructs a writer to
deploy every effect it names, every time. It assumed a rate belongs to the move.

The precise harvest shows it does not. Two constructions were rejected as
"too flowery", with the operator asking for "a much more analytical
straightforward way":

| rejected in precise | what it is | its standing in professional |
|---|---|---|
| "The damage came from the shape of the rule and not from the number we picked" | balanced antithesis | a recorded move, `sparingly` |
| "A floor cannot be satisfied by going lower" | aphoristic short landing | three confirmations, `sparingly` |

Both are correct professional moves. The short landing is among the
best-attested rules in the whole record. In precise they are noise sitting on
top of a measurement.

The same harvest produced the mirror case. He rewrote a first-person line to be
**more impersonal** — *"Better signal is obtained by asking the reader to pick
out defects in the prose, because this task can be performed independent of
preference"* — and called it "a more professional precise way to say it". The
impersonal construction is wrong in casual, unremarkable in professional, and
correct here for one specific job.

# Decision

**A rate is stated for a move in a register.** The same construction may be
`often` in one register, `sparingly` in another and `never` in a third, and a
rate recorded in one register's profile carries no authority in another.

`common.md` holds rules confirmed across registers under
[D0024](D0024-rules-true-in-more-than-one-register-live.md). A rule may be
shared **and still take a different rate per register** — the rule belongs in
the shared file, the rate belongs to each register profile. Where a register
states a rate, it wins over any rate in the shared file.

# Alternatives

- **One rate per move, as D0026 assumed** — rejected on the measurement. The
  short landing would have carried its `sparingly` into precise, where it was
  rejected outright, twice, in a single passage.
- **Duplicate the move into each register with its own rate** — rejected on
  [D0024](D0024-rules-true-in-more-than-one-register-live.md): copies drift and
  the corrected copy is whichever register was harvested last. Share the rule,
  split the rate.
- **Drop cross-register sharing and give each register its own full profile** —
  rejected: the head-noun rule has seven confirmations across two registers and
  is the same rule each time. Sharing is what stops it being rediscovered a
  third time.

# Consequences

- The precise profile records two moves as effectively `never` that the
  professional profile records as `sparingly`, and says why.
- `common.md` needs a rate column or a per-register note where a shared rule's
  frequency differs. It currently states one rate per rule.
- **A rate is a weaker claim than a rule.** The rule — that he lands a paragraph
  on a short flat line — survived into precise and was rejected there only as
  an *effect*. Rules generalise across registers more readily than rates do,
  and the harvest should record them separately.
- `/voice-harvest`'s promotion step needs qualifying: a rule named in a second
  register moves to the shared file, but its rate does not travel with it.
