---
id: G0002
type: goal
title: "humanize-me installs into another project in one step"
description: "Another project can take this library's voice skills and have them in force without reading how the library is built."
timestamp: "2026-11-08"
tags: [adoption, voice, skills]
status: active
---

# Goal

Someone with an unrelated repository can drop humanize-me's voice skills into
it and have an agent in that repository write human-facing prose differently —
without first understanding how humanize-me is put together.

# Why

The voice work and the packaging are separable, and the operator has settled
the order between them: make it adoptable first, then use the adopted version
to build their own voice setup "like any other end user would"
([D0012](../decisions/D0012-make-it-adoptable-first-then-dogfood-it-as.md)).

Adoptability first is what makes that dogfooding real. A voice setup built
in-tree would be exercised through paths no end user has, so the install
would stay untested exactly where it is most likely to be wrong.

# Signals

- A project that has never seen this repository installs the skills and its
  agent's human-facing prose changes, with no step that required reading
  humanize-me's internals.
- The operator's own voice setup is built through the adopted path, not in-tree.
- The install instructions are followed by someone who did not write them,
  and nothing has to be improvised.
