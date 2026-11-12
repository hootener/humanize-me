# humanize-me

A set of skills for coding agents, shipped as a plugin for Claude Code. It
changes what your agent writes when a person is going to read it, so the prose
sounds less like a robot wrote it.

Install the plugin and your agent picks up the behavior immediately. From there
you can point it at your own writing and build a profile, so the skills sound
like you and not like a generic competent writer.

## Why This Project Exists

The intent here is not perfect prose that sounds exactly like you and can be
pasted to another person unread. You own your voice, you own the way you sound
to a reader, and you own the responsibility that comes with saying something in
your own name. That ownership does not transfer to a tool. What these skills do
is hand you a draft that carries a much lower editing burden than standard LLM
output and is more straightforward for a reader to get through.

I'm tired of reading PR comments, code reviews, emails and Slack messages that
were obviously pasted straight out of an LLM, with no editing and no thought for
the person who has to read them. My hope is that a project like this makes some
of the text on the internet slightly less exhausting to read. You should not be
blindly pasting LLM output, handing it to someone and calling it your own prose.
If you're going to do it anyway, at least use something that makes the output
read better.

## Installing the Plugin

In Claude Code:

```
/plugin marketplace add hootener/humanize-me
/plugin install humanize-me
```

The three voices (casual, professional and precise) ship with general writing
craft, so the output will already read differently from stock agent prose. It
will not sound like you in particular.

## Using the Skills

Six skills install. Three of them are voices to write in. Three of them build
a profile so those three sound like you.

Your agent reads the descriptions and picks a voice on its own when it is
writing something a person will read. You can also just name one: *use
voice-professional for this PR description*.

### The three voices

| skill | what you write with it | what a claim rests on |
|---|---|---|
| `voice-casual` | a chat message, a quick reply, a note to someone you know well | your say-so, and no reasoning is owed |
| `voice-professional` | a decision memo, a status update, a PR description, a code review comment, a reply to a colleague | your judgment, owned and open to being wrong |
| `voice-precise` | an incident post-mortem, a measurement write-up, an analysis whose numbers someone will act on | evidence outside you, and the prose is exact about what it does and does not show |

These voices are three different levels of proving it to a reader, and you pick
by what you are claiming rather than by where the text is going. A Slack message
arguing for a schema change is casual in form and professional in what it owes
the reader -- your colleague wants to know why, not just what. A long formal
email that only confirms a meeting time is the other way around. Most real
writing is mixed, so write each part at the level its claims need.

### The three profile skills

| skill | what it does |
|---|---|
| `voice-gather` | collects your writing, proves you actually wrote it, sorts it by voice, and holds samples back so there is something clean left to test against |
| `voice-draft` | measures your writing and turns it into the profile file, recording what the corpus cannot support |
| `voice-harvest` | writes passages in your voice from your own content, asks you what is wrong with each one, and turns what you name into rules |

Run them in that order. The harvest is the part that does the work, and it is
worth running more than once.

## (optional) Building a Profile from Your Own Writing

The three skills above are a guided process: it gathers your writing, drafts a
profile out of it, then shows you generated text and asks what is wrong with it
until the profile is right. Expect it to take a while. Gathering is the slow
part.

Copy this prompt into Claude Code:

```
Walk me through building a voice profile from my own writing with voice-gather. Start by asking me where I write.
```

You end up with profiles at `~/.claude/voice/profile/<voice>.md`, and the skills
read them automatically. A team can commit a shared one at
`./voice/profile/<voice>.md` in a repository.

A profile is optional, and without one the skills still do the generic job.

Nothing personal ships with this repository. No profile is included and none is
loaded by default.

## Why Agent Prose Is Worth Fixing

Agents are good at the things people check. The output is factually correct,
grounded in what you gave the agent, and grammatically clean. None of those
qualities makes the text cheap to read, and working through a wall of agent
output is cognitively expensive.

When an agent writes, it already knows the whole story, and it writes as though
you know the story too. Nearly every other defect follows from that one habit.

Sentence shapes repeat, sentences come out short and clipped, and nouns and
articles the reader needs go missing. Participles dangle off clauses that give
them nothing to modify. Sentences trail off into prepositional phrases that make
you reread them. Those defects make a narrative hard to follow casually, and
reading agent output asks more of you than an email, a Slack message or a blog
post from a peer.

Those defects are not the whole problem, because writing also has grounds, the
facts behind what you say and how firmly you say them, and tone, the way you
speak. An agent has a hard time knowing when a claim should be stated plainly
and when it should be qualified. You come away unable to tell which parts of the
text the writer would stand behind.

## Where the Decisions Are Recorded

The decisions, experiments and retractions behind this project live in `brain/`
as linked Markdown, and you can browse that directory if you'd like. For how a
brain of this kind works in general, see https://github.com/hootener/brain.
REFERENCES.md lists the published research that informs this project.

## What Has Been Measured

Some of this has evidence behind it and some of it does not. The line matters if
you're deciding whether to install it.

**The harvest works.** Four rounds of generating passages and asking a writer
what is wrong with each one produced 75 specific rules. That is the method
`voice-harvest` implements, and it is the part of this project I would defend.

**Asking which version is better does not work**, which is why nothing here does
that. In the six prose trials I picked my own published writing out of a lineup
2 times in 6 -- chance -- and my own prose came out worst of the three arms on
average. People are bad at recognising their own voice, so asking them to rank
measures something other than what you wanted.

**A profile helps structure more than prose.** Across nine blind trials a voice
profile beat a no-guidance control 3 of 3 on headings and 0 of 6 on prose. That
split was found after the fact and the trial was small, so treat it as a lead
rather than a result. One of that profile's own markers turned out to make
output measurably worse than giving no instruction at all, and was withdrawn.

**The craft skill -- the part you install -- has no controlled trial behind
it.** Those trials tested a personal voice profile, which is not what ships.
`voice-gather` states its own evidence level as low; `voice-draft` has one test
against an unguided control and nothing else.

Every number, retraction and experiment is in `brain/`, including the ones that
went the wrong way. REFERENCES.md cites the published work the design rests on.

## Status

MIT licensed, and a work in progress. All three voices exist and have been
through review against real writing. The precise one has had one round where the
other two have had more, so I'd trust it least of the three.

Try it on something a person is actually going to read.
