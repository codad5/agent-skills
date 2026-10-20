# Phase 0 — Read before you ask

Goal: know enough, about both the UI and the code behind it, that every question in Phase 1 is one only the person can answer, and that every option you offer fits this project. Minutes, not hours. Scope searches to source folders — never grep `node_modules`, build output or vendored code.

## Do first: capability check

- **Can you see the UI?** A browser tool (built-in browser, Playwright, Chrome extension) and a running dev server. If not, say so plainly and ask for screenshots of the main screens, or for permission to start the dev server. Don't judge a UI from code alone and present it as an assessment.
- **Confirm the environment.** Which checkout, which data (sample data, staging, production)? A "missing data" or "404" on a dev server pointed at the wrong database looks like a design bug and isn't one (observed in a real handoff).

## Then read, in this order

1. **Instructions and docs.** `CLAUDE.md`, `AGENTS.md`, `README`, docs index, ADRs, `BRAND.md`, `STYLE_GUIDE.md`, design-system docs, plans, progress logs, handoff notes. These often answer half the intake: brand colour, fonts, styling rules, users, what was already tried.
2. **History.** Git log and PRs touching UI (`design`, `revamp`, `theme`, `token`, `polish`, `redesign`). Look for rejected passes and reversals — they are the most valuable thing you'll find. ("First pass too austere, read as AI", "purple haze in dark mode", "tried to fix the old UI in place, then rebuilt beside it".)
3. **The stack.** Framework and rendering model; styling system (Tailwind v3/v4, CSS modules, plain CSS, a UI kit); primitives (Radix, Base UI, a homegrown set); icons, charts, date picker, toasts. Count overlapping tools (three date pickers is a finding).
4. **The current design system.** Where tokens live and how many layers (raw palette → roles → utilities). Light/dark? Brandable? Density? How leaky: count raw hex/rgb in components, default-palette classes, arbitrary values, inline styles. Numbers make the case ("17 hex literals, 33 default-palette classes").
5. **What already exists and is unused.** Dead skeleton components, unused motion CSS, an old styleguide route. Audit before building something that's already half there.
6. **The screens.** The main 3–5 screens in the browser, light and dark, desktop and phone: layout, density, how surfaces separate (borders, shadows, tone), radius, type, what colour is used for, states (spinner or skeleton? "No data" or a teaching empty state?), overflow.
7. **What the brand looks like elsewhere.** The marketing site, the mobile app, printed material. An internal app usually should look like the same company.
8. **The code underneath** (always, even for a "just the look" request). Rendering model per route (how many pages are client components that fetch after load), where fetching happens (one seam or scattered `fetch`/axios in components), validation at the boundary, the error model, where state lives (URL, component, global store holding server data), how the client data library is used, `any` and lint-disable counts, the biggest components, duplicated pages, hard-wired providers, slow endpoints and bundle size if you can measure, test coverage of logic and flows. The full checklist is in [05-architecture-and-data.md](05-architecture-and-data.md) §1. Numbers make the case here too ("31 of 40 pages are client components; 275 `any`s").

## Then write: the current-state summary

One screen. It opens the plan later and frames the intake.

```md
## Current state
- Stack: Next.js App Router, Tailwind v4, Radix, lucide, Recharts.
- Design system: hex tokens in 2 layers, dark theme bolted on; 17 raw hex + 33 default-palette classes in components.
- Look: bordered white cards on white, accent on every button, Inter, icon-in-a-box on each stat card, spinner-only loading.
- Users: internal ops staff and non-technical founders (README).
- Brand elsewhere: marketing site is tonal, almost borderless, pill buttons.
- History: an in-place token pass last month; still looks the same.
- Code: every page a client component fetching in `useEffect`; filters in component state; 275 `any`; no error model.
- Score UI 5.5/10, code 4/10 (tables). Biggest win: the code. Open for the person: track, scope, keep or replace the accent, density.
```

Score each area out of 10 with one line of evidence:

| Area | Score | Evidence |
|---|---|---|
| Token foundation | 6 | Right layering, but hex and leaks |
| Visual coherence | 4 | Three button styles, two card styles |
| Hierarchy and density | 5 | Everything the same size and weight |
| States | 3 | Spinner everywhere, "No data" empties |
| Accessibility | 5 | Accent on white is 2.6:1 |
| Component structure | 4 | 800-line components, vendor UI imported directly |

And the code, in a second table with the same shape (rendering, data layer, errors, state, client data library, types, performance, structure, pluggability, tests; see [05](05-architecture-and-data.md) §1). Then say in one line where the effort pays off: the UI, the code or both. That line becomes the recommendation for the track question in Phase 1.

## Then: turn findings into the question list

For each decision area in [02-intake.md](02-intake.md), mark it:

- **Answered** → don't ask. State your assumption in the intake so they can correct it: "Your green stays the brand hue; buttons use a deeper step because white on mint fails contrast."
- **Partly answered** → ask narrowly, with a recommendation: "Keep the green to primary actions and good data, or use it more widely?"
- **Unknown** → ask with options built from what you found.

## What NOT to do

- Don't open the intake with questions the docs answer ("what's your brand colour?" when `BRAND.md` says it).
- Don't score or critique screens you haven't actually seen.
- Don't skip the history: repeating a pass the owner already rejected is the most expensive mistake available.
- Don't assume the problem is visual because the request says "redesign", or that it's code because the request says "refactor". Score both.
- Don't treat your first impression as the owner's problem statement. "It looks generic" might mean austere, cluttered, off-brand or lifeless — Phase 1 finds out which.
