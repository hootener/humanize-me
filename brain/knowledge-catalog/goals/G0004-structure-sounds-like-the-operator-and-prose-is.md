---
id: G0004
type: goal
title: "Structure sounds like the operator and prose is prose they would sign"
description: "Fidelity is the target where the operator can detect their own voice, and endorsement is the target where they cannot — because the measurement says those are different populations."
timestamp: "2026-11-10"
tags: [voice, registers, goal]
status: active
---

# Goal

An agent writing for a human reader produces:

- **structure the operator recognises as theirs** — headings, section shape, how
  a piece is cut up. Fidelity is the target here, and it is achievable.
- **prose the operator would put their name on** — built from defects they can
  name, not from what they prefer in a blind comparison.

This replaces [G0003](G0003-an-agent-writes-human-facing-prose-in-the.md), which
asked for one thing where the measurement found two.

# Why

G0003 asked that generated prose sound like the operator, and set as its signal
that *"a reader who knows the operator's writing, shown generated prose
alongside their real writing, cannot reliably sort them."*

Nine blind trials later, the operator could not sort them — he identified his
own writing at exactly chance and ranked his own published prose last in four
of six prose trials. **The signal was satisfied and it meant nothing.** A goal
whose success condition can be met by the writer failing to recognise himself
was measuring the wrong thing.

What the same trials did find is a split. On headings the profile beat a
no-guidance control 3 of 3 and the operator ranked his own text first or second
every time. On prose it beat it 0 of 6, and he preferred generated text to his
own. Fidelity is detectable in one population and not in the other, so one
target cannot serve both.

The prose half is deliberately **not** "prose the operator prefers". A blind
preference is the wrong instrument, and
[D0022](../decisions/D0022-the-preference-signal-is-named-defects-never-blind.md)
sets out why: the measured bias that flattens model output flattens human
raters too, so optimising on a preference ranking would walk this library
toward the generic prose it exists to remove.

# Signals

- **Structure**: shown only the headings of a generated piece and of their own,
  the operator picks their own, or prefers the generated set for a reason they
  would defend in writing.
- **Prose**: the operator sends a generated passage without editing it, to a
  real reader, under their own name.
- A defect the operator names once does not recur. The catalogue of named
  defects grows and the repeat rate falls.
- Neither half is judged by a blind "which sounds more like me" ranking of
  prose, that having been measured as uninformative
  ([D0018](../decisions/D0018-a-voice-profile-states-its-claims-checkably.md),
  as amended).
