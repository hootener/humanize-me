---
id: T0021
type: task
title: "Build the voice workshop"
description: "Four skills taking someone from a clone to voice registers tuned to them, built in evidence order — the proven step first."
status: In Progress
category: enhancement
initiative: voice
blocked_by: []
spec: ../../knowledge-catalog/specs/S0001-the-voice-workshop.md
timestamp: "2026-11-10"
tags: []
---

# What to build

The four skills in [S0001](../../knowledge-catalog/specs/S0001-the-voice-workshop.md):
`/voice-gather`, `/voice-draft`, `/voice-harvest`, `/voice-check`.

**Built in evidence order, not run order.** `/voice-harvest` is the only step
with a result behind it, so it is built first; the others are developed against
a workshop whose strongest leg already works. Each skill states its own
confidence level in its own text, so a user can tell a measured step from an
improvised one without opening `brain/`.

# Acceptance criteria

- [x] `/voice-harvest` exists, carries the ask-what-is-wrong rule with the
      measurement behind it, and states what it cannot do
- [ ] `/voice-gather` refuses an unusable corpus out loud rather than mining it
- [ ] `/voice-draft` derives per population and per register, and ships no
      floors
- [ ] `/voice-check` gates nothing
- [ ] Each skill names its own evidence level where the user will see it
- [ ] The operator builds his casual register through the workshop rather than
      by conversation — the test S0001 names

# Out of scope

- The casual and research craft skills. The workshop makes profiles; the
  register skills that read them belong to the library.
- Exemplar retrieval ([T0017](T0017-experiment-population-matched-exemplar-retrieval-versus-a-described.md)),
  which would change `/voice-draft`'s shape if it wins.

# Log

# Log

## 2026-11-10 — `/voice-harvest` built first, deliberately

162 lines. It leads with the rule that makes it work — ask what is wrong, never
which is better — and gives the measurement rather than asserting the principle:
α̂ = 0.57 and 0.65, p < 10⁻¹⁴, on human raters, so a preference ranking walks a
voice toward generic model prose while every marker stays green.

Everything in it is a thing that went wrong once. Verify briefs mechanically,
because the first one leaked 10 of 13 headings. Generate with a fresh writer,
because a session holding the profile cannot write a clean control. Normalise
the rendering, because leaving link syntax intact handicapped an arm in the
trials it won. Check whether a defect came from the brief before blaming the
writer, because three did. Separate spoken register from written, because
feedback arrives in speech.

Two sections carry what the day actually taught. **When a rule contradicts the
profile** — twice a person rejected prose that followed their own profile's
rule, and both times the rule was right and unconstrained rather than wrong, so
the instruction is to ask what separates this instance from the ones they like.
And **What this cannot do**, which states plainly that the harvest cannot tell
you whether a profile sounds like its owner, because people identify their own
writing at chance.

Listed in `plugin.json`. It holds no fact about any person, so it ships under
[D0013](../../knowledge-catalog/decisions/D0013-the-craft-ships-generic-and-the-voice-is.md)
like any other generic skill, and a clone has it too.
