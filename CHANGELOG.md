# Changelog

## product-frontend: gates after a field report

A real one-shot run of the skill produced an incomplete intake, skipped the prototype and showed mockups full of generated-UI tells; the owner needed five feedback rounds. Each change below closes one of those failures.

| Change | Where | Failure it prevents |
|---|---|---|
| **Gates G1–G6** with a table of what must exist before each phase, and "a one-shot run doesn't skip a gate" | SKILL.md | Phases skipped or reordered because the request "seemed clear" |
| **Intake coverage gate:** 12 mandatory items (project type, track, scope, density, light/dark, what "better" means, references, navigation, brand locks, devices, sample data, reply tone), printed as an Answered / Assumed / Unknown table; no mockups while anything is Unknown | 02-intake.md | Density, dark mode, references, nav, logo rules and screen sizes never asked; owner had to prompt |
| **References gate:** real screenshots fetched or requested, take/leave table written and cited by each direction; unreachable sites reported, never described from memory | 04 §1, SKILL.md | Directions built from imagination, which looked generated |
| **Prototype gate:** one self-contained HTML file, 2–3 directions differing on an axis, at least three screens (landing, main app, data-heavy), switches for direction/page/palette/theme, labelled sample data, contrast numbers printed; no plan, foundation or screens before a direction is chosen | 04 §2, 07 §1, SKILL.md | Plan written before any mockup |
| **Self-review loop before showing anything:** render at phone and desktop, look at the screenshots, fix obvious bugs, list and remove every banned item and tell, re-render, present with the count | 08 §4, 04 §3, SKILL.md | Unreviewed mockups with dark-on-dark buttons, wrapped placeholders and every known tell |
| **Explicit ban list** (gradients, glows, content shadows, orbs, centred everything, icon-in-box cards, fallback fonts, Inter and purple by default, emoji icons, uniform grids, gradient thumbnails, boxes everywhere), with exceptions only when the approved surface system assigns the effect a job | 08 §1 | Tells treated as soft advice |
| **Positive requirements:** embedded typeface, one icon set, real product as hero, colour roles table with measured contrast, colour on jobs not surfaces, varied sections, left-aligned content, specific copy, labelled sample data | 08 §2, SKILL.md | A page that avoids bans but still looks generic (fallback fonts, decorative hero) |
| **Brand colour + meaning hues** strategy with its rules (hues only on icons, chips and data; max two per area; dark ink on pale tint; every pair tested) | 04 colour strategies | Purple on everything |
| **Full-pass feedback decoding:** list every tell, remove all, re-render, re-check; repeated "looks AI" sends you back to references | 08 §6, 07 §6, SKILL.md | Five rounds removing one tell at a time |
| **Viewport sweep gate:** 14 sizes from 320 to 2560 wide, sideways phones and a 600px-tall window, with a script that fails on sideways scroll, clipping, overflow and small targets; no fixed pixel heights on content | 08 §5, 07 §4, SKILL.md | Layouts checked at two widths only |
| **Foundation gate:** tokens (primitives then roles), a style-guide page reviewed with the person, token tests that fail on raw colours, gradients, unassigned shadows and low contrast | 06 §5, 07 §3, SKILL.md | Screens built before the system that keeps them consistent |
| **Unattended-run protocol:** architecture contract first, shared core built by you, precise sub-agent briefs (owned files, forbidden files, tests, no commits), every result verified yourself | 07 §7, 10 | Inconsistent or unverified work when the owner steps away |
| **Reply tone** asked at intake and followed | 02, 10 | Unwanted praise and padding in replies |
| **Case study** of the run, anonymised | 12 §4 | Rules without the reason behind them |
