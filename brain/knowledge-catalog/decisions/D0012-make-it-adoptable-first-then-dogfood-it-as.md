---
id: D0012
type: decision
title: "Make it adoptable first, then dogfood it as an end user"
description: "The library is made installable before the operator's own voice setup is built, and that setup is then built through the published install path."
timestamp: "2026-11-08"
tags: [sequencing, adoption, imported]
status: draft
resource: "operator utterance, 2026-11-08, in the session that opened this project"
serves: ../goals/G0002-humanize-me-installs-into-another-project-in-one.md
invariant: "The operator's own voice setup is built through the same install path an outside project would use."
constrains: [skills]
---

# Context

Reconstructed from the operator's own words in an earlier session. It arrived
sideways — as the free-text note on an answer to a question about something
else, which is why it is recoverable at all. Quoted verbatim:

> "the goal here is to make this an adoptable project, then we'll use the
> adoptable version to make our own voice setup, like any other end user would"

The force is the ordering. Both halves of the work are real, and doing them in
the other order is the obvious temptation: the voice skills are the interesting
part, and the packaging feels like chores.

# Decision

Adoptability comes first. Once the library installs, the operator's own voice
setup is built by installing it the way an outside project would, rather than
by working inside the tree.

# Alternatives

- **Build the voice setup in-tree first, package it afterwards** — rejected:
  a setup built in-tree exercises paths no end user has, so the install stays
  untested in exactly the places it is most likely to be broken, and the first
  real adopter finds them instead of the operator.

# Consequences

- The install path is the operator's own path, so a defect in it costs them
  directly and gets found early.
- Voice work that would be easier to do in-tree waits, or gets done through
  the install and the friction is treated as a finding about the install.

# Log

Still `draft`. This is a reconstruction from a transcript, accepted by the
operator for the record but not yet confirmed as the standing wording.
