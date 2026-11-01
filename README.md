# Sportz

SvelteKit app served by `adapter-node`.

```sh
pnpm install
pnpm dev        # dev server
pnpm test       # unit tests
pnpm check      # types + svelte-check
pnpm build      # production build into ./build
```

## Docker

```sh
docker build -t sportz .
docker run -p 3000:3000 sportz
```

Health check: `GET /api/health`. Agent and contributor workflow: `AGENTS.md`.
