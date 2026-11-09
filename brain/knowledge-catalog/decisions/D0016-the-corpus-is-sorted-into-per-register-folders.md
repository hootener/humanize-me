---
id: D0016
type: decision
title: "The corpus is sorted into per-register folders by hand"
description: "The operator files each writing sample under the register it teaches, because the filing is a judgment the generator cannot make and should not guess."
timestamp: "2026-11-09"
tags: [voice, corpus, ingestion]
status: active
serves: ../goals/G0003-an-agent-writes-human-facing-prose-in-the.md
invariant: "A corpus sample's register is declared by the operator, never inferred by the generator."
constrains: [voice/corpus]
---

# Context

A corpus is mixed by nature. A blog post, a client email and an analysis
write-up are three different registers, and they arrive as a pile of files.
Something has to decide which sample teaches which register
([D0014](D0014-registers-are-organized-by-burden-of-proof-not.md)).

The generator could classify them. It would save the operator some filing and
it would be right most of the time.

The force against it is what a misfile costs. A classification error does not
announce itself; it quietly teaches one register from the wrong samples, and the
resulting profile is wrong in a way that reads as a voice rather than as a bug.
Worse, the axis is warrant, not topic — and warrant is the harder thing to read
off a document, because a casual note about a serious subject looks like a
professional one.

# Decision

The operator sorts the corpus into one folder per register. The generator reads
`casual/`, `professional/` and `research/` and never decides which a sample
belongs to.

The filing is treated as data rather than as chore. An operator putting a
document under `professional/` is asserting "this is how I sound when I am
staking my judgment on something" — a claim about themselves that no classifier
has access to.

# Alternatives

- **The generator classifies and the operator confirms** — rejected: it adds a
  review pass over every sample, and a misfile the operator skims past poisons
  a register silently. The confirmation step is the filing, done later and
  worse.
- **Per-file front matter or sidecar tags** — rejected: it survives moving
  files and allows one sample to serve two registers, but it means editing
  every sample on the way in, and the binaries that matter most here — PDFs and
  Word documents — cannot carry front matter at all.

# Consequences

- The operator does a few minutes of filing before a first build, and the
  generator has no classification step to get wrong.
- An empty register folder is a legible state: that register has no profile and
  falls back to generic craft under
  [D0015](D0015-a-voice-profile-is-optional-and-the-skills.md).
- Writing that never lands in a folder — anything read live through an
  integration — needs its own path, which is
  [D0017](D0017-writing-reached-through-mcp-is-distilled-in-flight.md).
- Extracting text from PDFs and Word documents is now on the critical path and
  is not yet decided.
