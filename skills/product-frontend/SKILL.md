---
name: product-frontend
description: Plan and build the everyday parts of a product's frontend, both how it looks and how it works — dashboards, admin consoles, internal tools, chat apps, settings, forms, marketing pages, mobile screens, printable documents. Not for showpiece work (games, 3D, heavy animation, illustration, experimental interactive art). Reads the codebase first, works out whether the real problem is the UI, the code underneath (rendering, data fetching, state, types, performance, structure) or both, and recommends working only where it pays. Asks only the questions that decide the outcome, shows options with a recommendation and the reason, asks what the project is to them (MVP, startup, client work, side project), sizes the effort options from their own pace and recommends patch, gradual adoption or a rebuild, writes a phased plan the person approves, then builds phase by phase with verification. Use whenever asked to "design", "redesign", "revamp", "restyle", "make it look better / premium / less AI", "set up a design system", "build the UI", "refactor the frontend", "clean up the data layer", "make it faster", "fix our state management", or similar. Never builds on a direction or plan the person hasn't approved, and never changes the look when told to work on logic only (or the logic when told to restyle only).
---

# Product Frontend

For the interfaces people work in every day, and the code that runs them: calm, clear, fast, consistent, accessible, and easy to change. This skill won't make showpiece animation or experimental visuals. It makes product frontends that are well organised, on-brand and honest, through a repeatable method.

It has no default colour, font, framework or "look": every decision comes from the codebase you read and the answers the person gives. What it does fix is the method and the engineering rules, because those separate a frontend that looks and works designed from one assembled from a prompt. Every rule here comes from a real project; [12-reference-cases.md](12-reference-cases.md) shows where.

**Not every job is a redesign.** A good-looking UI can sit on poor rendering choices, scattered fetching, misused state or an untyped data layer; an ugly UI can sit on sound code. Find out which, tell the person, and recommend working only on what needs it.

## Order of operations

1. **Phase 0 — Read before you ask.** Read [01-context-scan.md](01-context-scan.md). Scan the code, docs, history and (if you can see them) the screens. Score both the UI and the code out of 10 and write a short current-state summary. Then read [11-related-skills.md](11-related-skills.md) and suggest skills that fit this stack and surface. Never ask what the code already answers.
2. **Phase 1 — Intake.** Read [02-intake.md](02-intake.md). One focused round, each question with options, your recommendation and why. First **what the project is to them** (MVP for speed, startup building to scale, client project, long-lived product, side project), then the **track** (UI only / functionality and code only / both), then the **scope** (new / revamp / adjust / keep the layout and polish), then only what Phase 0 left open. Offer the layout rules in [09-layout-rules.md](09-layout-rules.md) with a recommendation.
   **Phase 1b — Size it.** Read [03-sizing-and-approach.md](03-sizing-and-approach.md). Calibrate effort from the person's own pace (git history, agent token usage, with permission), present 2–4 effort levels in days, commits and tokens, recommend one for what the project is to them, and say whether the fixes can go in gradually without breaking anything or whether rewriting now is cheaper.
3. **Phase 2 — Options.** UI track: read [04-directions-and-proposals.md](04-directions-and-proposals.md) and show 2–3 contrasting visual directions. Code track: read [05-architecture-and-data.md](05-architecture-and-data.md) and present the rendering, data and state options with a recommendation. Record each decision and what lost.
4. **Phase 3 — Plan.** Read [07-plan-and-build.md](07-plan-and-build.md). Write a plan in phases, each with its output, a review point, a size on 0–10 and the tests you suggest. **Stop and get it approved.** Say plainly when doing it properly means rewriting large parts.
5. **Phase 4 — Foundations.** UI: tokens, components, lint gates ([06-design-system.md](06-design-system.md)). Code: the data seam, error model, state placement ([05](05-architecture-and-data.md)). Before any screen.
6. **Phase 5 — Build phase by phase.** Per [07](07-plan-and-build.md): one screen or area at a time, verified, committed, tracked, with an update to the person after each.
7. **Phase 6 — Craft pass.** Read [08-craft-checklist.md](08-craft-checklist.md) and run every finished screen against it.
8. **Phase 7 — Final report.** Done and verified (with screenshots), what needs the person, what you recommend but didn't do, and what you noticed along the way.

Scale it to the ask: a one-section tweak is a light Phase 0, one or two questions, a one-line plan, build, check. A revamp, a new product, a design system or a data-layer rewrite is every phase. Working agreements (dev server, ports, commits, updates, tests) are in [10-working-agreements.md](10-working-agreements.md).

## Where output goes

Plans, decisions and progress go in the project's docs (match its layout; otherwise `docs/design/`): `PLAN.md`, a progress log, a tracker, one decision record per choice someone could question. Visual proposals go in `docs/design/proposals/` as self-contained HTML or SVG. Never leave a decision only in chat.

## Hard rules

- **Obey the track.** "Keep the UI as it is" means no visible change, proven by before/after screenshots. "Only restyle" means no behaviour or data-flow change. Suggestions for the other side go in the report.
- **Plan, size and get approval before building** anything bigger than a small fix. The person should always know how big the job is (0–10, or 0–100 if they want detail, plus days, commits and tokens at their pace), whether it can go in gradually or needs a rebuild, and which phase you're in.
- **Fit the effort to what the project is.** An MVP, a scaling startup and a client job with the same code get different recommendations; ask before recommending a rewrite.
- **Show before you build.** A visual direction nobody saw is how revamps get rejected; a cheap mockup first, whenever the look is in question.
- **Ask with options and a recommendation**, never an open "what do you want?". Build the options from this project, not a fixed list. The person's stated preference beats your recommendation; say once what you'd do differently, then do theirs well.
- **No default aesthetic or default architecture.** Purple gradients, Inter and icon grids are tells ([08](08-craft-checklist.md)); so is wrapping every fetch in a client library because that's the habit.
- **Judge by coherence, not taste.** Borders can be excellent; client rendering can be right. Respect what works, fix what doesn't, say which is which.
- **Every value is a token; every external call goes through one seam.** No raw colours or arbitrary values in components; no `fetch` in screens; sample data behind the same seam and schemas, never in production.
- **Every screen designs its states**: loading that matches the content's shape, empty that teaches, error that says what to do, offline, long or odd data.
- **Plain language and honesty.** Never invent numbers, testimonials or users; never claim a check you didn't run.
- **Not done until seen and checked**: screenshots at phone (360–390px) and desktop widths in light and dark, plus typecheck, lint, tests and build. If you couldn't, say so.
- **Follow the person's sketch or order before improving on it**, and say what you'd change and why.
