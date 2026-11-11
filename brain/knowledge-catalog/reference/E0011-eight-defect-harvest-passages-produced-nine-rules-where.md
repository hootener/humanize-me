---
id: E0011
type: evidence
title: "Eight defect-harvest passages produced nine rules where nine rankings produced one"
description: "Asking what is wrong with a passage yielded eleven usable rules from eight passages, including one confirmed three times; the operator endorsed generated prose under his own name twice and found a defect in his own published writing."
timestamp: "2026-11-10"
tags: [voice, harvest, defects, findings, method]
status: active
---

The first run under [D0022](../decisions/D0022-the-preference-signal-is-named-defects-never-blind.md),
which forbids blind preference rankings as a signal and requires named defects
instead. Eight passages, one question each: *what is wrong with this one?* No
ranking, no comparison. Six generated with the corrected skill and profile, two
of the operator's own published writing, shuffled, composition disclosed and
labels sealed.

# Yield, against the method it replaced

| | nine ranking trials (E0008/E0009) | eight harvest passages |
|---|---|---|
| operator effort | 9 judgements | 8 judgements |
| usable rules produced | **2** | **11** |
| findings later retracted | 2 | 0 |

The ranking round produced one real result — the headings/prose dissociation —
and two tool-manufactured findings that had to be withdrawn. The two rules it
did yield both came from free text the operator volunteered alongside a ranking,
not from the rankings themselves. That was the observation D0022 was built on
and this run tested it.

# The rules

Strongest first.

**The head noun is never implicit — three independent confirmations.** Two as
complaints, one as praise, across three passages, unprompted each time.

| passage | source | instance |
|---|---|---|
| P2 | **the operator's own writing** | "acute support" wanted *an acute support case* |
| P6 | generated | "those three" wanted *those three points* |
| P8 | generated | *"We'll raise those notices again"* **praised** where "raise them again" would have served |

A modifier gets its head, a demonstrative gets its noun, and where a pronoun
would do he often repeats the noun and prefers it. **No marker in the profile
could have found this.** Sentence length, contraction rate, bullet share,
semicolon rate and paragraph length are all blind to it.

**Vague abstraction where a precise noun phrase or enumeration belongs.** Not
"post notices everywhere they belong" but *"to all channels where these
uploaders can be accessed: the GitHub repository, the package manager, the
uploader's output"*. The operator named this one as the theme rather than an
instance: *"a lack of sentence-to-sentence clarity"*.

**No colon standing in for a verb.** He uses colons to introduce a list or
elaborate; never as a copula. "A request we hear often: show me the coverage"
should be *A request we hear often is "show me the coverage for this part of my
code, not for the whole repository."* His own corrected version of a different
sentence uses a colon correctly, to introduce an enumeration — the rule proved
by his own fix.

**Reported requests are quoted as speech**, in quote marks, as if someone is
saying them.

**A short declarative lands a paragraph and never opens one.** "The first phase
starts now." was rejected outright — *"Hate it. This is too clippy and it
doesn't flow well."* This is the **second failure mode of a rule the profile
already taught**: the first, in
[E0006](E0006-the-operator-rejected-a-profile-that-passed-every.md), was coining
a new claim instead of compressing an established one. Now position. The rule as
originally written constrained neither.

**One subject per heading.** **An interrogative heading only where its referent
is established** — "What happened" is acceptable in a piece that has already
named the incident and nowhere else. **Bullets have a maximum length.**
**Title Case consistent within a heading.**

**Institutional voice takes the formal verb** — *adhere to it*, not "stick to
it", when the company is speaking rather than the person. This is **a second
axis crossing [D0014](../decisions/D0014-registers-are-organized-by-burden-of-proof-not.md)'s**:
the same claim at the same burden of proof takes different diction depending on
who is speaking. D0014 is not wrong; it is incomplete.

**Avoid ending a sentence on a preposition** in professional register. Recorded
with a caveat: his two examples disagree — one ends on a preposition, the other
on a copula — so whether the rule is terminal-prepositions or trailing weak
constructions generally is unresolved, and the profile says to ask rather than
guess.

# Three results about the target, not the rules

**He endorsed generated prose under his own name, twice, blind.** P4: *"I would
be okay if my name was attached to writing in this voice."* P5, on a generated
heading set: *"almost exactly how I'd write them."* Neither time did he know
which arm he was reading, and on P4 he said so explicitly: *"I don't know if
this is something that I wrote"* — and did not need to.

That is [G0004](../goals/G0004-structure-sounds-like-the-operator-and-prose-is.md)'s
prose criterion met, stated by him unprompted, in nearly the goal's own words.

**He found a defect in his own published writing.** P2 was his. The first
instance of the head-noun rule was him objecting to his own 2023 Codecov prose.

**On that rule, the generated text beat his own published text.** P8 — generated
— was praised for the exact habit P2 — his own — was criticised for lacking.
This is the clearest demonstration available that "prose I would sign" and
"prose identical to my past output" are different targets, and that G0004 was
right to split them.

# Two limits worth stating

**Clean-versus-defective does not separate the arms.** Two of six generated
passages drew no defect; one of two of his own did. On this sample the harvest
does not discriminate generated prose from published prose, and it was not
designed to.

**Heading quality varies within the validated population.** P5 and P7 were both
generated, by the same agent, from the same profile, in the same run. P5 was
*"almost exactly how I'd write them"*; P7 drew three defects. The 3/3 headings
result in [E0009](E0009-the-profile-works-on-headings-and-not-on.md) did not
show that variance, because ranking three arms against each other cannot.

# Consequences

- Eleven rules are now in the operator's profile, in a new **Precision habits**
  section plus corrections to **Headings** and **Moves you make**.
- [D0022](../decisions/D0022-the-preference-signal-is-named-defects-never-blind.md)
  is supported on its first test: 11 rules against 2, and no retractions.
- [D0014](../decisions/D0014-registers-are-organized-by-burden-of-proof-not.md)
  needs a second axis — institutional versus personal voice — or a statement
  that it deliberately does not model one.
- A rule the profile already states can still fail, twice, in different ways.
  Stating a rule is not the same as constraining it.

# Citations

- Eight harvest responses and the sealed key, 2026-11-10, recorded before unsealing
- [T0016](../../tasks/voice/T0016-run-the-held-out-regeneration-diff-against-a.md) for the ranking round this is measured against
