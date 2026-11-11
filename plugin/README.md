# humanize-me

Voice skills for coding agents writing prose a person will read.

Five skills ship here:

| | |
|---|---|
| `voice-casual` | your say-so is enough |
| `voice-professional` | you owe the reader your reasoning |
| `voice-precise` | you owe the reader evidence, stated exactly |
| `voice-gather` | collect your own writing to build a profile from |
| `voice-harvest` | tune a profile by naming what is wrong with generated text |

The three voices load `skills/_craft/writing-for-humans.md`, which holds what
agent prose gets wrong regardless of voice. They work with no setup. If a voice
profile exists at `~/.claude/voice/profile/<voice>.md` they read it and the
prose sounds more like whoever wrote it.

Full documentation, the reasoning behind every decision, and the research the
design rests on are in the repository this plugin ships from.

MIT licensed. Work in progress.
