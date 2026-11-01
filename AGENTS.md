# Sportz

SvelteKit app (adapter-node) with TypeScript.

- Svelte 5 runes only (`$state`, `$derived`, `$props`, `$effect`); no Svelte 4 syntax (`export let`, `$:`, stores for local state).
- SvelteKit 3 config lives in `vite.config.ts` (no `svelte.config.js`).
- API endpoints: `src/routes/api/**/+server.ts`. Page data: `+page.server.ts` `load`.
- Verify with `npm run check` and `npm run build`.
- Container: `docker build -t sportz . && docker run -p 3000:3000 sportz`.
