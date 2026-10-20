---
name: product-frontend
description: Plan and build the everyday parts of a product's frontend, both how it looks and how it works — dashboards, admin consoles, internal tools, chat apps, settings, forms, marketing pages, mobile screens, printable documents. Not for showpiece work (games, 3D, heavy animation, illustration, experimental interactive art). Reads the codebase first, works out whether the real problem is the UI, the code underneath (rendering, data fetching, state, types, performance, structure) or both, and recommends working only where it pays. Runs a gated process: a complete intake checked against a printed coverage table, real references, a self-reviewed HTML prototype the person chooses from, then a sized, phased plan they approve, then foundations and screens with viewport and craft checks. Use whenever asked to "design", "redesign", "revamp", "restyle", "make it look better / premium / less AI", "set up a design system", "build the UI", "refactor the frontend", "clean up the data layer", "make it faster", "fix our state management", or similar. Never skips a gate, never shows output it hasn't reviewed, and never changes the look when told to work on logic only (or the logic when told to restyle only).
---

# Product Frontend

For the interfaces people work in every day, and the code that runs them: calm, clear, fast, consistent, accessible, and easy to change. This skill won't make showpiece animation or experimental visuals. It makes product frontends that are well organised, on-brand and honest, through a repeatable method.

It has no default colour, font, framework or "look": every decision comes from the codebase you read, real references and the answers the person gives. What it does fix is the method, because that separates a frontend that looks and works designed from one assembled from a prompt. Every rule here comes from a real project; [12-reference-cases.md](12-reference-cases.md) shows where.

**Not every job is a redesign.** A good-looking UI can sit on poor rendering choices, scattered fetching, misused state or an untyped data layer; an ugly UI can sit on sound code. Find out which, tell the person, and recommend working only on what needs it.

## Gates

The phases are gated. A gate is passed only when its output has been shown to the person in chat. Before starting a phase, point to the previous gate's output; if you can't, stop and go back. "The request seemed clear", "it's a one-shot run" and "they're in a hurry" don't skip a gate. For a small tweak the gates are small, not absent.

| Gate | Passed when | Never before it |
|---|---|---|
| **G1 Intake** | The coverage table is printed with no item Unknown ([02](02-intake.md)) | mockups, plans |
| **G2 References** | Real screenshots gathered and a take/leave table written ([04](04-directions-and-proposals.md) §1) | directions |
| **G3 Direction** (UI track) | The person chose a direction in a self-reviewed HTML prototype ([04](04-directions-and-proposals.md) §2–3) | plan, foundations, screens |
| **G4 Plan** | The person approved the sized, phased plan ([07](07-plan-and-build.md)) | foundations, code |
| **G5 Foundations** | Tokens, the style-guide page and token tests that fail on violations exist and pass ([06](06-design-system.md)) | screens |
| **G6 Screen done** | Self-review, viewport sweep and craft checklist pass ([08](08-craft-checklist.md)) | calling it done |

Code-only track: G2 and G3 become "rendering, data and state options presented, one chosen" ([05](05-architecture-and-data.md)).

## Order of operations

1. **Phase 0 — Read before you ask.** Read [01-context-scan.md](01-context-scan.md). Scan the code, docs, history and (if you can see them) the screens. Score both the UI and the code out of 10 and write a short current-state summary. Then read [11-related-skills.md](11-related-skills.md) and suggest skills that fit this stack and surface.
2. **Phase 1 — Intake → G1.** Read [02-intake.md](02-intake.md). Fill the coverage table from what the code and docs answer, ask every Unknown item in one round (options plus a recommendation each), print the table, and don't move on while anything is Unknown. Offer the layout rules in [09-layout-rules.md](09-layout-rules.md).
   **Phase 1b — Size it.** Read [03-sizing-and-approach.md](03-sizing-and-approach.md). Effort levels in days, commits and tokens at the person's pace; recommend one for what the project is to them; say whether it can go in gradually or needs a rebuild.
3. **Phase 2 — References and prototype → G2, G3.** UI track: read [04-directions-and-proposals.md](04-directions-and-proposals.md) and [13-ui-styles.md](13-ui-styles.md). Get real screenshots of the products named (or find references yourself), write the take/leave table, then build one self-contained HTML prototype with 2–3 directions, at least three screens and switches. Self-review it ([08](08-craft-checklist.md) §4) before showing it. Code track: read [05-architecture-and-data.md](05-architecture-and-data.md) and present options. Record each decision and what lost.
4. **Phase 3 — Plan → G4.** Read [07-plan-and-build.md](07-plan-and-build.md). A plan in phases on the chosen direction, each phase with its output, review point, size on 0–10 and suggested tests. Stop for approval.
5. **Phase 4 — Foundations → G5.** UI: tokens (primitives, then roles), the style-guide page, token tests that fail on raw colours, gradients, unassigned shadows and low contrast ([06](06-design-system.md)). Code: the data seam, error model, state placement ([05](05-architecture-and-data.md)).
6. **Phase 5 — Build phase by phase → G6 per screen.** Per [07](07-plan-and-build.md): one screen or area at a time, self-reviewed, swept across viewports, committed, tracked, with an update to the person after each. Motion and feedback per [14-motion-and-feedback.md](14-motion-and-feedback.md).
7. **Phase 6 — Craft pass.** [08-craft-checklist.md](08-craft-checklist.md) on every finished screen.
8. **Phase 7 — Final report.** Done and verified (with screenshots), what needs the person, what you recommend but didn't do, and what you noticed along the way.

Working agreements (dev server, ports, commits, updates, tests, unattended runs) are in [10-working-agreements.md](10-working-agreements.md).

## Where output goes

Plans, decisions and progress go in the project's docs (match its layout; otherwise `docs/design/`): `PLAN.md`, a progress log, a tracker, one decision record per choice someone could question. Visual proposals go in `docs/design/proposals/` as self-contained HTML. Never leave a decision only in chat.

## Hard rules

- **Pass every gate in order** (table above), printing each gate's output.
- **Obey the track.** "Keep the UI as it is" means no visible change, proven by before/after screenshots. "Only restyle" means no behaviour or data-flow change.
- **Build from references, not imagination.** Real screenshots of real products, decoded into a take/leave table, before any direction. If you can't reach a site, say so and use others; never describe a product from memory as if you'd looked.
- **Review before you show.** Render at phone and desktop widths, look at the screenshots yourself, list the tells and banned items ([08](08-craft-checklist.md) §1), fix every one plus any obvious bugs, re-render. Never present output you haven't looked at.
- **Meet the positive requirements**, not just the ban list: a real embedded typeface, one icon set at one stroke, the real product as the hero visual, a colour roles table with measured contrast, specific copy, labelled sample data ([08](08-craft-checklist.md) §2).
- **Fix feedback in full passes.** When the person says "looks like AI" or similar, list every tell on the screen, remove them all, re-render and re-check before showing again. Never one tell per round.
- **Plan, size and get approval before building**, with the size on 0–10 and in days, commits and tokens at their pace. Fit the effort to what the project is.
- **Ask with options and a recommendation**, never an open "what do you want?". Their stated preference beats your recommendation; say once what you'd do differently, then do theirs well.
- **Judge by coherence, not taste.** Borders can be excellent; client rendering can be right.
- **Every value is a token; every external call goes through one seam.** Tests fail on raw colours, gradients and shadows the surface system doesn't assign; no `fetch` in screens; sample data behind the same seam and schemas, never in production.
- **Every screen designs its states and answers every action**, even on a slow network ([14](14-motion-and-feedback.md)).
- **Responsive is a gate:** the viewport sweep ([08](08-craft-checklist.md) §5) passes with no sideways scroll, clipping, overflow or undersized targets; no fixed pixel heights on content.
- **Plain language and honesty.** Never invent numbers, testimonials or users; never claim a check you didn't run.
- **Follow the person's sketch or order before improving on it**, and say what you'd change and why.
