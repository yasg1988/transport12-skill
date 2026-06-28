# Deployment

Use this reference when deploying the main transport12 service.

## Rules

- Do not print secrets in final answers.
- Do not commit real server addresses, bot tokens, database passwords, SSH private keys, or production domains unless the user explicitly asks for public documentation.
- Always build before restart.
- Verify the service manager reports the service as active after restart.

## Typical Flow

1. Commit and push code.
2. Pull the repository on the server.
3. Run the TypeScript build.
4. Restart the service.
5. Check service status.

Example shape:

```bash
cd /opt/transport12
git pull --ff-only
pnpm run build
systemctl restart transport12
systemctl is-active transport12
```

Use the actual SSH command only from the local secure environment.
