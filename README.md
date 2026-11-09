# humanize-me

Voice skills you drop into a project so a coding agent writing prose **for a
human reader** stops sounding like a coding agent.

Text written to be consumed by another agent is out of scope and does not need
to sound like anyone.

## The idea

An agent's prose fails in a particular way, and it is not a failure of
formality. It asserts everything at the same temperature — hedging claims it
should state flatly, stating claims it should hedge — because it has no model
of what a given claim is resting on. A reader notices the uniformity before
they notice any individual word.

So the registers here are organized by **what a claim has to rest on**, not by
how formal the writing looks:

| Register | A claim rests on | Status |
|---|---|---|
| `voice-casual` | the writer's say-so | not yet written |
| `voice-professional` | the writer's judgment, stated as judgment and owned | available |
| `voice-research` | evidence outside the writer, cited | not yet written |

A register is picked by asking what the claims require, never by asking what
application the text is going into. A Slack message arguing for a schema change
is casual in medium and professional in warrant.

## Install

The repository is its own marketplace, so no third party is involved. Once it
is pushed to a host, that is:

```
/plugin marketplace add <owner>/humanize-me
/plugin install humanize-me
```

From a local clone, point the first command at the checkout directory instead.

That is the only install path. Nothing is copied into your project and nothing
is symlinked into `.claude/skills`.

## Sounding like you, rather than like nobody

The skills above ship generic. They hold the craft — what agent prose does
wrong, and what each register's claims owe the reader — and they know nothing
about any particular person.

To also sound like *you*, a **voice profile** describes how you write. The
skills read it when they write. It is optional: with no profile they still do
the generic job, so installing costs one step and never requires gathering a
corpus first.

A profile is resolved per register, project first:

```
./voice/profile/<register>.md        committed: a team's house voice
~/.claude/voice/profile/<register>.md   yours, in force everywhere
neither                              generic craft only
```

Per register rather than per profile, so a team can share a `professional.md`
through the repository while everyone's `casual.md` stays their own.

**The generator that builds a profile from your own writing is not built yet.**
When it is, it will read a corpus you have sorted by register, and anything it
reaches through an integration — your sent mail, say — it will read and distil
without ever writing a copy to disk.

## Why the project is shaped this way

The reasoning lives in `brain/`, as linked markdown rather than as folklore.
Start at `brain/knowledge-catalog/goals/` for what this is for, and
`brain/knowledge-catalog/decisions/` for why it is built this way — D0013
through D0020 cover the architecture above.

## License

MIT — see [LICENSE](LICENSE). That covers this repository's own work: the
register skills, the plugin manifests, this README and the project record under
`brain/knowledge-catalog/`, `brain/plans/` and `brain/tasks/`.

It does not cover the generic half of `brain/` — `brain/bin/`,
`brain/skills/`, the templates and the scaffolding — which is forked from an
upstream template at the revision recorded in `brain/config.md`. That
upstream states no license, so its terms are its author's to give and are not
restated here.
