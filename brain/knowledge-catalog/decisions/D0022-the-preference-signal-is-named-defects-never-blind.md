---
id: D0022
type: decision
title: "The preference signal is named defects, never blind rankings"
description: "What the library learns from the operator is defects they can name and defend; a blind preference ranking is rejected as a training signal because the bias it carries points at the generic prose this project exists to remove."
timestamp: "2026-11-10"
tags: [voice, preference, method, evaluation]
status: active
serves: ../goals/G0004-structure-sounds-like-the-operator-and-prose-is.md
invariant: "No artifact in this library is built or tuned from a blind preference ranking; the input is a defect the operator named."
constrains: [voice/profile, skills]
---

# Context

Nine blind trials established that the operator prefers generated prose to his
own, ranking his own published writing last in four of six prose trials and
identifying it at exactly chance (E0009). The obvious move is to treat that
preference as the target and tune toward it. He raised it himself: *"If I prefer
generated prose do we use how we ranked to build skills to generate prose for
me?"*

The force against it is a measurement already in this brain and not previously
connected to the result. *Verbalized Sampling* (arXiv 2510.01171, in E0007)
attributes model mode collapse to **typicality bias in the preference data**:
annotators prefer text with higher base-model log-probability beyond task
correctness. Decomposed with a Bradley-Terry model over 6,874
correctness-matched pairs, the typicality coefficient is **α̂ = 0.57 ± 0.07 and
0.65 ± 0.07, both p < 10⁻¹⁴**.

That bias was measured on **human raters**. The operator is a human rater. His
blind preference for generated prose is the predicted output of the bias, and
treating it as ground truth would point this library at the same attractor the
bias produced in the models — the "average, generic tone" diagnosed in
2509.14543, which is the thing the library exists to remove.

The reasons he gives are different in kind. "The bullet points are very long"
and "that heading names two things" are specific, articulable and defensible on
reflection. Two such remarks produced two countable candidate rules. Nine
rankings produced p = 0.508 and nothing to build.

# Decision

The library learns from **defects the operator names**. A blind preference
ranking is not a training signal and nothing is tuned on one.

A usable signal names something specific about a passage and would survive the
operator being asked to defend it in writing. "This one is better" does not
qualify. "The bullets run too long" does.

Rankings are retained as a **sanity check** — a run where the generated arms
sweep every trial is worth investigating — and never as the objective.

# Alternatives

- **Tune on the blind rankings** — rejected on the α̂ measurement above. It
  optimises toward typicality, which is the documented failure mode, and the
  marker block would not catch the drift because markers do not measure
  genericness.
- **Ask the operator to rank non-blind, knowing which is his** — rejected: it
  replaces typicality bias with ownership bias and measures neither voice nor
  quality.
- **Drop the operator from the loop and use a style-embedding score** —
  rejected for this purpose: E0007 puts the best such metric's correlation with
  an author's own judgement at r = 0.244 (n = 81, pre-registered), and
  [D0018](D0018-a-voice-profile-states-its-claims-checkably.md) as amended
  already confines it to a drift tripwire.

# Consequences

- Evaluation changes shape: **ask what is wrong with a passage before asking
  which is preferred**, and treat the free text as the result. The first run to
  do this produced two candidate markers from two offhand clauses.
- A defect catalogue becomes an artifact the project maintains, with a repeat
  rate as its measure — a defect named once and recurring is a failure of the
  catalogue, not of the operator.
- This bounds what [T0017](../../tasks/voice/T0017-experiment-population-matched-exemplar-retrieval-versus-a-described.md)
  can conclude. Its arms are still judged by ranking, so it can establish which
  method wins a comparison and cannot establish that the winner should be the
  target.
- The operator's attention is the scarce resource, and a reason costs about what
  a ranking costs while carrying more. The format change is free.
