---
id: T0013
type: task
title: "Restate the hedging rules as ownership and falsifiability"
description: "The professional register skill stops legislating how much a writer hedges and requires only that judgments have a holder and confidences could be wrong."
status: Testing
category: bug
initiative: voice
blocked_by: []
timestamp: "2026-11-09"
tags: [voice, craft, registers]
---

# What to build

An agent following the professional register skill leaves a heavily hedging
writer's voice intact while still catching the unowned, unfalsifiable claim
that the register exists to fix.

Three places in `skills/voice-professional/SKILL.md` encode the old rule:

- the conflict rule in **Load the voice profile**, which says warrant beats
  profile and treats hedging as warrant
- **Hedging what you should own**, which states the prohibition as a surface
  quantity
- **Stacked hedges**, which counts qualifiers

[D0020](../../knowledge-catalog/decisions/D0020-craft-governs-ownership-and-falsifiability-a-profile-governs.md)
replaces all three.

# Acceptance criteria

- [x] The conflict rule states that craft governs ownership and falsifiability
      and that hedge quantity and wording belong to the profile
- [x] No rule in the skill counts hedges or sets a hedging level
- [x] The failing example is failed for the stated reason — no holder, nothing
      falsifiable — and not for carrying a hedge
- [x] A hedge naming what the writer is unsure of passes at any quantity, and
      the skill says so with an example
- [x] The pre-send check asks the two questions D0020 names
- [x] `voice-casual` and `voice-research` placeholders record that they inherit
      this rule before they are written

# Out of scope

- The casual and research craft. They inherit the rule, not the prose.
- The profile format. [D0020](../../knowledge-catalog/decisions/D0020-craft-governs-ownership-and-falsifiability-a-profile-governs.md)
  says hedge quantity is a profile concern; how the profile states it is the
  format spec's problem.
- [E0004](../../knowledge-catalog/reference/E0004-what-the-professional-craft-skill-could-not-say.md)'s
  other finding, that the countable half of a profile is the minority of its
  value. Unresolved and separate.

# Log

## 2026-11-09 — applied

Five edits to `skills/voice-professional/SKILL.md`:

- the conflict rule now names the two things craft asks of a claim and hands
  everything else, hedge quantity and wording included, to the profile
- *Hedging what you should own* became *Claims nobody holds, at confidences
  nobody could be wrong about*, and says outright that the failure is not the
  hedge — with the heavily hedged version of the same claim shown passing
- *Stacked hedges* became *Qualifiers that leave nothing behind*, failing the
  example for leaving no falsifiable claim rather than for carrying three
  qualifiers, and showing three qualifiers that do say something
- *Over-qualifying the obvious* became *Qualification that doesn't track the
  uncertainty* — about tracking rather than amount, so it no longer sets a level
- the pre-send check is four questions, the first two being the craft, marked
  as the ones no voice excuses

Nothing in the skill counts hedges or sets a hedging level now, checked by
grep for the old formulations.

The `voice-casual` and `voice-research` placeholders each record that they
inherit [D0020](../../knowledge-catalog/decisions/D0020-craft-governs-ownership-and-falsifiability-a-profile-governs.md)
before their craft is written, so the rule does not have to be rediscovered
twice.

One thing worth noting: the skill's opening section already stated the rule
correctly — *"a holder and a confidence you could be wrong about"* — and the
failure list contradicted it four sections later. The decision was already
latent in the skill; what was wrong was the prose written against it.
