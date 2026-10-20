# Phase 2 (UI track) — References, prototype and direction

Goal: build directions from real products, show them in one self-contained prototype the person can switch through, get one chosen, and record why the others lost. This is the cheapest place to be wrong. Building tokens, a plan or screens on a direction nobody saw is the most expensive mistake available, and directions built from imagination come out looking generated.

Three steps, in order. Gates G2 and G3 in [SKILL.md](SKILL.md).

## 1. References first (gate G2)

**No direction before references.** Building from imagination is what produces the generated look; building from real products is what fixes it (observed: five rounds of "still looks AI" ended the moment real screenshots were decoded).

1. **Get real screenshots** of the products the person named (intake G1 asked for two or three they love and one they dislike). If they named none, pick two or three that fit the app type from [13-ui-styles.md](13-ui-styles.md) and say which and why.
2. **Fetch them yourself** where you can: a design-reference MCP connector, a headless browser or a browser tool (landing page, main app screen, a dense data screen). Or ask the person for screenshots of logged-in screens you can't reach.
3. **If a site can't be reached** (blocked, needs login, the sandbox has no network), say so plainly and use other references. Never describe a product from memory as if you'd looked at it.
4. **Decode each one** (below) and write the **take / leave table**. Save the screenshots and the table in `docs/design/references/` and summarise the table in chat.

### Decoding screenshots and references

Extract, don't copy:

1. **Canvas and surfaces:** how many tones, how far apart (lightness steps), what separates panels (tone, border, shadow).
2. **Lines:** where borders appear, their weight and colour relative to surfaces; whether interaction changes border colour or weight.
3. **Radius:** by role (pills for pressables? cards? inputs?).
4. **Colour:** what colour is used for and how much of the screen it covers; status colours; whether neutrals are tinted.
5. **Type:** families, weights (large display text is often light, not bold), the scale, text colours, figure style.
6. **Icons:** one family? stroke or filled? weight?
7. **Density:** body size, row height, gaps within vs between groups.
8. **Components and patterns:** nav shape, cards, tables, detail pages, empty states, the signature element.
9. **What the hero shows:** usually the real product at full fidelity, not decoration.

| Reference | Take | Leave |
|---|---|---|
| A search product the person loves | Large light-weight geometric sans, pill controls, tonal fills instead of borders, colour only on actions | Its exact palette |
| A video platform | Real content cards with duration badges and chips; one icon family | Its density on the home feed |
| A dashboard they liked | Big number with a range pill and a caption | Too much empty space per number |
| A screen they dislike | — | Purple accent, icon-in-a-box on every card |

Name what you can't tell from a static image (hover, motion, dark mode) and ask or propose.

## 2. The prototype (gate G3)

**No plan, no foundation, no screens until the person has seen and chosen a direction in this prototype.** Not a written description of directions; the actual page.

**What a direction is:** a set of decisions that work together, with a name and a one-line character, each citing which "take" items from §1 it uses:
- **Feel:** calm/dense, friendly/colourful, bold/editorial.
- **Colour strategy** (below) and the palette.
- **Surfaces:** one of the systems in [06](06-design-system.md) §2.
- **Type:** the actual typeface (embedded), scale, figures.
- **Density and rhythm.**
- **Signature element:** the one thing that makes it this product.

Directions must differ on at least one axis (tonal vs hairline, calm vs colourful, sans vs editorial). "The same layout in three purples" isn't a choice.

**The prototype file must have:**
- **One self-contained HTML file** (inline CSS and JS; fonts and one icon library may load from a pinned CDN), saved to `docs/design/proposals/`, opening with a visible line: "Proposal only: nothing in the code uses this yet."
- **2–3 directions**, switchable.
- **At least three screens:** the public landing page (if the product has one), the main app screen, and one data-heavy result screen. Switchable.
- **Switches** for direction, page, palette (2–3 per direction where colour is open) and light/dark, so the person can answer in one message ("A or C, but the purple hurts my eyes").
- **Sample data clearly labelled as sample,** realistic, in the product's language and locale.
- **The required items** from [08](08-craft-checklist.md) §2: a real embedded typeface, one icon set, the real product as the hero visual, and a **colour roles table with contrast numbers printed** for each direction and palette.
- **Both themes reviewed critically,** light first: one approved mockup's dark mode put the brand hue on every surface and shipped that way.

Smaller formats for narrower questions: a **palette-switching page** (`data-palette` on the root) when only colour is open; an **SVG or HTML swatch sheet** (the same mini UI per option, values in hex and OKLCH, a character note, measured contrast, one marked RECOMMENDED, the current colour "for comparison"). These supplement the prototype; they don't replace it for a new direction.

## 3. Self-review before showing

Run the self-review loop in [08](08-craft-checklist.md) §4 on every direction, page and theme of the prototype: render, look at the screenshots, fix obvious bugs, list and remove every banned item and tell, re-render. Present with the result ("0 banned items; all text pairs ≥ 4.5:1").

When the person reacts, decode feedback in full passes ([08](08-craft-checklist.md) §6), never one tell per round.

## Colour strategies to offer

| Strategy | Fits | Watch |
|---|---|---|
| **Monochrome, colour from content** | Media products (thumbnails, video, photos carry the colour) | Needs strong type and hierarchy to not feel empty |
| **One rationed accent** | Dense tools, ops consoles, developer products | Accent only for the primary action, active nav, focus, live progress, good data; can read austere for consumer audiences |
| **Brand colour + meaning hues** | Products with many kinds of signal (research, analytics, content tools, friendly dashboards) | Rules below |
| **Meaning-assigned tints** | Friendly products for non-technical users; dashboards of many metrics | Each metric owns a tint permanently (money collected is always amber); status colours separate; bg + ink pairs |
| **Colour blocks** | Marketing, bold brands | Section rhythm, not app chrome |

**Brand colour + meaning hues** (it produced the approved result in a research product): one brand colour for identity and primary actions, plus a small set of sharp hues that each mean exactly one thing (growth, research, check this, hot, visual, sound, problem). Rules:
- hues only on icons, chips and data, never on big surfaces;
- at most two hues in any one area;
- text on a hue uses dark ink on a pale tint of it, not white on saturated colour;
- every pair contrast-tested, with the numbers printed in the colour roles table.

Whatever the strategy, build **ramps with roles, not single colours.** For a purple brand, don't use one purple everywhere:

| Role | Step | Used for |
|---|---|---|
| `accent` | deep (passes 4.5:1 with white text) | the one primary action |
| `accent-hover` | one step deeper | hover |
| `accent-subtle` | very pale tint | selected rows, emphasis panels |
| `accent-fg` | deep, for text on light | links, active labels |
| `focus` | mid, vivid | focus rings |
| neutrals | greys tinted slightly toward the hue (light mode) | canvas, surfaces, borders |
| dark mode | near-neutral greys; hue only in accents and tints | avoids the "purple haze" |

Explain it in the person's terms: "one purple everywhere makes every element compete; a ramp with jobs makes the important thing obvious and the rest calm."

## Recording the decision

Write a decision record (ADR or a decisions section in the plan): what was chosen, the domain reason, and one **"lost because"** line per alternative ("violet: the default AI-product colour, says nothing about the product"; "red: blurs with the danger state"). Keep strong alternatives as switchable token sets when cheap.

If the person defers a decision (often the accent), keep a neutral placeholder in the tokens, note it as open, and remind them before the screen pass needs it.

## What NOT to do

- Don't write a plan, set up tokens or build screens before a direction is chosen in the prototype.
- Don't build a direction from imagination; cite the references it takes from.
- Don't show a prototype you haven't self-reviewed.
- Don't show three versions of the same idea. Contrast an axis.
- Don't present colour without contrast numbers, or light without dark.
- Don't silently override the person's colour; critique it, recommend, let them choose.
- Don't copy a reference wholesale. Take parts, say what you're leaving and why.
