---
id: S0001
type: spec
title: The voice workshop
description: "Four skills that take a person from cloning this repository to holding voice registers tuned to them, with the evidence behind each step stated so nobody mistakes a guess for a result."
initiative: voice
status: active
serves: ../goals/G0005-someone-can-produce-their-own-voice-registers-by.md
timestamp: "2026-11-10"
tags: [workshop, process, skills, spec]
---

## Problem Statement

[G0005](../goals/G0005-someone-can-produce-their-own-voice-registers-by.md) says
a person clones this repository, runs a guided process against their own
writing, and leaves with registers tuned to them. No such process exists. What
exists is a transcript of one being improvised over a single day, in
conversation, by someone who already knew the project.

Every step of that day was done by hand: finding the corpus, checking bylines,
splitting train from test, writing the profile, building comparison pages,
sealing keys. A stranger with a clone has none of it.

The hard part is not the sequence. It is that **one step of the four has
evidence behind it and the other three do not**, and a workshop that presents
four confident skills would repeat the exact mistake this project spent a day
measuring.

## Solution

Four skills, run in order, each leaving an artifact the next one reads. The
confidence level of each is stated in the skill itself, where the user will see
it.

| | skill | what it produces | evidence |
|---|---|---|---|
| 1 | `/voice-gather` | a corpus, sorted by register, split train/held-out | none — improvised once |
| 2 | `/voice-draft` | a first profile per register | weak — produced one profile that lost 0/6 on prose |
| 3 | `/voice-harvest` | named defects, encoded as rules | **two runs, 26 rules, no retractions** |
| 4 | `/voice-check` | markers measured, as diagnostics only | negative — markers failed as a gate, one was harmful |

**Build order is 3, 1, 2, 4.** The harvest is the proven step and the one that
makes the rest worth having. Building it first also means the others are
developed by a workshop that already works on its strongest leg.

### 1. `/voice-gather`

Collects writing and sorts it. The day this was done by hand it produced four
findings a script would have missed, and they become this skill's requirements:

- **Check bylines.** A company blog's other ten posts belonged to a co-founder.
  Assuming "their company's blog" means "their writing" would have put 8,500
  words of someone else's voice into the corpus.
- **Try the feed before giving up on the page.** Medium returned 403 to every
  fetch of the HTML and served full post content over RSS.
- **Sort by register by hand**, per
  [D0016](../decisions/D0016-the-corpus-is-sorted-into-per-register-folders.md).
  Never classify for the user.
- **Hold samples back before anything reads them**, per
  [D0018](../decisions/D0018-a-voice-profile-states-its-claims-checkably.md) as
  amended — and extract them mechanically. "Held out of the build" was treated
  as "unseen" once, and it was not, because a human eyeballed the boundaries.
- **Integrations are read in flight and never written to disk**, per
  [D0017](../decisions/D0017-writing-reached-through-mcp-is-distilled-in-flight.md).
- **Refuse unusable corpora out loud.** A private notes repository turned out to
  be 93% hiring material about named candidates. The right answer was to use
  none of it and say why.

### 2. `/voice-draft`

Derives a first profile from the corpus. Constrained by what went wrong:

- **Per text population**, per
  [D0021](../decisions/D0021-a-profile-is-derived-per-text-population-not.md) —
  paragraphs, headings, list items, captions, measured separately. Headings were
  omitted once and the omission was the first thing the operator rejected.
- **Per register**, never pooled. A contraction floor averaged over a tenfold
  spread forced output two to nine times away from the writer's real rate
  ([E0010](../reference/E0010-a-pooled-marker-floor-pushed-output-away-from.md)).
- **Markers carry no floors and no targets.** Diagnostics, stated as such in the
  file.
- **An `Unstable` section is mandatory**, for habits the corpus contradicts
  itself on. Without one the draft asserts a coin-flip as a fact.
- The output says what it has **not** checked.

### 3. `/voice-harvest` — the proven step

Generates passages from content-only briefs, shows them, asks **what is wrong
with this one**, and encodes what the user names.

- **Never ask which is better.** [D0022](../decisions/D0022-the-preference-signal-is-named-defects-never-blind.md):
  a blind preference ranking is tuning on typicality bias. Rankings yielded
  p = 0.51; the free text alongside them yielded every durable rule.
- **Briefs carry content and no expression.** Verified mechanically — the first
  brief written leaked 10 of 13 headings and would have made the heading
  question untestable.
- **A fresh writer generates**, never the session holding the profile.
- **Separate what the user says from the medium they say it in.** Spoken
  feedback carries spoken register; "whatever" is not a written habit.
- **Attribute defects correctly.** Three defects the operator named were
  introduced by the *brief*, not the writer. A harvest that blames the writer
  for the brief's phrasing produces rules aimed at nothing.
- Rules are appended to the profile, and a rule named once should not need
  naming twice.

### 4. `/voice-check`

Measures markers and reports them. **It gates nothing.** A document passed 8 of
8 markers and was rejected by its author; the marker that differed most between
arms was the one doing harm. It also measures the right population — a first
attempt counted figure captions as sentences.

## User Stories

1. As someone who has just cloned this, I want to be told which step to run
   first and what it will cost me, so that I do not have to read the repository
   to begin.
2. As someone with published writing scattered across several sites, I want the
   corpus gathered without being asked to find every URL myself.
3. As someone whose corpus is mostly other people's confidential information, I
   want to be told it is unusable rather than have it quietly mined.
4. As someone reviewing generated prose, I want to be asked what is wrong with
   it, not which of three versions I prefer.
5. As someone who named a defect once, I want it fixed in the profile without
   editing a file myself.
6. As an adopter, I want to know which parts of this have evidence behind them
   and which are guesses, before I spend an afternoon on it.

## Implementation Decisions

- The workshop is **cloned, not installed**. D0019 as amended: the plugin is the
  library's only install path; the workshop is a different artifact.
- Output is **profiles**, read by generic skills, per
  [D0013](../decisions/D0013-the-craft-ships-generic-and-the-voice-is.md).
  Baking a voice into a copied skill forfeits the update path D0013 was bought
  for. **This is the open question flagged in D0019's amendment and is settled
  here only for the workshop's output format, not for how a user deploys it.**
- Each skill states its own evidence level in its own text. A user should be
  able to tell a measured step from an improvised one without reading `brain/`.
- The operator's registers ship as examples under
  [D0023](../decisions/D0023-the-operator-s-own-registers-ship-as-worked.md),
  and the workshop may read them to show what a filled-in profile looks like.

## Testing Decisions

- The workshop is tested by the operator building his **casual** register with
  it, having built professional by hand. That is the comparison that matters:
  same person, same method, one run improvised and one run guided.
- A step is "working" when it produces an artifact the operator does not
  hand-correct afterwards.
- `/voice-harvest` is the only step with a prior result to beat: 11 rules from
  8 passages, no retractions.

## Out of Scope

- The casual and research craft skills. The workshop produces profiles; the
  register skills that read them are the library's half.
- Exemplar retrieval
  ([T0017](../../tasks/voice/T0017-experiment-population-matched-exemplar-retrieval-versus-a-described.md)).
  If verbatim passages beat descriptions, `/voice-draft` changes shape — but
  that experiment has not run.
- Any automated style metric. [E0007](../reference/E0007-state-of-the-art-for-reproducing-a-specific.md)
  puts the best one's correlation with an author's own judgement at r = 0.244.
- Fine-tuning and activation steering, both ruled out on evidence and on API
  access respectively.

## Further Notes

The uncomfortable thing this spec is built on: the workshop's most valuable
step is the one where a person reads prose and says what is wrong with it. That
is not automatable, it costs the user real attention, and every attempt today to
replace it with a measurement produced either nothing or a false finding.

The workshop's honest pitch is therefore not "this makes an agent sound like
you". It is "this is a structured way to spend an hour of your attention, and
here is what an hour bought the person who built it".
