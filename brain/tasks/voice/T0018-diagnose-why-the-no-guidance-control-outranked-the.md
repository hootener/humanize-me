---
id: T0018
type: task
title: "Diagnose why the no-guidance control outranked the profile on prose"
description: "Explain why the arm given no style guidance outranked the shipped profile in all six prose trials, before anything further is built on the profile."
status: Testing
category: bug
initiative: voice
blocked_by: []
spec: <optional relative link to ../../knowledge-catalog/specs/...>
timestamp: "2026-11-10"
tags: []
---

# What to build

An explanation for [E0009](../../knowledge-catalog/reference/E0009-the-profile-works-on-headings-and-not-on.md)'s
prose result: the arm given no style guidance outranked the shipped profile in
**6 of 6** prose trials. Either the craft skill and profile degrade prose, or
the comparison was flawed. Both answers are actionable and the project should
not build anything further on the profile until it knows which.



# Acceptance criteria

- [x] A measured explanation, not an impression
- [x] Any flaw in the comparison itself recorded, including flaws that cut
      against the finding
- [x] The result stated whichever way it falls, including against what ships

# Log

## 2026-11-10 — diagnosed; two defects in what ships

Full findings in [E0010](../../knowledge-catalog/reference/E0010-a-pooled-marker-floor-pushed-output-away-from.md).

**The marker floor was harmful as an instruction.** The operator's contraction
rate spans 4.0 to 37.7 per 1,000 words across his own corpus and tracks
register. The profile carries a *floor* of 15, derived from the pooled mean. All
three test pieces are announcements, where his real rate is 4–12. The profile
arm produced 18, 21 and 38; the control, instructed in nothing, produced 1.2,
1.8 and 5.9. **The control was closer to his real register rate than the profile
was.** A floor cannot be satisfied downward, so the instruction had no way to be
right.

**The profile arm destroyed every hyperlink** — 6 of 6 across three documents,
against the control's 6 of 6 kept — plus an *Update:* label and a sentence of
installation instructions. Numbers survived, markup did not, which points at
rewriting as the mechanism. Nothing in the shipped skill or profile says to
preserve content through a rewrite.

**A flaw in the comparison, against the result.** The trial renderer stripped
bold, italic and code markup but not link syntax, so the control's excerpts
showed raw `[text](url)` while the profile's showed clean prose. The control was
handicapped in the trials it won. Fix before the next run.
