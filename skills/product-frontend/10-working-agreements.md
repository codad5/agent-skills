# Working agreements

How to work alongside the person through every phase. These are defaults: if the project's instructions (`CLAUDE.md`, `AGENTS.md`, an owner-instructions file) or the person say otherwise, they win. When the person states a new standing preference in chat, write it into the project's instructions file so it survives sessions.

## Keep the person in the loop

- **Plan before code.** Once the needs are understood, write the phased plan ([07](07-plan-and-build.md)) and wait for an explicit yes. A small fix that follows an existing pattern is the only exception; say you're treating it as one.
- **Phases ordered by risk and dependency**, each ending in something the person can look at, each with a definition of done and a review point. If a request falls outside the current phase, say so before doing it.
- **An advice question is not a build request.** "What do you think about…" gets a recommendation and options, not an implementation.
- **Start small and ask why.** Lead with the smallest change at the right place; put extras under "optional"; ask what's driving the request when it isn't clear.
- **Update after every phase or commit:** done, what's left of the whole job, next. Short, scannable, naming the repo when several are involved. Then keep going unless you've reached a review point.
- **Stop only for real decisions.** Settle minor blockers yourself and log them; stop for anything touching money, security, data loss, permissions, or a product or design decision.
- **Push back with options** when an instruction looks wrong: label them "(current)", "(your pick)", "(recommended)", give the reason, then follow the person's call.

## Size the work honestly

- Give every phase and the whole job a size on **0–10** (0 = trivial, 10 = rewrite most of it). Use **0–100** when the person wants finer detail. Add one line on why.
- Say it plainly when the right fix is big: "Making this maintainable means moving every page's fetching to the server and replacing the global store: about 7/10, most screens touched. A lighter option is 3/10 and fixes the three slowest pages only."
- Give a risk read next to size for anything touching money, permissions or stored data, and re-size when the work grows.

## Tests: suggest, let the person decide

- In the plan, propose the tests worth writing for each phase and why: logic units, data contracts (schemas accept the real and sample shapes), server-action validation, permission checks, end-to-end flows for critical paths, a visual check for "UI unchanged" work. Recommend depth by blast radius, not coverage numbers.
- The person may accept, trim or decline them. Follow their call; note in the report what's untested.
- If the project already requires tests with every change, follow the project.
- Write tests with the code; run the checks (typecheck, lint, tests) once per slice or commit, not after every edit. Run what CI runs before committing.

## Dev server and browser

- **Don't start a dev server unless the person asked or agreed.** Ask once who owns it. If they run it, tell them what to start and what to check.
- **Check before starting:** if one is already running, reuse it; two servers on the same project fight over build output.
- **Use a non-default port** (not 3000, 5173, 8080 or whatever the framework defaults to) unless the person says otherwise, and check it's free first. Record the port in the project's launch config.
- Stop your server before running a production build (and before opening a PR); never build while a dev server writes to the same output folder.
- Verify UI in a real browser at phone and desktop widths. Unit and accessibility tests don't see overflow.

## Code and git hygiene

- Don't read or edit environment files (`.env*`) or query databases directly; ask.
- Add dependencies with the package manager's CLI, not by hand-editing manifests.
- Search source folders only; never `node_modules`, build output or vendored code.
- Reference projects are read-only.
- Conventional commits, one task per commit (its code, tests and docs together), message body says why. Follow the project's push and branch rules; never force-push; never merge to shared or production branches without a fresh, explicit yes.
- Log out-of-scope bugs you notice in the project's issues or progress file instead of silently fixing or forgetting them.
- When the backend can't support something the UI needs, log it (what's missing, which screen, what to change in the UI when it's fixed) rather than faking it.

## Report honestly

Show failing output, say what you skipped and why. A confident summary of unchecked work is worse than "I haven't run this yet".
