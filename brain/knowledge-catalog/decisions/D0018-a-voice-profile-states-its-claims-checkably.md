---
id: D0018
type: decision
title: "A voice profile states its claims checkably"
description: "A profile asserts what it can in countable form and records how and when it was verified, so a thin register is visible as thin instead of reading as settled."
timestamp: "2026-11-09"
tags: [voice, profile, verification]
status: amended
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

# Amendment — 2026-11-10

*The decision stands: a profile must state its claims checkably and record how
it was verified. What it got wrong is the weight, and the silence about which
population a check is good for.*

**Markers are diagnostics, not a gate.** The original text treats countable
markers as the mechanical half of verification, and three runs have now
contradicted that reading:

- A document passed **8 of 8 markers** and the operator rejected it as an
  impression of his voice
  ([E0006](../reference/E0006-the-operator-rejected-a-profile-that-passed-every.md)).
- Marker ranges inherit the genre of the corpus they were measured on, so a
  profile built from blog prose fails an instructional document for reasons
  that are not voice
  ([E0005](../reference/E0005-markers-are-genre-sensitive-and-the-checker-must.md)).
- A marker can be **unsatisfiable by construction**: the post-mortem brief
  mandates six lists, putting bullet share at 44% against a `bullet_share_max`
  of 0.30 before a word is written.

A failing marker is now a question to ask, never a verdict to issue. Nothing may
be gated on one.

**A verification claim must name the population it covers.** Nine blind trials
split cleanly: the profile beat a no-guidance control **3/3 on headings and 0/6
on prose**, Fisher p = 0.012
(E0009).
Pooled across populations the effect is invisible. "Verified" without a named
population is therefore not a checkable claim, which is
[D0021](D0021-a-profile-is-derived-per-text-population-not.md) applied to the
`verified:` field rather than to the profile's body.

**The author is not a general-purpose instrument, and the profile must say so.**
The original assumed the held-out comparison was the strong check and the
operator the ultimate judge. He identified his own writing at **exactly chance**
(3/9) and ranked his own published prose **last in 4 of 6 prose trials**. He
discriminates on headings and does not on prose excerpts. This is
E0007's
r = 0.244 — the published correlation between an author's own judgment and the
best authorship metric, n = 81, pre-registered — reproduced here on a sample of
one.

So a `verified:` field records **who or what judged, on which population, and
how many trials**, and a profile verified only by its author's reaction to prose
is recorded as weakly verified rather than as verified.

**What does not change.** A profile still states its claims countably wherever
a claim can be counted, still records its provenance and its date, and still
says what has *not* been checked. The original paragraph on holding samples back
stands, and the held-out diff remains the only check in this design that has
ever caught anything.
