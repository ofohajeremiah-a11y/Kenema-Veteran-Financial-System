# Kenema Veteran Financial Management System

A Node.js web application for managing members, monthly contributions, expenditures, user roles and financial summaries.

## Deployment notes

This version is prepared for Render with a **persistent disk**. The disk is important because the application stores its records in a JSON database file. The included `render.yaml` mounts a 1 GB persistent disk at `/var/data` and configures the app to store its database there.

**Important:** Render persistent disks require a paid web-service plan. Do not deploy this version on a free service if you intend to retain financial records. Without persistent storage, records may be lost during a restart or redeployment. This JSON-file design is suitable for a small, single-instance deployment; for larger or multi-instance production use, migrate to PostgreSQL.

## Deploy with Render Blueprint

1. Upload this project to a new GitHub repository. Do not upload `.env`, `.vscode`, or the local `data` folder.
2. In Render, choose **New + → Blueprint** and connect the GitHub repository.
3. Render reads `render.yaml`. It creates a Starter web service and a persistent disk.
4. When prompted for `ADMIN_PASSWORD`, enter a unique password of at least 12 characters. Store it safely; do not commit it to GitHub.
5. Deploy. Wait for the service to become **Live**.
6. Open the Render URL. Sign in with username `admin` and the `ADMIN_PASSWORD` value you supplied.
7. Immediately create a second administrator account from User Accounts, sign in as that account, and remove/retire the initial account if desired.

## Local development

Requires Node.js 20 or newer.

```bash
npm install
npm run check
npm start
```

Open http://localhost:3000. Local default account is `admin` / `admin123`; change it after signing in. This local default is not used on Render because production requires `ADMIN_PASSWORD`.

## Data and backups

The database is stored at `${DATA_DIR}/db.json` (defaults to `./data/db.json` locally). Back up the persistent disk data regularly. A persistent disk protects against ordinary deploy/restart filesystem resets, but it is not a substitute for independent backups.

## Security reminders

- Never commit passwords, API keys, `.env` files, or database contents.
- Use a unique strong production administrator password.
- Limit access to trusted association administrators and staff.
- Do not treat this lightweight JSON-backed app as a high-assurance accounting or banking platform. Verify totals and maintain independent backups.
