# Football Sim Deployment Guide

> **Last updated:** 2026-05-02
> **See also:** [system-architecture.md](system-architecture.md) | [configuration-guide.md](configuration-guide.md) | [api-reference.md](api-reference.md)

## Deployment Model

Football Sim deploys as two separate services:

| Service | Stack | Host |
|---------|-------|------|
| Frontend SPA | React 19 + Vite 8 | Vercel |
| Stateful API | Express 5 + SQLite | Fly.io |

The SPA talks to the API through `VITE_API_URL`. There is no SSR tier.

## Backend Deployment

The backend uses a multi-stage Docker build:

- builder stage installs deps and compiles TypeScript
- runtime stage installs production deps plus native build tooling and `ffmpeg`
- SQLite data is mounted at `/data`

Current Fly.io runtime characteristics:

- app: `football-sim`
- region: `iad`
- VM: `shared-cpu-1x`
- memory: `1024mb`
- persistent mount: `football_sim_data -> /data`
- `auto_stop_machines = off` to avoid breaking stateful SSE usage

### Required Fly secrets

```bash
fly secrets set JWT_SECRET="$(openssl rand -hex 32)" --app football-sim
fly secrets set ALLOWED_ORIGINS="https://your-frontend.vercel.app" --app football-sim
```

Optional radio and preview secrets:

```bash
fly secrets set ALLOW_VERCEL_PREVIEWS="true" --app football-sim
fly secrets set OPENAI_API_KEY="sk-..." --app football-sim
fly secrets set R2_ACCOUNT_ID="..." --app football-sim
fly secrets set R2_ACCESS_KEY_ID="..." --app football-sim
fly secrets set R2_SECRET_ACCESS_KEY="..." --app football-sim
fly secrets set R2_BUCKET_NAME="..." --app football-sim
fly secrets set R2_PUBLIC_URL="..." --app football-sim
```

## Frontend Deployment

Vercel should target the `web/` directory with:

- build command: `npm run build`
- output directory: `dist`
- environment variable: `VITE_API_URL=https://football-sim.fly.dev`

In local development, Vite proxies backend routes to `localhost:3000`; production uses `VITE_API_URL`.

## CI and Verification

The deploy workflow is expected to gate on backend build plus balance checks before promotion.

Recommended verification before deploy:

```bash
npm run build
npm test
npm run balance:ci
cd web && npm run build
cd web && npm run lint
```

If UI-facing work changed Game Day or league flows, run browser-level verification as well.

## Operations Notes

- SQLite persistence lives on the Fly volume, not inside the container image.
- WAL mode is enabled for better concurrent-read behavior.
- Replay and notification data live in supporting DB tables, not just the league blob.
- Radio generation is optional and should not block core deployment if secrets are intentionally absent.

## Common Checks

```bash
fly status --app football-sim
fly logs --app football-sim
fly ssh console --app football-sim
fly volumes list --app football-sim
```

Use these first when investigating a failed deploy, a missing volume mount, or an environment-variable issue.
