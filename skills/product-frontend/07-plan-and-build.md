# Phases 3 and 5 — Plan and build

Goal: an approved, phased plan, then the work built one phase and one screen at a time, each verified and logged, with the person updated after each, so progress survives sessions and any agent can pick it up.

## 1. The plan (write it once the needs are clear; get it approved before building anything bigger than a small fix)

The plan is how the person stays in the loop: they see the whole job, its size, the order, and where they'll be asked to look. Write it as a local Markdown file in the project's docs, not only in chat.

```md
# <Product> frontend plan

## 1. Current state — UI <score>/10, code <score>/10   (from Phase 0, with both scored tables)
## 2. Project, track, scope, effort                    (what it is to them; UI / code / both; new / revamp / adjust / polish; effort level chosen and why; gradual or rebuild; what stays untouched)
## 3. Direction                                       (UI track: chosen direction, references take/leave, colour strategy, what lost and why)
## 4. Design system                                   (tokens, surfaces, type, density, motion, layout rules if accepted)
## 5. Architecture and data                           (code track: rendering model, data seam, sample data, errors, state, permissions; only what changes)
## 6. Signature components                            (the few things that make it this product)
## 7. Information architecture                        (nav groups, screens, what each answers)
## 8. Phases                                          (table below)
## 9. Tests proposed                                  (per phase, with the reason; the person may trim or decline)
## 10. Rules to revisit                               (existing choices you'll change and why)
## 11. Decisions                                      (table: question, decision, record link)
```

The phases table is the heart of it:

| # | Phase | Output the person can see | Size (0–10) | Risk | Tests proposed | Review point |
|---|---|---|---|---|---|---|
| 1 | Foundations: tokens, fonts, lint gates | Gallery route with every primitive, light and dark | 3 | low | contrast test, token drift test | **You review the gallery before screens** |
| 2 | Data seam + sample data | Home renders from sample data with the badge on | 4 | low | schema contract tests (live and sample) | — |
| 3 | Home and the main list | Two screens done, screenshots at phone and desktop | 5 | medium | action validation, list flow end-to-end | **You review the first screens** |
| … | | | | | | |
| | **Whole job** | | **7/10** — touches most screens; data layer replaced | | | |

- **Order phases by risk and dependency**, not preference: foundations before screens, the seam before the screens that use it, the riskiest unknown early. Each phase ends in something demonstrable and has a definition of done (checks green, tracker ticked, progress entry written).
- **Size honestly** on 0–10 (0–100 if the person wants detail), with one line of why. When the maintainable fix is a rewrite, say so and offer the lighter alternative with its own size and what it leaves unfixed.
- **Mark the review points.** These are the places you stop and wait: the direction, the gallery, the first screen, each section, the cutover.
- **Then stop and ask for approval.** "Here's the plan: 6 phases, about 7/10 overall. I'd stop for your review after phases 1 and 3. Approve, or change anything?" Don't start phase 1 until they say yes.

Keep it plain: "Payouts waiting for approval: 4" beats "actionable KPI surface".

## 2. Beside or in place

- **Beside (recommended for revamps):** the new UI lives in its own route group or behind a flag with its own root layout and stylesheet; it never imports old UI code (lint); screens move over one at a time; the old UI stays reachable until cutover, then becomes opt-in. Owners rejected in-place token sweeps twice in our history because the result was "the old page with tokens swapped in".
- **In place:** for small apps or a polish pass. Still do tokens and components first, then sweep.
- **"Shell pass" for huge pages:** when a page is too big to rebuild safely now, wrap it in the new shell and components (page body, header, data cards) with logic untouched, mark it for a deeper rebuild, and move on.

## 3. Rollout order

1. **Foundations:** tokens, fonts (self-hosted), theme switching without flash, lint rules, the design-system import alias.
2. **Primitives**, each with tests (and an accessibility check), then **patterns** (shell, page header, data table, detail layout, states), then **charts**.
3. **Gallery review with the person.** Nothing screen-level before this.
4. **Screens**, highest traffic first (home, the main list and its detail), then the rest by area.
5. **Verification:** end-to-end flows, permissions per role, screenshots light/dark, accessibility.
6. **Cutover**, then the old UI opt-in or removed.

## 4. Per-screen loop

1. Look at the live screen and the approved direction side by side.
2. Decide what the screen answers; cut what doesn't serve it; fold what's rarely needed (show what's being worked on, collapse the rest).
3. Map every element to a component; build or extend missing ones first (never hand-roll in the page).
4. Compose: one primary action in the header; secondary forms in dialogs or sheets; long forms become pages with sections, not giant modals.
5. Design every state: skeleton, empty, error, offline, long values, many rows, zero rows.
6. Wire data through the seam per the agreed rendering model ([05](05-architecture-and-data.md)): view state in the URL, writes validated on both sides. On a code-only track, steps 2–5 don't apply: keep the markup and classes identical and take before/after screenshots.
7. Check permissions are unchanged (UI and server).
8. **Verify in a browser** (a dev server only if the person agreed, on a non-default port; see [10](10-working-agreements.md)): phone (360 and 390px) and desktop (1280–1440px), light and dark, long formatted money, slow data. No horizontal scroll on the page. Screenshot.
9. Typecheck, lint, the agreed tests, build. One commit per screen or area, pushed if the project pushes every commit.
10. Tick the tracker with the commit hash, and post a short update: done, what's left of the whole job, next.

## 5. Tracking and handoff

- **Screen tracker** (`docs/design/TRACKER.md`): one row per screen, independent columns: Loads · Routed · Styled · States · Verified (phone/desktop, light/dark), with the commit hash beside each tick; 🟡 for shell-pass-only.
- **Progress log** at the end of each session: done, found along the way (not fixed), next, open questions.
- **Handoff note** when work changes hands: read-first list, environment setup, the per-screen loop, component inventory, gotchas, what's left, the rules the owner cares about most.
- **Owner instructions file** for standing preferences said in chat (push every commit, review flow, style rules), so they survive sessions.

## 6. Feedback rounds

Owner feedback is often vague ("it's just there", "looks generated"). Turn it into concrete levers before changing anything: depth? motion? personality (a ghost icon, a signature element)? hierarchy? density? colour? Propose two or three with your recommendation, try the risky ones in a throwaway preview (light and dark) first, then apply inside the shared component so every screen benefits.

## What NOT to do

- Don't start building before the plan is approved, or screens before the direction and the gallery are.
- Don't hide the size of the job. A surprise rewrite halfway through breaks trust; say it in the plan.
- Don't report a screen done without having seen it at phone and desktop width in both themes.
- Don't mix old and new UI code in one screen.
- Don't fix a visual issue in one page when it lives in a component; fix the component.
- Don't let progress live only in chat.
