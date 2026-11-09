---
id: D0018
type: decision
title: "A voice profile states its claims checkably"
description: "A profile asserts what it can in countable form and records how and when it was verified, so a thin register is visible as thin instead of reading as settled."
timestamp: "2026-11-09"
tags: [voice, profile, verification]
status: active
serves: ../goals/G0003-an-agent-writes-human-facing-prose-in-the.md
invariant: "Every register profile carries machine-readable markers and a dated record of how it was verified."
constrains: [voice/profile]
---

# Context

The central claim of this library is "this sounds like you," which is the
easiest kind of claim to assert and the hardest to test. A generator will
always produce something confident-looking, and an operator reading their own
profile is the worst available judge of whether it is accurate — it will feel
right because it was written to.

[D0001](../../example/knowledge-catalog/decisions/D0001-claims-must-be-checkable.md)
applies directly: a profile whose claims cannot be checked costs its reader the
thing they would have found by looking at their own writing.

Two mechanisms are available and they have different requirements. Countable
markers — sentence length distribution, banned openers, em-dash rate, bullet
ratio — can be measured in output by a script, with no model and no samples. A
held-out comparison — reserve some samples, regenerate one from its own brief,
diff against the real thing — is a much stronger signal and needs the originals
to still exist, which under
[D0017](D0017-writing-reached-through-mcp-is-distilled-in-flight.md) they
sometimes do not.

# Decision

A register profile states its claims countably wherever a claim can be counted,
in machine-readable frontmatter, and carries prose only for what genuinely
cannot be counted.

It also records its own provenance and verification: what it was built from, how
many samples, how many were held out, which checks ran and on what date. A
register verified only by markers says so. A register whose held-out comparison
cannot be re-run says that too.

The two checks are kept distinct because they survive differently. Markers are
measured once from the writing and checked forever against generated output.
The held-out comparison needs the samples and is recorded as a dated
attestation when it cannot be repeated.

# Alternatives

- **Markers only** — rejected as the whole scheme: fully mechanical and fast,
  but a passage can hit every number and still not sound like the operator.
  Kept as one of the two halves.
- **Blind comparison by the operator alone** — rejected as the whole scheme:
  honest and needs no infrastructure, but it is a hand judgment every time, so
  it cannot run unattended and cannot catch a regression. Kept as the shape of
  the held-out check.
- **No verification, tune by feel** — rejected: it is the fastest route to a
  working first version, and it leaves the library unable to tell an adopter
  whether their profile is any good, which is the failure
  [D0001](../../example/knowledge-catalog/decisions/D0001-claims-must-be-checkable.md)
  exists to prevent.

# Consequences

- The profile format has a parseable section, so it is an interface and not
  just a document.
- A checker has to exist for the markers to mean anything, and it must run with
  no model in the loop.
- The generator has to hold samples back, which costs profile quality on a
  small corpus — and a minimum viable corpus size per register is now an open
  question.
- A register's trustworthiness is readable off its own file, which is what
  lets the thin ones be treated as thin.
