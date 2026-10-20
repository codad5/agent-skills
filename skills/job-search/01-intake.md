# Phase 1 — Intake

Ask these before searching anything, unless an existing persona or profile doc for this person already answers a given item (reuse it, don't re-ask). Keep this to one focused round of questions where possible — use `AskUserQuestion` for the ones with clean multiple-choice answers, free text for the rest.

## Required fields

1. **Target role(s) and seniority.** Primary role (e.g. "backend software engineer"), acceptable adjacent roles (e.g. "full-stack or frontend if pay justifies it"), and seniority level. Don't assume — someone's primary and acceptable-adjacent roles can differ a lot.
2. **Core skills to match against.** Pull from an existing resume/persona doc if available; otherwise ask directly.
3. **Location and work-mode constraints** — this is the one most sessions will get wrong by defaulting to a generic assumption:
   - Remote-anywhere acceptable? (usually yes, confirm)
   - Which specific countries/regions are viable for a **remote** role — i.e. where can they legally be paid from/work for, without a visa? (this varies a lot by person — a Nigeria-based person can usually take remote roles from US/EU companies with no visa; someone else's legal situation may differ — ask, don't assume the answer that applied to a past user)
   - Which countries/regions would they consider **relocating** to, and only if the employer **sponsors the visa**? If they wouldn't relocate at all, say so.
   - Which specific **cities** would they accept a fully **on-site/physical** role in (their own city/region, not "anywhere")? Get exact city names, not just "my country."
4. **Pay floor for on-site/physical roles**, in the person's own currency, and whether it's monthly/annual. This is separate from remote-role pay expectations — an on-site role in the person's home city has a different market rate than a remote role paid by a foreign company, and they will likely differ. If the person doesn't have a hard floor for remote roles, that's fine — many remote roles from foreign companies clear any reasonable local floor automatically, but confirm this assumption with them rather than asserting it.
5. **What to do when a listing has no salary info.** Default: note "not disclosed" in the doc; if the application platform/form has a field for the applicant to state expected/desired pay, offer to fill that field with a reasoned figure — confirm the number with the person before it goes in any doc that looks like a submittable answer.
6. **How many jobs to shortlist.** Ask for a number (e.g. 10 / 20 / 50) rather than assuming — this changes how broad the platform search needs to be.
7. **Recency window.** Confirm the "how old can a listing be" preference (this skill's default assumption, to offer as a starting point, is "posted within the last week, prefer last 3 days" — but ask, don't assume every user wants that).
8. **Platforms to search.** Offer a sensible default list (general job boards: LinkedIn Jobs, Indeed; startup-focused: Y Combinator's Work at a Startup, Wellfound; plus career pages of specific companies the person names) and let the person add/remove. Ask if they have specific companies in mind (this is often the highest-signal input — a person naming two or three specific companies tells you a lot about the tier/style of company they're targeting) and, if they want suggestions, propose comparable companies for them to confirm rather than picking silently.

   When proposing companies, pick sources that actually fit the person's stated region/target market rather than defaulting to a US/Silicon-Valley list — pull from whichever of these are relevant: YC's own company directory (ycombinator.com/companies, filterable by region/industry/batch) and Work at a Startup itself, a16z's portfolio page for VC-backed startups, and — importantly — regional/local sources: for a Nigeria/Africa-focused search that means known fintech/tech employers (e.g. Paystack, Flutterwave or Moniepoint-tier fintechs), for other regions substitute the equivalent local ecosystem (e.g. YC Europe/LatAm batches, a regional startup-directory site, or well-known local employers the person can name). Don't reuse a company list from a past session/user as a generic default — derive it from this person's actual stated region and target company tier.

   Note: Stack Overflow's old job-listing/apply flow was discontinued in 2022, but `stackoverflow.com/jobs/companies` is a live company directory (profiles filterable by tag/location) — useful for discovering companies to check, not for browsing live job postings directly. Verify current behavior before relying on it, since Stack Overflow has changed this area of the site before.
9. **Resume status.** Do they have an existing resume/CV to reference? Where does it live? Is it current, or does it need a refresh first (an existing persona or profile doc may already answer this).
10. **Working-hours flexibility.** Confirm whether timezone/working-hours overlap with the employer is a real constraint or a non-issue — affects which remote roles are worth including.

## What NOT to do

- Don't assume a default answer for any of the above based on a previous user's constraints from an earlier session — this skill must ask fresh every time unless a same-project persona doc already has the answer on record.
- Don't skip straight to searching because "the request sounds clear enough" — a missing visa/location constraint is the single most common way this skill would waste effort producing docs for jobs the person can't actually take.
