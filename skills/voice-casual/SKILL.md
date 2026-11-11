---
name: voice-casual
description: Use when writing something a person will read where your say-so is enough and no reasoning is owed — a chat message, a quick reply, a note to someone you know well. Not for text another agent will consume.
---

# Casual voice

## What a claim here rests on

**Your say-so.** Nothing more is owed. The reader either takes your word or
asks, and both are fine.

That is the whole definition. The professional voice owes the reader your
reasoning; the precise voice owes them evidence. This one owes neither, which is
what makes it casual — not the contractions, and not the punctuation.

## Picking this voice

Ask what the claims need to rest on. Do **not** ask what application the text is
going into.

A Slack message arguing for a schema change is a casual medium that needs the
professional voice, because your colleague is owed the reasoning. A long formal
email confirming a time is a professional medium carrying a casual claim.

| | |
|---|---|
| this voice | your word is enough |
| `voice-professional` | the reader needs your reasoning to act |
| `voice-precise` | your judgment is not enough; it needs evidence |

## Load the shared craft and your profile

**Read `../_craft/writing-for-humans.md` first.** It holds what agent prose gets
wrong in every voice — reader-modelling, correctness, rationed effects, the
sentences and vocabulary that give a machine away. Most of the work is there.

Then look for a profile for this voice, in order, and stop at the first hit:

1. `./voice/profile/casual.md` — in the project: a team's shared voice
2. `~/.claude/voice/profile/casual.md` — the writer's own

If either exists, also load `common.md` from the same directory and apply it
alongside; it holds rules that writer follows in every voice. Where a profile
and `common.md` disagree, the profile wins.

**A miss is expected and is not an error.** Say which mode you are in, once,
before you write:

- found → `voice: casual, profile <path>`
- neither → `voice: casual, generic craft (no profile found)`

Without a profile you do the generic job, and that is a real mode rather than a
degraded one. A profile makes the prose sound like one particular person; the
craft makes it stop sounding like a machine, which is most of the value.

## What casual actually is

Casual is **unplanned**, not clipped. This surprises people and it is measured:
in one corpus, casual sentences ran *longer* than the same writer's published
prose, because clauses chain with *and*, *but*, *so* and *because*, and the
sentence ends when the thought does rather than when it is shapely.

So do not write casual by writing short. Write it by writing unguarded.

**A story arrives in pieces.** Several consecutive messages, each a beat, rather
than one paragraph. Collapsing them into a block is the single most reliable way
to make chat read as a memo.

**Contractions throughout.** This is the one surface marker that genuinely
tracks the register.

**Fragments are allowed** where a person would actually use one. Correctly
punctuated — see the shared craft on correctness — but a fragment with a full
stop is still a fragment.

## What it is not

**Not sloppy.** Correct spelling, punctuation and capitalisation, always. A
corpus of real chat messages will show lowercase openings and missing full
stops; those are what happens when someone types fast into a box, and copying
them imitates the typing rather than the writing. The reader did not watch it
being typed.

**Not jokey by default.** Humour belongs here more than anywhere else, and it is
still `sparingly` — once in a piece, at the end of an explanation where a flat
summary would otherwise land, and never at the reader's expense. A joke built on
a number is almost always the wrong joke.

**Not familiar with strangers.** Casual is about what a claim rests on, not
about intimacy. Writing to someone you do not know, the warmth is unearned.

## Before you send it

1. **Would the claims here need defending?** If yes, this is the wrong voice.
2. **Is everything correctly spelled and punctuated**, however informal?
3. **Does it arrive in pieces**, or has a conversation been compressed into a
   paragraph?
4. **Is there exactly one effect in it**, at most — one joke, or one short
   landing, or one aside?
