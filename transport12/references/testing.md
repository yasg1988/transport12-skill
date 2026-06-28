# Testing

Use this reference before committing transport12 changes.

## Main transport12

```bash
pnpm run build
```

For API changes, run targeted local or deployed endpoint checks with non-secret environment values.

## transport12-mcp

```bash
pnpm run build
```

When a reachable API base URL is available:

```bash
TRANSPORT12_API_BASE_URL=https://your-transport12-api.example pnpm run smoke
```

Do not commit the actual production URL unless the user explicitly decides it is public documentation.

## transport12-skill

```bash
python C:\Users\YAkunin\.codex\skills\.system\skill-creator\scripts\quick_validate.py D:\transport\transport12-skill\transport12
```

## Public-Safety Search

Before publishing docs or companion repo changes, search for forbidden internal references, real domains, and secrets:

```bash
rg -n "transport12\.yasg\.ru|token|password|пароль|closed internal" README.md .env.example transport12 src scripts docs
```

Adjust the path list for the current repository.
