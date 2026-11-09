---
id: T0014
type: task
title: "License the project MIT and complete the plugin manifest"
description: "The repository carries an MIT LICENSE scoped to its own work, and plugin.json asserts the licence now that there is a file backing the claim."
status: Testing
category: enhancement
initiative: voice
blocked_by: []
timestamp: "2026-11-09"
tags: [plugin, licensing, release]
---

# What to build

Someone who installs or forks this repository can tell what they are allowed to
do with it, and the plugin manifest's `license` field is backed by a file
rather than asserted.

[T0011](T0011-ship-the-plugin-skeleton-so-the-library-installs.md) deliberately
omitted `license` from `plugin.json` because there was no LICENSE file, and
recorded that it needed deciding before a release. The operator has decided:
MIT.

# Acceptance criteria

- [x] `LICENSE` at the repository root, MIT, naming the copyright holder and
      year
- [x] The file holds the licence text and nothing else, so licence detection
      reads it
- [x] `plugin.json` carries `"license": "MIT"`
- [x] The README states what the licence does and does not cover

# Out of scope

- A git remote, and the `repository` and `homepage` fields that depend on one.
  Still open from
  [T0011](T0011-ship-the-plugin-skeleton-so-the-library-installs.md).
- Chasing the brain template's upstream licence. Noted below; not this task's
  job to resolve.

# Log

## 2026-11-09 — licensed, and scoped on purpose

MIT, copyright Eli Hooten, 2026. `LICENSE` holds the licence text alone —
GitHub and most tooling parse that file to detect a licence, and prepending a
scope note would have broken detection. The scoping lives in the README
instead.

**The scope is narrower than the repository.** `brain/` is forked from an
upstream template at the revision in
[config.md](../../config.md), and that upstream carries no LICENSE file and no
licence statement anywhere — checked by searching for a licence file and for
the words in `README.md`, `INIT.md` and `config.md`. Its terms are therefore
unstated, and they are its author's to give. MIT-licensing it here would assert
a grant the operator is not in a position to make, so the README says the
licence covers this repository's own work — the register skills, the manifests,
the README and the project record — and not `brain/bin/`, `brain/skills/` or
the scaffolding.

This is [D0001](../../example/knowledge-catalog/decisions/D0001-claims-must-be-checkable.md)
on a claim that happens to be legal rather than technical: a licence file is a
claim about what a reader may do, and one that overreaches costs them more than
silence would.

Worth chasing with the template's author, since the template exists to be
adopted ([G0001](../../example/knowledge-catalog/goals/G0001-a-brain-others-can-adopt.md))
and an adopter cannot redistribute what has no stated terms. Not a blocker for
this project, which is not redistributing the brain.
