# Reference — UI styles and where they fit

A catalogue of the styles product UIs are usually built in: what defines each, what kind of app it suits, and what to watch. Use it in Phase 1 and 2 to build options from, and to explain a recommendation ("bordered, because your users work in a dark editor all day"). It is a starting point, not a menu to pick from blind: the person's brand, users and references decide, and most real products combine two styles (one for the app, one for marketing).

## The axes every style is a mix of

Name the axes when you present options; it makes the choice concrete.

| Axis | Range |
|---|---|
| **Separation** | tone (surfaces of different lightness) ↔ lines (hairline borders) ↔ space alone |
| **Depth** | flat and shadowless ↔ soft shadows only on floating things ↔ elevation everywhere ↔ hard offset shadows |
| **Colour** | monochrome (colour from content) ↔ one rationed accent ↔ meaning-assigned tints ↔ colour blocks |
| **Density** | spacious ↔ comfortable ↔ dense |
| **Shape** | sharp ↔ soft radius by role ↔ pills everywhere |
| **Theme** | light-first ↔ both ↔ dark-first or true black |
| **Type** | one quiet UI face ↔ UI face plus display face ↔ type as the main visual |

## The styles

### 1. Tonal, almost borderless
- **Defined by:** a soft grey canvas, panels in the lightest tone floating on it, sunken "wells" inside panels; borders only for row dividers; shadows only on floating things; subtle tinted emphasis panels; often pill controls.
- **Best for:** admin consoles, ops and back-office tools, SaaS dashboards used by non-technical staff, CRMs, billing and settings; any app whose marketing site is already soft and rounded.
- **Watch:** tone steps too close to read on a cheap screen; muted text failing contrast on the darker canvas; dark mode needs hairlines where tones bunch together.
- **Look at:** Close, Stripe's newer dashboard, Notion, Apple's settings apps.

### 2. Hairline bordered
- **Defined by:** a measured lightness ladder with the border a step above every surface; neutrals tinted toward the accent; one 1px weight everywhere; interaction changes the line's colour, never its weight; hairlines between rows instead of a card around each block; dividers and pressable outlines in different colours.
- **Best for:** developer tools, dark or true-black creative tools (video, audio, design), media products, dense data where structure must be visible, technical audiences.
- **Watch:** borders as decoration around every block (the generic look); lines that vanish near white in light mode; outline buttons in the divider colour reading as plain text.
- **Look at:** Linear, Vercel, GitHub, Raycast.

### 3. Somewhat borderless (hybrid)
- **Defined by:** tone separates areas (page, panels); hairlines separate items inside dense areas (tables, settings lists, form sections); no element gets both.
- **Best for:** products that mix calm overviews with dense data: analytics, finance, healthcare and HR systems, marketplaces' seller tools.
- **Watch:** drifting into "some panels bordered, some not" with no rule.

### 4. Flat and shadowless
- **Defined by:** no shadows anywhere; depth from tone or lines only; often paired with true black (shadows can't be seen) or with print-like light UIs.
- **Best for:** dark-first tools, editorial and document UIs, anything that should feel calm and printable.
- **Watch:** menus and dialogs need *some* separation: a border, a stronger tone or a scrim behind them.

### 5. Monochrome, colour from content
- **Defined by:** greys and one neutral accent; thumbnails, photos, video and charts provide the colour; strong type hierarchy carries the rest.
- **Best for:** media and creator tools, photo and video apps, galleries, e-commerce catalogues, portfolios.
- **Watch:** feels empty without content; needs good empty states and type.
- **Look at:** YouTube Studio, Apple Photos, Figma's chrome.

### 6. Friendly and colourful (meaning-assigned tints)
- **Defined by:** a set of tints in background + ink pairs, each owned permanently by a meaning (money collected is always amber); status colours kept separate; warm plain copy; quiet tables and forms.
- **Best for:** education, schools, family, health and wellbeing, community products, consumer apps, and dashboards of many different metrics for non-technical users.
- **Watch:** rainbow chips with no meaning; colour on every element; the same tint meaning two things.
- **Look at:** Duolingo (louder), Notion's colours, Headspace.

### 7. Dense data
- **Defined by:** small type (12–13px), tight rows, tabular figures, many columns, keyboard first, colour almost only for change and status.
- **Best for:** trading and finance terminals, monitoring and logs, analytics for power users, internal tools used all day.
- **Watch:** unusable on phones (design a separate mobile view); beginners need an easier entry.
- **Look at:** Grafana, Datadog, Bloomberg-style terminals, Airtable grids.

### 8. Cards and feeds
- **Defined by:** content as repeated cards in a grid or feed, imagery first, generous radius, clear tap targets.
- **Best for:** social and content discovery, marketplaces, listings (homes, cars, jobs), mobile-first consumer apps.
- **Watch:** using cards for things that aren't items (every settings block in a card); all cards the same weight.
- **Look at:** Airbnb, Pinterest, the App Store.

### 9. Conversational
- **Defined by:** a message thread, a composer that grows, streaming and typing states, inline rich content (tables, code, files, actions), a history sidebar.
- **Best for:** chat apps, AI assistants, support and inbox tools.
- **Watch:** walls of text; long-message readability (line length, code blocks); designing empty, loading and error states for each message, not just for the page.
- **Look at:** ChatGPT, Claude, Intercom, Slack.

### 10. Native platform
- **Defined by:** the platform's own patterns and components (Apple's Human Interface Guidelines, Material 3), system fonts, standard navigation.
- **Best for:** mobile apps where familiarity beats brand; enterprise mobile; anything that must feel "built in".
- **Watch:** brand gets thin; mixing iOS and Android patterns in one app.

### 11. Editorial, type-led
- **Defined by:** big confident type, a display face, rhythm and whitespace as the design, numbered sections, few images.
- **Best for:** marketing sites, docs, blogs, changelogs, reports, portfolios.
- **Watch:** too sparse for an app; slow-loading web fonts.
- **Look at:** Stripe Press, well-made documentation sites, magazines.

### 12. Bold blocks and hard shadows (neo-brutalist)
- **Defined by:** solid colour blocks, thick outlines, hard offset shadows, playful type.
- **Best for:** marketing for bold brands, creator and indie products, campaigns, a signature element used sparingly inside an app.
- **Watch:** tiring as everyday app chrome; accessibility of colour pairs.
- **Look at:** Gumroad.

### Usually avoid for product UI
- **Glassmorphism** (frosted translucent panels): fine for overlays on media or an OS-like shell; poor contrast and performance as everyday app chrome.
- **Neumorphism** (soft extruded shapes): controls hard to see, fails contrast.
- **Gradient-and-glow "AI" look** (purple gradients, blurred orbs, glowing cards): the most common generated tell; says nothing about the product.

## Quick map: app type → styles to offer

| App type | Offer first | Also worth showing |
|---|---|---|
| Admin console, back office, CRM | Tonal | Hybrid; Bordered for technical teams |
| Developer tool | Bordered | Flat dark; Dense |
| Creative or media tool | Bordered, true black | Monochrome |
| Analytics, finance, health records | Hybrid | Dense; Tonal |
| Education, school, family, community | Friendly colourful | Tonal |
| Marketplace, listings, social | Cards and feeds | Tonal for seller tools |
| Chat app, AI assistant | Conversational on Tonal or Flat | Bordered for developer-facing assistants |
| Mobile consumer app | Native platform or Cards | Friendly colourful |
| Marketing site | Editorial | Bold blocks; match the app's surfaces |
| Printable documents (invoices, reports) | Flat and shadowless, light | — |

Show at least two that contrast on one axis (Phase 2). The rest of the decision comes from the brand and from screenshots the person likes.

## Finding more references

When the person has no references, or you want real examples of a pattern (an onboarding flow, a pricing page, a data table, a chat composer), look at real products rather than inventing.

**Where to look:**

| Source | Good for | Note |
|---|---|---|
| **Mobbin** | Real screens and flows from shipped web, iOS and Android apps, searchable by pattern | The best fit for product UI; much of it needs an account |
| **Page Flows** | Recorded user flows (onboarding, checkout, settings) | Flows rather than single screens |
| **Refero** | Web app screens by pattern and component | Product-focused |
| **Dribbble, Behance** | Mood, colour and type ideas | Mostly concepts, not shipped products; treat as inspiration, never as a spec |
| **Land-book, Lapa Ninja, SaaS Landing Page, One Page Love** | Landing and marketing pages | For marketing work |
| **Public design systems:** Material 3, Apple HIG, Fluent, Carbon, Polaris, Atlassian, GOV.UK | Components with the reasoning behind them, accessibility notes | Free and authoritative |
| **component.gallery** | How many systems build the same component | Good for naming and comparing |

**How to access them:**
1. **Check your tools first.** If a design-reference MCP server or connector is available (for example one for Mobbin or Figma, or the platform's own), use it: it's faster and returns structured results.
2. **Otherwise use a browser tool** (built-in browser, Playwright, Claude in Chrome) to search the site, open three to six relevant examples, and take screenshots.
3. **If a site needs an account or a paid plan,** don't sign in for the person. Ask whether they want to log in themselves in the browser session, or to send screenshots.
4. **If you have neither,** say so and ask the person for screenshots or links, or propose references by name from this file.

**What to do with them:** decode each one ([04](04-directions-and-proposals.md): surfaces, lines, colour, type, density, patterns), write the take/leave table, and turn the "take" column into tokens and components. Use references to analyse, never to copy: no copied assets, logos, illustrations or a competitor's exact look.

## What NOT to do

- Don't pick a style because it's fashionable or because it's your default. Tie it to the users, the app type and the brand.
- Don't present a single style. Contrast at least one axis.
- Don't treat Dribbble shots as proof something works; check shipped products for that.
- Don't sign in to reference sites on the person's behalf or scrape paid content.
