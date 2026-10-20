# Agent skills

Open-source skills for AI coding agents: Claude Code, Cursor, Codex, Gemini CLI, Copilot and any other agent that reads `SKILL.md`. Each skill is a folder of plain Markdown: a short `SKILL.md` that routes the agent through phases, plus one file per phase.

## Skills

| Skill | For | Install |
|---|---|---|
| [`product-frontend`](#product-frontend) | Everyday product UI and the code behind it: dashboards, admin tools, chat apps, forms, marketing pages | `npx skills add codad5/agent-skills --skill product-frontend` |
| [`job-search`](#job-search) | Finding real job listings and preparing every application (it never applies for you) | `npx skills add codad5/agent-skills --skill job-search` |

See every skill in the repo, with descriptions, without installing anything:

```sh
npx skills add codad5/agent-skills --list
```

Install them all at once with `npx skills add codad5/agent-skills`.

## Before you start

- **Node.js 22 or newer**, for `npx`. That's all: no account, no login, no config. The repo is public.
- Run the command **inside the folder you want the skill in**: your project for `product-frontend`, or your job-search working folder for `job-search`.
- Useful flags:
  - `-a claude-code` installs for one agent and skips the agent prompt (other values include `cursor`, `codex`, `gemini-cli`, `github-copilot`).
  - `-g` installs for every project on this machine instead of just this folder.
  - `-y` accepts the defaults without prompting.
- **After installing, start a new agent session** so it picks the skill up.
- Check what's installed with `npx skills list`.

### Or let your agent set it up

Copy this into your agent as it is: nothing to fill in. Add a skill name at the end if you already know which one you want; leave it off and the agent will help you choose.

```text
Set up a skill for me from https://github.com/codad5/agent-skills.

1. Run `npx skills add codad5/agent-skills --list` to see every skill in the repo with
   its description. If npx isn't available, read the repo's README and each
   skills/*/SKILL.md instead.
2. If I named a skill below, use it. If I didn't, show me the list in one line per
   skill, ask what I want to get done, and recommend the skill that fits best with
   one line on why. Wait for my answer.
3. Work out which agent you are and install the chosen skill for this folder only:
   `npx skills add codad5/agent-skills --skill <chosen skill> -a <your agent id> -y`
   (claude-code, cursor, codex, gemini-cli, github-copilot, windsurf or opencode).
   Without npx, clone the repo and copy skills/<chosen skill>/ into this folder's
   skills directory (.claude/skills/ for Claude Code, .agents/skills/ for most others).
4. Read the installed SKILL.md and tell me in two lines what it does, what it needs
   from me (tools, files, permissions) and whether I should start a new session.

Skill (optional):
```

---

## product-frontend

Plans and builds the everyday parts of a product's frontend: both how it looks and how it works. It reads your codebase first and works out whether the real problem is the UI, the code underneath (rendering, data fetching, state, types, performance) or both. It recommends working only where it pays, and it obeys "keep the UI as it is" or "only restyle".

**Not for** showpiece work: games, 3D, heavy animation, illustration or experimental interactive art.

### Set up

```sh
cd your-project
npx skills add codad5/agent-skills --skill product-frontend -a claude-code
```

**Helps if available, but optional:**
- a browser tool for the agent (Claude Code's built-in browser, a Playwright MCP server, or the Claude in Chrome extension), so it can see and screenshot your screens. Without one it asks you for screenshots.
- permission to run your dev server. It won't start one unless you agree, and it uses a non-default port.

### What to do next

1. Open a new agent session in the project.
2. Ask in your own words, or type `/product-frontend` in Claude Code. For example:
   - "Revamp our dashboard, it looks generated."
   - "Keep the UI exactly as it is, but our pages are slow and the data fetching is a mess."
   - "Set up a design system before we build the settings pages."
   - "Polish this page without moving anything."
3. Expect, in order:
   - a short read of your code, with the UI and the code each scored out of 10;
   - one round of questions with a recommended answer for each: what the project is to you (MVP, startup, client work, side project), UI or code or both, and scope;
   - effort options sized in days, commits and tokens, with a recommendation and whether it can go in gradually or needs a rebuild;
   - visual directions (UI work) or architecture options (code work) to choose from;
   - **a phased plan for you to approve. Nothing is built before you say yes.**
4. Then it builds phase by phase. After each phase it sends a short update and stops at the review points in the plan.

Plans, decisions and progress are saved in your project's docs (`docs/design/` by default), so a later session can pick up where the last one stopped.

### Files

| File | What it covers |
|---|---|
| [SKILL.md](skills/product-frontend/SKILL.md) | The order of phases and the hard rules |
| [01-context-scan.md](skills/product-frontend/01-context-scan.md) | Reading the code, docs, history and screens; scoring |
| [02-intake.md](skills/product-frontend/02-intake.md) | Which questions to ask and how |
| [03-sizing-and-approach.md](skills/product-frontend/03-sizing-and-approach.md) | Project type, effort levels, patch vs rewrite |
| [04-directions-and-proposals.md](skills/product-frontend/04-directions-and-proposals.md) | Showing visual options; colour ramps; decoding screenshots |
| [05-architecture-and-data.md](skills/product-frontend/05-architecture-and-data.md) | Rendering, the data seam, sample data, state, performance |
| [06-design-system.md](skills/product-frontend/06-design-system.md) | Tokens, surfaces, components, enforcement |
| [07-plan-and-build.md](skills/product-frontend/07-plan-and-build.md) | The phased plan, the per-screen loop, tracking |
| [08-craft-checklist.md](skills/product-frontend/08-craft-checklist.md) | The final quality pass |
| [09-layout-rules.md](skills/product-frontend/09-layout-rules.md) | Optional box layout rules (gap-only spacing, tokens only) |
| [10-working-agreements.md](skills/product-frontend/10-working-agreements.md) | Dev server, tests, commits, updates |
| [11-related-skills.md](skills/product-frontend/11-related-skills.md) | Finding other skills that fit your stack |
| [12-reference-cases.md](skills/product-frontend/12-reference-cases.md) | The real projects behind the rules |

---

## job-search

Searches live job boards and company career pages, filters listings against your real constraints (location, visa, remote vs on-site pay floor, role fit) and gives you a shortlist to prune. Then, for each job you approve, it writes one complete doc: how to apply, every form question answered, a tailored resume and cover letter, an ATS keyword check, when to apply, and an honest fit score.

**It never applies, sends emails or submits forms.** You do that yourself.

### Set up

```sh
mkdir job-search && cd job-search      # any folder you'll keep your search in
npx skills add codad5/agent-skills --skill job-search -a claude-code
```

**Needed:**
- **a browser tool** for the agent (Claude Code's built-in browser, a Playwright MCP server, or the Claude in Chrome extension). Listings must be read live, so without one the skill stops and asks you to enable one.

**Recommended:**
- your current resume or CV in the folder (Markdown, PDF or DOCX), so it can match against it and tailor copies;
- being logged in to LinkedIn or other job boards in that browser. It can work without this, but results are better with it. It never changes your account settings.

### What to do next

1. Open a new agent session in the folder.
2. Ask: "Find me jobs", or type `/job-search` in Claude Code.
3. Answer one round of questions:
   - target roles and seniority;
   - where you can work remotely without a visa, where you'd relocate with sponsorship, and which cities you'd accept on-site;
   - your pay floor;
   - how many jobs and how recent;
   - which platforms and companies.
4. Review the shortlist (`YYYY-MM-DD/shortlist.md`) and say which jobs to keep.
5. Get one doc per approved job in the same date folder, and a `00-INDEX.md` listing every search, its jobs, their status and what the market keeps asking for that your resume doesn't show.
6. Apply yourself, using the docs.

### Files

| File | What it covers |
|---|---|
| [SKILL.md](skills/job-search/SKILL.md) | The order of phases, output layout, hard rules |
| [01-intake.md](skills/job-search/01-intake.md) | The questions it asks before searching |
| [02-shortlist.md](skills/job-search/02-shortlist.md) | Searching, filtering, the shortlist |
| [03-per-job-doc.md](skills/job-search/03-per-job-doc.md) | The per-job document template |
| [04-resume-and-ats.md](skills/job-search/04-resume-and-ats.md) | Tailoring resumes and ATS-safe PDFs |

---

## Install without npx

```sh
git clone https://github.com/codad5/agent-skills.git
```

Copy the skill's folder to where your agent looks for skills:

| Agent | This project | Every project |
|---|---|---|
| Claude Code | `.claude/skills/<skill-name>/` | `~/.claude/skills/<skill-name>/` |
| Agents that read `.agents/` (Codex, Cursor and others) | `.agents/skills/<skill-name>/` | `~/.agents/skills/<skill-name>/` |

```sh
mkdir -p .claude/skills
cp -r agent-skills/skills/product-frontend .claude/skills/
```

On Windows PowerShell: `Copy-Item -Recurse agent-skills\skills\product-frontend .claude\skills\`.

To update later, run the `npx skills add` command again, or pull the repo and copy the folder again.

## Find more skills

```sh
npx skills find design system
npx skills find nextjs
```

Or browse [skills.sh](https://skills.sh). `product-frontend` also looks for skills that fit your stack and suggests them, but it asks before installing anything.

## Contributing

Issues and pull requests are welcome. Keep the style: plain imperative prose, every rule with a reason, a "What NOT to do" section at the end of each phase file, and nothing personal or project-specific baked in.

## License

[MIT](LICENSE)
