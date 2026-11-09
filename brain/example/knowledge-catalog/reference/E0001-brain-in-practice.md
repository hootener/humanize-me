---
id: E0001
type: evidence
title: The brain in practice
description: "A running record of what the brain catches, costs and changes in use, appended as it happens so claims about the system can be checked rather than asserted."
timestamp: "2026-10-30"
tags: [brain, meta]
status: active
append_only: true
---

# The brain in practice

**`timestamp` is when this record was opened, not when it was last appended.**
A running record that re-dated itself on every entry would invalidate every
citation of it the moment anyone wrote a new one — the direction rule would
see a node from October citing one from November, correctly, because the
timestamp would be lying about what the file is. Each entry below carries its
own date; the frontmatter carries the file's.

Appended as findings happen. `/grill-change` reads this first: it is where the
places changes have actually gone wrong in this project accumulate.

## 2026-11-07 — the first adoption into a project already in flight

A consulting engagement with 21 dated decisions, 27 reference documents, 6
tasks and roughly 50,000 words of narrative, none of it written for this
brain. Twelve defects surfaced in a day. **Not one was found by the template's
own checks**, and the reason is structural: the template passes its own linter
by construction, because the same hand wrote both.

### What found what

Deliberate testing during development found **mechanical** bugs — and it found
them well, so this is not an argument against it:

- A five-task fixture showed `bin/ancestry` returning 8 documents of which 5
  were sideways peers, because `blocked_by` was being walked as lineage.
- The same fixture showed `--claims` surfacing 4 of 9 assertions, silently.
- Simulating the CI job showed the graph-currency step would have **failed on
  every run forever**: each build stamps a fresh timestamp onto a
  single-line payload, so a rebuild-and-diff always reports a change.
- Running the post-commit hook for the first time showed it printing nothing —
  invoked through its symlink, `dirname $0/..` resolved to `.git`, so it found
  no `bin/reconcile` and exited 0 having checked nothing. **A hook that checks
  nothing is indistinguishable from a clean repository.**
- A workspace test showed sibling mode was entirely non-functional: skills
  linked where Claude Code never looks, and the `brain/...` prefix every
  document uses unresolvable from anywhere work happens.

Adoption into a real project found a different **class** — design defects that
no amount of self-testing would reach, because they only appear when the
content was not written for the system:

- **The documented install path for the default mode was wrong.** The README
  said `git clone` into `<project>/brain`, which leaves a `.git` inside the
  brain so the host repo tracks a gitlink: measured, **1 tracked entry instead
  of 80 files**. The knowledge would have been invisible to the repository it
  exists to be versioned with.
- **A fresh install greeted its first adopter with 17 dangling links**, because
  `bin/adopt` relocated the template's own record and left everything pointing
  at it. It moved `goals/` and `decisions/` as whole directories, taking each
  `index.md` with them, and left `tasks/formalize` — this project's own
  backlog — sitting in the adopter's tracker.
- **The taxonomy was too strict for imported material.** 21 decisions written
  in the host project's own shape carried none of this brain's required body
  headings. Enforcing them on import forces a choice between mangling real
  reasoning and inventing an `# Alternatives` section to satisfy a linter —
  and the second is what D0001 forbids.
- **An invariant misfired on a real edge.** `lint`'s direction rule treated
  `blocked_by` as a citation, so a September task that discovered a November
  blocker was reported as citing a node newer than itself. `bin/ancestry`
  already drew that distinction; `lint` did not.
- **A heuristic produced five false positives on real prose.** `bin/stale`
  only looked *backwards* for words that scope a count. Every miss scoped
  itself afterwards: *"two decisions below"*, *"two decisions per email"*,
  *"750 tasks/mo"*, *"eleven numbered decisions of its own"*, *"Three
  decisions handed back"*.

### The invariants earned their keep, twice, against their own author

Porting the decisions, I set `serves: G0001` on all 21 — and the direction
rule rejected every one of them. The goal was stated **2026-11-04**; a
decision from July cannot serve a goal that did not exist. The rule caught the
exact thing it was written to forbid, in an import written by the person who
wrote the rule, where a human reviewer would almost certainly have waved it
through. The YAML hazard check caught 9 titles carrying an unquoted `: ` in
the same pass.

This is the strongest evidence so far that these checks are doing work rather
than ceremony.

### A claim this record made and had to retract

An early reading reported *"zero cross-links between the 21 decisions — a flat
pile, not a graph."* **That was wrong.** The relink pass found **174
cross-references across 59 files**. They had always existed, as backticked
prose paths that no tool could follow, and the measurement had counted only
markdown links.

The lesson is about the measurement, not the catalog: **`bin/lint` validates
`](…)` links and nothing else**, so a project can accumulate hundreds of path
references that rot silently and pass every check.

### What the brain could not represent

Three gaps that the adoption exposed and that remain open:

1. **Open questions have no node type.** 69 flagged items collapsed into a
   single 1,119-line evidence node. There is no way to say "this is an
   unresolved question with an owner" short of making it a task, which it is
   not.
2. **The status vocabulary discards the reason.** The host's statuses carried
   *why* — *"Blocked — handles frozen by Ashlee 2026-11-02 until the new site
   is done"*. The seven-value enum keeps none of that, so an
   `imported_status:` field was invented mid-port to avoid losing it.
3. **Retroactive intent has no path.** 20 of 21 decisions and 6 of 6 tasks
   have no lineage to a goal, which is true and worth knowing. But D0002
   forbids an older node citing a newer one, so a goal articulated today can
   never be named by the work that was in fact serving it. The brain can
   *detect* missing intent and offers no way to supply it after the fact.

## 2026-11-08 — the greenfield cold start, first finding

A session that did not build this brain was asked to adopt it into an empty
project, with no guidance beyond the README. It got stuck on the first step
after install.

**`bin/adopt` ends by saying "now run `/brain-init`", and you cannot.** Claude
Code discovers skills when a session *starts*, so the `.claude/skills` link
`adopt` has just made is invisible to the session that ran it. The skill does
not exist yet. Neither `adopt` nor the README said to restart.

A documentation gap, not a defect — one line in each — but a telling one:
the only person who could not have hit it is the one who wrote the install,
because they already had the skills loaded from somewhere else. This is the
same blindness as the linter passing by construction, in the first five
minutes of the adopter's experience.

**It also raises a real question about distribution.** Claude Code installs
skills natively through plugins: a repository carrying
`.claude-plugin/plugin.json` and `marketplace.json` is its own marketplace,
and `/plugin install` puts its skills in `~/.claude/plugins` at user scope.
That would not remove the restart — skills are still discovered at session
start — but it would move it to a harmless moment, *before* any brain exists,
rather than stranding the adopter mid-install.

The open conflict is that a plugin and `adopt`'s symlink would both supply the
same skills. It is a fork, not a patch, and it is recorded as such rather than
taken unilaterally in the middle of the experiment that found it.

### Cost

Roughly a day, of which the port itself was perhaps an hour. The rest was
fixing what the port revealed — which is the correct ratio for a first
adoption and should not be read as the steady-state cost.
