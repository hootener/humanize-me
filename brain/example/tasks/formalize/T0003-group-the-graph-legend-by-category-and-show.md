---
id: T0003
type: task
title: Group the graph legend by category and show ids in node labels
description: "Group the graph legend by category and show ids in node labels"
status: Ready for Development
category: enhancement
initiative: formalize
blocked_by: []
timestamp: "2026-11-07"
tags: [brain, formalize]
---

# What to build

The legend lists types alphabetically, which reads as an alphabet rather than
as the model. Grouping by the four categories of
[D0002](../../knowledge-catalog/decisions/D0002-four-categories.md) makes the
graph teach the shape the way `docs/lineage.svg` does.

Node labels show the title only, so a node seen in the graph cannot be quoted
in a commit message or a journal without opening it.

# Acceptance criteria

- [ ] Legend groups type swatches under Intent, Approach, Action, Evidence, in that order
- [ ] A node's label is prefixed with its id
- [ ] `@intent` and the other three category names work as filters
- [ ] Existing `#tag`, `@type` and `@status` filters are unchanged

# Out of scope

- Anything not named in the acceptance criteria above

# Log
