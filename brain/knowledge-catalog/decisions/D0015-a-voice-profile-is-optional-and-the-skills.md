---
id: D0015
type: decision
title: "A voice profile is optional and the skills degrade without one"
description: "The register skills do the generic job with no profile present, so installing the library costs one step and never requires gathering a corpus first."
timestamp: "2026-11-09"
tags: [voice, adoption, profile]
status: active
serves: ../goals/G0002-humanize-me-installs-into-another-project-in-one.md
invariant: "Every register skill produces useful prose with no profile present, and says which mode it is in."
constrains: [skills]
---

# Context

[G0002](../goals/G0002-humanize-me-installs-into-another-project-in-one.md)
asks that the library install in one step without the adopter reading its
internals. The architecture in
[D0013](D0013-the-craft-ships-generic-and-the-voice-is.md) puts the personal
half in a generated profile.

If the skills need that profile to function, the two pull against each other.
Installing would cost one step plus a corpus-gathering project: sorting
documents, extracting text, running a generator, reviewing output. That is not
one step, and it asks for the investment before the adopter has seen anything
work.

It also gets the value backwards. The craft half — what agent prose does wrong,
and what warrant each register owes — is most of the benefit and needs nothing
from the adopter.

# Decision

A profile is optional. With none present, every register skill does the generic
job: it writes at the register's level of warrant and avoids what agent prose
does wrong. With a profile, it also sounds like the operator.

A skill states which mode it is in rather than leaving the adopter to guess
whether their profile was found.

# Alternatives

- **Require a profile** — rejected: it makes the install one step plus a
  project, and asks for the corpus work before the adopter has evidence the
  library is worth it.
- **Ship a default profile, generic and overridable** — rejected: a profile
  describes a particular person, so a default one describes a person who does
  not exist. It would read as a voice rather than as an absence, and the
  adopter would be tuning away from someone imaginary instead of starting from
  craft.

# Consequences

- The craft in each register skill has to stand alone as prose guidance,
  reviewable with no corpus in hand.
- Profile lookup is a miss, not an error. A skill finding nothing proceeds.
- The adopter's path has a real first stop: install, use it, and gather a
  corpus later if the generic version earns it.
- This is what makes the plugin install in
  [D0019](D0019-humanize-me-ships-as-a-claude-code-plugin.md) safe, since
  user-scoped skills are present in projects that will never have a profile.
