---
id: D0029
type: decision
title: "The profile file format is a contract with four consumers, so it gets a skill that writes it"
description: "Three shipped skills read the profile file and one appends to it, and until now nothing specified its shape; voice-draft owns the format and the step that produces it."
timestamp: "2026-11-11"
tags: [voice, profile, skills, format, plugin]
status: active
serves: ../goals/G0004-structure-sounds-like-the-operator-and-prose-is.md
invariant: "The profile file's frontmatter contract is specified in exactly one place, and every skill that reads or writes a profile agrees with it."
constrains: [skills, voice/profile]
---

# Context

The voice workshop shipped as two skills: `voice-gather` collects a corpus and
`voice-harvest` tunes a profile against the person's judgement. Between them
sits the step that actually writes the file, and it had no skill. It was
performed four times — `common`, `professional`, `casual`, `precise` — by an
agent improvising from the conversation it was in.

Two things followed.

**A dangling reference shipped.** `voice-gather`'s description read "Run before
voice-draft", naming a skill that did not exist. It was installed in that state.

**An undocumented format acquired four consumers.** The three voice skills read
a profile at write time, and `voice-harvest` appends rules to it. None of them
specifies its shape. Writing it four times produced four variations: `register`
against `scope`, `why_this_file_exists` in one file only, `train`/`held_out` in
one, `load_with` in two of four.

The worst of it is that the most important thing anyone knows about profiles
lives in that format and nowhere else. The line
`markers:  # diagnostics, not a gate and not a target` carries
[E0010](../reference/E0010-a-pooled-marker-floor-pushed-output-away-from.md) —
that a marker written as a floor pushed output *away* from the writer, and an
arm given no guidance at all landed closer to him than the profile did. A
drafting agent not told this will write floors, because floors are checkable.
That is the failure mode, it is measured, and it existed only as a YAML comment
in one person's private file.

# Decision

**`voice-draft` ships, and it owns the format.** It runs between `voice-gather`
and `voice-harvest`, and it holds the frontmatter contract, the marker rules,
and the findings that govern how a corpus becomes a file.

It states its evidence level as **low, and lower than the two skills either
side of it** — gathering has failures behind it, harvesting has a measured
result behind it, and this step has four builds in three days. Its content is
accordingly almost all prohibition: what poisons a profile before the harvest
can correct it.

# Alternatives

- **Leave the step to the agent, document the format in a README** — rejected.
  A format read by four skills needs to be specified where the skills are, and
  the README is not loaded at write time. It also leaves the marker finding
  unstated at the one moment it is needed.
- **Fold drafting into `voice-gather`** — rejected on load. Gather is already
  about proving authorship, which is a different and larger job; a reader
  invoking it to collect writing should not have the marker rules in context.
- **Fold drafting into `voice-harvest`** — rejected on ordering. The harvest
  requires a profile to exist. A skill cannot be its own precondition.
- **Fix the dangling reference and ship five skills** — rejected: it hides the
  gap rather than closing it, and the gap is the step where the measured harm
  happens.

# Consequences

- Six skills ship instead of five. The plugin manifest, `voice-gather`'s
  handoff and the README's reference table are updated together.
- **The format now has one owner and four consumers, which is a thing that can
  drift.** A change to the frontmatter contract has to reach the three voice
  skills' loading instructions and `voice-harvest`'s append step. Nothing
  enforces that today beyond this decision.
- The skill asserts a contract that the four existing profiles do not all
  satisfy. They were written before it. They are the operator's own and do not
  ship, so this costs nothing externally, but any claim that the format is
  uniform is false until they are reconciled.
- `voice-draft` has no harvest behind it and cannot get one the way a voice
  profile can, because its output is a file rather than prose a person can
  react to. Its evidence level will stay low until a second person builds a
  profile with it.
