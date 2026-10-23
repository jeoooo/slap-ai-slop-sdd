# Demo 1: pure vibe

One prompt. No spec, no rules file. **Scope: frontend only.** The demo is a website built in the browser layer, with no backend and no full-stack work. This branch holds only the prompt; the project the agent works in comes from the shared `starter` branch.

## Prerequisites

- **Node.js** (current LTS) and npm, to install and run the project.
- **git**, to clone the repo and switch branches.
- **A coding agent**: Cursor, Claude Code, Antigravity, Copilot, or similar. Any one works.
- **The same agent and model for both demos**, so the results are comparable.

## Run it

1. **Get the repo and switch to this branch.**

   ```sh
   git clone https://github.com/jeoooo/slap-ai-slop-sdd.git
   cd slap-ai-slop-sdd
   git checkout demo-1
   ```

2. **Bring in the starter project** (SvelteKit + Ark UI, no page yet). It is identical for both demos.

   ```sh
   git checkout starter -- .gitignore .npmrc .vscode package.json package-lock.json tsconfig.json vite.config.ts src static
   npm install
   ```

3. **Mark the starting point** so you can diff against it later.

   ```sh
   git add -A
   git commit -m "Starter: SvelteKit + Ark UI"
   git tag demo-1-starter
   ```

## Chapters

The demo runs in three chapters. Each chapter has its own branch, built on the one before, and a tag on its last commit, so you can check out any point or diff two chapters.

| Chapter | Branch | Tag | What it holds |
|---|---|---|---|
| 1. First result | `demo-1-ch1-first-result` | `demo-1-ch1` | What the one prompt produced |
| 2. Follow-ups | `demo-1-ch2-follow-ups` | `demo-1-ch2` | The page after a few casual follow-ups |
| 3. Final | `demo-1-ch3-final` | `demo-1-ch3` | The page where you stopped: the final result |

For every chapter, do the same three things:

1. **Create the chapter branch** from the previous one (chapter 1 starts from `demo-1`): `git switch -c demo-1-ch1-first-result`
2. **Run the chapter** (below).
3. **Commit and tag it**: `git add -A`, `git commit -m "Demo 1 chapter 1: first result"`, `git tag demo-1-ch1`

## Run it

Open your agent in this folder:

- **Claude Code:** run `claude` in the folder.
- **Antigravity CLI:** run `agy` in the folder.

**Chapter 1: first result.** Paste the prompt from `demo/prompt.md`. That is the only input. Then run what it built and look at it:

```sh
npm run dev
```

Open the URL it prints. For a production check, run `npm run build && npm run preview`. Commit and tag chapter 1.

**Chapter 2: follow-ups.** Keep it casual and short ("make it prettier"). Don't mention accessibility, SEO, responsive layout or the palette. Commit and tag chapter 2.

**Chapter 3: final.** Stop when you would stop. Commit and tag chapter 3, then give it the usual names:

```sh
git branch after-demo-1
git tag demo-1-after
```

## Compare

- `git diff demo-1-starter demo-1-after`: everything the agent built.
- `git diff demo-1-ch1 demo-1-ch2`: what the follow-ups changed (swap in any two chapter tags).
- `git diff demo-1-after demo-2-after`: this approach against the spec-first one.

See `main` for the full demo hub.
