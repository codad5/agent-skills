# Reference cases

Three real revamps behind this skill. Read them for how decisions were made and what went wrong — not as looks to copy. Each product's answer was different because its users and domain were.

## 1. An internal operations console (healthcare admin)

**Context.** Staff (support, ops, finance) and non-technical founders use it all day to look up a patient, approve a payout, compare weeks. The old UI scored 5.5/10: hex tokens leaking into components (17 raw hex, 33 default-palette classes), 170 of 254 files client-rendered, three date pickers, `Loading...` fallbacks, brand-tinted bordered stat cards with an icon on top.

**What didn't work.** A first pass restyled the old UI in place: a token layer, a palette sweep, new fonts, a "complete dashboard UI pass". It still felt the same.

**What did.**
- Rebuilt **beside** the old UI under its own route group and root layout; screens moved one at a time; the old UI stayed reachable until cutover, then became opt-in.
- A written plan: current state scored, references with take/leave (Linear's shell, Stripe's data, Vercel's type), design system, phases, and an ADR per decision.
- **Calm and dense, accent rationed:** the brand green only for the primary action, active nav and focus, and good data; everything else neutral. A deeper green for buttons because white on the brand mint was 2.6:1.
- **Tonal, almost borderless surfaces** to match the brand's website: soft grey canvas, white panels, grey wells; borders only for row dividers; pill controls.
- A UI face with real tabular figures plus the brand's display face only for titles and headline numbers.
- Tokens in three OKLCH layers with the framework palette switched off; lint errors for margins, raw colours and arbitrary values; a contrast test reading the real CSS; a validated chart palette (the draft failed colour-blind separation on blue next to violet).
- A component gallery reviewed before any screen.
- Signature pieces: a "needs attention" inbox on Home, an activity heatmap, stat cards with a range pill, plain-language definitions on hover and change coloured by whether it's good, ⌘K, person previews everywhere.

**Lessons from running it.** Plain language mattered more than polish ("Not tracked (before 7 Oct)" instead of "Unknown"; explaining what "Abandoned" means). Numbers had to be checked against the backend before display. Sensible defaults (this quarter, not all time), collapsing sections that don't need attention, confirming wide-impact switches, and previewing what end users receive all came from owner feedback.

## 2. A school management product (app + marketing site)

**Context.** School staff, students and parents, many not fluent with software, often on phones.

**What didn't work.**
- The original: dark by default, an always-dark sidebar, glow blobs, rainbow icon chips. The owner said it "looks like AI slop".
- A second pass following a written brief ("Stripe clean", one accent, lighter titles, borders over shadows) was rejected as too austere — also "AI slop".
- The marketing page was redone twice in one day; uniform sections with the same card and the same fade read as generated.
- The approved mockup's dark mode put the brand purple on every surface; it shipped as a "purple haze" and had to be rebased onto near-neutral greys.

**What did.**
- The owner's own words plus reference screenshots per surface, turned into a synthesis ("Notion's approachability with Stripe's precision").
- **A standalone HTML mockup** of the dashboard with real local sample data, light and dark, and a switch between the four personas. Approved in one round; written up as the spec.
- **Friendly and colourful, but disciplined:** six tints in bg + ink pairs, each owned by a metric by meaning (money collected is always amber, outstanding always rose), status colours separate, tables and forms kept quiet.
- Each persona's dashboard framed by the question it answers ("Is the money coming in, and what's stuck?"). Warm, plain copy.
- Component-first: a page is a composition; extract the second time a pattern appears.
- Mobile-first for phone personas; a tracker per page (Loads / Routed / Styled with commit hashes); a "shell pass" for huge pages; detailed handoff notes.
- Marketing: section rhythm as the design, numbered sections, type as structure, the real product, no invented numbers, works with JS off, self-hosted fonts, consent-gated analytics, SEO basics.

**Lesson.** Building from a written direction without a cheap visual cost three passes. Show contrasting directions first, and ask "calm or colourful?" explicitly.

## 3. A short-video creation product (bordered, true-black UI)

**Context.** Creators making ranked short videos; the product's output is visual.

**How the direction was chosen.**
- SVG sheets showing the same mini UI per option, each with values, a character note and measured contrast — exploring axes, not just hues (soft accents, sharp accent rules, sharp + subtle, monochrome, grey ladders, colour blocks). The owner's original lavender was kept "for comparison" and critiqued on the sheet (2.7:1 contrast, gradient a common AI tell).
- The owner deferred, then chose from **a finished landing page that switched four named palettes live**: true black with highlighter yellow and one variable typeface. The record gives each loser a "lost because" line (violet: the default AI colour; red: blurs with danger). Alternates stay as switchable token sets.

**Why its borders work.** A measured lightness ladder with the border a step above every surface; greys tinted toward the accent; one 1px weight where interaction changes colour, not weight; dividers and pressable outlines use different colours (a divider-coloured outline button looked like plain text); hairline rows instead of a card per block; borders instead of shadows on black; a single signature device (an offset outline frame) reserved for the few things meant to be pressed first.

**What went wrong.** A new marketing site shipped without anyone looking at it and was rated 1/10: crammed cards with no sign they were clickable, gaps so large it looked generated, drift from the owner's sketch, the wrong audience named. The rule since: screenshot at phone and desktop width before reporting, and follow the owner's sketch before improving on it. Other fixes: fold rarely used controls, use the desktop's width, redraw native controls for dark mode, self-host fonts.
