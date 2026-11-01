# Sportz

SvelteKit app served by `adapter-node`.

```sh
npm install
npm run dev      # dev server
npm test         # unit tests
npm run check    # types + svelte-check
npm run build    # production build into ./build
```

## Docker

```sh
docker build -t sportz .
docker run -p 3000:3000 sportz
```

Health check: `GET /api/health`. Agent and contributor workflow: `AGENTS.md`.
