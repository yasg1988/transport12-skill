# Localization

Use this reference for user-facing text in the main transport12 service.

Localization is a main-service concern. MCP tools should return data, not localized bot-style answers.

## Adding Text

1. Add a stable key to the Russian dictionary in `src/i18n/index.ts`.
2. Use the key in Telegram, VK Mini App, or server-rendered UI.
3. Add verified translations where available.
4. If a translation is uncertain, prefer a fallback over an invented term.
5. If VK needs the key, add it to `vkI18nKeys` in `src/web/vkapp.ts`.
6. Run `pnpm run build`.

## Fallbacks

Use fallbacks for stable technical labels and known missing translations. Do not hide missing product text by silently inventing translations.

## Out Of Scope For MCP

- language selection;
- localized answer generation;
- Telegram/VK menu text;
- favorite labels and per-user UI state.
