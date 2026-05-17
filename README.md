# microservice2 Setup Guide

`microservice2` is a Laravel API with its own PostgreSQL container. It is served through Nginx on port `9005`.

## Prerequisites

- Docker Desktop
- Docker Compose

## Docker Setup

1. Copy the Laravel environment file:

   ```powershell
   Copy-Item .env.example .env
   ```

   On macOS, Linux, Git Bash, or WSL:

   ```bash
   cp .env.example .env
   ```

2. Update `.env` for Docker:

   ```env
   DB_CONNECTION=pgsql
   DB_HOST=db
   DB_PORT=5432
   DB_DATABASE=microservice2
   DB_USERNAME=postgres
   DB_PASSWORD=postgres
   ```

3. Build and start the stack:

   ```bash
   docker compose up -d --build
   ```

4. Generate the app key and run migrations:

   ```bash
   docker compose exec app php artisan key:generate
   docker compose exec app php artisan migrate --seed
   ```

Open:

```text
http://localhost:9005
```

PostgreSQL is exposed to your machine as `localhost:5447`.

## Useful Commands

```bash
docker compose exec app php artisan test
docker compose exec app php artisan migrate:fresh --seed
docker compose down
```

To remove the database volume too:

```bash
docker compose down -v
```

