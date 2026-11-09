---
id: D0011
type: decision
title: "Only prose with a human reader is in scope"
description: "The voice skills govern prose written to be read by a person; text written for another agent to consume is explicitly out of scope."
timestamp: "2026-11-08"
tags: [scope, voice, imported]
status: draft
resource: "~/.claude/projects/-Users-hootener-Source-hootener-humanize-me/fd429e6f-6113-4db7-b8d7-43a91509d077.jsonl (operator utterance, [typed], via bin/utterances)"
invariant: "A voice skill in this library applies only where the output has a human reader."
constrains: [skills]
---

# Context

Reconstructed from the operator's own words in an earlier session, not written
at the time. Quoted verbatim:

> "this repo is intended to be a repository of skills that we'll include into
> other projects to help coding agents sound less like coding agents and more
> like a human when they're writing prose _intended to be ingested by humans_.
> We do not care about prose that will be consumed by agents."

The force is that an agent writes a great deal of text, and most of it is read
by another agent — tool arguments, structured output, intermediate notes.
Treating all of it as prose to be humanized would make the library both
enormous and wrong, since agent-facing text benefits from exactly the
flat explicitness this library is trying to remove.

# Decision

A voice skill in this library applies only to prose with a human reader.
Text written to be consumed by another agent is out of scope and does not need
to sound like anyone.

# Alternatives

- **Govern all prose an agent emits** — rejected by the operator in the same
  breath as the scope was set: "We do not care about prose that will be
  consumed by agents."

# Consequences

- Every skill in this library has to be able to say who its reader is, and a
  skill that cannot is probably the wrong shape.
- Agent-to-agent output is left alone deliberately, so its flatness is not a
  defect this project is obliged to fix.

# Log

Still `draft`. This is a reconstruction from a transcript, accepted by the
operator for the record but not yet confirmed as the standing wording.
