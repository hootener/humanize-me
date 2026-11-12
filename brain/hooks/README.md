# hooks

Layer 1 of keeping the brain current
([D0007](../knowledge-catalog/decisions/D0007-status-ownership.md)): the part
that cannot be forgotten, because nobody has to remember it.

| Hook | Runs | Does |
|---|---|---|
| `pre-commit` | before every commit | blocks a commit carrying personal data of a detectable shape ([D0030](../knowledge-catalog/decisions/D0030-personal-data-is-scrubbed-before-a-commit.md)) |
| `post-commit` | after every commit | prints status drift the repository contradicts, and the decisions governing the files just changed |

`pre-commit` is the one hook that blocks, and the asymmetry is why: a wrong
status is corrected by the next commit, while an email address in history is
corrected by rewriting history on every clone that already pulled it.

The post-commit hook's two rules matter more than what it checks:

1. **It never guesses semantics.** Anything ambiguous is left for `/audit`. Its
   whole value is that its output can be trusted unread, and one wrong guess
   ends that.
2. **It never edits and never blocks.** It runs after the commit exists, so
   there is no index to corrupt, and it only prints.

## Install

`bin/adopt` puts it in `.git/hooks/post-commit`. It is **local to your clone** —
not shared with the team, not committed — so removing it is deleting that file.

```bash
ln -sf ../../brain/hooks/pre-commit  .git/hooks/pre-commit    # by hand
ln -sf ../../brain/hooks/post-commit .git/hooks/post-commit
```

## Claude Code

The same reconciliation is worth running at the end of an agent turn, where
editing is safe and the agent receives the output as feedback. Add to
`.claude/settings.json`:

```json
{
  "hooks": {
    "Stop": [
      { "matcher": "", "hooks": [
        { "type": "command", "command": "brain/bin/reconcile" }
      ]}
    ]
  }
}
```

The git hook is the floor — it covers humans and any agent. This one is the
accelerator for Claude Code specifically.
