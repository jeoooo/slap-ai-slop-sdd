# slap-ai-slop-sdd

Home of the two demos for the talk **"You're Still the Engineer: Spec-Driven Development in the Agentic Era"** (Slap the AI Slop!, Davao City).

Both demos build the same fictional landing page (a Davao durian coffee brand) with the same stack: **SvelteKit (Svelte 5, TypeScript) + Ark UI** (`@ark-ui/svelte`), plain CSS. No backend, no `.env`, no API keys.

**Scope: frontend only.** Both demos show a website being made in the frontend. There is no backend and no full-stack work, in the prompts, the specs or the code.

## The demos

| Demo | Starting point | Result | Approach |
|---|---|---|---|
| 1 | branch `demo-1` | branch `after-demo-1` | Pure vibe: one prompt, no spec |
| 2 | branch `demo-2` | branch `after-demo-2` | Spec first: rules file, skill, frontend-developer, reviewer and git subagents, Impeccable design skill, spec flow |

`main` (this branch) is the hub: just this README. The shared starter project (SvelteKit + Ark UI, no page yet) lives on the `starter` branch. Each demo starts on `demo-N` and ends on `after-demo-N`, with one branch and tag per chapter in between (see Chapters).

## Run a demo yourself

The demos work in **Claude Code** and the **Antigravity CLI**; any other coding agent works too. Each branch README has a short section for both.

Each demo branch has its own README with the exact steps and the prompts to use. Start there:

- **Demo 1, pure vibe:** `git checkout demo-1`, then follow its `README.md`. The one prompt is in `demo/prompt.md`.
- **Demo 2, spec first:** `git checkout demo-2`, then follow its `README.md`. The three prompts are in `demo/`.

Use the same agent and the same model for both demos, and the prompts exactly as written, so the results are comparable. Any coding agent works.

## Chapters

Each demo is recorded in chapters. Every chapter has a branch, built on the one before, and a tag on its last commit. Browse them in GitHub's branch dropdown, or check out a tag.

**Demo 1, pure vibe** (3 chapters)

| Chapter | Branch | Tag |
|---|---|---|
| 1. First result | `demo-1-ch1-first-result` | `demo-1-ch1` |
| 2. Follow-ups | `demo-1-ch2-follow-ups` | `demo-1-ch2` |
| 3. Final | `demo-1-ch3-final` | `demo-1-ch3` |

**Demo 2, spec first** (6 chapters)

| Chapter | Branch | Tag |
|---|---|---|
| 1. Constitution | `demo-2-ch1-constitution` | `demo-2-ch1` |
| 2. Specify | `demo-2-ch2-specify` | `demo-2-ch2` |
| 3. Plan | `demo-2-ch3-plan` | `demo-2-ch3` |
| 4. Tasks | `demo-2-ch4-tasks` | `demo-2-ch4` |
| 5. Implement | `demo-2-ch5-implement` | `demo-2-ch5` |
| 6. Review | `demo-2-ch6-review` | `demo-2-ch6` |

## What the other branches and tags mean

- **`demo-N`** (branch): the starting point, where the agent starts working. Tagged `demo-N-starter`.
- **`after-demo-N`** (branch): the final result, the same commit as the last chapter. Tagged `demo-N-after`.
- **`demo-N-before`** (tag): markdown only, no code. Demo 1 has the one-line prompt. Demo 2 has the rules file, the skill (two copies), three subagents and the three spec prompts. It is the same commit as the `demo-N` branch before the starter is added.
- **`demo-N-starter`** (tag): `before` plus the shared starter project from the `starter` branch.

A branch and a tag can't share a name without confusing git, so chapter tags are short (`demo-2-ch3`) and chapter branches are long (`demo-2-ch3-plan`).

## See what changed

```sh
git diff demo-1-starter demo-1-after   # everything the agent built in Demo 1
git diff demo-2-starter demo-2-after   # everything the agent built in Demo 2 (specs + code)
git diff demo-1-after demo-2-after     # the two approaches side by side
git diff demo-2-ch2 demo-2-ch3         # what one chapter added (swap in any two chapter tags)
git diff demo-1-before demo-1-after    # everything, including the starter files
```

## What is in each `before` (markdown only, no code)

`demo-1-before`
```
├── README.md                  steps to run Demo 1
└── demo/
    └── prompt.md              the one prompt for Demo 1
```

`demo-2-before`
```
├── README.md                  steps to run Demo 2
├── CLAUDE.md                  rules file (read by Claude Code)
├── AGENTS.md                  same rules file (read by Antigravity CLI)
├── .claude/
│   ├── agents/spec-reviewer.md          Claude Code only
│   ├── agents/frontend-developer.md     Claude Code only: builds the page, uses Impeccable
│   ├── agents/gitops.md                 Claude Code only: commits with Conventional Commits
│   └── skills/landing-page-qa/SKILL.md  skill for Claude Code
├── .agents/
│   └── skills/landing-page-qa/SKILL.md  same skill for Antigravity CLI
└── demo/
    ├── README.md
    ├── 1-constitution-prompt.md
    ├── 2-specify-prompt.md
    └── 3-plan-prompt.md
```

## Run a result

```sh
git checkout after-demo-1    # or after-demo-2
npm install
npm run dev
npm run build && npm run preview
```
