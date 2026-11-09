---
id: T0002
type: task
title: Add --owner and --mine to bin/status, and owner inheritance from plan to spec
description: "Add --owner and --mine to bin/status, and owner inheritance from plan to spec"
status: Ready for Development
category: enhancement
initiative: formalize
blocked_by: []
timestamp: "2026-11-07"
tags: [brain, formalize]
---

# What to build

Ownership attaches at Approach and above and is inherited downward; a task's
owner is its plan's owner unless overridden. Claims already cover *who is on it
now*, so no `assigned_to` field is added — a field duplicating a claim will
drift.

Must not make solo use heavier: with no `owner:` anywhere, every flag is a
no-op and the output is unchanged.

# Acceptance criteria

- [ ] `bin/status --owner <name>` filters to nodes owned by that team or person
- [ ] `bin/status --mine` resolves the current worker name the way a claim does
- [ ] An owner is inherited from the task's spec, and from that spec's plan, unless set locally
- [ ] With no `owner:` set anywhere, output is byte-identical to today's

# Out of scope

- Anything not named in the acceptance criteria above

# Log
