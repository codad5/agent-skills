---
name: job-search
description: Search (never apply) for job listings across major platforms and company career pages, filter them against a person's real constraints (location, visa, remote/onsite pay floor, role fit), and produce one detailed markdown doc per shortlisted job — application method, every form question answered, tailored resume/cover letter, and an honest fit assessment. Use whenever asked to "find me jobs", "search for openings", "job hunt", or similar. Never submits any application — documentation only, the person applies themselves.
---

# Job Search & Application-Prep

This skill is region-agnostic and person-agnostic. It has no baked-in assumptions about who the user is, where they live, or what they want — every constraint below comes from asking, not guessing.

## Order of operations

1. **Phase 0 — Capability check.** Confirm a browser-automation tool is actually available and usable (e.g. Playwright, Claude-in-Chrome). If none is available, say so plainly and ask the user to enable one rather than attempting to fake results from memory/training data — job listings and their posted dates must be looked up live, never guessed.
2. **Phase 1 — Intake.** Read [01-intake.md](01-intake.md). If a persona or profile doc already exists for this person (for example from an earlier profile-optimisation pass), read it first and only ask what it doesn't already cover. Otherwise ask the intake questions directly. Do not proceed to searching until the required fields are answered.
3. **Phase 2 — Shortlist pass.** Read [02-shortlist.md](02-shortlist.md). Search the agreed platforms, apply the person's filters, and produce **one single shortlist document** (not full per-job docs yet) for the person to review and prune. Do not build tailored resumes/cover letters at this stage — that cost is only worth paying after the person confirms which jobs they actually want.
4. **Phase 3 — Per-job documentation.** Read [03-per-job-doc.md](03-per-job-doc.md). For each job the person approves from the shortlist, produce one complete markdown file per the template.
5. **Phase 4 — Resume/ATS handling.** Read [04-resume-and-ats.md](04-resume-and-ats.md) whenever a job needs a resume decision (use existing vs. tailor a new one) or a PDF conversion.
6. **Phase 5 — Final index.** Produce one index file listing every job documented, its shortlist status, and next action, so the person has a single place to work from. Include a **market-signal summary**: across every listing actually read during the search (not just the shortlisted ones), note any skill/tool/requirement that came up repeatedly and the person doesn't currently have or underweights in their resume — this is free signal gathered along the way, not extra searching. Be direct and specific ("Kafka appeared in 6 of the roles you'd otherwise match well — worth a line in your resume if you've used it, or a gap to note if not") rather than vague encouragement. If the resume itself looks weak against what the market is actually asking for in this pass, say so plainly — this is more useful to the person than a comfortable summary.

## Where output goes

Group every search by date. Each search day gets a folder named `YYYY-MM-DD` inside the person's job-search working folder, holding that day's `shortlist.md` and every per-job doc written that day. Keep one `00-INDEX.md` at the top of the working folder that lists each date folder, the roles in it, and known outcomes (rejected, ineligible, pending). Never put a new day's files into an old day's folder, and move nothing into a shared "old" folder. When something from an earlier day is still relevant, link to it by relative path (`../2026-09-12/name.md`) instead of copying it.

## Hard rules

- **Never submit an application, never send an email, never fill and submit a web form.** This skill produces documentation for a human to act on. Drafting the content of an answer is in scope; clicking submit is never in scope.
- **Never fabricate a posting.** Every job in the shortlist must come from an actual live page visited during this session. If a platform can't be reached or a search returns nothing, say so — don't fill the gap with a plausible-sounding invented listing.
- **Never fabricate salary.** If a listing has no pay information, say "not disclosed" — don't estimate one and present it as fact. Only note a desired-pay figure where the platform/form has a field for the person to state their own expectation.
- **Respect the person's constraints exactly as given**, not a generic default. A location/visa/pay filter that isn't explicitly satisfied disqualifies a listing — don't include a job "just in case" or because it's otherwise impressive.
- **Timezone-aware scheduling.** "Best time to apply" must account for the likely business hours of whoever receives the application (recruiter/hiring team), not just the person's own local time. State both: the person's local time AND what that means for the other side (e.g. "Tuesday 9am your time — note that's still nighttime in \[recruiter's likely timezone], so don't expect a same-day read").
- **Recency matters.** Respect the person's stated recency window; if a listing's posted date is unclear or unverifiable, say so rather than assuming it's fresh.
- **Honest match-strength scoring.** Score fit against the actual listing requirements, not against how much the person would like the job. A low score is useful information, not a failure to hide.
- **Two-pass cost discipline.** Never build a full per-job doc (resume tailoring, cover letter, form-question answers) before the person has approved that specific job from the shortlist — that work is expensive and shouldn't be spent on jobs that get rejected on sight.
