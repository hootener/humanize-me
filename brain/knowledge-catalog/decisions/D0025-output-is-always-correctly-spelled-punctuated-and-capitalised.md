---
id: D0025
type: decision
title: "Output is always correctly spelled, punctuated and capitalised"
description: "A corpus records how someone types; the library produces how they write. Mechanical artefacts of fast or informal typing are observed, recorded, and never reproduced."
timestamp: "2026-11-11"
tags: [voice, craft, output, registers]
status: active
serves: ../goals/G0004-structure-sounds-like-the-operator-and-prose-is.md
invariant: "Prose produced by this library is correctly spelled, punctuated and capitalised in every register, whatever the corpus shows."
constrains: [skills, voice/profile]
---

# Context

The casual profile's two most distinctive measurements are that the operator's
Slack messages start lowercase (40 of 73) and end without terminal punctuation
(63 of 73). They are the clearest signal separating casual from every other
register he writes in, and they were written into the profile as features to
reproduce.

A generator then applied the lowercase rule to sentence starts *inside* a
message, and he queried it twice. Pressed on the general case, he settled it:

> no matter what the voice is, output run through Humanize Me should always have
> proper grammar and punctuation, etc.

The measurements are correct. The inference from them was wrong. Those
artefacts are what happens when a person types quickly into a chat box, and a
tool that reproduces them is imitating the **typing**, not the **writing**.

The same error sits in the professional profile, which notes that his unedited
comments contain typos and that smoothing them to publication finish is "its own
kind of wrong". Half of that is right — the register should not be inflated to
published polish — and half invites reproducing mistakes.

# Decision

**Prose produced by this library is correctly spelled, punctuated and
capitalised, in every register, regardless of what a corpus shows.**

A corpus records how someone types. The library produces how they write. Where
those differ the writing wins, because a reader receiving generated text did not
watch it being typed and has no reason to read sloppiness as intimacy.

Mechanical production artefacts are **observed and recorded in the profile as
not-to-be-reproduced**, not silently dropped. A reader of the profile should be
able to see that the measurement was taken and that the decision not to use it
was deliberate.

What this covers: capitalisation, terminal punctuation, spelling, typos,
doubled words, and dropped articles where they were dropped in haste.

What this does **not** touch, because these are voice and not accident:
contraction rate, sentence length, fragments used deliberately, informal
diction, profanity, how a message is broken into parts, or the absence of
semicolons.

# Alternatives

- **Reproduce the artefacts faithfully** — rejected by the operator directly.
  It is also the reading that makes a voice profile a liability: the more
  accurately it imitates fast typing, the worse the output looks to anyone who
  did not write it.
- **Drop the measurements from the profile** — rejected: they are true, they
  were expensive to get, and a later reader finding lowercase message starts in
  a corpus should be able to see that this was already noticed and decided
  rather than missed.
- **Let each register decide** — rejected: the operator stated it as a blanket
  rule, and a per-register answer would mean the question gets re-litigated
  every time a register is built.

# Consequences

- The casual profile's two headline markers move from "reproduce this" to
  "observed, do not reproduce". They stay in the file with the measurement
  intact.
- The professional profile's note that typos survive in unedited writing is
  corrected the same way.
- A general craft rule goes in the register skills, where it reaches adopters
  who never build a profile at all.
- **This is a new category the profile format does not have**: a measurement
  that is accurate and must not be applied. It needs a place of its own, beside
  `markers` and `Unstable — do not assert`.
- The casual register loses its two most distinctive reproducible markers, which
  makes an already thin profile thinner. What remains is sentence rhythm,
  diction, message segmentation and humour — all of which are voice rather than
  typing, and all of which are what should have been there anyway.
