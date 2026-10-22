---
name: social-optimization
description: End-to-end process for auditing and optimizing a person's professional online presence (LinkedIn, X, GitHub, Instagram, portfolio site) — researching who they actually are before touching any copy, then platform-specific rules for what to do, in what order, and what to avoid. Use whenever asked to "optimize my LinkedIn/X/GitHub/profile", "audit my personal brand", "clean up my socials", or similar.
---

# Social / Professional Presence Optimization

This is the entry point. Do not start editing any live profile before Phase 0 is done — every mistake in the run this skill came from happened from acting before understanding the person well enough.

## Order of operations

1. **Phase 0 — Research the person.** Read [01-research-identity.md](01-research-identity.md) first, every time, even if you think you already know the user. Produces a private persona/dossier file that every later phase reads from.
2. **Phase 1 — Draft, don't apply.** Turn research into concrete copy (headline, About/bio, per-entry descriptions) and show it to the user before writing anything live. Get sign-off on tone/positioning decisions (see "Hard rules" below) before touching a single platform.
3. **Phase 2 — Platform passes, one at a time.** Do NOT parallelize across platforms in one breath — finish and verify one platform before starting the next. Order by leverage: LinkedIn first (highest recruiter/investor visibility), then GitHub (developer-facing), then X, then Instagram, then portfolio site content. Each platform has its own file:
   - [02-linkedin.md](02-linkedin.md)
   - [03-github.md](03-github.md)
   - [04-x-twitter.md](04-x-twitter.md)
   - [05-instagram.md](05-instagram.md)
   - [06-portfolio-site.md](06-portfolio-site.md)
4. **Phase 3 — Visual assets.** If a banner/cover image is needed, read [07-banner-generation.md](07-banner-generation.md) before generating anything. Never use AI image generation for this — see that file for why and how.
5. **Phase 4 — Final report.** Produce one checklist covering every platform touched: what's done, what's confirmed working (not just "saved" — actually re-verified after a fresh reload), what needs the user to do manually and why, and what was recommended but not applied pending their decision.

## Hard rules (each one comes from a real problem in a real run)

- **Consent before reading or changing anything personal.** Ask before visiting the person's logged-in profiles, before querying their own AI assistants about them (Phase 0 steps 3–4), and before every live edit. Editing a profile is public; get an explicit yes for each platform pass, and never post new content, send messages or connection requests, or change account settings beyond what they approved.
- **Check the platform's terms.** Some platforms restrict automated activity. Where automation is risky or blocked, draft the exact copy and click-path and let the person apply it themselves.

- **Never invent a number or metric.** Every stat in any bio/About/description must be something the subject can point at and defend if asked. If in doubt, ask the person before publishing it.
- **Attribute correctly.** If growth, revenue, or outcomes were driven by someone else (a co-founder's audience, a team effort), the copy must credit that — "the platform grew to X" not "I grew it to X" — even if less flashy. Ask directly if unclear who drove what.
- **Ask before assuming self-labels.** Don't guess whether someone wants to be called "full-stack," "backend engineer," "software engineer," etc. In one real run, different platforms used different labels for the same person; only the person's own explicit statement settles it, not what their old bios happen to say.
- **Specific beats impressive.** A checkable, concrete claim ("in production four weeks after the first commit") beats an adjective ("blazing fast"), but a raw process metric that doesn't map to what a reader cares about (commit count) can still miss the point — ask "does this actually sell me" if unsure, don't assume more detail is always better.
- **Every experience/project description gets bullets + a closing "Technologies:" line where the platform supports it** — for scannability and for search indexing (recruiters and platform search both reward this). A dense paragraph is a defect, not a stylistic choice.
- **Re-verify after every save, with a fresh page load.** Several "successful" saves in one run silently failed (LinkedIn's Services checkbox is the clearest example — the UI visually updated, the click fired, and the change still did not persist on reload). Trust a reload, not a click confirmation.
- **Don't stop at the first blocker.** Multiple sections in one run were wrongly marked "can't be automated" on the first failed attempt, when the real fix was a different URL pattern or a properly-dispatched event. Try at least: (a) the obvious button, (b) a direct edit-URL pattern matching sibling sections that did work, (c) reading the actual DOM for the real control before giving up.
- **Watch for auto-side-effects.** LinkedIn silently overwrites the profile headline when a new *current* position is saved elsewhere. Re-check unrelated fields after any save that touches "current" status.
- **Think about placement, not just wording.** A fact deserves its own structured section (e.g., a company → Experience entry) if it's ongoing/significant, not just a sentence buried in a summary paragraph. Ask "where does this actually need to live for the reader who scans instead of reads" before deciding a paragraph mention is enough.
- **Every product/project has a "wedge vs. real bet" if the person is a founder.** Don't describe a product by its surface feature list alone — ask what the founder's actual longer-term bet is, and reflect that (clearly marked as vision/ambition, not as an accomplished fact) in copy that's allowed to be aspirational (About sections, pitch decks), while keeping accomplished-fact sections (resume bullets) strictly to what's shipped.

## Where things are stored

- Research dossier and persona doc: `.tmp/<name>_persona_clone.md` and `.tmp/<name>_profile_dossier.md` in the project repo (make sure `.tmp/` is gitignored first). Never commit these; they may contain candid personal-insecurity notes the person shared for calibration purposes only, not for anyone else to read.
- Raw research captures (screenshots, page text dumps, other AI chat exports): `.tmp/research/`.
- Generated visual assets (banners, etc.): `.tmp/banner/` or `.tmp/assets/`.
- A running checklist per optimization pass: `.tmp/<platform>_checklist.md`.
- Keep `.tmp/` (or wherever these files live) out of version control: add it to `.gitignore` before writing the dossier.
