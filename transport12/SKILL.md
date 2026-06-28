---
name: transport12
description: Work on the transport12 project, its HTTP API, Telegram bot, VK Mini App, MCP integration, localization, deployment, and transport data workflows. Use when Codex is asked to change, debug, document, or extend transport12 or its companion repositories.
---

# Transport12

Use this skill for transport12 engineering work. Treat transport12 as a standalone public-facing transport service with its own API, bots, mini apps, and companion integrations.

## Core Rules

- Do not mention or depend on closed internal systems in public code, documentation, commits, or companion repositories.
- Do not put production domains, tokens, SSH credentials, bot tokens, database passwords, or provider secrets into repositories.
- External AI integrations, including MCP, must call the transport12 HTTP API. Do not duplicate direct source-provider parsing in companion clients.
- Do not model favorites, language selection, localized answer generation, main menus, or Telegram/VK button flows as MCP or skill responsibilities.
- Keep user-facing text localized through `src/i18n/index.ts`; avoid hardcoded UI strings in bots and apps.
- For uncertain minority-language terms, prefer an explicit fallback over an invented translation.
- Before deployment, run the project build and verify the service is active after restart.

## Main Repository

The main app normally lives in `D:\transport\transport12`.

Important files:

- `src/server.ts` - Fastify API, webhook, static VK Mini App routes.
- `src/bot/telegram.ts` - Telegram bot flows and keyboards.
- `src/web/vkapp.ts` - VK Mini App HTML/CSS/JS generator.
- `src/i18n/index.ts` - locale dictionaries, fallbacks, language ordering.
- `src/transport/*` - normalized routes, stops, vehicle helpers.
- source adapter directories - internal data adapters used only by transport12.
- `README.md` and `.env.example` - public-safe documentation and configuration examples.

## API Boundary

For new clients and companion repos, use only transport12 API endpoints. Do not call source adapters directly from companion projects.

Common endpoints:

- `GET /health`
- `GET /api/v1/routes`
- `GET /api/v1/routes/:routeId`
- `GET /api/v1/routes/:routeId/stops`
- `GET /api/v1/stops/search?q=...`
- `GET /api/v1/stops/near?lat=...&lng=...`
- `GET /api/v1/stops/:stationId/routes`
- `GET /api/v1/stops/:stationId/forecast`
- `GET /api/v1/vehicles?routeId=...`
- `GET /api/v1/vehicles/:deviceCode/forecast`
- `GET /api/v1/bus-station/destinations/search?q=...`
- `GET /api/v1/bus-station/races?destinationId=...&date=dd.mm.yyyy`

For richer API details, read `references/api.md`.

## Localization

When adding a button, label, error, or status message:

1. Add a key to the Russian dictionary.
2. Add verified translations where available.
3. Add a fallback in `t()` only when missing translations are expected.
4. Add the key to VK translation export if VK uses it.
5. Build and spot-check at least Russian plus one non-Russian locale.

## Deployment

Use the main repository's established deployment flow. Never print secrets in final answers.

Typical verification:

```bash
pnpm run build
```

For production restart, use the configured server access from the local environment, then verify `systemctl is-active transport12` returns `active`.
