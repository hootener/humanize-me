---
name: voice-gather
description: Use when collecting someone's writing to build or extend a voice profile — finding sources, proving they actually wrote them, sorting by register, and holding samples back. Run before voice-draft.
---

# Gathering a corpus

**Evidence level: low.** This skill is assembled from one person's corpus being
gathered by hand over two days. Every rule below is something that went wrong
once and was caught. None of it has been tested on a second person.

The failure this guards against is not a thin corpus. It is a corpus of **the
wrong person's writing**, which produces a confident profile describing nobody.
That happened three times in two days and was caught three times by checking.

## First, prove they wrote it

This is the whole job. Everything else is logistics.

### Agent-authored text is the dangerous one

A corpus drawn from recent work by someone who uses coding agents is
**contaminated by default**. Measured on one developer's GitHub comments:

| | 2026 (agent era) | pre-Aug-2025 |
|---|---|---|
| em-dashes | 67% of comments | **0%** |
| bold `**headers**` | 42% | 1% |
| literal `Co-Authored-By: Claude` | 7% | 0% |

30,739 words, indistinguishable from his at a glance, and it would have taught
his profile to imitate the thing this library exists to remove.

**Ask the person for a date.** They know when they started using agents, and no
heuristic beats that answer. Apply the cut to the **item's own timestamp**, not
its parent's — a 2026 comment on a 2023 issue is still agent-era.

Then check what survives. Tells, roughly in order of reliability: an explicit
co-authorship trailer; em-dash rate far above the person's other writing;
`##` headings inside short-form text; `**Bold Label:**` lines; the words
*Summary*, *Test plan*, *What changed*; and a structural uniformity across
items that a human writing on different days does not produce.

**"They committed it" is not authorship.**

### Bots post under human accounts

Of 224 comments attributed to one user, **136 were a coverage bot** posting
reports under his account. They carried tables, badges and emoji shortcodes, and
they pushed the measured semicolon rate to fifteen times his real one.

Filter by content, not by author. Drop anything matching the shape of a
generated report, then re-measure and ask whether the numbers moved.

### Check bylines before believing a source

A company blog's other ten posts belonged to a co-founder. Taking "their
company's blog" to mean "their writing" would have put 8,500 words of someone
else's voice into the corpus.

Every multi-author source gets checked per item.

**And ask which parts they wrote.** Authorship is not all-or-nothing in
collaborative work. One author on a three-author paper identified the specific
sections he had written — about 3,000 words inside a 9,000-word paper where he
was third author, and therefore a source that a byline check alone would have
discarded entirely. Only the person can answer this, so ask rather than infer
from position.

**Watch for house style masquerading as voice.** The more gatekept a source, the
less of the author survives in it. Measured on one writer: his peer-reviewed
papers carry near-zero first person and heavy passive construction, and his own
public incident post-mortem — same register, same demand for evidence — runs 35
times the first person and a fifth of the passive. The papers are accurate
measurements of prose he wrote, and they describe the journal rather than the
person. Record which sources passed an editor, a reviewer or a style guide, and
weight them accordingly.

### Sanity-check every marker that surprises you

A semicolon rate fifteen times expected was bot tables. A heading count twice
expected was a parser treating YAML as headings. **A measurement tool that has
not been checked against a case whose answer you already know will invent
findings**, and they will be specific and plausible.

## Finding the sources

Ask the person where they write. Then:

- **Try the feed before giving up on the page.** One platform returned 403 to
  every HTML fetch and served full post content over RSS at `/feed/@user`.
- **Sitemaps enumerate what a blog index hides.** `/sitemap.xml` found eleven
  posts where the blog page 404'd.
- **An author page gives you the per-item bylines** you need for the check
  above.
- Interviews and Q&A: take **only the subject's answers**. The questions are the
  interviewer's and the section headings are the publication's.

## Sort by register, by hand

Per the voice taxonomy, a voice is set by **how much a claim has to be proved**
to its reader, not by how formal the writing looks. Do not classify for them — a misfile teaches one
register from the wrong samples and reads as a voice rather than as a bug.

Give them folders and let them file. Their filing is itself data: someone
putting a document under `professional/` is asserting something about it that no
classifier has access to.

**Expect the obvious answer to be wrong.** One writer described his
laid-back-audience blog posts as "professional, just for a more relaxed
audience" — which makes them professional in warrant and useless as a casual
corpus, however casual they sound.

## Sort by edited and unedited too

This is a second axis and it matters as much as register.

Published prose passed an editor. Comments, email, chat and review notes did
not. Measured on one writer, the two modes disagreed on **exclamation marks**
(zero published, 1.45/1k unedited), **first person** ("we" 5:1 published, "I"
2.7:1 unedited) and **parentheticals** (2–6/1k against 13.3).

An agent is almost always asked to write in the **unedited** mode. A corpus of
only published work describes the output of a process the agent is not part of.

Record which each source is. A profile built from one and applied to the other
will be confidently wrong.

## Privacy is a gathering decision, not a later one

- Anything reached through a live integration — mail, chat, documents — is
  **read in flight and never written to disk**. Observations go into the
  profile; the text does not.
- A pasted private conversation is the same thing arriving by hand. Take the
  subject's turns only. The other participants did not consent to anything.
- Scrub third-party names from every example that reaches a file.
- **Refuse an unusable corpus out loud.** One private repository was 93% hiring
  material about named candidates — interview notes and reference checks. The
  right answer was to use none of it and say why, not to mine it carefully.

## Hold samples back before anything reads them

Reserve a portion for later verification, and **extract it mechanically**.

"Held out of the build" was once treated as "unseen" when a person had eyeballed
the article boundaries by hand and read a third of the text doing it. Held out
means never read, by anyone, including you.

Hold back whole items, not fragments, and prefer the ones closest in genre to
what the profile will actually be asked to write.

## What good looks like

No defensible minimum exists. For reference, from one profile that has been
revised twice: 5,685 words of published prose was enough to produce a working
heading section and a prose section that measurably did not work; a second
corpus of 7,612 unedited words contradicted three of its rules.

A register with **under a thousand words** is a sketch. Say so in the profile
rather than letting its confidence match the others.

## When you are done

Report what you gathered, per register and per mode, with word counts; what you
rejected and why; what you held back; and what the corpus still lacks. The gaps
belong in the profile's own `gaps:` field, where the next reader will see them.

Then hand off to `voice-draft`, which turns the report into the file.
