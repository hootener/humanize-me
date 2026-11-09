---
id: T0001
type: task
title: Teach bin/relevant to defer to bin/constraints once decisions declare what they govern
description: "Teach bin/relevant to defer to bin/constraints once decisions declare what they govern"
status: Ready for Development
category: enhancement
initiative: formalize
blocked_by: []
timestamp: "2026-11-07"
tags: [brain, formalize]
---

# What to build

`bin/relevant` prints **every** decision on every call, because its own
docstring admits term matching misses the one that matters. That backstop stops
working exactly when the record grows big enough to need it: four lines at
seventeen decisions, noise at eighty.

`bin/constraints` now answers the same question by lookup instead of guess —
see [D0005](../../knowledge-catalog/decisions/D0005-intent-layer-wiring.md).
Retire the backstop once enough decisions declare `constrains:`.

# Acceptance criteria

- [ ] `bin/relevant` no longer prints the full decision index unconditionally
- [ ] It prints the count of decisions declaring no `constrains:`, since those can never match a diff
- [ ] `/grill-change` runs both tools and the guidance in its step 1 still holds

# Out of scope

- Anything not named in the acceptance criteria above

# Log
