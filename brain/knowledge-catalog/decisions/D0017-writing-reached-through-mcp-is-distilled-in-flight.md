---
id: D0017
type: decision
title: "Writing reached through MCP is distilled in flight and never stored"
description: "Mail and documents read through an integration are observed and turned into profile assertions in the session that reads them; no copy of the personal text is written to disk."
timestamp: "2026-11-09"
tags: [voice, corpus, privacy, mcp]
status: active
serves: ../goals/G0003-an-agent-writes-human-facing-prose-in-the.md
invariant: "Personal text reached through an integration is never written to disk, and a profile built that way records that its samples are gone."
constrains: [voice/corpus, voice/profile]
---

# Context

Not all of the operator's writing is a file they can file. The most useful
casual corpus anyone has is their sent mail, and it is reachable live through
an integration rather than as a folder — the operator's framing was "go look at
these emails."

The obvious shape is an ingest step: pull the threads, strip quoted replies and
signatures, write plain text into `voice/corpus/casual/`, and gitignore it.
That is reproducible, re-runnable, auditable, and keeps every later check
working.

It also means the operator's mail is sitting in a working directory, where a
gitignore is the only thing between it and a commit, and where it will be
picked up by backups, search indexes and every agent that reads the tree
afterwards. The operator weighed this and chose the other way.

# Decision

Writing reached through an integration is read, observed and distilled within
the session that reads it. Observations go into the profile. No copy of the
personal text is written to disk — not raw, not extracted, not redacted.

A profile built this way records that its samples are gone, so a later reader
knows which of its claims can still be rechecked
([D0018](D0018-a-voice-profile-states-its-claims-checkably.md)).

# Alternatives

- **Materialize as gitignored plain text** — rejected by the operator: a
  gitignore is the only safeguard, and the extracted mail outlives the reason
  it was fetched.
- **Materialize with names, addresses and figures stripped** — rejected: it
  keeps most of the voice signal and reduces the exposure rather than removing
  it, while mangling some samples and losing how the operator writes about
  specific things. The exposure is the part the operator wanted gone.

# Consequences

- A re-run means re-reading the mail. There is no cached corpus to rebuild
  from, and the integration has to be connected again.
- Countable markers survive this intact: they are measured while reading and
  asserted in the profile, and they are checked thereafter against *generated*
  output, which needs no samples.
- A held-out comparison against the real writing can only run inside the
  session that has access. It becomes a dated attestation rather than a
  repeatable check.
- The casual register will therefore be the least verifiable one, since it is
  the register most likely to come from mail. The profile states this rather
  than hiding it.
