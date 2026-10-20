# Phase 6 — Craft pass

Goal: every finished screen checked against the habits that make a UI read as generated, the levers that make it read as designed, and its surface's own rules. Run it per screen before marking it done.

## 1. The tells

Three or more and the screen reads as generated, however clean the code.

| Tell | Instead |
|---|---|
| Three-column grid of icon + bold title + two grey lines | Vary block shape by content; not everything is a card |
| Purple-to-blue gradient; violet as the default accent | A palette with a domain reason; gradients only with a job |
| Every block in a bordered rounded card | A card only for a real boundary; otherwise spacing, alignment, hairline rows |
| Icon in a tinted box on every stat card | Let the label and number lead; icons only where they aid scanning |
| Same gap everywhere | Tight within a group, wide between groups, widest between sections |
| Everything centred | Centre a hero; left-align content |
| Free-floating blurred colour orbs, glows | Depth from one mechanism (tone, hairline, shadow) |
| Brand hue on every surface in dark mode ("purple haze") | Near-neutral dark surfaces; hue in accents and tints only |
| Austere monochrome dashboard for a friendly audience | Meaning-assigned tints or a rationed accent, chosen with the person |
| A row of same-coloured cards | Hierarchy, or tints by meaning |
| Emoji as icons, mixed icon sets | One icon set, one stroke |
| Vague copy ("Revolutionise your workflow") | The specific sentence; written before the layout |
| Spinner on an empty page; "No data" | Skeletons shaped like the content; empty states that teach |
| Abstract stock illustration, 3D blobs, "team at laptop" | The real product or an honest built mockup |
| Invented numbers, logos, testimonials | Real numbers, or none |
| Every section the same height and shape | Vary density and shape; a dense section earns the breathing room after it |
| Marketing spacing in a tool | Tools are dense |
| Narrow centred column on a wide screen | Use the width; start beside the sidebar |

Review questions: **Could this be any other product?** **Delete the icon, the border, the card — is it worse?** If not, delete it.

## 2. The levers that create quality

1. **Hierarchy with size, weight, colour and spacing together**, in the fewest levels. Three text colours (`fg`, `fg-muted`, `fg-subtle`) do more than five sizes. Body line height ~1.5–1.6 matters more than font size.
2. **Density matched to the job.** Tables over cards when people compare or scan. Show the numbers that drive a decision.
3. **States.** Loading (skeleton), empty (teaches, with the action right there), error (what happened, what to do, a request id), offline, permission denied (names what's missing), long and odd data.
4. **Motion that explains**, under 200ms: panels slide from the edge they're anchored to, dialogs scale in from ~96%, numbers tween on first view, lists stagger once. Decorative motion is removed.
5. **Optical alignment** where maths looks wrong.
6. **Plain language.** "Not tracked (before 7 Oct 2026)" beats "Unknown"; "Billed, not paid" beats "Potential revenue delta". Explain statuses in one line where people see them. A non-technical owner should understand every screen from its headings and numbers alone.
7. **Honest numbers.** Check figures against the source before showing them; label samples as samples; say "not available yet" instead of a misleading zero.
8. **Defaults that fit the job.** The period people actually look at (this quarter, not all time); sections collapsed when they don't need attention and open when they do; destructive or wide-impact switches confirmed with what will happen.
9. **Show the outcome.** Preview what a user will receive (a notification, an email, a WhatsApp message with its button) next to the settings that shape it.

## 3. Per surface

**Dashboards and admin consoles.** Home answers "what needs a human now?" before showing stats. Big numbers with a plain label, a range pill and a definition on hover; change coloured by whether it's good (more churn is red even though it went up). One primary action per screen. ⌘K to jump to a record. Person previews wherever a person appears. Lists with URL filters, clear empty states, pagination that can jump. Dense, calm, neutral; colour carries meaning.

**Chat interfaces.** The conversation is the product: messages dominant, chrome minimal. Clear speaker distinction without heavy bubbles everywhere; readable line length (~60–75 characters); timestamps and status quiet until needed. Streaming text without layout jumps; a visible stop control; errors inline on the message that failed with a retry. Composer always reachable, growing with content, keyboard-first (Enter to send, Shift+Enter newline, shown once). Empty state offers real starting prompts. Long code and tables scroll inside the message, not the page. Mobile: composer above the keyboard, no hidden actions behind hover.

**Marketing pages.** Lead with the outcome and show the real product on the first screen. Section rhythm is the design: vary background, width and shape (dark → vivid → white → tint …), never two identical sections in a row. Type as structure (large headlines running 2–3 lines, numbered sections). One claim per section, specific and defensible; no invented social proof. Works with JS off; reveals fail visible; reduced motion respected. Self-hosted fonts with preload (one site went from 4.1s to 2.2s LCP); per-page title, description, canonical, one `h1` with the head keyword, OG image, structured data; analytics only after consent. Check 360/768/1280/1920 with no horizontal scroll.

**Forms and settings.** Grouped by what people are trying to do, with a short description per group. Labels above fields, hints under them, errors on the field in plain words. Save per section, sending only what changed; show what's saved. Collapse sections that don't need attention. Preview the effect. Confirm wide-impact changes in a dialog that says what happens.

**Mobile and phone-first portals.** Design at 360–390px first. Sidebar becomes a drawer; tables become stacked cards or a contained horizontal scroll; tap targets at least 40px; the primary action reachable without scrolling; long money values must fit; no fixed heights that spill.

**Printable documents** (receipts, invoices, report cards). Masthead, document title rule, details band, tabular figures, totals summary, print CSS for A4/Letter; matches the app's tokens.

## 4. Pre-flight checklist (per screen)

- [ ] No raw colours, arbitrary values, margins or `space-*`; padding symmetric; `absolute` only in `relative`.
- [ ] Built from shared components; nothing appearance-related hand-rolled in the page.
- [ ] Every state designed: skeleton, empty, error, offline, long data.
- [ ] Every action acknowledged within ~100ms; no full-page blocking; failures keep input and offer retry; checked on a throttled network ([14](14-motion-and-feedback.md)).
- [ ] Copy plain and specific; statuses explained; numbers checked and formatted (tabular figures).
- [ ] Contrast AA in light and dark; focus visible; keyboard works; reduced motion respected.
- [ ] Seen in a browser at phone and desktop width, light and dark; no horizontal scroll; screenshots taken.
- [ ] Fewer than three tells from §1.
- [ ] Typecheck, lint, tests and build pass.

## What NOT to do

- Don't mark a screen done from the code alone.
- Don't add personality with decoration (glows, bouncing icons, gradients without a job).
- Don't fix one page's symptom when the component is the cause.
- Don't polish the happy path and leave the states for later.
