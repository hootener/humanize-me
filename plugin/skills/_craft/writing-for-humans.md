# Writing for a human reader

Shared craft for every voice in this library. The three voice skills —
`voice-casual`, `voice-professional`, `voice-precise` — each load this file
alongside their own.

Nothing here is about any particular person. It is what agent prose gets wrong,
and it applies whether or not anyone has built a voice profile.

## Write for a reader who is not you

**Everything in this section is register-independent craft.** It applies to
casual and precise writing identically, and it exists here only because this is
the first register written. When the others are written it should move to a
shared layer.

These are the failures of a writer who has read the source material and forgotten
that the reader has not. They were named by a reviewer going through a generated
document paragraph by paragraph, and three of them recurred three times each in
one pass.

**Introduce a term before you use it.** Measured three times in one document:
*guidance*, then *grounds* and *tone*, then *register* — each used as though
established, none introduced. The reviewer's diagnosis is the clearest statement
of it: *"Since the writer knows everything ahead of time, it writes like you,
the reader, know everything ahead of time."*

The fix is cheap and does not need a definitions section. **Gloss inline, on
first use, in a parenthesis**: "a casual medium (a chat app)", "evidence-based
contexts where evidence and empirical facts are important". Four words, in
passing, and the term is earned.

**Every fact earns its place by answering a question the reader has right
there.** Measured five times in one document. An install section explained that
nothing is symlinked into the project — true, load-bearing in the project's own
decision record, and meaningless to someone who has never considered the
alternative. The reviewer: *"I understand what you're saying. I just don't know
why you're saying it here. Why do these things matter?"*

This is the mirror of the rule above. One writes as though the reader **knows**
what the author knows; this writes as though the reader **cares** what the
author cares about. Both come from failing to model the reader as a separate
person with their own questions at that moment.

The hazard is sharpest when a project keeps a written record of its own
reasoning. A fact can travel from a decision record, to an internal note, to a
stranger's install instructions, without anyone at any step asking whether the
stranger needed it.

**Say what the thing does before you say how to use it.** A document that
diagnoses a problem, describes a taxonomy and then gives install commands has
skipped the sentence the reader came for. *"It's like we didn't really come to a
point."*

**An opening carries the broad takeaway.** Nuance, metrics and caveats belong to
the section that owns them. An introduction reaching for terms it has not earned
is usually an introduction doing a later section's job.

**Do not explain someone else's concept.** Link to it. A README is not the place
to teach a dependency.

**A heading says what its section does for the reader, not what it contains.**
"The Three Registers" announces a count and was rejected outright — the reviewer
could not even propose a fix, which is itself a signal that a heading has failed
below the level of wording.

**Say it plainly.** "Carries no model of the grounds on which a claim rests" is
philosophy-shaped. Say what happens instead. Abstract nominalisations are the
most reliable way to sound like nobody.

**Do not restate a complete statement.** A sentence that adds nothing to the one
before it reads as padding even when it is true.

**Compression is for landings, not explanations.** A short declarative closing a
paragraph earns its brevity. An explanation does not — give it the room it
needs. The same reviewer who cut a redundant sentence expanded a compressed
example into a full one in the same pass.

## Keep what you were given, and invent nothing

Two failures sit either side of a rewrite, and only one of them is loud.

**Do not invent what you were not given.** This is measured. Asked to write
three technical posts from briefs containing no URLs, a writer produced **six
fabricated hyperlinks** — documentation pages, an app install page, an archived
blog post — every one correctly shaped for the product in question, plausible,
and not supplied by anything. Plausible-looking links are the easiest thing in the
world to generate and among the worst things to be wrong about, because a reader
clicks them.

So: no URL you were not given. No version number, date, metric, name or quoted
error you were not given. If the source says a link belongs somewhere and does
not say where it points, say so in words and leave the link out. *"Installation
happens on GitHub"* is correct; `[on GitHub](https://github.com/apps/...)` is a
guess wearing a link's clothes.

**And keep what you were given.** Rewriting moves whole sentences, and the
things most easily lost are the ones that sit outside a sentence rather than
inside one — a link, a label like *Update:* or *Deprecated:*, a standalone
instruction, a caveat in its own clause. Numbers tend to survive because they
ride along inside a clause being reworded. Separate objects do not.

Before finishing, check the output still carries every link, number, identifier,
product term, meaningful label, caveat and reader instruction that the input had
— no more and no fewer.

**Where voice and content conflict, content wins.** A sentence that sounds
exactly like the writer and omits where to click is worse than a flat sentence
that tells the reader where to click.

## Correctness is not negotiable by a voice

**Whatever a voice profile says, the prose you produce is correctly spelled,
punctuated and capitalised.**

A corpus records how someone types. You are producing how they write. Those
differ, and where they differ the writing wins — a reader receiving generated
text did not watch it being typed and has no reason to read sloppiness as
intimacy.

This matters because the most *distinctive* measurements in an informal corpus
are often the mechanical ones. One casual corpus had 55% of messages starting
lowercase and 86% ending with no full stop. Those are the clearest fingerprints
in the whole sample and they are the wrong thing to copy: they are artefacts of
a chat box, not features of a voice.

So: **lowercase message openings, missing terminal punctuation, typos, doubled
words and dropped articles are never reproduced**, however faithfully they were
measured.

What a profile *does* govern, and what you should follow closely: contraction
rate, sentence length and rhythm, deliberate fragments, informal diction,
profanity, how text is broken into messages or paragraphs, and punctuation the
writer genuinely avoids — a writer who never uses a semicolon should still never
get one.

If a profile instructs you to write incorrectly, the profile is describing
typing. Follow its voice and fix its spelling.

## The moves everyone overuses

**Every move below is good and every one of them is an effect.** An effect used
every time it could be stops being an effect. Each carries a rate:

| rate | meaning |
|---|---|
| `always` | a rule, not a move |
| `often` | the default way to do this |
| `sparingly` | at most once in a piece, and not in consecutive pieces |
| `once per piece` | one, and the piece is worse with two |

**Rates are spent across everything a reader sees at once**, not per document.
Where several pieces go to one reader, count across the set. This is measured:
a writer given a list of effects used three of them twice each across six short
passages, and every single use was defensible alone.

**A short line lands a long one** — `sparingly`. It compresses what the long
sentence established; it never introduces a new idea. **Two short sentences in
sequence have nothing to land against**, and a conjunction is the alternative.
Alternate between them. Choosing the same solution every time is the error.

**Don't announce a move before making it** — `never`. "Here's the dumb part."
"The interesting thing is." Foreshadowing at sentence scale. Make the move.

**Reframe** — `once per piece`. One sentence that relocates the problem is
worth having. Two is a mannerism.

**Rhetorical questions as transitions** — `sparingly`.

## Sentences that give the writer away

**Don't leave a head noun implicit** — `always`. A modifier gets its head, a
demonstrative gets its noun, and a sentence does not end on a bare *that*.
"Taken together those three" wants *those three points*. The failure also
appears in openings — "Small one, but it's been living in my head" — and inside
jokes, where a pronoun that resolves to the wrong noun breaks the joke on
grammar before it breaks on comedy.

**Replace a vague abstraction with a precise phrase or an enumeration** —
`always`. Not "post notices everywhere they belong" but "post notices to the
GitHub repository, the package manager and the uploader's own output."

**No trailing weak phrase** — `always`. A sentence does not end on a
preposition, an adverbial, or anything that adds nothing after the point has
landed. "left a stray folder in my repo on the way through" stops at *repo*.

**Don't narrate yourself from outside** — `always`. "I watched myself answer it
badly in real time" is a camera angle, not a sentence. "I blew it" is the
sentence.

**Plain verbs over gerund subjects** — `often`. Not "You landing on Bioshock is
the part I can't get past."

**Prefer an explicit causal connective to a relative clause** — `often`. "the
only idea that works **because** it hands the time back", not "the only one of
these ideas **that** hands the time back". Say why, not merely which.

**Attribute in words; leave identifiers to a references section** — `often`.
Inline arXiv IDs, bare URLs and citation keys clog prose a person has to read.
"A study of 400 authors found" belongs in the sentence; the identifier belongs
at the bottom.

**Pick one variety of English and hold it.** Mixing "realising" with "color" is
a tell on its own.

## Vocabulary that marks the machine

Avoid, regardless of voice: *delve*, *leverage* as a verb, *utilize*, *robust*,
*seamless*, *tapestry*, *landscape* as a metaphor, *navigate* as a metaphor,
*it's worth noting that*, *it's important to note*, *in today's fast-paced*,
*at the end of the day*, *that being said*, *a testament to*, *underscores the
importance of*.

**Em-dashes are the most recognisable punctuation tell there is.** Heavy
em-dash use reads as machine-written to anyone who reads much generated prose.
Use them rarely, or use a comma, a colon or a full stop instead.

The same goes for the shape: three-item lists where two would do, every
paragraph the same length, every section opening with a one-sentence summary of
itself.
