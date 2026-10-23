# Demo 2: spec first

Spec-driven development: write the rules and the spec first, then let the agent build from them. **Scope: frontend only.** The demo is a website built in the browser layer, with no backend and no full-stack work. This branch holds only the inputs (markdown, no code). The project the agent works in comes from the shared `starter` branch.

## What is in this branch

| File | What it is | Used by |
|---|---|---|
| `CLAUDE.md`, `AGENTS.md` | Rules file: scope, stack, rules, brand tokens. Identical copies. | Claude Code, Antigravity CLI |
| `.claude/skills/landing-page-qa/SKILL.md`, `.agents/skills/landing-page-qa/SKILL.md` | Checklist skill for checking the page. Identical copies. | Claude Code, Antigravity CLI |
| `static/devfest-banner.webp` | The DevFest Davao 2026 promo banner. Part of the inputs; the spec points the DevFest band at it. Step 2 of "Set up" keeps it. | Both |
| `DESIGN.md` | Visual and interaction rules: color, type, layout, components, motion. Read before UI work. | Both |
| `.claude/agents/frontend-developer.md` | Subagent that builds the page, using Impeccable for design | Claude Code |
| `.claude/agents/spec-reviewer.md` | Subagent that reports spec mismatches only | Claude Code |
| `.claude/agents/gitops.md` | Subagent that commits with Conventional Commits | Claude Code |
| `.claude/agents/documenter.md` | Subagent that writes the website docs to `docs/website.md` | Claude Code |
| `demo/run-all-prompt.md` | One prompt that runs every phase, from constitution to docs | Both |
| `demo/1-constitution-prompt.md`, `demo/2-specify-prompt.md`, `demo/3-plan-prompt.md` | The three phase inputs, in order. The one-prompt run reads them. | Both |

The Antigravity CLI has no user-defined subagents, so it gets the same four jobs as plain prompts (see "Run it"). Keep each pair of identical copies in sync.

## Prerequisites

- **Node.js** (current LTS) and npm, to install and run the project.
- **git**, to clone the repo and switch branches.
- **A coding agent**: Cursor, Claude Code, Antigravity, Copilot, or similar. Any one works.
- **The same agent and model for both demos**, so the results are comparable.
- **[Spec Kit](https://github.com/github/spec-kit)** (optional), installed with [uv](https://docs.astral.sh/uv/). Without it, follow "No Spec Kit?" below.

## Set up

1. **Get the repo and switch to this branch.**

   ```sh
   git clone https://github.com/jeoooo/slap-ai-slop-sdd.git
   cd slap-ai-slop-sdd
   git checkout demo-2
   ```

2. **Bring in the starter project** (SvelteKit + Ark UI, no page yet). It is identical for both demos.

   ```sh
   git checkout starter -- .gitignore .npmrc .vscode package.json package-lock.json tsconfig.json vite.config.ts src static
   npm install
   ```

3. **Install the design skill.** [Impeccable](https://impeccable.style) is a design skill the implementation step uses. It is an input to this demo, like the rules file, so install it before marking the starting point.

   ```sh
   npx impeccable install
   ```

   Choose your agent (Claude Code or Antigravity) and install it into the project. Restart or reload your agent afterward. Installer options can change, so check the [Impeccable README](https://github.com/pbakaus/impeccable) if a prompt differs.

4. **Mark the starting point** so you can diff against it later.

   ```sh
   git add -A
   git commit -m "Starter: SvelteKit + Ark UI"
   git tag demo-2-starter
   ```

## Run it (one prompt)

This is the main path. It keeps the demo short: one message, and the agent does every phase.

1. Set up as above, then create one branch for the run: `git switch -c demo-2-run`
2. Open your agent in this folder and send `demo/run-all-prompt.md` as your only message: type `@demo/run-all-prompt.md` (the agent attaches the file), or paste its contents.
3. It runs six phases in order (constitution, specify, plan, tasks, implement, review) and then writes `docs/website.md`. It commits after each phase with Conventional Commits and never pushes. Don't add anything else while it runs.
4. Run what it built (see "Run what it built"), then mark the result (see "Mark the final result").

The phases still map to the six chapters below, so you can compare them. To keep chapter tags, tag each phase commit by hand afterwards:

```sh
git log --oneline          # find the commit for each phase, oldest first
git tag demo-2-ch1 <sha>   # constitution; repeat for ch2 to ch6
```

The run depends on the agent being able to use the Spec Kit commands from a prompt. If it can't, it writes `specs/*.md` itself, as in "No Spec Kit?" below. Do a dry run before you record.

## Step by step (optional)

Use this path to run each chapter on its own, for example to show one phase in detail. The one-prompt run covers the same ground.

### Chapters

The demo runs in six chapters. Each chapter has its own branch, built on the one before, and a tag on its last commit, so you can check out any point or diff two chapters.

| Chapter | Branch | Tag | What it adds |
|---|---|---|---|
| 1. Constitution | `demo-2-ch1-constitution` | `demo-2-ch1` | The project constitution |
| 2. Specify | `demo-2-ch2-specify` | `demo-2-ch2` | The feature spec |
| 3. Plan | `demo-2-ch3-plan` | `demo-2-ch3` | The implementation plan |
| 4. Tasks | `demo-2-ch4-tasks` | `demo-2-ch4` | The task list |
| 5. Implement | `demo-2-ch5-implement` | `demo-2-ch5` | The page, built |
| 6. Review | `demo-2-ch6-review` | `demo-2-ch6` | QA and review fixes, plus `docs/website.md`: the final result |

For every chapter, do the same four things:

1. **Create the chapter branch** from the previous one (chapter 1 starts from `demo-2`): `git switch -c demo-2-ch1-constitution`
2. **Run the step** (see "Run it step by step" below).
3. **Commit it.** Claude Code: `Use the gitops subagent to commit the work.` Antigravity CLI: `Commit the work using Conventional Commits.` Expect messages like `docs: add constitution` or `feat(hero): add headline and reserve-a-pack cta`. Neither agent pushes.
4. **Tag it**: `git tag demo-2-ch1`

### Run it step by step (with Spec Kit)

1. **Install Spec Kit and add it to this folder.** It needs [uv](https://docs.astral.sh/uv/).

   ```sh
   uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
   ```

   Then add it for your agent:

   - **Claude Code:** `specify init --here --integration claude`
   - **Antigravity CLI:** `specify init --here --integration agy` (writes skills to `.agents/skills/`)

   Flags and command names change between versions, so check `specify --help` if one is rejected. The rules file, skill and reviewer subagent from this branch must stay in place.

2. **Open your agent in this folder** and run the steps in order. Type the command, then paste the contents of the matching file. Clear the chat between steps if the agent drifts; it keeps what it needs in the files it writes.

   | Chapter | Command | Paste |
   |---|---|---|
   | 1. Constitution | `/speckit-constitution` | `demo/1-constitution-prompt.md` |
   | 2. Specify (what and why, no technology) | `/speckit-specify` | `demo/2-specify-prompt.md` |
   | 3. Plan (the how) | `/speckit-plan` | `demo/3-plan-prompt.md` |
   | 4. Tasks | `/speckit-tasks` | nothing; skim the list |
   | 5. Implement | `/speckit-implement` | nothing |

   For chapter 5, tell the agent how to build:

   - **Claude Code:** `Use the frontend-developer subagent to implement the tasks.` It runs Impeccable (`/impeccable init`, then critique, audit and polish) as it goes.
   - **Antigravity CLI:** `Implement the tasks and use the impeccable skill for design: run init first, then critique, audit and polish when the page is built.`

   Type `/` in your agent to confirm the command names in your version. The Antigravity CLI integration installs skills, so its commands may be named differently.

3. **Chapter 6: review.** First ask the agent to run the `landing-page-qa` skill. Then review:

   - **Claude Code:** ask it to use the `spec-reviewer` subagent, then `fix the failures the spec-reviewer reported`.
   - **Antigravity CLI:** ask `Review the page against the spec and list only the mismatches`, then `fix those mismatches`.

   Fix only what the review flags. Then write the docs:

   - **Claude Code:** `Use the documenter subagent to document the website.`
   - **Antigravity CLI:** `Read the spec, CLAUDE.md and the built page, then write docs/website.md: overview, how to run it, file structure, each page section, the Ark UI parts, brand tokens, accessibility and SEO, and constraints. Describe only what the code does. Edit no other file.`

   Check that `docs/website.md` exists and matches the page. Then commit and tag chapter 6 as above.

### No Spec Kit?

The prompts are plain text, so the method works in any agent without the CLI. Skip the install and give each step as a plain instruction that says where to write the result, followed by the contents of the same file:

| Chapter | Instruction | Paste |
|---|---|---|
| 1. Constitution | "Write a project constitution to `specs/constitution.md` from these principles:" | `demo/1-constitution-prompt.md` |
| 2. Specify | "Write a feature spec to `specs/spec.md` from this. What and why only, no technology:" | `demo/2-specify-prompt.md` |
| 3. Plan | "Write an implementation plan to `specs/plan.md` from this spec and constitution:" | `demo/3-plan-prompt.md` |
| 4. Tasks | "Break the plan into an ordered checklist in `specs/tasks.md`." | nothing |
| 5. Implement | "Implement the tasks in order and tick each one off. Use the impeccable skill for design: init first, then critique, audit and polish." (Claude Code: add "Use the frontend-developer subagent.") | nothing |

Then review as in chapter 6 above. The no-Spec Kit steps are the same for Claude Code and the Antigravity CLI. Without Spec Kit's templates the spec files will be less uniform from run to run. The process is the same: specs first, code second.

## Run what it built

```sh
npm run dev
```

Open the URL it prints. For a production check, run `npm run build && npm run preview`.

## Mark the final result

Chapter 6 is the final result. Give it the usual names too:

```sh
git status                  # should be clean, with docs/website.md committed
git branch after-demo-2
git tag demo-2-after
```

Don't add a second spec or extra instructions while you run it. The point is to compare the two processes fairly.

## Compare

- `git diff demo-2-starter demo-2-after`: the specs, plan, tasks and code the agent produced.
- `git diff demo-2-ch2 demo-2-ch3`: what any one chapter added (swap in any two chapter tags).
- `git diff demo-1-after demo-2-after`: this approach against pure vibe.

See `main` for the full demo hub.
