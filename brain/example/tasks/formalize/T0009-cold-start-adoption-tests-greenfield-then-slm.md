---
id: T0009
type: task
title: "Cold-start adoption tests: greenfield, then SLM"
description: "Have an agent that did not build this brain adopt it, twice: once into an empty project and once into a project with four years of its own conventions."
status: In Progress
category: enhancement
initiative: formalize
blocked_by: []
timestamp: "2026-11-08"
tags: [brain, formalize, adoption]
---

# What to build

Not a build. Two experiments, run by a Claude session that did **not** write
this brain, because the author is the worst available tester — the template
passes its own linter by construction, and the same blindness applies to the
person driving the port.

[T0005](T0005-add-bin-selftest-adopt-into-a-throwaway-host.md) covers the
mechanical install. What neither it nor anybody else has tested is the
**onboarding path a human and a cold agent actually walk**: README →
`bin/adopt` → `CLAUDE.md` → `/brain-init`.

**Scenario A — greenfield.** A brand-new, empty project. `/brain-init` has
nothing to import and nothing to mine, so the first goal is its only real
output. Unknown whether it degrades gracefully or reads as broken.

**Scenario B — a project with its own conventions.** Four initiatives, seven
decisions, fifty-seven tasks, two node types this brain deliberately does not
have (`intent`, `handoff`), two it deleted (`context`,
`initiative-pointer`), and **no version control at all**, so the
date-recovery advice in `/brain-init` is unavailable.

The deliverable is the friction, not the ported brain. Whatever the cold
session finds confusing, missing or wrong goes to
[E0001](../../knowledge-catalog/reference/E0001-brain-in-practice.md) and
becomes tasks from there.

# Acceptance criteria

- [ ] Scenario A run by a session with no prior context; its transcript audited
- [ ] Scenario B run the same way
- [ ] Every point of friction recorded in E0001, separated into documentation
      gaps and real defects
- [ ] Anything that turned out to be a defect has a task

# Out of scope

- Doing either port myself. That would answer a different question.

# Log

## 2026-11-08 — Scenario A under way

Predictions recorded before the run, so they can be scored rather than
reconstructed afterwards:

1. `bin/adopt` refuses on a project not yet `git init`ed, which a brand-new
   folder usually is not. The message points at `git init` or `--sibling`.
2. `/brain-init` steps 2-4 — import ADRs, seed the glossary, mine the
   transcript history — all come up empty on a new project. Untested whether
   that reads as graceful or as broken.
3. The first goal is the only substantive output. If the session does not push
   for one, the brain starts with an unterminated lineage and no tool will say
   so until something is built.
4. `example/` may be mistaken for the adopter's own content rather than a
   worked example.
