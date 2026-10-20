# Phase 6 — Craft pass, self-review and viewport sweep

Goal: nothing reaches the person looking generated, broken or untested on real screen sizes. This file is used three times: on every prototype before it's shown (Phase 2), on every screen before it's called done (Phase 5), and whenever the person gives visual feedback.

## 1. The ban list and the tells

**Banned by default.** None of these appear in a first proposal or a finished screen. The only exception is when the person asks for one, or the approved surface system gives it a specific job ([06](06-design-system.md) §2: soft shadows on floating menus in a tonal system, elevation in an elevated-cards system); then it's a token, not a one-off.

- Gradients (backgrounds, buttons, text, borders)
- Glows and coloured halos
- Drop shadows on page content
- Blurred colour orbs or blobs
- Centred everything (headings, body text, cards)
- Icon-in-a-tinted-box cards; the three-column "icon, bold title, two grey lines" grid
- Fallback or system font stacks as the product's face (Georgia, Times, Arial, `system-ui` alone)
- Inter by default (fine only when the brand uses it or the person chooses it)
- Purple or violet on white by default
- Emoji or text glyphs as icons; mixed icon sets
- Uniform card grids where every block is the same card
- Gradient placeholder thumbnails with pills on them
- Hairline boxes around every block

**The tells.** Each one makes a screen read more generated. Count them.

| Tell | Instead |
|---|---|
| Every block in a bordered rounded card | A card only for a real boundary; otherwise spacing, alignment, hairline rows |
| Icon in a tinted box on every stat card | Let the label and number lead; icons only where they aid scanning |
| Same gap everywhere | Tight within a group, wide between groups, widest between sections |
| Brand hue on every surface in dark mode ("purple haze") | Near-neutral dark surfaces; hue in accents and tints only |
| Austere monochrome dashboard for a friendly audience | Meaning-assigned hues or a rationed accent, chosen with the person |
| A row of same-coloured cards | Hierarchy, or hues by meaning |
| Vague copy ("Revolutionise your workflow") | The specific sentence; written before the layout |
| Spinner on an empty page; "No data" | Skeletons shaped like the content; empty states that teach |
| Abstract stock illustration, 3D blobs, "team at laptop" | The real product or an honest built mockup |
| Invented numbers, logos, testimonials | Real numbers, or none |
| Every section the same height and shape | Vary density and shape; a dense section earns the breathing room after it |
| Marketing spacing in a tool | Tools are dense |
| Narrow centred column on a wide screen | Use the width; start beside the sidebar |
| Colour on big surfaces | Colour on actions, icons, chips and data |

Review questions: **Could this be any other product?** **Delete the icon, the border, the card: is it worse?** If not, delete it.

## 2. Required in every proposal and screen

Avoiding the ban list isn't enough; these are what make a page look designed.

- **A real typeface, embedded:** a font file (self-hosted, or a pinned webfont link in a prototype) chosen for the product, with real tabular figures for numbers. A fallback stack alone looks generated.
- **One icon library at one stroke weight and size scale.** Never mixed sets, never emoji.
- **The real product as the hero visual:** the actual main screen with realistic data (result cards, badges, numbers), not decoration or an abstract illustration.
- **A colour roles table with measured contrast:** each colour's job, and the ratio of every text/background pair printed (target 4.5:1 for text, 3:1 for large text and controls).
- **Colour on jobs, not surfaces:** brand colour for identity and primary actions; any extra hues each mean one thing and appear on icons, chips and data, at most two per area, dark ink on a pale tint for text.
- **Varied section shapes** on marketing pages; **left-aligned content** (centre only a short hero line if at all).
- **Specific copy** in the product's own terms.
- **Honest sample data,** labelled as sample where a real person could mistake it for real.

## 3. The levers that create quality

1. **Hierarchy with size, weight, colour and spacing together**, in the fewest levels. Three text colours (`fg`, `fg-muted`, `fg-subtle`) do more than five sizes. Body line height ~1.5–1.6.
2. **Density matched to the job.** Tables over cards when people compare or scan.
3. **States.** Loading (skeleton), empty (teaches, with the action right there), error (what happened, what to do, a request id), offline, permission denied (names what's missing), long and odd data.
4. **Motion that explains**, under 200ms ([14](14-motion-and-feedback.md)). Decorative motion is removed.
5. **Optical alignment** where maths looks wrong.
6. **Plain language.** "Not tracked (before 7 Oct 2026)" beats "Unknown"; "Billed, not paid" beats "Potential revenue delta".
7. **Honest numbers.** Check figures against the source; label samples; "not available yet" instead of a misleading zero.
8. **Defaults that fit the job.** The period people actually look at; sections collapsed when they don't need attention; wide-impact switches confirmed with what will happen.
9. **Show the outcome.** Preview what a user will receive next to the settings that shape it.

## 4. Self-review loop (before showing anything)

Run this on every prototype and every screen, before the person sees it:

1. **Render** at a phone width (390px) and a desktop width (1440px), light and dark, and **look at each screenshot yourself.** Not the code: the image.
2. **Fix obvious bugs first:** text the same colour as its background (dark text on a dark button), wrapped or clipped placeholders and labels, see-through sticky headers, overlapping elements, broken images, horizontal scroll.
3. **List every banned item and every tell** (§1) on the screen, with where it is.
4. **Check the requirements** (§2): typeface loaded (not falling back), one icon set, real product shown, contrast numbers printed.
5. **Fix all of them**, re-render, and repeat from step 1 until the ban list is clear and no tells remain that you can't justify.
6. **Present with the result:** "Self-reviewed at 390 and 1440, light and dark: 0 banned items, 0 tells; all text pairs ≥ 4.5:1 (table below)."

If you can't render or see screenshots, say so before presenting, and ask the person for screenshots or permission to set up a browser.

## 5. Viewport sweep (a gate for every screen)

Check every screen at these sizes:

| Width × height | Why |
|---|---|
| 320 × 568 | smallest phones |
| 360 × 740 | common Android |
| 390 × 844 | common iPhone |
| 430 × 932 | large phones |
| 568 × 320 | small phone sideways |
| 844 × 390 | phone sideways |
| 768 × 1024 | tablet portrait |
| 1024 × 768 | tablet landscape, small laptop |
| 1280 × 600 | short laptop window |
| 1280 × 800 | laptop |
| 1440 × 900 | common desktop |
| 1680 × 1050 | large laptop |
| 1920 × 1080 | desktop monitor |
| 2560 × 1440 | large monitor |

It **fails** on: sideways scroll; clipped or cut-off content; elements sticking out of their container or the viewport; controls smaller than 40 × 40px on touch sizes; text overlapping; content hidden behind sticky bars with no way to reach it. **Never give content a fixed pixel height;** let it grow, and use min-heights or the layout's own sizing.

A script makes the sweep fast and repeatable (Playwright shown; adapt to your browser tool):

```js
// for each size: await page.setViewportSize({ width, height }); then:
const problems = await page.evaluate(() => {
  const out = [];
  const vw = document.documentElement.clientWidth;
  if (document.documentElement.scrollWidth > vw) out.push(`sideways scroll: ${document.documentElement.scrollWidth} > ${vw}`);
  for (const el of document.querySelectorAll("body *")) {
    const r = el.getBoundingClientRect();
    if (r.width === 0 || getComputedStyle(el).visibility === "hidden") continue;
    if (r.right > vw + 1) out.push(`sticks out: ${el.tagName}.${el.className}`);
    const s = getComputedStyle(el);
    if ((s.overflow === "hidden" || s.textOverflow === "clip") && el.scrollWidth > el.clientWidth + 1 && !el.closest("[data-allow-clip]"))
      out.push(`clipped: ${el.tagName}.${el.className}`);
    if (el.matches("a, button, input, select, [role=button]") && vw < 768 && (r.width < 40 || r.height < 40))
      out.push(`small target ${Math.round(r.width)}×${Math.round(r.height)}: ${el.tagName}.${el.className}`);
  }
  return out;
});
```

Screenshot at least the phone, sideways phone, short-window and desktop sizes, and look at them.

## 6. Decoding visual feedback

When the person says "it looks like AI", "vibecoded", "generic", "something's off":
1. **Don't fix the one thing they named and re-show.** That turns into five rounds.
2. Run §1 on every screen in one pass and list everything you find, including what they didn't mention.
3. Remove all of it, re-render, run the self-review loop (§4), then show, with the list of what changed.
4. If the feedback is about a feeling ("cold", "busy", "just there"), translate it into levers (depth, colour, density, type, motion, personality), propose two or three with a recommendation, and try them in a throwaway preview first.
5. Ask whether the references still hold: repeated "looks generated" usually means the direction was built from imagination, not references; go back to G2.

## 7. Per surface

**Dashboards and admin consoles.** Home answers "what needs a human now?" before showing stats. Big numbers with a plain label, a range pill and a definition on hover; change coloured by whether it's good. One primary action per screen. ⌘K to jump to a record. Lists with URL filters, clear empty states, pagination that can jump. Dense, calm; colour carries meaning.

**Chat interfaces.** Messages dominant, chrome minimal. Clear speaker distinction without heavy bubbles everywhere; readable line length (~60–75 characters); timestamps quiet until needed. Streaming without layout jumps; a visible stop control; errors inline with a retry. Composer always reachable, growing with content, Enter to send, Shift+Enter for a new line. Empty state offers real starting prompts. Long code and tables scroll inside the message. Mobile: composer above the keyboard.

**Marketing pages.** Lead with the outcome and show the real product on the first screen. Vary section background, width and shape; never two identical sections in a row. Type as structure. One specific, defensible claim per section; no invented social proof. Works with JS off; reveals fail visible. Self-hosted fonts with preload; per-page title, description, canonical, one `h1`, OG image, structured data; analytics only after consent.

**Forms and settings.** Grouped by what people are trying to do. Labels above fields, hints under them, errors on the field in plain words. Save per section, sending only what changed. Preview the effect. Confirm wide-impact changes with what will happen.

**Mobile and phone-first portals.** Design at 360–390px first. Sidebar becomes a drawer; tables become stacked cards or a contained horizontal scroll; tap targets at least 40px; the primary action reachable without scrolling; long values must fit.

**Printable documents** (receipts, invoices, report cards). Masthead, title rule, details band, tabular figures, totals summary, print CSS for A4/Letter; the app's tokens.

## 8. Pre-flight checklist (per screen)

- [ ] Self-review loop (§4) done; screenshots looked at.
- [ ] Ban list clear; tells listed and fixed; requirements (§2) met.
- [ ] Viewport sweep (§5) passes at all 14 sizes.
- [ ] No raw colours, arbitrary values, margins or `space-*`; padding symmetric; `absolute` only in `relative`.
- [ ] Built from shared components; nothing appearance-related hand-rolled in the page.
- [ ] Every state designed: skeleton, empty, error, offline, long data.
- [ ] Every action acknowledged within ~100ms; no full-page blocking; failures keep input and offer retry; checked on a throttled network ([14](14-motion-and-feedback.md)).
- [ ] Copy plain and specific; numbers checked and formatted (tabular figures).
- [ ] Contrast AA in light and dark (numbers recorded); focus visible; keyboard works; reduced motion respected.
- [ ] Typecheck, lint, tests and build pass.

## What NOT to do

- Don't show anything you haven't rendered and looked at.
- Don't fix feedback one item per round.
- Don't mark a screen done from the code alone or from two widths.
- Don't add personality with decoration (glows, bouncing icons, gradients).
- Don't fix one page's symptom when the component is the cause.
