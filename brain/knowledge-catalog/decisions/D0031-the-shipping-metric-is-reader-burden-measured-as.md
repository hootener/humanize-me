---
id: D0031
type: decision
title: "The shipping metric is reader burden, measured as work the reader does"
description: "The project's claim is that prose is cheaper to read and edit, not that it sounds like someone; the metric is editing effort and named defects, and readability formulas are a guard-rail that must never become a target."
timestamp: "2026-11-12"
tags: [readability, metrics, goals, method, release]
status: active
serves: ../goals/G0004-structure-sounds-like-the-operator-and-prose-is.md
invariant: "A claim shipped about this project is stated in terms of work the reader does, and no readability formula is ever used as an objective."
constrains: [experiments, readme, skills]
---

# Context

Every trial so far has asked a version of *does this sound like him?* That
question is hard in a way the literature has not solved: the best published
style metric correlates with an author's own judgement at r = 0.244, and in
this project's own trials he identified his own prose at chance and ranked it
worst of three arms on average
([E0008](../reference/E0008-the-profile-did-not-beat-the-control-and.md)).

Meanwhile the README does not actually promise that. It promises prose that is
**"less exhausting to read"** and carries **"a much lower editing burden"**.
Those are claims about the reader's work, not about resemblance, and the
project has never measured either one.

So the metric was being chosen against the wrong question. Reader burden is
both what is claimed and far more tractable than voice fidelity.

# Decision

**Ship against reader burden.** A public claim about this project is stated as
work the reader does, and is backed by one of these:

| tier | measure | what it is for |
|---|---|---|
| primary | **edit distance to send** — give a person the draft and the brief, ask them to make it sendable, measure what they changed | the literal README promise, "lower editing burden" |
| workhorse | **named defects per 100 words** — the harvest question, scored between arms instead of used as a tuning loop | cheap, already the only signal with a result behind it ([E0011](../reference/E0011-eight-defect-harvest-passages-produced-nine-rules-where.md)) |
| aspirational | **time to comprehension**, with questions confirming the text was read | the strongest version of the claim; needs readers this project does not yet have |

**A readability formula is a guard-rail and never an objective.** Flesch and
Flesch-Kincaid may be reported alongside a result to show that an arm did not
win by chopping sentences. They may not be optimised toward, cited as evidence
of improvement, or put in the README as a number that went up.

[E0015](../reference/E0015-classical-readability-formulas-rank-agent-prose-above-the.md)
is why. Every agent text in this project scores 10 to 24 Flesch points **more
readable** than the human writing it is imitating, and the best-scoring text of
all is the one written with no guidance. The formulas reward short clipped
sentences, which is the first item on the README's own defect list. Optimising
them walks directly into the failure.

# Alternatives

- **Keep voice fidelity as the headline claim** — rejected. It is not what the
  README promises, it is not what a user installs this for, and five trials
  have shown it is close to unmeasurable with the instruments available.
- **Ship against Flesch or Flesch-Kincaid** — rejected on E0015. The metric is
  inverted on this corpus.
- **Ship against an LLM judge scoring readability** — not rejected, not
  adopted. It has to be calibrated against named defects on held-out passages
  before it can be believed, and that calibration is a task, not an assumption.
- **Make no shipping claim and present the project as research** — rejected by
  the operator, who chose the tool framing for the README. This decision is
  what makes that framing honest.

# Consequences

- **The shipped craft skill becomes the first thing to test**, since it is what
  a stranger installs and it has no trial behind it at all. Craft against
  no-craft, scored by named defects per 100 words.
- The voice profiles are now instrumental rather than the point, and **they may
  lose**. If a profile does not reduce reader burden, that is a result and it
  gets reported. [G0004](../goals/G0004-structure-sounds-like-the-operator-and-prose-is.md)
  keeps fidelity as its own goal for the workshop half of the project; this
  decision governs what is claimed publicly.
- Both primary measures need a reader who is not the operator. The judge
  bottleneck stops being a nuisance and becomes the thing that gates the
  project's main claim.
- Readability formulas stay in the toolkit as a gaming check, which means every
  experiment reporting a burden result should report them too.
