# Phase 1b — Sizing the work and choosing patch vs rewrite

Goal: recommend the right amount of work for what this project is to the person, show the effort options in numbers they can weigh (time, commits, tokens), and say plainly whether the fixes can be applied gradually without breaking anything or whether rewriting now is cheaper.

Do this between Phase 0 and the plan: after you've scored the UI and the code, before you suggest an approach.

## 1. First ask what the project is to them

The same codebase deserves different advice depending on what it's for. Ask this before recommending patch or rewrite; it's usually one multiple-choice question plus one free-text line.

| The project is… | What matters | Usually recommend |
|---|---|---|
| **An MVP racing for speed** | Shipping and learning this month | Patch what blocks users; adopt the rules for new code only; no rewrite unless the base actively slows shipping |
| **A startup building to scale** | Changing fast without breaking; hiring others into it | Fix the foundations now (data seam, tokens, state), rebuild beside the old UI if the base fights every change; it only gets dearer |
| **A client project** | Deadline, budget, handover, who maintains it after | The scope they're paying for; leave it clean and documented for the next developer; flag bigger issues in the report with a size, don't do them unasked |
| **A long-lived product or internal tool** | Maintainability, consistency, onboarding | Systematic: design system and seam, then screen by screen |
| **A side project or learning project** | Their time, their enjoyment, what they want to learn | Whatever they enjoy; offer the "proper" way as a learning option, not a requirement |

Also ask, if it isn't obvious: how long it should live, who else works on it, and whether a deadline is coming. Say what you assumed if the docs already answer it.

## 2. Calibrate effort from the person's own pace

Estimates mean more in their own units. If they have history, measure it; otherwise use the reference points below and say so.

**From git** (this repo, or another of theirs they point you to; ask before reading other repos):

```sh
git log --reverse --format='%h %ad %s' --date=short | head -1   # first commit
git log -1 --format='%h %ad %s' --date=short                    # last commit
git rev-list --count --no-merges HEAD                           # commits
git log --no-merges --format=%ad --date=short | sort -u | wc -l # active days
git ls-files | grep -E '\.(ts|tsx|js|jsx|css|vue|svelte)$' | xargs wc -l | tail -1   # source lines
git log --no-merges --shortstat --format= -- <path>             # churn for one area (e.g. a rewrite folder)
```

Derive: lines of finished source per active day, commits per active day, and the size of the area you'd touch (pages, components, lines).

**From agent usage**, only with the person's permission (it reads their local history): many coding agents keep per-session usage locally or in a dashboard (for example, Claude Code transcripts under `~/.claude/projects/<project>/*.jsonl` carry `usage` per response). Sum output tokens and context (cache) tokens per project; divide by commits and by lines.

**Reference points** (two real projects by one developer working with an agent; use only when the person has no history of their own, and say they're someone else's numbers):

| | Full-stack product built from scratch | Frontend rebuilt beside the old one |
|---|---|---|
| Calendar span / active days | 25 / 13 | 16 / 9 |
| Commits | ~380 | ~105 |
| Source lines at the end | ~60k | ~27k (replacing ~30k) |
| Lines per active day | ~4.5k | ~3k |
| Output tokens | ~6.3M (~16k per commit) | ~1.6M (~15k per commit) |
| Context tokens re-read | ~3B | ~0.85B |

Rules of thumb from these: about **15k output tokens per commit-sized task**, about **60–100k output tokens per thousand lines of finished code**, and context re-reading runs a few hundred times the output, so a larger codebase costs more per change even when the change is small. A rewrite of N thousand lines takes roughly N/3 active days at that pace.

## 3. Present effort levels, recommend one

Give 2–4 levels that fit what you found, each with what it fixes, what it leaves, a 0–10 size (0–100 if they want detail), the estimate in their units, and the risk. Recommend one, tied to section 1.

| Level | What it means | Fixes | Leaves | Size | Estimate |
|---|---|---|---|---|---|
| **Patch** | Fix the worst spots in place | The three slowest pages, the broken states | Scattered fetching, the global store | 2 | ~1 active day, ~10 commits, ~150k output tokens |
| **Adopt going forward** | Add the seam and tokens now; new and touched code follows them; old code migrates when it's next edited | Every new feature is right; old code improves over time | A mixed codebase for months | 3 | ~2 days for the foundation, then ~10% extra on each feature |
| **Rebuild beside** | New route group or flag, screens move one at a time, old stays reachable until cutover | Everything, without a risky switch-over day | Two UIs side by side during the move | 7 | ~9 active days for ~27k lines, ~100 commits, ~1.5M output tokens |
| **Rewrite in place** | Replace it all at once | Everything | Nothing usable until it's done | 8 | Similar effort, more risk; rarely the right call |

> For a startup that's about to hire and add features fast, I'd recommend **Rebuild beside** (7/10, about two working weeks at your pace): every feature you add on the current base will need redoing later. If shipping this month matters more, **Adopt going forward** (3/10) gets new work right and leaves the rest for later. Which one?

## 4. Gradual or rewrite now: how to tell

**Say "we can apply this going forward and it won't break anything"** when:
- the problems are local (some pages, some components, the styling) rather than in the foundation;
- old and new can live together: tokens alongside old classes, new data functions alongside old fetches, a new component used screen by screen;
- each step can be guarded (a test, a before/after screenshot) and shipped on its own;
- the person needs to keep shipping features meanwhile.

Then name the rule that new and touched code follows, and how the rest migrates (when next edited, or a screen per week).

**Say "it's best to rewrite now"** when:
- the foundation fights every change (no way to add tokens; every page coupled to one global store; the rendering model is wrong everywhere), so fixing each screen costs about as much as rebuilding it;
- big growth is coming (features, users, developers) and would be built on the bad base: cheaper before than after;
- the codebase is still small or early, so a rewrite is cheap;
- earlier in-place passes have already failed (check the history);
- a framework or library move is needed anyway.

Even then, prefer **rebuild beside** over a big-bang rewrite: the old one keeps working, and each screen moves when it's ready.

Say which one you see, why, and what the other would cost: "This can go gradually: tokens and the data seam can be added without touching existing screens (3/10). A rewrite isn't worth it at this size."

## What NOT to do

- Don't recommend a rewrite before knowing what the project is to them. An MVP and a scaling startup with the same code get different advice.
- Don't give sizes without units the person can feel (days, commits, tokens), or present someone else's numbers as theirs.
- Don't read their other repos or their agent history without asking.
- Don't hide the cost of the option you recommend, or the cost of not doing it.
