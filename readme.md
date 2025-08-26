# MySQL in Docker Compose
<!-- Polished README for the MysqlDocker project -->
# MySQL with Docker Compose

A minimal Docker Compose setup for running MySQL locally with persistent storage and an optional phpMyAdmin web UI.

## Overview

- Services:
  - `db` — MySQL server (image configurable via `MYSQL_VERSION`, default: `5.7`).
  - `phpmyadmin` — phpMyAdmin web UI (optional) for database management.

This repository is intended for development, testing, and learning. It's not configured for production use.

## Default environment variables

These defaults are defined in `docker-compose.yml`. Override them via a `.env` file or environment variables.

- `MYSQL_DATABASE` — db
- `MYSQL_USER` — dbuser
- `MYSQL_PASSWORD` — iamPassword
- `MYSQL_ROOT_PASSWORD` — 1234

## Persistent data & configuration

- `./data` is mounted to `/var/lib/mysql` inside the container to persist database files across restarts.
- `./config/my.cnf` is mounted into `/etc/mysql/conf.d/my.cnf` to provide custom MySQL configuration.

Ensure those directories/files exist and that Docker has permission to read/write them.

## Quick start (PowerShell)

Open PowerShell in the project root and run:

```powershell
# Start containers in the background
docker compose up -d

# Stream logs from the database service
docker compose logs -f db

# Stop and remove containers
docker compose down

# Stop and remove containers and volumes (deletes database files)
docker compose down -v
```

If your environment still uses the legacy command, use `docker-compose` instead of `docker compose`.

## Access

- MySQL: localhost:3306
- phpMyAdmin: http://localhost:8080

phpMyAdmin is configured to connect to the `db` service. Use `MYSQL_USER`/`MYSQL_PASSWORD` or `root` with `MYSQL_ROOT_PASSWORD` to log in.

## Troubleshooting

- Container won't start: check logs with `docker compose logs db` and look for permission or configuration errors.
- Permission problems on Windows: ensure Docker Desktop has file sharing access to the repository folder and that antivirus or indexing services aren't locking files.
- Reinitialize data: removing `./data` will reset the database (this deletes all data).

## Files of interest

- `docker-compose.yml` — Compose file describing services and mounts.
- `config/my.cnf` — Custom MySQL configuration applied at container startup.

## Next steps (optional)

- Add a `.env.example` file to document environment variables.
- Add a healthcheck or simple startup script to wait for MySQL readiness.
- Harden passwords and avoid exposing ports for production.

---

If you'd like, I can add a `.env.example` file to this repo or include a short PowerShell script that waits for MySQL to be ready before running migrations—tell me which you prefer.
