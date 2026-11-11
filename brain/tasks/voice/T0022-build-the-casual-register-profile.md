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
- [ ] A harvest run against it, with the named defects encoded

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
