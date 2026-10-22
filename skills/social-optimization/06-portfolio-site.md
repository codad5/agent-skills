# Portfolio site content audit

## Do first
1. Compare the site's resume/about content against the freshly-refreshed LinkedIn About — they should tell the *same* honest story (same numbers, same framing of growth/attribution), not two different versions that could be caught contradicting each other.
2. Check for any content-management pattern already in place (e.g. a markdown file the site reads directly, like `content/resume.md`) before proposing structural changes — work within the existing pattern rather than introducing a new one.

## What NOT to do
- Don't restructure the site's architecture as part of a content/copy pass unless asked — this phase is about the words, not the codebase, unless the person explicitly broadens scope.
- Don't publish anything containing the person's professional insecurities, private research notes, or the raw persona dossier — those live in `.tmp/` (gitignored) precisely because they're for calibrating tone, not for public consumption. A portfolio site is a *public* surface; treat every file destined for it as such, and double-check anything before it's wired into a public route or committed to a public repo.
