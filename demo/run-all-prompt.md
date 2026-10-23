Run everything below as one task. Do not stop between phases and do not ask me anything.

---

Build the Duriano Coffee landing page spec-first, end to end, in one run. Follow `CLAUDE.md` (or `AGENTS.md`) and `DESIGN.md` throughout.

The inputs are three files in `demo/`. In each, ignore the first line and the `---` and use everything after it as the content for that phase. Do not edit these files.

Run the phases in order. Use the Spec Kit command for each phase if it exists in this project. If you cannot run it, write the result yourself to the file named below. Either way, the content must come from the input file.

1. **Constitution**: `/speckit-constitution` with `demo/1-constitution-prompt.md` (fallback: `specs/constitution.md`).
2. **Specify**: `/speckit-specify` with `demo/2-specify-prompt.md` (fallback: `specs/spec.md`). What and why only, no technology.
3. **Plan**: `/speckit-plan` with `demo/3-plan-prompt.md` (fallback: `specs/plan.md`). This is where technology goes.
4. **Tasks**: `/speckit-tasks` (fallback: `specs/tasks.md`, an ordered checklist).
5. **Implement**: `/speckit-implement`. Build the tasks in order and tick each off. Use the impeccable skill for design: run init first, then critique, audit and polish when the page is built. (Claude Code: use the `frontend-developer` subagent.)
6. **Review**: run the `landing-page-qa` skill, then review the page against the spec and list only the mismatches. (Claude Code: use the `spec-reviewer` subagent.) Fix only what they flag, then run `npm run check` and `npm run build`.
7. **Docs**: write `docs/website.md` from the finished page. (Claude Code: use the `documenter` subagent.)

After each phase, commit its work with Conventional Commits (Claude Code: use the `gitops` subagent), so there is one commit per phase, in this order: `docs: add constitution`, `docs: add spec`, `docs: add plan`, `docs: add tasks`, `feat: ...` for the page, `fix: ...` for the review fixes, `docs: add website docs`. Do not push. Do not create branches or tags.

Finish with a short summary: what each phase produced, the QA and review results, and anything you skipped.
