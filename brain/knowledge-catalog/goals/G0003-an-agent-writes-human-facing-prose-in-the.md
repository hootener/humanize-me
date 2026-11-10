---
id: G0003
type: goal
title: "An agent writes human-facing prose in the operator's own voice"
description: "Prose an agent writes for a person to read sounds like the person who installed the library, at the right level of warrant for what the prose is doing."
timestamp: "2026-11-09"
tags: [voice, registers, profile]
superseded_by: G0004-structure-sounds-like-the-operator-and-prose-is.md
status: superseded
---

# Goal

An agent working in a project writes prose for human readers that sounds like
the operator rather than like an agent — and picks the right register for what
the prose is being asked to do, rather than writing everything at one pitch.

This is the other half of the project. [G0002](G0002-humanize-me-installs-into-another-project-in-one.md)
is about the library arriving; this is about what arriving is worth.

# Why

An agent's prose fails in a particular way, and it is not a failure of
formality. It asserts everything at the same temperature: it hedges claims that
should be stated flatly and states claims that should be hedged, because it has
no model of what a given claim is resting on. A reader notices the uniformity
before they notice any individual word.

Fixing that needs two things the library has to keep apart. One is craft, the
same for everyone — what to stop doing, and how much warrant a claim at this
pitch has to carry. The other is the operator, who is not the same as anyone
else and cannot be guessed at from first principles. Only the second needs
their writing to exist; the first is worth having on its own
([D0015](../decisions/D0015-a-voice-profile-is-optional-and-the-skills.md)).

Scope is set by [D0011](../decisions/D0011-only-prose-with-a-human-reader-is-in.md):
prose with a human reader. Agent-facing text is left alone.

# Signals

- The operator can read a passage the agent wrote and not flinch at it.
- Asked for a Slack reply and a post-mortem on the same subject, the agent
  produces prose that differs in what its claims rest on, not merely in
  whether it used contractions.
- A reader who knows the operator's writing, shown generated prose alongside
  their real writing, cannot reliably sort them.
- A register's profile says how well grounded it is, so a thin one is visible
  as thin rather than passing as settled
  ([D0018](../decisions/D0018-a-voice-profile-states-its-claims-checkably.md)).

# Superseded — 2026-11-10

Replaced by [G0004](G0004-structure-sounds-like-the-operator-and-prose-is.md).

Not because the ambition was wrong, but because the third signal above —
*"a reader who knows the operator's writing… cannot reliably sort them"* — was
**met, and meant nothing.** In nine blind trials the operator identified his own
writing at exactly chance and ranked his own published prose last in four of six
prose trials. A success condition that a writer satisfies by failing to
recognise himself is not a success condition.

The measurement also found that fidelity is detectable in structure and not in
prose, so the single target here was two targets wearing one goal's frontmatter.
