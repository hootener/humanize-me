---
id: T0010
type: task
title: "Decide whether the brain ships as a Claude Code plugin"
description: "The skills half is generic and global by nature, which is what a plugin installs; the catalog half is per-project, which a plugin cannot carry. Decide whether to split them."
status: Not Ready
category: question
initiative: formalize
blocked_by: []
timestamp: "2026-11-08"
tags: [brain, formalize, distribution]
---

# What to build

A decision, not a build. Raised by the greenfield cold start, recorded in
[E0001](../../knowledge-catalog/reference/E0001-brain-in-practice.md).

The brain already splits cleanly: `bin/` and `skills/` are generic and are
the only half upstream ever changes; `knowledge-catalog/`, `tasks/`,
`plans/` and `brief/` are the project's own. A Claude Code plugin installs
the first half natively, at user scope, versioned — and cannot carry the
second at all.

Verified against a plugin installed on this machine: a repository holding
`.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` is its
own marketplace, installs to `~/.claude/plugins/cache/<marketplace>/<name>/<version>`,
and records the commit it came from. The comparable plugin ships a setup skill
whose job is writing the **per-repo adaptation layer** — exactly what
`knowledge-catalog/reference/agent-skills/` is here.

**What it would fix.** The restart would move to a harmless moment, before any
brain exists, instead of stranding the adopter between `bin/adopt` and
`/brain-init`. Updates would stop being "re-copy two directories".

**The conflict to resolve.** A plugin and `bin/adopt`'s `.claude/skills`
symlink would both supply the same skills. It is one or the other, not both.
And globally-installed skills would be present in projects with no brain,
where every one of them would fail looking for `brain/` — they would need to
notice and say so rather than error.

**The part a plugin cannot take.** `bin/` is called by path from the skills
(`brain/bin/lint`). Moving it into the plugin means the tools must locate the
brain themselves, as the commit hook already does from the git root. That is a
separate change and should not be bundled into this decision.

# Acceptance criteria

- [ ] A decision recorded either way, with the alternatives weighed
- [ ] If yes: which half ships as the plugin, what `bin/adopt` stops doing, and
      how a skill behaves in a project with no brain
- [ ] If no: how an adopter is spared the mid-install restart instead

# Out of scope

- Moving `bin/` into the plugin. Separate decision.
- Publishing to the official marketplace.

# Log

## 2026-11-08 — raised

Deliberately not decided mid-experiment: changing the install mechanism while
a cold-start test of that mechanism is running would invalidate the test.
