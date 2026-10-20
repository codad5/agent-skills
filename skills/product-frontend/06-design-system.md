# Phase 4 (UI track) — Design system

Goal: a foundation where the look is driven entirely by tokens and a small set of owned components, enforced by lint, so screens can't drift and a theme, brand or density change is one file. Build this before screens: a screen pass on one-off CSS is redone later.

Adapt the mechanics to the stack (Tailwind, CSS modules, plain CSS, React Native, Flutter); keep the principles.

## 1. Tokens

**Three layers.** Components only ever touch the top one.

```
tokens/
  primitives.css   raw ramps (gray, brand, status hues), OKLCH. Never used by components.
  themes/light.css role → primitive   (:root, [data-theme="light"])
  themes/dark.css  role → primitive   ([data-theme="dark"])
  brands/<name>.css brand hue and its steps ([data-brand])
  tokens.css       exposes roles as utilities (Tailwind v4: plain `@theme`, not `inline`, so values resolve at runtime)
```

- **OKLCH** for primitives: equal numeric steps look like equal perceived steps, so tints and ladders stay even.
- **Runtime switching:** theme × brand × density as data attributes. A new theme, brand or palette is one file; any subtree can switch (a light island in a dark page).
- **Switch the framework's default palette off** (Tailwind v4: `--color-*: initial`), so `bg-green-500` and `text-[13px]` simply don't exist.
- **Roles, named by job:** `canvas`, `surface`, `surface-raised`, `surface-sunken`, `surface-hover`, `overlay`, `border`, `border-strong`, `fg`, `fg-muted`, `fg-subtle`, `fg-disabled`, `accent` (+ `-hover`, `-subtle`, `-fg`, `on-accent`), `brand`, `focus`, `success/warning/danger/info` (each + `-subtle`), `chart-1…6`, `heat-0…4`.
- **Write each token's purpose beside it.** A token nobody can describe gets misused, and adding one is a design decision.
- **Other scales are tokens too:** type roles (not just sizes: `display`, `numeral`, `heading`, `body`, `meta`), radius, shadow/elevation, motion durations and easing, z-index layers, layout (page max width, gutter), density (control heights, row padding).
- **Status colours are semantic only:** success = paid/active, warning = pending/partial, danger = failed/overdue, info = in progress. Never reused as "series 4".
- **Data viz:** a categorical palette in a fixed order, validated for colour-blind separation in both themes (one draft failed on blue next to violet); a single-hue sequential scale for heatmaps.
- **Tests:** a contrast test that reads the real token files and checks every text/background pair, focus visibility and panel separation in both themes; a drift test for any JS-side colour constants (charts, OG images).

## 2. Surfaces and lines: three systems that all work

**Tonal (almost borderless).** Content is separated by surface tone, not lines. Calm, few lines, and often what a brand's marketing site already does. Works when:
- **three tones do the layering:** `canvas` (soft grey page background) → `surface` (panels floating on it) → `surface-sunken` (grey "wells" inside a panel that group related content; inputs). The steps must be far enough apart to read on a cheap screen and close enough to stay calm;
- **borders are for dividers only:** rows in tables and lists, a header rule. Panels and cards carry no border. To separate two blocks, change the tone or use spacing; never add a border;
- **emphasis panels use subtle tints** (`accent-subtle`, `info-subtle`, …) instead of a heavier outline;
- **elevation only for things that float** (menus, popovers, dialogs, toasts): `surface-raised` plus one soft shadow. Panels on the page don't get shadows;
- **dark mode keeps the same steps inverted**, and panels may take a hairline where tone alone is too low-contrast (dark tones sit closer together);
- **contrast is checked on all three tones**, not just white. A darker canvas can push muted text and warning colours under 4.5:1, so you may need to darken them a step;
- **pill controls** (buttons, segmented controls, tabs, badges fully rounded) often go with it, especially when the brand's CTAs are pills.

**Somewhat borderless (hybrid).** Tonal layering for the page and panels, plus a hairline system only where structure is dense: data tables, settings lists, form sections. Pick this when screens mix calm overviews with dense data. The rule that keeps it coherent: tone separates *areas*, hairlines separate *items inside an area*, and the same element never gets both.

**Bordered (hairline system).** Works when it's a system, not decoration:
- a measured lightness ladder where the border sits a step above every surface, so one hairline reads on canvas and panel alike;
- neutrals tinted toward the accent, so lines belong to the palette;
- one weight (1px; inset ring for inputs, no layout shift); interaction changes colour, not weight;
- a border's job decides its colour — dividers use `border`, pressable outlines use a stronger `fg-subtle` (a divider-coloured outline button looks like plain text on dark);
- hairlines between rows, not a box around every block;
- on true black, borders replace shadows (dark shadows vanish, light ones glow).

**Worked example: why one product uses borders and another doesn't** (OKLCH lightness from two real token sets):

| | Bordered, true-black creative tool | Tonal, light ops console |
|---|---|---|
| Canvas → panel → raised | 0% → 17.8% → 22.3% | soft grey → 100% (white) → wells at 97.2% |
| Border | 29%: a step above every surface, so one hairline reads on all of them | 91.8%: used only for row dividers |
| Neutrals | tinted toward the yellow accent (hue ~90, chroma ≤ 0.011) | tinted toward the mint brand (hue 170, chroma ≤ 0.005) |
| Depth | no shadows (invisible on black); borders do the job | tone does the job; one soft shadow only on menus and dialogs |
| Why it fits | the content (video) is the colour; structure must stay visible on black | calm all-day work; matches the soft marketing site |

More styles and where each fits: [13-ui-styles.md](13-ui-styles.md).

Either way: **radius by role** (pills for pressables, a smaller radius for inputs and wells, larger for panels) and **depth from one consistent mechanism**. Check border and control contrast in light and dark separately: a border 9–10 lightness points off near-white is hard to see even when dark mode is fine.

## 3. Components

- **Three tiers:** `primitives/` (Button, Input, Select, Dialog, Tabs, Disclosure… no product knowledge), `patterns/` (AppShell, PageHeader, DataTable, StatCard, DetailLayout, EmptyState, ErrorState…), `charts/`. Product code imports one entry point (`@/ds`).
- **Wrap every vendor primitive**, not just complex ones (a rule with exceptions can't be linted). Only the wrapper folder may import Radix/Base UI/cmdk/Recharts. Swapping the library is a change inside one folder.
- **One prop vocabulary:** `variant`, `size`, `tone`, via CVA or equivalent. Few variants: a third button style is a design decision, not a prop to add.
- **`className` from outside is for layout only**, never appearance; appearance overrides from callers are how a design system becomes advisory.
- **Every data component ships a skeleton** with identical dimensions, exported from a server-safe file if the framework splits server/client.
- **States as components:** EmptyState (teaches the next action), ErrorState (by error kind, with next step and a request id), Forbidden (names the missing permission), Offline, NoResults.
- **Wrap or redraw native controls** in dark UIs (white-on-white `<select>`, grey-square switches).
- **Extract the second time a pattern appears**, not the fifth. Drift (two toggle styles, inconsistent tab widths) is a missing component.
- **A live gallery route** renders every component in every variant and state, light and dark side by side. Review there before screens.

## 4. Styling rules (recommended standard; the person decides)

The full rules with examples are in [09-layout-rules.md](09-layout-rules.md). Offer them in Phase 1 with a recommendation; once accepted, they are binding. Summary:

- **Every element is a box.** Parents arrange children with flex or grid; spacing between children is the parent's `gap`.
- **No margins:** no `m-*`, `mx-auto`, `space-x-*`, `space-y-*`. A component never sets its own outer spacing, so it drops into any layout.
- **Deliberate rhythm:** tight inside a group (`gap-1.5`/`gap-2`), wider between groups (`gap-6`), widest between sections (`gap-10`). Not the same gap everywhere.
- **Padding is internal and symmetric** (`p-4`, `px-6 py-3`). One-sided padding only with a comment saying why.
- **`absolute` only inside a `relative` parent.**
- **Page centring with symmetric padding** computed from the max width (`px-page`: max(gutter, (100% − max-width)/2)), not `mx-auto max-w-*`.
- **Colour, radius, shadow, type from role utilities only.** No raw hex/rgb/oklch, no arbitrary values. When the utility system can't express it, inline style reading a variable (`style={{ background: "var(--gradient-hero)" }}`). New need → new token.
- **Density:** tools dense (body 14px, meta 12px, rows ~40px/36px compact); marketing generous.
- **Motion:** token durations, ease-out, under 200ms, transform and opacity only, explains origin, respects reduced motion. Hide-until-JS reveals must fail visible.
- **Optical alignment wins** where maths looks wrong (an icon beside text, a rounded shape beside a square) — the one place symmetry yields, with a comment.
- **Dates and numbers through shared formatters** (one timezone, grouped figures, compact money, tabular numerals); never ad-hoc formatting in a screen.

## 5. Enforcement

Lint, because humans and AI completions default to margins and raw colours:

- errors for margins/`space-*`, arbitrary values, raw colours, `any`;
- `no-restricted-imports` for vendor UI outside the wrapper folder and for old UI code from new code;
- stylelint (or equivalent) keeping token definitions in the token files;
- grep gates in handoffs: free-floating blur orbs = 0, `dark:` overrides in pages = 0 (tokens handle theme), monospace only for identifiers.

An escape hatch needs a written reason; three disables of the same rule means the rule needs discussing.

## 6. Arranging the project

```
design-system/   tokens/, primitives/, patterns/, charts/, motion/, lib/   (the only place vendor UI lives)
app/ or src/     routes and screens: compositions of design-system components plus data
server/          (if server-first) data functions, http client returning a typed Result, error classifier, session
lib/             shared pure helpers: formatters, permissions, domain labels and mappings
docs/            adr/, standards/ (styling, error handling), design/ (proposals, plan, tracker)
```

- **Screens are compositions.** If you're writing `<div className="rounded-xl …">` in a page, stop and make or extend a component.
- **Server-first where the stack allows:** data fetched on the server, view state (filters, tabs, page) in the URL, mutations through server actions, each section in its own suspense boundary with a matching skeleton.
- **One error model:** every backend call returns a typed result; errors are classified once (unauthenticated, forbidden, not found, validation, conflict, rate-limited, unavailable, network, contract) and each kind has one UI.
- **Permission-aware UI** from one source shared with the server: hide what can't be used, or show it disabled with the reason; always enforce server-side too.
- **One library per job** (icons, dates, date picker, toasts, charts); replacing overlapping libraries is part of the system.

## What NOT to do

- Don't let components use primitives or raw values "just this once".
- Don't build a dark theme by inverting light or painting the brand hue on every surface.
- Don't add a variant to escape a design decision.
- Don't start screens before the gallery has been reviewed.
- Don't skip lint enforcement because "we'll be careful": drift starts in the first week.
