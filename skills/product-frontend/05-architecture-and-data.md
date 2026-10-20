# Phases 2 and 4 (code track) — Architecture, data and functionality

Goal: the code behind the screens is as deliberate as the screens: a rendering model chosen for reasons, data behind a seam so sources (live, sample, a future provider) are swappable, state in the right place, errors handled once, and performance and quality measured. Often this is the part that actually needs work; a UI can look fine and sit on a slow, fragile, untyped data layer.

Run this phase whenever the scope includes functionality, and always assess it in Phase 0 even when the ask is "just the look": if the real problem is here, say so.

## 1. Assess before proposing

Score the engineering side the same way as the UI (out of 10, one line of evidence each):

| Area | Look for |
|---|---|
| Rendering model | How much is client-rendered that needn't be; pages that render empty then fetch; waterfalls |
| Data layer | One seam or fetches scattered in components; typed responses; validation at the boundary |
| Errors | One classified error model or ad-hoc `try/catch` and "Something went wrong" |
| State | Server data duplicated into client state; filters lost on refresh; prop drilling; global store for local state |
| Client data library | React Query/SWR used well (keys, invalidation) or wrapped around server calls for no reason |
| Types | `any` count, `eslint-disable` count, untyped API responses |
| Performance | Bundle size per route, heavy libraries on every page, unneeded re-renders, uncached repeat calls, slow endpoints |
| Structure | 600–800-line components, duplicated per-entity pages instead of one template, hard-coded vendors |
| Pluggability | Can a provider, data source or library be swapped in one place? |
| Tests | Logic, data contracts, flows |

Then tell the person where the effort pays off, plainly: "The UI is in decent shape (7/10). The problem is underneath: every page is a client component fetching after load, filters live in component state, and there are 275 `any`s. I'd leave the styling alone and fix rendering and the data layer first."

## 2. Rendering: choose for reasons, then do it well

**Default recommendation for frameworks that support it (e.g. Next.js App Router): server-first.**
- Pages are async server components that fetch on the server; first paint has data.
- Each independent section streams in its own suspense boundary with a skeleton of the same shape, so a slow chart never blocks a table.
- View state (filters, sort, page, tab, date range) lives in the URL, parsed and validated in one place: shareable, back-button safe, rendered right on the first request.
- Writes go through server actions with validation on both sides, `useActionState` for pending and errors, optimistic updates where predictable, then revalidation.
- Client components only where interaction needs them (menus, dialogs, charts, editors, live views).
- Why: less JavaScript, no empty-then-fetch flash, secrets and tokens stay on the server, simpler state.

**If the person prefers client-side** (an SPA, an existing React Query setup, offline needs, a separate API team), do that well instead of arguing:
- one data library (TanStack Query, SWR), query keys per resource, sensible stale times, invalidation after mutations, optimistic updates with rollback;
- still keep view state in the URL; still validate responses at the boundary; still one error model;
- loading skeletons per section, not a page spinner; prefetch on hover for likely navigation.

**Hybrid is normal:** server-render reads, keep a client query library only for genuinely live data (polling a conversation, progress of a job).

Record the choice and its reasons as a decision; note when to revisit ("a screen needs sub-second live updates").

## 3. The data seam: pluggable and replaceable

Every external call goes through one place, behind an interface the screens don't see past.

- **One client** (e.g. `server/http.ts`) for each backend, returning a typed `Result<T> = { ok: true, data } | { ok: false, error }`. It never throws for expected failures, adds auth, timeouts and request ids, and logs one structured line per call.
- **Data functions per resource** (`server/data/patients.ts`: `listPatients(params)`, `getPatient(id)`) that the screens call. Screens never build URLs or parse responses.
- **Validate at the boundary** with a schema (zod or equivalent). A mismatch is a `contract` error, logged loudly, never passed to the UI as garbage. Lenient on optional fields (`.catch()` defaults), strict on the ones the screen depends on.
- **Errors classified once** into kinds (unauthenticated, forbidden, not found, validation, conflict, rate limited, unavailable, network, contract, unknown), each with one UI and a next step. Backend error codes map to user-facing messages in one catalogue; raw backend text never reaches a user.
- **Sample data behind the same seam.** A mock/sample adapter answers the same data functions, switched by an environment flag or a dev cookie, never active in production. Its output goes through **the same schema** as the live response, so a mock drifting from the backend fails as a contract error. Show a visible "Sample data" badge when it's on. This lets the UI be built and reviewed before the backend exists, and lets tests run offline.
- **Ports and adapters for providers.** Payments, email, storage, analytics, maps, AI models: an interface in the app, one adapter per provider, chosen by configuration. Swapping a provider is an adapter change.
- **Wrap vendor libraries** (UI primitives, charts, date pickers, toasts) so replacing one is a change in one folder (see [06](06-design-system.md)).
- **Config-driven templates** over copy-pasted pages: one partner page driven by data instead of a page per partner; one insights template driven by a metric registry.
- **One owner per number.** When two sources can answer the same question (a live admin API and an analytics pipeline), each metric has one registered source, a plain-language definition and a trend direction, so the same metric never shows two values. Optional sources degrade to a designed "not connected in this environment" state.
- **Check numbers against the source.** Before showing a figure, read how the backend computes it; log gaps (endpoints missing or returning too little) in a backend-gaps document with what to change in the UI when each is fixed.

## 4. State: put each kind in its place

| Kind | Where |
|---|---|
| Server data | Fetched on the server (or one client query cache); never copied into a global store |
| View state (filters, tabs, page, range) | The URL |
| Form state | The form (native forms + server actions, or a form library), validated on both sides |
| Ephemeral UI (open menu, hover) | Component state |
| Truly global client state (theme, density, a draft) | A small context or store, persisted where needed (cookie for theme to avoid flash) |

A global store holding server data is the most common smell: stale data, manual syncing, bugs on refresh.

## 5. Performance and quality

- Measure first: bundle per route, slowest endpoints (with timings), Lighthouse/LCP for public pages. Fix the biggest number.
- Load heavy pieces only where used (dynamic import for maps, editors, big charts); check a new dependency didn't land in the shared bundle every page loads.
- Cache and dedupe repeat reads within a request; avoid request waterfalls (parallel fetches, independent suspense sections).
- Timeouts per call that match the endpoint, retries only for safe reads and connection failures, never for timeouts that would double the load.
- Strict types (no `any`), small components, one library per job, tests where they pay: logic units, data contracts (schemas accept the real and sample shapes), server action validation, end-to-end flows for the critical paths.

## 6. When the person says "keep the UI exactly as it is"

Obey it precisely. Change behaviour, data flow and code structure; don't touch appearance.

- Keep the rendered markup and classes identical unless a change is required to move logic (and then keep the output pixel-identical).
- Prove it: screenshot the affected screens before and after at the same widths and themes, or run visual snapshot tests, and report "no visual change".
- If you notice a UI problem along the way, list it as a suggestion in the final report; don't fix it.

The same applies in reverse: "only restyle, don't touch the logic" means no data-flow or behaviour changes, even ones you'd recommend.

## What NOT to do

- Don't redesign a UI whose real problem is the code, or rewrite code when the ask is only the look.
- Don't force server-side rendering on a person who chose client-side for their reasons; do their choice well and note the trade-off once.
- Don't let screens call `fetch` directly or parse raw responses.
- Don't let sample data bypass the schemas, or be reachable in production.
- Don't hard-wire a provider or vendor library across the codebase.
- Don't trust a number on screen you haven't traced to its source.
