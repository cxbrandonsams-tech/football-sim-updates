# Football Sim Configuration Guide

> **Last updated:** 2026-05-02
> **See also:** [deployment-guide.md](deployment-guide.md) | [project-overview.md](project-overview.md) | [api-reference.md](api-reference.md)

## Environment Variables

### Backend

| Variable | Required in prod | Purpose |
|----------|------------------|---------|
| `NODE_ENV` | Yes | Must be `production` in production |
| `DATA_DIR` | No | SQLite data directory, defaults to `./data` locally |
| `JWT_SECRET` | Yes | JWT signing secret; production refuses the dev default |
| `ALLOWED_ORIGINS` | Yes | Comma-separated allowed frontend origins |
| `ALLOW_VERCEL_PREVIEWS` | No | Allow `*.vercel.app` preview origins |
| `ALLOW_LEGACY_COACH_WIPE` | No | Dangerous one-time legacy reset switch |
| `OPENAI_API_KEY` | No | Required for radio generation |
| `R2_ACCOUNT_ID` | No | R2 config for radio assets |
| `R2_ACCESS_KEY_ID` | No | R2 access key |
| `R2_SECRET_ACCESS_KEY` | No | R2 secret |
| `R2_BUCKET_NAME` | No | R2 bucket |
| `R2_PUBLIC_URL` | No | Public R2 URL prefix |

### Frontend

| Variable | Required in prod | Purpose |
|----------|------------------|---------|
| `VITE_API_URL` | Yes | Backend origin used by the SPA |

## Local Development Defaults

Local development works without extra env vars:

```bash
npm run dev
cd web && npm run dev
```

The backend uses the repo-local `data/` directory and permissive dev CORS defaults.

## Security Guardrails

- Production startup fails if `JWT_SECRET` is missing, too short, or still using the development default.
- Production startup fails if `ALLOWED_ORIGINS` is empty.
- Team-management routes require authenticated league access and an owned team seat.
- SSE access is token-gated through authenticated stream-token issuance.
- `ALLOW_LEGACY_COACH_WIPE=true` is intentionally destructive and should stay off in ordinary environments.

## Important Runtime Constants

These values are current in the shipped codebase:

| Area | Current value |
|------|---------------|
| Salary cap | `255` |
| Max roster size | `56` |
| Min roster size | `45` |
| Regular season length | `18` weeks |
| Hall of Fame threshold | `175` |
| Ring of Honor threshold | `85` |
| Jersey retirement threshold | `130` |
| Hall of Fame wait | `3` seasons |
| Max Hall inductees/year | `7` |
| Training Camp rerolls | `1 / 2 / 3` for Developer HC tiers |
| Live SSE cadence | `8000ms` |
| Quick SSE cadence | `2000ms` |

## Core Configuration Surfaces

- Simulation tuning lives in `src/engine/config.ts`.
- Frontend API wiring lives in `web/src/api.ts` and `web/vite.config.ts`.
- Deployment-specific values live in `fly.toml` plus Vercel project settings.

## Verification Commands

```bash
npm run build
npm test
npm run balance:ci
cd web && npm run build
cd web && npm run lint
```

Use these before promoting configuration changes that affect runtime behavior, deployment safety, or balance gates.
