# Phase 3 — Per-job documentation

One markdown file per approved job. Suggested filename: `<company>-<role-slug>.md`.

## Template

```markdown
# <Company> — <Role Title>

- **Link:** <job posting URL>
- **Posted:** <date, as stated by platform> (<n> days old as of <today's date>)
- **Platform:** <LinkedIn / Indeed / YC / Wellfound / company career page / other>
- **Location / work mode:** <remote-anywhere / remote-region-restricted / onsite city / hybrid>
- **Pay:** <as disclosed, with currency and period> — or "Not disclosed" — or "Not disclosed; platform allows stating expected pay, suggested figure: <X>, confirm before use"
- **Visa/relocation:** <sponsors visa: yes/no/unstated> <relocation assistance: yes/no/unstated>

## When to apply

Weigh all of these, not just timezone — they can point in different directions, and when they conflict, freshness/expiry/competition wins over "ideal" recruiter timezone:

- **Posting freshness**: minutes-old means the recruiter is plausibly active right now — that's a real, time-limited advantage worth taking immediately even outside their "ideal" hours. Hours-old on a listing posted late in the recruiter's day likely means they've already gone offline for the day — timezone timing matters more here.
- **Applicant/view count, if the platform shows it**: a high or fast-climbing count means competition is already stacking up — waiting for a theoretically better time can mean arriving buried under 200 other applicants. High competition pushes toward applying immediately and also raises the bar noted in the profile-match section below.
- **Expiry risk**: if the "ideal" recruiter-timezone window is far enough out that the listing might close, get filled, or age past the point of being a fresh application first, immediacy wins outright — say so explicitly ("apply now rather than waiting for Monday — at this posting's pace it may not still be open").
- **Recruiter timezone**, as before — the tie-breaker when freshness/competition/expiry don't force immediacy.

State a clear recommendation (immediate vs a specific window) and the reasoning behind it in these terms — not just a timezone conversion. E.g.: "Apply now — posted 20 minutes ago, no applicant count shown yet, this is the freshness window." or "Posted 6 hours ago, 40+ applicants already, in a fast-moving space — apply immediately rather than waiting, competition is already building." or "Posted 2 days ago, low activity, no urgency signal — Tuesday ~9am <company HQ timezone> (which is <local equivalent> for you) is a reasonable window, but immediate is never wrong here either."
## About the company & who to connect with

A few sentences on what the company actually does and why this role likely exists (product area, team, recent context if visible on the listing/company page) — not generic boilerplate copied from their About page. If the platform shows who posted the job (e.g. a LinkedIn job poster's profile, a named recruiter/hiring manager) or the listing names a team/hiring manager, note who that is and suggest a concrete, low-pressure way to use it — e.g. "the poster is <name>, <title> at <company>; worth a connection request mentioning this specific role rather than a cold generic one" or "no poster identified on this listing — LinkedIn's 'People who work here' on the company page may surface someone on the target team to reach out to." Never fabricate a name or contact if the platform doesn't show one.

## Application method

<Either:>

### If email
- **Send to:** <address>
- <Any stated subject line format or required attachments>

### If form
List every question the form asks, with a drafted answer for each:
1. **<question as it appears on the form>**
   <drafted answer>
2. ...

## Competing-business check (do this before Resume and Cover letter)

Check whether the person runs their own business, studio, or side project that does the *same kind of work* as the target employer, not just whether they're "a founder" in general. Running a client-services/consulting/agency business and applying to another client-services/consulting/agency company is a real, specific risk: a small or founder-led employer can read "this candidate runs a studio that does what we do" as "will they be distracted, moonlight, compete for our clients, or really commit here," not as relevant experience. This risk is much smaller or absent when the person's side venture is a different shape of business than the target employer (a personal open-source tool, a different industry, a pure product vs. the target's pure product) — judge the actual overlap, don't apply this caution reflexively to every founder/side-project situation.

**When the overlap is real, say so to the person directly and visibly** — a short callout in the doc (e.g. "⚠️ Your resume may read as a conflict here: you run \<their venture\>, which does the same kind of work as \<employer\>") and the same point surfaced in chat, not just a silent adjustment buried in how the cover letter gets worded. This is their business risk to weigh, not something to quietly route around on their behalf.

Then, for both Resume and Cover letter: don't lead with the competing venture's existence or brand it as the headline qualification — extract the underlying, transferable proof points instead (specific technical work, end-to-end ownership demonstrated on named projects) and let those carry the pitch. **Don't remove the venture from the resume entirely to hide the overlap** — if the person's other public profiles (LinkedIn, portfolio site) already show it, and they usually will, an inconsistency between "resume shows nothing" and "LinkedIn shows an active founder role" reads worse than the original concern: it looks like deliberate concealment once discovered, not just a busy person. A lighter touch is safer and just as effective — reword the *language* of the relevant bullets so they don't echo the target employer's own positioning back at them (e.g. drop phrasing like "client engagements," "discovery to handover" when applying to a company that describes its own business the same way), while keeping the role and its real accomplishments visible. If reframing isn't enough and the person wants a more substantial resume restructure, don't invent a replacement experience entry to fill the gap — ask them for the real substance of a real past role first; padding with plausible-sounding but unverified achievements breaks the same honesty rule as everywhere else in this skill.

Don't invent an answer for how they'd handle time-commitment/conflict-of-interest questions if it comes up in an interview — that's their call to make, ask them rather than guessing.

## ATS keyword match

Pull the real, recurring keywords and phrases from this specific JD — the technologies, the domain terms (e.g. "reconciliation," "multi-tenant," "event-driven"), and the exact seniority/years language — and check each one against what the current default resume actually says, not what the person could truthfully claim in conversation. This section is written for whoever works on the resume next (the person, or another AI pass), so it has to be usable as a starting point without them re-reading the whole JD.

Format as a small table:

| JD keyword/phrase | On resume now? | Where / how to close the gap |
|---|---|---|
| <exact term from the JD> | Yes, verbatim / Yes, different wording / No | <if yes-different-wording: the resume's actual phrase, and whether swapping in the JD's exact term is honest and worth it — ATS parsers often match literal strings, so "Postgres" vs "PostgreSQL" or "CI/CD" vs "continuous integration" can matter> <if no: is this a real gap (say so plainly, per the relevance-bar rule above) or something true but simply unwritten (name the real project/fact that would support adding it, but do not add it yourself without the person confirming it's accurate)> |

Keep this table honest to the same rules as everything else in this skill: never suggest adding a keyword the person can't back up, and don't pad the table with weak or tenuous terms just to look thorough. A short table naming the 5-10 terms that actually matter for this JD is more useful than a long one restating the whole posting.

## Resume

<Either: "Use existing resume as-is — matches well because <reason>." or "Tailored version created: <path to new resume file>." Explain the specific changes made and why, tied to this listing's actual requirements — not a generic tailoring note. Apply the competing-business check above before finalizing.>

## Cover letter

<Only if the listing/form asks for one. Draft it here in full, specific to this company and role — reference something concrete about what they do, not a template with the name swapped in. Apply the competing-business check above before finalizing.>

## Profile match strength

<Honest assessment against the LISTING'S stated requirements, not against how appealing the job is. Structure: what matches well, what's a stretch or gap, an overall read (e.g. "strong match," "plausible but you'd be competing against candidates with X," "long shot — missing Y and Z"). Factor in applicant/view count if the platform shows it — a high count against a merely-average match should lower confidence, not just competitiveness commentary. Don't inflate this to be encouraging — the person needs the real read to prioritize where to put their energy.>
```

## Notes

- If a form's questions can't be seen without starting the application flow (common on some ATS platforms), note that limitation explicitly rather than guessing what they'll be — the person may need to check themselves and report back.
- If a job requires an account/login on a third-party ATS to even view the form, say so — this skill can document the fact of that requirement without creating the account itself.
- **LinkedIn's job-description body can fail to render** in some sessions/page variants (the description panel stays empty or stuck loading). When the "Apply" button routes to the employer's own site/ATS rather than an agency, follow that link and read the JD there instead of fighting LinkedIn's rendering — it's usually more complete anyway, and has caught real discrepancies with LinkedIn's own location tag (e.g. a listing tagged "EMEA (Remote)" on LinkedIn whose actual posting specified a hybrid office in a specific city, no remote-anywhere option). Always trust the employer's own posting over LinkedIn's summary tags when they conflict, and flag the discrepancy in the doc rather than silently using whichever is more convenient.
- **A "Fully Remote" or "Remote" label on the listing itself doesn't guarantee the person is actually eligible** — some application forms (seen directly on a Teamtailor-powered listing) have a required "Location" field with a hard-coded dropdown of eligible countries/states that's more restrictive than the listing's own label suggests. If the person's location isn't confirmed as clearly eligible from the listing text alone, open the actual application form far enough to check for a location/eligibility field before treating the job as a real candidate — this is worth doing even during Phase 3 documentation, not just Phase 2 shortlisting, since it can reverse an earlier "ambiguous, worth trying" read into a hard no. Stop and flag it plainly rather than filling in the rest of the form once this is confirmed negative.
- **Re-verify each listing is still live when building its Phase 3 doc**, even if it was live minutes-to-hours earlier during the Phase 2 shortlist pass — company career-board postings can be filled/pulled/replaced that fast (seen directly: a listing gone, replaced by a different role in the same slot, within the same session). If a listing has disappeared, say so plainly rather than writing a doc as if it's still open, and don't silently substitute a different listing without flagging the swap to the person.
- **Watch for AI-training-data contractor gigs disguised as normal engineering job titles** (seen from postings routed through micro1 and similar "AI data lab" platforms) — a listing titled "Senior Software Engineer" or "Frontend Developer" can actually be a part-time contractor role writing/reviewing code samples to train AI models, not a product-engineering job. Always read the real posting body, not just the title, and flag this prominently if the actual work is data-labeling/training-data generation rather than the software engineering role the person asked for — don't build out a full application-prep doc for a role-type mismatch like this without checking first.
