# feedback

**Raw inbound, local only. Nothing here is in source control.**

Session transcripts, an adopter's notes, a bug report someone emailed. The
material a finding is derived *from*, before anybody has decided what it means.

| | |
|---|---|
| What lives here | transcripts, raw reports, screenshots of someone else's confusion |
| Where findings go | [`knowledge-catalog/reference/E0001-brain-in-practice.md`](../example/knowledge-catalog/reference/E0001-brain-in-practice.md) |
| In git? | **no** — see `.gitignore` |

## The line: raw stays out, anything a node cites comes in

Feedback does not sit outside the model — **it is Evidence**, and the loop
Intent → Approach → Action → Evidence → *amends* → Intent
([D0002](../example/knowledge-catalog/decisions/D0002-four-categories.md)) was built
for exactly this. A goal or a decision shaped by what an adopter found is a
node citing an older node, which is legal and ordinary.

That is precisely why the raw material cannot be the citation. **A node may
not cite a file that is not in the repository** — a reader cannot check it,
which is [D0001](../example/knowledge-catalog/decisions/D0001-claims-must-be-checkable.md)
broken at the one point it matters most.

So the split is by role, not by format:

| | Where | In git |
|---|---|---|
| The raw session, report or transcript | `feedback/` | no |
| The curated findings a node may cite | `knowledge-catalog/reference/` as `evidence` | **yes**, with `resource:` naming the raw |

The greenfield adoption produced both: an 1,800-line transcript, and a
279-line document of nine findings each carrying the command that reproduces
it. Only the second is citable, and only the second is committed.

## Why findings are committed and the raw material is not

A finding has to be checkable ([D0001](../example/knowledge-catalog/decisions/D0001-claims-must-be-checkable.md)),
so E0001 **quotes the lines it rests on** — the same discipline `bin/stale`
follows when it prints the sentence it objects to. The quote is what makes the
claim checkable; the full transcript is what the quote came from.

Keeping the raw material out of git is deliberate on three counts. It
accumulates fast — one adoption is 1,800 lines, and there will be many. It is
**unreviewed**, so a transcript may carry a path, a key or a client's name that
nobody chose to publish. And nobody re-reads it: once the findings are in
E0001, the transcript is spent.

The same shape as a `confidential/` directory in a client project: referenced
by path, read locally, never committed.

## Naming

`YYYY-MM-DD-<scenario>-<project>.md` — so a finding in E0001 can name its
source even though a reader may not have the file.
