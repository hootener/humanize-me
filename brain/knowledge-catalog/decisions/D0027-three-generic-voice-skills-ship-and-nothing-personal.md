---
id: D0027
type: decision
title: "Three generic voice skills ship and nothing personal does"
description: "The rules learned from one person are generalised into three craft skills plus a shared craft file; no profile ships, nothing loads automatically, and the privacy question stops being something to manage."
timestamp: "2026-11-11"
tags: [voice, architecture, skills, adoption, privacy]
status: active
serves: ../goals/G0002-humanize-me-installs-into-another-project-in-one.md
invariant: "Only generic craft ships. No profile derived from a particular person is distributed or loaded by default."
constrains: [skills, voice/profile, .claude-plugin]
---

# Context

[D0023](D0023-the-operator-s-own-registers-ship-as-worked.md) had the operator's
own profiles shipping as worked examples that nothing loaded. He then asked for
them to load as defaults, so the plugin would do something visible out of the
box, and separately asked that the repository not advertise whose writing they
came from.

That combination does not hold together. The brain documents the corpus in
detail because the measurements are the evidence, the repository carries his
name in `LICENSE` and `plugin.json`, and an adopter reading `brain/` connects
"the operator" to the repository owner in one step. De-identifying the record
would have cost the evidence and bought very little.

He then found the answer neither option contained:

> We probably don't want to use my trained samples exactly, but what we can do
> is take the rules that I've built and modify them to be a bit more generic.
> For example maybe the generic voice doesn't try for humor as much.

Eighty-seven rules had accumulated across three profiles from two defect
harvests and a README review. Sorting them showed most were **craft wearing
personal clothes** — head nouns, vague abstractions, trailing weak phrases,
rationed effects, reader-modelling — and only a minority were genuinely his.

# Decision

**Three generic voice skills ship: `voice-casual`, `voice-professional`,
`voice-precise`.** They hold generalised craft and no fact about any person.

**Shared craft lives once**, in `skills/_craft/writing-for-humans.md`, loaded by
all three. Triplicating it would drift, and the corrected copy would be whichever
voice was edited last — the argument
[D0024](D0024-rules-true-in-more-than-one-register-live.md) already made for
profiles, applied to skills.

**No profile ships.** A user's own profile at `~/.claude/voice/profile/` still
takes effect when present, and the skills still degrade to generic craft without
one, per [D0015](D0015-a-voice-profile-is-optional-and-the-skills.md).

Rules were sorted three ways:

- **Generalised into craft** — the structural and reader-facing ones, plus six
  of the operator's verbatim corrections whose underlying principle transfers
  even though the instance does not.
- **Dropped** — pure diction. His reach-for list, "y'all", spelled-out ranges,
  the idiom corrections.
- **Replaced by a differently-justified rule.** His no-em-dash habit is
  personal. **Em-dash overuse is also the most recognisable punctuation tell of
  machine prose**, which is true for everyone, so the rule ships on that footing
  instead. A *reach-for* vocabulary list became an *avoid* list for the same
  reason: a generic voice needs words to avoid far more than words to reach for.

# Alternatives

- **Ship his profiles as loaded defaults** — rejected with him: every adopter
  would write in one particular person's voice until they noticed. Generic prose
  is nobody's; this would be somebody else's.
- **Ship them as inert examples** ([D0023](D0023-the-operator-s-own-registers-ship-as-worked.md))
  — superseded. It was the right answer while the only alternative was shipping
  a person's voice, and it is worse than shipping generalised craft.
- **Scrub the brain of corpus detail** — rejected: the corpus *is* the evidence.
  Strip it and E0011 and E0012 become assertions.

# Consequences

- [D0023](D0023-the-operator-s-own-registers-ship-as-worked.md) is superseded.
  Nothing ships as an example, because nothing personal ships at all.
- **The privacy question dissolves rather than being managed.** No personal
  profile is distributed, so there is nothing to de-identify and the brain can
  keep its evidence intact.
- The operator keeps his own profiles at user scope, where they were always the
  only copy. Nothing in the repository ever held them.
- `voice-precise` and `voice-casual` exist as real skills for the first time —
  both were placeholders this morning — and all five skills are now in the
  manifest.
- **The generic voices are untested.** Everything measured so far was measured
  on one person's profile. A rule that survived generalisation may have lost the
  thing that made it work.
