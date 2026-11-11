---
id: E0012
type: evidence
title: "Unedited professional writing contradicts three absolutes in the profile"
description: "7,612 words of the operator's own GitHub comments from before he used coding agents put exclamation marks, the first-person ratio and parenthetical rate outside the ranges a published-only corpus produced, and settle the em-dash question at zero."
timestamp: "2026-11-11"
tags: [voice, corpus, genre, markers, findings]
status: active
---

The professional profile was built from seven published pieces — blog posts and
one interview, all edited. [E0005](E0005-markers-are-genre-sensitive-and-the-checker-must.md)
flagged that gap the day it was built: *"no email, no internal writing, no
long-form documents — all sources are published posts, which are edited and may
be flatter than this writer's working prose."* This closes it.

# The corpus, and what it cost to get

GitHub issue and PR comments authored by the operator. The first pull was
**unusable and nearly poisoned the profile**.

**208 of 209 comments were from 2026**, the period in which he uses coding
agents heavily, and they carry the tells: em-dashes in **67%**, bold headers in
42%, literal `Co-Authored-By: Claude` in 7%, and long structured review
documents with `##` headings and `**Verdict:**` lines. 206 of 209 came from one
repository — his current work. Training a voice profile on 30,739 words of
agent prose would have been the worst available outcome for this project.

The operator supplied the cut: **before August 2025**. Re-pulled with the filter
applied to the *comment* timestamp rather than the thread's, since a 2026
comment on a 2023 issue is still agent-era.

That yielded 224 comments, of which **136 were not written by a human at all** —
Codecov's bot posts coverage reports under his account. After removing those and
stripping code, URLs, markdown links and CLI flags: **88 comments, 7,612 words,
2014 to mid-2025.** Zero `Co-Authored-By`, zero em-dashes, 1% bold headers.

An intermediate pass reported a semicolon rate of 18.8 per thousand — fifteen
times anything in his prose. It came entirely from bot-generated coverage
tables. Caught before it reached the profile, unlike two findings yesterday.

# What it contradicts

| | published, edited | unedited | profile said |
|---|---|---|---|
| median sentence | 15–22 | **13** | 15–22 |
| share under 10 words | 15–18% | **33%** | min 15% |
| contractions /1k | 4–12 announcements | **26** | floor of 15, since withdrawn |
| parentheticals /1k | 2–6 | **13.3** | 2–6 |
| exclamation marks | zero | **1.45/1k** | *"Zero. Not one."* |
| first person | "we" 5:1 over "I" | **"I" 2.7:1 over "we"** | we 5:1 |
| em-dashes | present | **zero in 7,612 words** | *"unstable, do not assert"* |

Three of those were stated in the profile as **absolutes**, and all three were
artefacts of reading only edited prose.

**The em-dash question is settled.** Recorded as unstable on 2026-11-09 because
the published corpus split by venue. Corrected on 2026-11-10 toward `--` on the
strength of his sent mail. Now confirmed: **zero em-dashes in 7,612 words of his
own typing.** The published em-dashes were an editor's.

# Why this matters beyond the numbers

**The mode an agent writes in is the unedited one.** Comments, email, chat,
review notes, handoff documents — none of it passes an editor. A profile built
from published prose describes the output of a process the agent is not part
of, and then instructs the agent to imitate the output rather than the author.

This is the third form of the same error.
[E0005](E0005-markers-are-genre-sensitive-and-the-checker-must.md) found marker
ranges genre-bound. [E0010](E0010-a-pooled-marker-floor-pushed-output-away-from.md)
found a pooled marker harmful as an instruction. This finds a marker correct for
the corpus it was measured on and wrong for the writing anyone would actually
ask for.

Unedited prose also carries things published prose does not: "Thanks" at
1.58/1k, "Sorry" at 0.39, occasional emoticons, and visible typos. The courtesy
is not an affectation, and polishing unedited output to publication finish is
its own kind of infidelity.

# Consequences

- The profile gains an **Edited and unedited are different modes** section with
  both columns, and instructs the reader to **default to unedited**.
- Three absolutes are corrected in place rather than deleted, with the
  conditions they were missing.
- [D0016](../decisions/D0016-the-corpus-is-sorted-into-per-register-folders.md)
  asks the operator to sort a corpus by register. It should also ask whether a
  source is edited, and **whether it was written by an agent** — a requirement
  [S0001](../specs/S0001-the-voice-workshop.md)'s `/voice-gather` does not yet
  carry.
- The casual register still has only 806 words. This pull was aimed at casual
  and found professional.

# Citations

- `gh api search/issues q="commenter:hootener created:<2025-08-01"`, pulled
  2026-11-11; 224 comments, 88 usable after filtering bots and code
- `~/.claude/voice/profile/professional.md`, revised the same day
