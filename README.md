# Agent skills

Open-source skills for AI coding agents (Claude Code, Cursor, Codex, Gemini CLI, Copilot and others that read `SKILL.md`). Each skill is a folder of plain Markdown: a short `SKILL.md` that routes the agent through phases, and one file per phase.

## Skills

| Skill | What it does |
|---|---|
| [`product-frontend`](skills/product-frontend/SKILL.md) | Plans and builds the everyday parts of a product's frontend, both how it looks and how it works: dashboards, admin tools, chat apps, settings, forms, marketing pages. It reads the codebase first, works out whether the real problem is the UI, the code underneath or both, asks only the questions that decide the outcome, sizes the effort options from your own pace, writes a phased plan for your approval, then builds and verifies. It is **not** for showpiece work: games, 3D, heavy animation or experimental interactive art. |

## Install

### With the `skills` CLI (recommended)

Requires Node.js 22 or newer.

```sh
# one skill, into the current project
npx skills add codad5/agent-skills --skill product-frontend

# for a specific agent only
npx skills add codad5/agent-skills --skill product-frontend -a claude-code

# for every project on this machine
npx skills add codad5/agent-skills --skill product-frontend -g

# see what's in the repo first
npx skills add codad5/agent-skills --list
```

Check what you have with `npx skills list`, and update with `npx skills update`.

### Manually with git

```sh
git clone https://github.com/codad5/agent-skills.git
```

Then copy the skill folder where your agent looks for skills:

| Agent | Project | Everywhere |
|---|---|---|
| Claude Code | `.claude/skills/product-frontend/` | `~/.claude/skills/product-frontend/` |
| Agents that read `.agents/` (Codex, Cursor and others) | `.agents/skills/product-frontend/` | `~/.agents/skills/product-frontend/` |

```sh
# example: Claude Code, this project only
mkdir -p .claude/skills
cp -r agent-skills/skills/product-frontend .claude/skills/
```

On Windows PowerShell: `Copy-Item -Recurse agent-skills\skills\product-frontend .claude\skills\`.

## Use

Most agents load a skill when your request matches its description. For example, "revamp our dashboard", "make this look less generated", "set up a design system", "our pages are slow, clean up the data fetching" or "keep the UI as is but fix the state management". You can also call it by name: in Claude Code, type `/product-frontend`.

The skill asks before it builds. Expect a short round of questions with recommended answers, effort options to choose from, and a plan to approve.

## Find more skills

```sh
npx skills find design system
npx skills find nextjs
```

Or browse [skills.sh](https://skills.sh). The `product-frontend` skill also searches for skills that fit your stack and suggests them before installing anything.

## Contributing

Issues and pull requests are welcome. Keep the style: plain imperative prose, every rule with a reason, a "What NOT to do" section at the end of each phase file, and no default aesthetic or framework baked in.

## License

[MIT](LICENSE)
