---
id: T0004
type: task
title: Give bin/stale a per-project facts file so a host project can add a count without editing Python
description: "Give bin/stale a per-project facts file so a host project can add a count without editing Python"
status: Ready for Development
category: enhancement
initiative: formalize
blocked_by: []
timestamp: "2026-11-07"
tags: [brain, formalize]
---

# What to build

`facts()` is the right design but adding a count means editing Python, so a
host project that wants "tests" or "migrations" checked either patches the
script or goes without. Named as gap 2 in
[E0002](../../knowledge-catalog/reference/E0002-portability-findings.md).

# Acceptance criteria

- [ ] A project declares a countable fact by naming a command and a noun in a config file, not in Python
- [ ] A missing or malformed config leaves the two built-in facts working
- [ ] `bin/stale` still exits 1 when a declared count contradicts the repository

# Out of scope

- Anything not named in the acceptance criteria above

# Log
