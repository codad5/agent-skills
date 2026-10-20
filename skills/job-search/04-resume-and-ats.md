# Phase 4 — Resume and ATS handling

## Deciding whether to tailor

- If the person's existing resume already emphasizes the skills/experience the listing asks for, say so and use it as-is — don't manufacture busywork by tailoring when it isn't needed.
- If a listing leans heavily on something the default resume underweights (e.g. a specific stack, a specific kind of scale, a specific domain), create a tailored variant as its own markdown file rather than overwriting the person's main resume.
- Any tailored copy must stay within the same honesty rules as everything else this person's materials follow (if a persona or profile doc exists for them, its voice/honesty rules apply here too: specific over impressive, never invent a number, credit collaborators, admit what's in progress).

## Converting to a properly ATS-checked PDF

- A resume that looks fine visually can still fail ATS parsing (tables, multi-column layouts, text-in-images, unusual fonts, headers/footers holding real content). Before converting, check the source markdown/document for these failure modes and flag any found.
- Prefer a straightforward single-column layout, standard section headers (Experience, Education, Skills), and plain text — this is what parses reliably across ATS systems, not a design-forward multi-column resume.
- If a conversion tool is available in the environment, use it and verify the output PDF actually contains selectable/extractable text (not a flattened image) — this is the single most common ATS-breaking mistake.
- Name the output file clearly, e.g. `<name>-resume-<company>.pdf` if tailored per job, or `<name>-resume.pdf` for the general one.

## What NOT to do

- Don't silently replace the person's existing default resume file — tailored versions are additions, not overwrites, unless the person asks for the default itself to be updated.
- Don't invent achievements or metrics to better match a listing — a gap in the profile-match assessment (Phase 3) is more useful and more honest than a resume that oversells.
