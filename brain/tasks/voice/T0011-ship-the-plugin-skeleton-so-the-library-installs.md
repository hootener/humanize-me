---
id: T0011
type: task
title: "Ship the plugin skeleton so the library installs"
description: "The repository becomes its own Claude Code marketplace, so the register skills can be installed and exercised through the path a real adopter uses."
status: Testing
category: enhancement
initiative: voice
blocked_by: []
timestamp: "2026-11-09"
tags: [plugin, adoption, distribution]
---

# What to build

Someone who has never seen this repository can add it as a marketplace,
install the plugin, and have the register skills present in every project they
open — with nothing copied into any project and no profile required.

Concretely: `.claude-plugin/plugin.json` naming the plugin and listing its
skill paths, `.claude-plugin/marketplace.json` making the repository its own
marketplace, and the three register skill directories the manifest points at.

The skills may be stubs at this point. The thing being built is the install
path, and [D0019](../../knowledge-catalog/decisions/D0019-humanize-me-ships-as-a-claude-code-plugin.md)
makes it the only one there is — so it has to work before any content written
for it can be exercised the way an adopter will meet it.

# Acceptance criteria

- [x] `.claude-plugin/plugin.json` validates and lists every skill directory
      that holds a written skill, with no path naming a directory that does not
      (amended — see Log)
- [x] `.claude-plugin/marketplace.json` present, so the repository needs no
      third-party marketplace to be installable
- [x] The three register directories exist with the names the manifest will use
- [x] Nothing is written into any host project: no `.claude/skills` symlink and
      no copied skill directory, per
      [D0019](../../knowledge-catalog/decisions/D0019-humanize-me-ships-as-a-claude-code-plugin.md)
- [x] A README section states the install command

# Out of scope

- The craft content of any register skill. That is
  [T0012](T0012-write-the-professional-register-craft-skill.md).
- The generator, the profile format and the marker checker.
- Publishing to the official marketplace. Self-hosted is the whole point.

# Log

## 2026-11-09 — built, acceptance criteria amended

`.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` written and
validated as JSON; `marketplace.json` uses `"source": "./"`, so the repository
is its own marketplace with no URL to go stale.

**Criterion amended rather than quietly satisfied.** It originally asked the
manifest to list every skill directory *that exists*, and all three to exist.
Both halves held, so the manifest would have listed `voice-casual` and
`voice-research` — which have no craft written. A stub skill that loads and
produces nothing useful is worse than an absent one, and it would have
contradicted [D0015](../../knowledge-catalog/decisions/D0015-a-voice-profile-is-optional-and-the-skills.md),
which promises every register skill produces useful prose. So the directories
exist and carry a `PLACEHOLDER.md` saying what the register is and that the
craft is unwritten, and the manifest lists only `voice-professional`. Adding a
register is one `SKILL.md` plus one manifest line.

`repository`, `homepage` and `license` are **omitted** from `plugin.json`, and
the README's install command is written as `<owner>/humanize-me`. There is no
git remote and no LICENSE file, so asserting any of them would have put an
unchecked claim in a manifest — which is
[D0001](../../example/knowledge-catalog/decisions/D0001-claims-must-be-checkable.md)
applied to packaging. Both need deciding before a first release.
