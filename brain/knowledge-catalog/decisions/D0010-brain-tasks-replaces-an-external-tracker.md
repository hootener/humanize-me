---
id: D0010
type: decision
title: "brain/tasks replaces an external tracker"
description: "The brain's task files are the only tracker this project has; nothing is mirrored to GitHub Issues."
timestamp: "2026-11-08"
tags: [brain, tracker, process]
status: active
serves: ../goals/G0002-humanize-me-installs-into-another-project-in-one.md
invariant: "A unit of work on this project exists as a file under brain/tasks/ and nowhere else."
constrains: [brain/tasks, brain/config.md]
---

# Context

`/brain-init` asks where issues live and whether `brain/tasks/` should mirror
that or replace it. This project has no external tracker in use yet: the
repository has no commits and no issues, so there is nothing to mirror and the
question is genuinely open rather than inherited.

The forces are that a mirror has to be kept in step by hand, and that the
blocking edges `/to-tasks` writes only mean anything where the tool can read
them.

# Decision

`brain/tasks/` is the tracker. Work on this project is a task file in the
brain, and there is no second system holding the same ticket.

# Alternatives

- **GitHub Issues as canonical, `brain/tasks/` mirroring it** — rejected: two
  places holding the same ticket have to be kept in step by somebody
  remembering to, which is the class of upkeep this brain exists to replace
  with a tool.
- **GitHub Issues replacing `brain/tasks/`** — rejected: the lineage edges
  would then live outside the brain, so `bin/status`, the claimable frontier
  and the forward walk would all go quiet. The tracker would work and the
  thing that makes the tracker worth having would not.

# Consequences

- `config.md` records `tracker: brain/tasks`.
- `bin/status` and `bin/reconcile` are the whole picture of outstanding work;
  there is nowhere else to check.
- If this project ever takes outside contributors, this decision is the one to
  revisit first — an external contributor cannot file a task they cannot push.
