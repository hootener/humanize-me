---
id: D0030
type: decision
title: "Personal data is scrubbed before a commit, not before a release"
description: "The repository is public, so history is the thing that must be clean; a pre-commit gate blocks what has a detectable shape and a human read covers what does not."
timestamp: "2026-11-12"
tags: [privacy, process, release, hooks, tooling]
status: active
serves: ../goals/G0004-structure-sounds-like-the-operator-and-prose-is.md
invariant: "No commit on this repository contains personal data; the check runs before the commit exists, not before a release."
constrains: [hooks, bin, ci]
---

# Context

Personal data was removed from this repository **the day it was published**, in
a single pre-publication sweep. That sweep found a client relationship named by
path in two nodes and a session-transcript path on one machine in two more. It
worked because the repository was still private and nothing had to be rewritten.

That is the last time it will be that cheap. The repository is public now. A
commit that carries an email address is carried by every clone and every fork
within minutes, and removing it means rewriting history for all of them — which
mostly does not happen, so the data stays.

The sweep was also a one-off performed because someone remembered to ask for
it. [D0007](D0007-status-ownership.md) already takes the position that the part
of a process which cannot be forgotten is the part nobody has to remember.

A further reason this cannot wait for release: **this project's subject matter
is other people's writing.** The corpus work reads mail, chat and private
repositories. [D0017](D0017-writing-reached-through-mcp-is-distilled-in-flight.md)
keeps that text off disk in the first place, and this decision is the gate
behind it for anything that leaks through a measurement script, a scratch file
or a quoted example.

# Decision

**Nothing is committed without being scrubbed first.** The check runs at
pre-commit and blocks.

Three layers, and the division between them is what makes the claim honest:

| layer | catches | |
|---|---|---|
| `bin/scrub` at pre-commit | email, phone, street address, postcode, credentials, auth tokens, private keys, home-directory paths, session-transcript ids | blocks |
| `bin/scrub --all` in CI | the same, over every tracked file, so a missing local hook is caught before merge | fails the build |
| a person, before publishing anything new | person names, client relationships, quoted private conversation | judgment |

**The third row is not a formality.** Every finding in the pre-publication sweep
was in that row — a client project named by path, and a local transcript
reference. The scrubber would have caught neither. A tool that implied otherwise
would be exactly the confident, stale claim
[D0001](../../example/knowledge-catalog/decisions/D0001-claims-must-be-checkable.md)
exists to prevent, so `bin/scrub --all` prints what it does not check every time
it runs clean.

`pre-commit` is the only hook here that blocks, and the asymmetry is the
justification: a wrong status in the record is corrected by the next commit,
while an address in history is corrected by rewriting history on every clone
that already pulled it.

# Alternatives

- **Keep the pre-publication sweep and repeat it per release** — rejected. It
  depends on someone remembering, it was a one-off the first time, and by the
  time a release comes round the data is already in history.
- **post-commit, matching the existing hook's never-block rule** — rejected on
  the asymmetry above. After the commit exists is after it is too late.
- **CI only** — rejected as the sole layer. CI catches it before merge, which
  is better than nothing, but the data is already in a pushed branch by then and
  on a public repository that is already a disclosure.
- **A scrubber that also tries to detect names** — rejected. Name detection
  without a corpus of known names is guesswork, and a gate that cries wolf gets
  bypassed with `--no-verify`, which costs more than it saves.

# Consequences

- `bin/scrub` is verified against planted samples rather than assumed: 11
  findings across every category on a file carrying one of each, and no false
  positive on a file of placeholders (`@example.com`, `<YOUR_KEY_HERE>`,
  `noreply@`, templated `/Users/<you>/`). The hook was confirmed to block a
  real commit.
- `ALLOW` in `bin/scrub` is a list of holes in the gate. Every entry needs a
  justification in the comment beside it, and the list stays short.
- **`--no-verify` defeats this entirely**, and nothing can stop that. CI is the
  reason it is not fatal.
- Work now happens on branches with pull requests rather than commits straight
  to `main`, which gives CI a place to run the scrub before anything merges.
