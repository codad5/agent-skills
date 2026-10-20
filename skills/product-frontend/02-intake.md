# Phase 1 — Intake

Goal: settle the decisions that change the outcome, in one focused round, without asking anything the code already told you.

This is not a fixed questionnaire. Below is a bank of decision areas. For each, Phase 0 tells you whether to skip it (answered), ask narrowly (partly answered) or ask fully (unknown). The questions you actually send should read as if written for this project — the options come from what you found, not from this file.

## How to ask

- **One round where possible.** Use a multiple-choice tool (e.g. `AskUserQuestion`) for clean choices, free text for the rest. Group related questions; don't drip-feed.
- **Every question carries options, a recommendation and a one-line reason.** "Light by default with dark as a full alternative (recommended: your staff work in daylight and the marketing site is light)." Mark the recommended option first.
- **Always offer "show me first".** For anything visual, "show me options before I decide" is a valid answer, and it routes to Phase 2.
- **Build options from context.** Not "pick a colour", but "keep your mint as the brand hue (recommended), shift it deeper for contrast, or explore a new hue — here's why I'd keep it."
- **Say what you assumed.** List the things you didn't ask because the code answered them, so the person can correct one line instead of answering ten questions.
- **Their words beat your guesses.** If the person states a preference, it outranks your recommendation; you may still say once, plainly, what you'd do differently and why.

## Q0a — What the project is to them (always first)

MVP racing for speed, startup building to scale, client project, long-lived product or internal tool, side or learning project? Plus how long it should live, who else works on it, any deadline. It decides how much work to recommend; [03](03-sizing-and-approach.md) has the table. Skip if the docs say it, and state the assumption.

## Q0 — Track

Is this about how it looks, how it works, or both? Phase 0 scored both sides; lead with what you found.

| Option | What it means | Then |
|---|---|---|
| **UI only** | Look, layout, components; behaviour and data flow stay as they are | Q1 and the visual areas; no logic changes |
| **Functionality and code only** | Rendering, data fetching, state, errors, types, performance, structure; **the UI stays pixel-identical** | Skip the visual areas; ask the engineering ones; plan the before/after visual check ([05 §6](05-architecture-and-data.md)) |
| **Both** | A rewrite like a v1 → v2 | Everything |

Recommend from the evidence, even against the wording of the request: "You asked for a redesign, but the screens are in decent shape (7/10). The pain you describe (slow pages, filters resetting) is the code: client-side fetching after load and filters held in component state (4/10). I'd recommend functionality-only first, keeping the UI exactly as it is." The person decides; if they choose a track, never drift outside it.

## Q1 — Scope

Every later question depends on it.

| Option | What it means | Then |
|---|---|---|
| **New build** | No UI yet, or starting fresh | All areas below |
| **Revamp** | Replace the look and structure | All areas; and Q1b |
| **Adjust** | Change specific screens or components | Only the areas those screens touch |
| **Keep the layout, make it nicer** | Same placement and flow, better look | The "polish" branch below |

**Q1b (revamp only) — beside or in place?** Build the new UI beside the old one (a new route group or flag, screens move over one at a time, old stays reachable) or restyle in place? Recommend beside for anything big: an in-place token sweep tends to produce "the old page with tokens swapped in", which owners reject (observed twice). In place suits a small app or a light polish.

### The polish branch ("keep placement, make it nicer")

Ask what's bothering them, then offer levers, each with your read of whether it'd help *here*:

1. **Colour.** "Keep the colours, refine them, or let me suggest a palette?" If refine/suggest: propose a role-based ramp instead of one flat colour — for example, not one purple everywhere but a set with jobs: a deep step for the primary action, a pale tint for selected rows and emphasis panels, a mid step for focus and links, a near-neutral tinted grey for surfaces. Show it (Phase 2).
2. **Surfaces.** "Separate panels by tone (soft canvas, white panels, grey wells), by tone with hairlines only inside dense tables, or by hairline borders?" Recommend from what they have: a bordered UI with inconsistent weights usually needs a border system, not removal.
3. **Type.** Hierarchy (size, weight and three text colours), a display face for titles and headline numbers, tabular figures for amounts.
4. **Density and spacing.** Tighter tables, deliberate rhythm (tight in a group, wide between sections).
5. **Life.** Skeletons, motion that explains (under 200ms), hover states, empty states that teach.
6. **States and copy.** Errors with next steps, plain-language labels.

Recommend the two or three levers with the biggest effect for this UI, and say why ("your issue is mostly hierarchy and states; the colours are fine").

## The decision bank

Ask the ones Phase 0 left open. Each lists why it matters and a good default to recommend when the context doesn't point elsewhere.

1. **Users and surfaces.** Who uses each surface, on what device, how comfortable with software? Which surfaces are in scope (app, marketing, portals, emails, printable documents), in what order? *Why:* drives density, mobile-first, copy tone. Non-technical users and phone-first portals change everything.
2. **What each main screen must answer.** "Home answers: what needs a human right now?" One question per screen or per persona. *Why:* stops dashboards becoming walls of numbers nobody acts on.
3. **Calm and restrained, or friendly and colourful?** Show both if unsure. *Why:* the most expensive unasked question. A dense ops console reads best calm, with one rationed accent; a consumer or school product for non-technical users may read as "generated" when austere, and need a meaning-assigned tint palette. Neither is always right.
4. **References.** "Send 2–4 products or screenshots you like, per surface, and say what you like about each — and one you dislike." Then you decode them ([04](04-directions-and-proposals.md)). *Default:* offer two or three styles from [13-ui-styles.md](13-ui-styles.md) that fit the app type, find real examples of each (Mobbin, Page Flows, Refero, public design systems; through an MCP connector or a browser tool if you have one), and propose references that fit the product type (e.g. Linear's shell, Stripe's data display, Vercel's type for a dashboard; editorial magazines for marketing) and let them confirm.
5. **Brand constraints.** Fixed logo colours, fonts, existing site. Confirm against the actual logo files, not memory. *Default:* keep the brand hue, fix contrast with a deeper step.
6. **Colour strategy.** Monochrome (colour from content), one rationed accent, one sharp accent plus subtle ones, a meaning-assigned tint set, colour blocks. Which colours must stay off-brand (status, data, third-party tiles)? *Default for tools:* one rationed accent — the primary action, active nav, focus, good data — and separate status colours.
7. **Light, dark or both; default?** *Default:* both, following the system; dark as its own designed palette, never the light one inverted with brand hue on every surface.
8. **Surfaces and lines.** Which separation system: tonal (almost borderless), hybrid, bordered hairline, elevated cards, spacing only, dark tonal, grouped inset lists, translucent layers or hard-shadow outlines? Offer the two or three that fit the app type, each with products that use it ([06](06-design-system.md) §2 has the table). Radius by role? *Default:* follow the brand's existing site. Any of them can look excellent when applied as a system.
9. **Type.** One family or a pairing (UI face + display face)? A signature device? Self-hosted? *Default:* a UI face legible at 12–14px with real tabular figures, a display face only for titles and headline numbers; avoid the default face of every generated UI unless the brand uses it.
10. **Density.** Per surface. *Default:* tools dense (14px body, ~40px table rows), marketing generous.
11. **Motion and playfulness.** How much? Must content work with JS off (marketing)? See [14-motion-and-feedback.md](14-motion-and-feedback.md). *Default:* motion only to explain where something came from, under 200ms, reduced-motion respected, content visible if JS fails.
12. **Imagery and claims.** Real screenshots, built mockups, illustration, photography? Which numbers and claims are true? *Default:* the real product; no invented numbers.
13. **Copy tone.** Warm or formal; whose voice. *Default:* plain and specific; labels a non-technical owner understands.
14. **Accessibility, performance, SEO, privacy.** Contrast target, Lighthouse/LCP targets, keywords, analytics consent, what must never be tracked (e.g. a portal with children's data). *Default:* WCAG AA in both themes, self-hosted fonts, consent-gated analytics on marketing only.
15. **Rendering and data fetching.** Server-first, client-side with a query library, or a hybrid? *Default:* server-first where the framework supports it (less JavaScript, data on first paint, secrets stay on the server), a client query library only for live views. If they prefer client-side, do it well ([05](05-architecture-and-data.md)).
16. **State.** Where view state lives (URL recommended), whether a global store stays, which form approach. *Default:* server data never copied into a global store.
17. **Pluggability and sample data.** Which providers or data sources might be swapped (payments, email, analytics, an API that isn't ready)? Want a sample-data mode to build and review before the backend is done? *Default:* one data seam per backend, sample data behind it validated by the same schemas, switched by a flag, never in production.
18. **Layout rules.** Offer [09-layout-rules.md](09-layout-rules.md) (gap-only spacing, symmetric padding, `absolute` inside `relative`, tokens only): recommended for almost all product UI; less suited to animation- or graphics-heavy work. Accept, adapt or skip?
19. **Tests.** Propose the tests worth writing (logic, data contracts, flows, a visual check) with your recommendation; they may trim or decline ([10](10-working-agreements.md)). *Default:* whatever the project already requires.
20. **Dev server.** Who runs it? May you start one, and on which port? *Default:* don't start it unless they agree; never the framework's default port; reuse one that's already running.
21. **Their sketch or order.** "Do you have a sketch, an order, or a page you want first?" *Why:* ignoring a sketch cost one project a full rebuild.
22. **Review and approval.** How will they review (screenshots at phone and desktop, a staging link, a live gallery)? Who approves, at which stage (directions, gallery, first screen, each section)?

## Example of a good intake message

> I read the code and the docs. Assumptions (tell me if any is wrong): Next.js App Router, Tailwind v4; mint #21ba9b stays the brand hue; users are internal staff and non-technical founders; both themes.
>
> 1. **Project** — I read this as a startup product that will grow and hire (from the README). Right, or is speed to launch the priority?
> 2. **Track** — UI and code together (recommended: the screens look dated and every page fetches on the client after load), UI only, or code only with the look unchanged?
> 3. **Scope** — Revamp beside the current UI under `/v2` (recommended: the in-place token pass last month didn't change how it feels), revamp in place, or polish only?
> 4. **Feel** — Calm and dense with the green rationed to actions and good data (recommended for an all-day ops tool), or friendlier with a colour per metric? I can show both side by side first.
> 5. **Surfaces** — Tonal like your marketing site (recommended: same company, calmer screens) or a bordered system?
> 6. **References** — Any products you want it to feel like? If not, I'll propose Linear's shell, Stripe's tables and detail pages, Vercel's type, and show you.

## What NOT to do

- Don't ask an open "what style/colours do you want?". It hands design back to the person and gets a vague answer.
- Don't ask what the code answers, and don't reuse a previous project's answers as defaults for this one.
- Don't skip "calm or colourful" because you have a favourite. It's cheap to show both, and expensive to guess wrong.
- Don't present one option. Two or three, contrasting, with a recommendation.
- Don't recommend a redesign when the problem is the code, or a rewrite when the problem is the look.
- Don't start building because "the request sounds clear enough". A scope or feel mismatch wastes a whole pass.
