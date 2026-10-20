# Phase 2 (UI track) — Directions and proposals

Goal: turn the answers into 2–3 directions the person can see and compare, get one chosen, and record why the others lost. This is the cheapest place to be wrong; building tokens and screens on a direction nobody saw is the most expensive.

## What a direction is

A direction is a set of decisions that work together, with a name and a one-line character:

- **Feel:** calm/dense vs friendly/colourful vs bold/editorial.
- **Colour strategy** (below) and the actual palette.
- **Surfaces:** tonal (almost borderless), hybrid or bordered, radius by role, depth (shadow, hairline, offset frame).
- **Type:** UI face, display face, scale, figures.
- **Density and rhythm.**
- **Signature element:** the one thing that makes it this product (an activity heatmap, a numeral style, an offset frame on primary cards, numbered marketing sections).

Make the directions genuinely different — "same layout in three purples" isn't a choice. Contrast at least one axis: calm vs colourful, tonal vs bordered, monochrome vs accented.

## How to show it

Pick the cheapest format that answers the question, in this order of preference:

1. **A self-contained HTML mockup** of one real screen (the home/dashboard, or the landing hero), with its own `:root` tokens, light and dark via `prefers-color-scheme` or a toggle, and realistic sample data in the product's language and locale. A segmented control can switch personas or directions. This was how a twice-rejected app direction finally got approved in one go.
2. **A prototype that switches palettes live** (`data-palette="a|b|c"` on the root, each a token override set). Choosing from a finished page beats choosing from swatches; one owner deferred the colour decision until they could do exactly this.
3. **SVG or HTML swatch sheets** for colour alone: the same mini UI repeated per option (nav, hero line, primary and secondary buttons, a selected row, a progress bar, a focus ring), each labelled with its values (hex and OKLCH), a one-line character note and its **measured contrast ratio**. Mark one RECOMMENDED. Include the current colour "for comparison" and critique it on the sheet if it fails.

Every proposal file says "Proposal only: nothing in the code uses this yet." Save to `docs/design/proposals/`.

**Review every theme of the mockup critically**, not just light. One approved mockup's dark mode put the brand hue on every surface ("purple haze") and it shipped that way.

## Colour strategies to offer

| Strategy | Fits | Watch |
|---|---|---|
| **Monochrome, colour from content** | Media products (thumbnails, video, photos carry the colour) | Needs strong type and hierarchy to not feel empty |
| **One rationed accent** | Dense tools, ops consoles, developer products | Accent only for the primary action, active nav, focus, live progress, good data; can read austere for consumer audiences |
| **One sharp accent + subtle ones** | Products needing energy without noise | Sharp at most one or two things per screen; never a gradient between them |
| **Meaning-assigned tints** | Friendly products for non-technical users; dashboards of many metrics | Each metric owns a tint permanently (money collected is always amber); status colours stay a separate set; tints in bg + ink pairs |
| **Colour blocks** | Marketing, bold brands | Section rhythm, not app chrome |

Whatever the strategy, build **ramps with roles, not single colours.** For a purple brand, don't use one purple everywhere; define jobs:

| Role | Step | Used for |
|---|---|---|
| `accent` | deep (passes 4.5:1 with white text) | the one primary action |
| `accent-hover` | one step deeper | hover |
| `accent-subtle` | very pale tint | selected rows, emphasis panels |
| `accent-fg` | deep, for text on light | links, active labels |
| `focus` | mid, vivid | focus rings |
| neutrals | greys tinted slightly toward the hue (light mode) | canvas, surfaces, borders |
| dark mode | near-neutral cool greys; hue only in accents and tints | avoids the "AI purple haze" |

Explain the recommendation in the person's terms: "one purple everywhere makes every element compete; a ramp with jobs makes the important thing obvious and the rest calm."

## Decoding screenshots and references

When the person sends screenshots or names products, extract, don't copy:

1. **Canvas and surfaces:** how many tones, how far apart (lightness steps), what separates panels (tone, border, shadow).
2. **Lines:** where borders appear (around panels? only between rows?), their weight and colour relative to surfaces; whether interaction changes border colour or weight.
3. **Radius:** by role (pills for pressables? cards? inputs?).
4. **Colour:** what the accent is used for and how much of the screen it covers; status colours; whether neutrals are tinted.
5. **Type:** families, weights, the scale, text colours used for hierarchy, figure style.
6. **Density:** body size, row height, gaps within vs between groups.
7. **Components and patterns:** nav shape, stat cards, tables, detail pages, empty states, the signature element.
8. **Motion and life:** what moves and why.

Then write a **take / leave table** per reference, and translate the "take" column into tokens:

| Reference | Take | Leave |
|---|---|---|
| Linear | Quiet sidebar, tight type, ⌘K, motion under 200ms | Ultra-minimal density (we have more numbers) |
| Stripe Dashboard | Tables, detail pages, status pills, money formatting | Its blue |
| A screenshot the person liked | Big number with a time-range pill and caption | Too much empty space per number |
| A screenshot they disliked | — | Purple accent, icon-in-a-box on every card (generic tell) |

Name what you can't tell from a static image (hover, motion, dark mode) and ask or propose.

## Recording the decision

Write a decision record (ADR or a decisions section in the plan): what was chosen, the domain reason ("yellow on black is the language of broadcast lower-thirds and rank numbers"), and one **"lost because"** line per alternative ("violet: the default AI-product colour, says nothing about the product"; "red: blurs with the danger state"). Keep strong alternatives as switchable token sets when cheap, so revisiting is one attribute, not a rebuild.

If the person defers a decision (often the accent), keep a neutral placeholder in the tokens, note it as open, and remind them before the screen pass needs it: the change is one file; re-reviewing every screen is what costs.

## What NOT to do

- Don't build tokens or screens on a written direction alone. Show it.
- Don't show three versions of the same idea. Contrast an axis.
- Don't present colour without contrast numbers, or light without dark.
- Don't silently override the person's colour; critique it on the sheet, recommend, let them choose.
- Don't copy a reference wholesale. Take parts, say what you're leaving and why.
