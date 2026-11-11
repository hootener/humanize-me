---
id: T0022
type: task
title: "Build the casual register profile"
description: "A casual profile from 1,254 words of pasted Slack, with the two markers that define the register and a gaps field that says how thin it is."
status: In Progress
category: enhancement
initiative: voice
blocked_by: []
spec: ../../knowledge-catalog/specs/S0001-the-voice-workshop.md
timestamp: "2026-11-10"
tags: []
---

# What to build

A casual register profile for the operator, and the first real exercise of
[S0001](../../knowledge-catalog/specs/S0001-the-voice-workshop.md)'s workshop —
gather, draft, harvest — on a register that did not exist.

# Acceptance criteria

- [x] A corpus whose authorship is proven, not assumed
- [x] Privacy handled at gathering time, not after
- [x] A profile whose markers were measured rather than reasoned
- [x] A `gaps:` field stating what the corpus does not cover
- [x] A harvest run against it, with the named defects encoded

# Out of scope

- A `voice-casual` craft skill. The workshop makes profiles; the register
  skills are the library's half and casual's is still a placeholder.
- The research register.

# Log

# Log

## 2026-11-11 — gathered, drafted, harvest generated

**Gathering went wrong twice before it went right**, which is the whole reason
`/voice-gather` now leads with *prove they wrote it*.

The first pull aimed at casual was 209 GitHub comments, **208 of them from
2026** — the operator's agent-assisted period. Em-dashes in 67%, bold headers in
42%, literal `Co-Authored-By: Claude` in 7%. 30,739 words of agent prose, one
filter from his own voice profile. The operator supplied the fix himself:
anything before August 2025.

The re-pull returned 224 comments of which **136 were a coverage bot** posting
under his account. What survived — 88 comments, 7,612 words — turned out to be
*professional* in warrant, not casual, and went to the other register as
[E0012](../../knowledge-catalog/reference/E0012-unedited-professional-writing-contradicts-three-absolutes-in-the.md).

So casual rests on **1,254 words of Slack DMs**, pasted in two batches. His
turns only, third-party names scrubbed, raw threads deleted after measuring per
[D0017](../../knowledge-catalog/decisions/D0017-writing-reached-through-mcp-is-distilled-in-flight.md) —
two friends who did not consent to any of this.

**Two markers define the register**, and neither appears anywhere in his
professional writing in either mode: messages start lowercase (40 of 73) and
stop without terminal punctuation (63 of 73). The inconsistency is itself the
marker, so the profile warns that a mechanical pattern would read as fake.

**Casual sentences are longer, not shorter** — median 23.5 against 15–22
published and 13 unedited, measured identically on both batches. Casual means
unplanned, not clipped. Reasoning rather than measuring would have had this
backwards, which is now the third time that has been true this week.

Harvest generated and awaiting judgement: six passages, 735 words, content drawn
from things that happened today so the operator judges voice rather than
accuracy. No held-out casual exists to calibrate against, and the page says so.

**A fourth measurement artefact**, caught before reporting: sentence medians of
35 to 129 were the splitter treating each unpunctuated message as one sentence.
Words-per-message is the right measure — 14.1 generated against 17.2 corpus.

## 2026-11-11 — harvest run: 28 rules from six passages

Best yield of any round. Six passages produced **28 rules, eleven of them high
severity**, against eleven from eight passages in the professional harvest.

**Three rules arrived in both registers and forced an architectural change.**
The head noun is never implicit, now at five confirmations across two registers.
A vague abstraction gets replaced by a precise phrase. And no trailing weak
phrase — where the casual instance *settled* an ambiguity the professional
profile had recorded and could not resolve, because his two professional
examples disagreed on whether the rule was about prepositions specifically. "On
the way through" is adverbial and he cut it for the same reason, so the rule is
trailing weak phrases generally.

That is [D0024](../../knowledge-catalog/decisions/D0024-rules-true-in-more-than-one-register-live.md):
cross-register rules live in `common.md`, loaded alongside the register profile,
with the register winning on conflict. The shared layer was in the first design
sketch for this project and was never built, because until now nothing had
earned a place in it. Seven rules now have.

**Two defects were mine, not the generator's.** The lowercase marker was
measured on *message* starts and the generator extended it to sentence starts
inside a message; he queried it twice, in two passages, both times as a
question. And the generator drifted British across three consecutive passages —
"unlabelled", "realising", "in amongst" — with nothing in the profile saying
not to. Both are now stated.

**One finding cannot be verified**, and the reason is structural. The
post-full-stop capitalisation rate cannot be re-measured because the corpus was
deleted after measuring, per
[D0017](../../knowledge-catalog/decisions/D0017-writing-reached-through-mcp-is-distilled-in-flight.md).
His two queries are the evidence and will have to be. In-flight-only handling
means findings arrive after the data is gone, which D0017's consequences do not
currently mention.

**He named the failure mode better than the project had:** *"You've thrown a
dart and hit the target, but not the bullseye."* Several rejected lines were the
right move executed by someone else — and he rejected a domestic metaphor while
his corpus is full of domestic metaphors. The instinct is right, the instance is
wrong, and no profile here can yet tell them apart.

**And he called this project's central formulation "too claudy."**
[D0014](../../knowledge-catalog/decisions/D0014-registers-are-organized-by-burden-of-proof-not.md)
defines registers by "what a claim has to rest on". His version: *"three
different levels of proving it or showing your work."* The taxonomy can be right
while its wording is unusable in the product.

## 2026-11-11 — second harvest: 25 rules, and the defects changed kind

Six new passages on a deliberately wider range of subjects. **25 rules**, and
the three mechanical corrections from round one all held: lowercase message
starts went from 46 of 52 to **0 of 40**, British spellings from three passages
to **none**, em-dashes and semicolons stayed at zero.

**The defects moved from structure to rhythm.** Round one found verbless
fragments, flat signoffs, bare demonstratives and jokes built on numbers. Round
two found three moves used **too often** — foreshadowing, paired clipped
sentences, and the asyndetic triplet — none of which he called wrong. That is
[D0026](../../knowledge-catalog/decisions/D0026-every-move-in-a-profile-carries-a-frequency.md):
every move now carries a rate, and rates are counted across the whole batch
because his strongest complaint was explicitly cross-passage.

**He resolved a contradiction in his own feedback.** Clipped sentences were
overused in P1 and P2 and praised in P5. The difference is the setup: *"a very
short, sort of deprecating humorous sentence after a long sentence, so the flow
is really nice."* A short line lands a long one; a pair of them has nothing to
land against. That is the condition the short-landing rule had lacked through
four confirmations, and it is now in `common.md`.

**The implicit-referent rule reached seven confirmations**, including one inside
a joke — "and now it whistles" could only refer to the sixteen-year-old, so the
punchline failed on grammar before it failed on comedy.

**One passage was judged good as a whole**, the first in twelve: *"that's
actually a pretty good paragraph."* One bad clause, one long sentence, four
endorsed lines.

Five endorsed punchlines now, five for five, identical in construction every
time: self-directed, landing the passage, containing no number.
