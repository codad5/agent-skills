# Phase 2 — Shortlist pass

Goal: one shortlist document, built from real live searches, that the person can prune before any expensive per-job work happens.

## Per-platform notes

- **LinkedIn Jobs**: if the browser session is already logged in as the person, use LinkedIn's own filters (date posted, remote, location) rather than re-deriving them by hand — faster and more reliable than manual scanning.
- **Indeed**: similar filter support; check login state before assuming personalization features work.
- **Y Combinator's Work at a Startup / YC Jobs**: strong signal for startup-tier roles; usually doesn't require login to browse.
- **Wellfound (formerly AngelList Talent)**: similar startup focus; check whether salary/equity is disclosed per listing since it often is here more than elsewhere.
- **Company career pages**: for named companies, go directly to their careers page rather than searching a third-party aggregator for them — aggregators can be stale or missing postings a company's own page has.
- **Social feeds, if the person is already logged in to that browser session**: X/Twitter search, and the person's own Facebook/Instagram/LinkedIn feed (not the dedicated job-listing sections already covered above) can surface postings shared by companies, recruiters, or the person's own network that never make it to a formal job board — worth a quick check when a browser session is authenticated, skip silently if it isn't (never prompt the person to log in just for this). Treat results the same as any other source: real posting, real link, same filters applied.
- **Google Search / Google for Jobs**: a plain Google search for the role plus "jobs" surfaces Google's own aggregated job-listings panel (pulled from many boards and company sites at once), which can catch postings the other platforms missed. If the browser session is logged into a Google account, results and any inline "Apply"/save buttons can be personalized to that account (location, search history, saved jobs) — that's fine to use as signal, but still verify each listing's real source/link the same as any other, and never click an inline Apply/save button since that can register an action against the logged-in account.
- Note whichever platforms actually required login vs. worked anonymously, and whether personalized results changed anything — worth recording in the skill later if it caused a real problem.

## Faster, more reliable data than the browser (use these when the browser lags or lazy-loads)

- **LinkedIn public guest endpoints need no login and return whole result pages:** `https://www.linkedin.com/jobs-guest/jobs/api/seeMoreJobPostings/search?keywords=...&location=...&f_TPR=r604800&sortBy=DD&start=0` (25 cards per page, add `&f_WT=2` for remote), and `https://www.linkedin.com/jobs-guest/jobs/api/jobPosting/<jobId>` for the full description text, which the logged-in page often fails to render. Running 15 to 20 stack-specific queries this way surfaced far more than scrolling the browser list, and it catches jobs the person's own default search never shows.
- **Greenhouse public API** (`https://boards-api.greenhouse.io/v1/boards/<company>/jobs/<id>?questions=true`) returns the full posting, the pay range, and the exact application form questions including dropdown options, without touching the form. Use it to check a location or country dropdown for the person's country before recommending a role. The board token is usually the company name but not always, so try a couple of variants.
- Lever (`api.lever.co/v0/postings/<company>?mode=json`) and Ashby (`api.ashbyhq.com/posting-api/job-board/<company>`) have similar public endpoints.
- Jobs the person saved as social posts (X, and so on) often have no link. Search the company name on LinkedIn or its own job board, and say plainly when a post can't be verified instead of guessing which company it is.

## Generic keyword queries return noise; domain-specific compound queries return signal

Observed directly: a plain "backend engineer" or "software engineer" LinkedIn/browser query, even filtered to the person's location, surfaced mostly game-studio roles, quant-trading roles, staffing-agency contractor gigs, and internships — high volume, low relevance. A person's own social feed and a handful of direct company checks, by contrast, surfaced several strong matches in one pass. The difference was specificity: the good listings clustered around the person's actual domain, not just their language/framework.

**Fix: always run compound queries that pair the role with the person's real domain, not just the role alone.** After the intake step establishes the person's core stack and the kind of work they actually do (payments, fintech, health, logistics, whatever it is), build queries like `<role> <domain>` (e.g. "backend engineer fintech remote", "payments engineer remote Africa", "backend developer SaaS Nigeria") and, once a few strong matches are found, extract the phrases that keep recurring across them (for a payments backend engineer, say: Node.js, TypeScript, multi-tenant, ledger, reconciliation, webhook, event-driven, queue) and run a follow-up pass of queries built from those specific phrases. A role-only query is a reasonable first pass to establish volume, but don't stop there — the domain-plus-role and phrase-specific queries are where the real signal is.

## What to capture per listing during this pass (lightweight — no drafting yet)

- Title, company, location/remote status, posted date (as stated by the platform)
- Link
- Whether it clears the person's location/visa constraint (yes/no/unclear — if unclear, say what's ambiguous rather than guessing)
- Pay, if disclosed (state the currency and period as given, don't convert/estimate)
- A quick one-line fit note (not a full assessment yet)

## Output

One markdown file (e.g. `shortlist.md`) with a table or list of everything found, grouped by platform or by fit, whichever is more scannable. Present this to the person and get explicit confirmation of which jobs to carry into Phase 3 before doing anything else with them — including sorting/prioritizing, that's their call to make once they see the list, not something to decide for them.

## What NOT to do

- Don't write a tailored resume, cover letter, or answer any form questions during this pass — that's Phase 3, and only for jobs the person actually picks.
- Don't silently drop a listing that fails a filter — list it with the reason it was excluded (or excluded to a separate "didn't qualify" section) so the person can override a judgment call if the skill got it wrong.

## Relevance bar

The job description must actually match the person well — role, seniority, and core skills — not just clear the location/pay/visa filters. A remote EMEA-tagged listing that clears every hard filter but is a poor skills/seniority match is noise, not a candidate. Read the actual JD, not just the title, before including something as a fit; when it's a stretch, say so plainly in the one-line fit note rather than padding the shortlist with weak matches to hit a target count. A shorter, honest shortlist beats a padded one.

Match on transferable skill, not literal keyword overlap — a listing naming a specific tool the person hasn't used is not automatically a miss if they have a closely analogous tool in the same category and the surrounding stack/seniority fits: RabbitMQ/Celery/BullMQ experience is a reasonable stand-in for a Kafka requirement, React/Angular for a Vue requirement, one SQL database for another, etc. Judge by "could plausibly ramp on this specific gap fast given what they've actually built," not by a keyword checklist. Still name the gap honestly in the fit note (e.g. "JD asks for Kafka; you've used RabbitMQ/BullMQ — same category, different tool, worth mentioning in the application") rather than silently treating it as a full match.

Be conservative about what counts as transferable — this only holds within the same underlying paradigm/ecosystem, not across genuinely different ones. React Native and Flutter are both "mobile," but different language, different rendering model, different toolchain — knowing one is a weak signal for the other, not a real substitute; don't wave that through as a match. Depth matters too: a requirement backed by only ~1 year of hands-on experience with the *adjacent* tool itself is a thin transfer, not a solid one — say so ("technically used React Native, but only ~1 year, and the JD wants Flutter specifically — real gap, not a close analog") rather than rounding up to "qualified." When unsure whether two things are close enough to count, err toward naming it as a gap and let the person judge, rather than quietly assuming transfer.

## When the platform's own search/filters are working against the person

If the person is logged in to a job board and its own search/recommendation defaults are visibly not surfacing good matches (e.g. keyword too broad/narrow, wrong location default, missing a filter that would clearly help), that's worth surfacing — don't just silently work around it every time. Ask once, early, whether they'd like:
- a one-time pass where the skill just compensates for it this run (broader manual querying, extra filtering) with no changes to their account, or
- concrete advice on better search keywords/filters/saved-search settings to fix it going forward on that platform.

Don't touch the person's saved filters/search settings on the platform itself without their say-so — this is advice to give, not an account change to make unilaterally.
