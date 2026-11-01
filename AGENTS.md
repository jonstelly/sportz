# Sportz

SvelteKit 3 + Svelte 5 + TypeScript web app, `adapter-node`, shipped as one Docker container. Domain language: `GLOSSARY.md`; decisions: `docs/adr/` (both created on demand).

## Workflow (mandatory)

- Every change, however small, follows the process; no naked implementation.
- Before any edit, read `docs/agents/workflow.md`, `docs/agents/issue-tracker.md`, `docs/agents/domain.md`, and the relevant `GLOSSARY.md` terms and ADRs.
- Route through the skills named in `workflow.md`; load each with the skill tool. Work happens under a tracked issue; a ready ticket runs through `implement`.
- A user request ("fix X") selects the work, not the route. Settled work skips planning ceremony only; it keeps its ticket and `implement`.
- If the issue is not `ready-for-agent`, or a required skill will not load: stop and tell the user.
- Record decisions in the issue, spec, ADR or `GLOSSARY.md`, not chat only.

## Commands

Run from the repo root.

- `npm run dev`: dev server
- `npm run check`: svelte-check + types
- `npm test`: Vitest, single run (`npm run test:unit` watches)
- `npm run build` / `npm run preview`: production build / serve it
- `docker build -t sportz . && docker run -p 3000:3000 sportz`

## Architecture

- API: `src/routes/api/**/+server.ts`. Page data: `+page.server.ts` `load`. Shared code: `src/lib`.
- Tests sit beside the code as `*.spec.ts`.

## Constraints

- Svelte 5 runes only (`$state`, `$derived`, `$props`, `$effect`); `runes: true` is enforced in `vite.config.ts`.
- Config lives in `vite.config.ts`; SvelteKit 3 has no `svelte.config.js`.
- Add dependencies only when the task needs them.

## Delivery

- Mainline flow. `main` is protected; never commit or push to it.
- Branch from `origin/main`: `feature/<topic>`, `fix/<topic>`; spec children use `ticket/<issue-number>`, landed on the spec's `feature/<topic>`.
- Commits carry `Refs #N`; the completing commit carries `Closes #N`. A parent closes with its last child.
- The agent opens the PR (`pr` skill, `gh pr create --base main`) after checks and review; humans review and merge.
- The current `initial` branch carries the bootstrap work; new work follows the flow above.

## Verification

- Inner loop: `npm test` for changed behavior. Changed behavior gets a regression test.
- Before handoff: `npm run check`, `npm test`, `npm run build`. Run the Docker build when `Dockerfile` or dependencies change.

## Agent skills

### Issue tracker

Issues live in GitHub Issues (jonstelly/sportz) via the `gh` CLI. See `docs/agents/issue-tracker.md`.

### Triage labels

Default five-label vocabulary (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: root `GLOSSARY.md` and `docs/adr/`. See `docs/agents/domain.md`.
