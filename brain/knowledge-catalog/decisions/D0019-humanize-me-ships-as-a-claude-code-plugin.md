---
id: D0019
type: decision
title: "humanize-me ships as a Claude Code plugin and the profile lives at user scope"
description: "The library is its own marketplace and installs once at user scope; the profile sits beside it per user, with a per-register project override for a shared house voice."
timestamp: "2026-11-09"
tags: [distribution, adoption, plugin, profile]
status: active
serves: ../goals/G0002-humanize-me-installs-into-another-project-in-one.md
invariant: "The plugin is the only install path, and a register's profile is resolved from the project first and the user second."
constrains: [.claude-plugin, skills, voice/profile]
---

# Context

[T0010](../../example/tasks/formalize/T0010-decide-whether-the-brain-ships-as-a-claude.md)
asked this question of the brain and found it genuinely hard, for a reason that
does not apply here. The brain's non-generic half is **per-project** — a
catalog of one project's goals and decisions — and a user-scoped plugin cannot
carry that at all. So the brain had to decide whether to split itself.

humanize-me splits the other way. Its non-generic half is **per-person**: a
description of how one human writes. User scope is not a limitation for that,
it is the correct scope. Nearly everything else — the register skills, the
generator, the marker checker — is identical in every install.

Verified against the plugins installed on this machine rather than assumed: a
repository carrying `.claude-plugin/plugin.json` and
`.claude-plugin/marketplace.json` is its own marketplace with no third party
involved; it installs to
`~/.claude/plugins/cache/<marketplace>/<name>/<version>`; and the install
record stamps `"scope": "user"` alongside the commit it came from, so the
version in force is a fact rather than a guess.

The design before this decision put the profile inside each adopting project.
That makes the operator's voice a property of a repository, so it gets copied
into every repository they work in and drifts between them. A person's casual
voice is not a property of a project.

# Decision

The library ships as a Claude Code plugin, and that is the only install path.
There is no directory copy and no symlink into a project's `.claude/skills`.

A register's profile is resolved per register, project first:

1. `./voice/profile/<register>.md` — committed to the repository: a team's
   house voice
2. `~/.claude/voice/profile/<register>.md` — the operator's own, in force
   everywhere
3. neither — generic craft only, under
   [D0015](D0015-a-voice-profile-is-optional-and-the-skills.md)

Resolution is **per register rather than per profile**, which is what gets the
case that matters: a team commits a shared `professional.md` and `research.md`
while each member's `casual.md` stays their own. Nobody chooses between a house
voice and their own voice.

# Alternatives

- **Copy or symlink the skills into each project** — rejected: it reinstalls
  per repository, has no version record, and makes every upstream improvement a
  manual re-copy.
- **Support both the plugin and a directory install** —
  rejected on [T0010](../../example/tasks/formalize/T0010-decide-whether-the-brain-ships-as-a-claude.md)'s
  reasoning: two mechanisms supplying the same skills is a conflict rather than
  a convenience, and the adopter has to understand both to debug either.
- **Keep the profile in the project only** — rejected: the operator's voice
  then gets duplicated into every repository and drifts, and a new project
  starts with no voice despite the operator having one.
- **Keep the profile at user scope only** — rejected: it forecloses a team
  sharing a house voice through the repository, which the per-register
  resolution gets for almost nothing.

# Consequences

- [G0002](../goals/G0002-humanize-me-installs-into-another-project-in-one.md)
  is satisfied more cheaply than it was written. Its outcome was "installs in
  one step without reading the internals"; under a plugin it installs once and
  is in force in every project, so the per-project step disappears rather than
  getting smaller. The goal's wording survives the change because it names an
  outcome and not a mechanism.
- The register skills are present in projects where nobody wants them. This is
  the hazard [T0010](../../example/tasks/formalize/T0010-decide-whether-the-brain-ships-as-a-claude.md)
  raised, where a globally installed skill fails looking for something that
  isn't there. It does not bite here: under
  [D0015](D0015-a-voice-profile-is-optional-and-the-skills.md) a missing
  profile is a miss, not an error.
- The skills now update independently of the profile, so the profile format in
  [D0013](D0013-the-craft-ships-generic-and-the-voice-is.md) becomes a
  compatibility surface across versions. A format change has to keep reading
  profiles written by older generators, or say loudly that it cannot.
- The repository takes on marketplace plumbing: `plugin.json`,
  `marketplace.json`, a version and a changelog.
- `voice/profile/` in a project is a committed artifact and must not be
  confused with a corpus. A corpus is never committed, and under
  [D0017](D0017-writing-reached-through-mcp-is-distilled-in-flight.md) the
  personal text behind a casual profile is never written down at all.
