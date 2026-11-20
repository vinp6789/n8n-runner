# n8n-runner

<p align="left">
  <img src="https://img.shields.io/badge/n8n-self--hosted-EA4B71?logo=n8n&logoColor=white" alt="n8n"/>
  <img src="https://img.shields.io/badge/Node.js-runtime-339933?logo=nodedotjs&logoColor=white" alt="Node.js"/>
</p>

A minimal deployable wrapper for a **self-hosted n8n** instance: one `package.json`
that installs n8n, so any Node.js platform (a VPS, Docker or a PaaS such as
Railway) can build and run it with no extra code.

I use n8n as the scheduler and glue for my other services. It triggers pipeline
stages in [aegis-final](https://github.com/vinp6789/aegis-final) and scheduled runs in
[qalert_test](https://github.com/vinp6789/qalert_test), and sends alerts to Telegram.

## Run

```bash
npm install
npx n8n start          # UI on http://localhost:5678
```

## Recommended production settings

Set these as environment variables on the host. Never commit them.

| Variable | Why |
|---|---|
| `N8N_ENCRYPTION_KEY` | Encrypts stored credentials. Keep it stable across restarts. |
| `N8N_BASIC_AUTH_ACTIVE` / user management | Keeps the editor from being exposed publicly without a login |
| `DB_TYPE=postgresdb` + `DB_POSTGRESDB_*` | Durable storage instead of local SQLite |
| `WEBHOOK_URL` | Correct public URL for webhook triggers |
| `GENERIC_TIMEZONE=Asia/Kolkata` | Schedules fire in local time |

> **Tip:** pin the n8n version in `package.json` (instead of `"*"`) so builds are reproducible and upgrades are deliberate.
