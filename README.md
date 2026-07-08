# Postgres/PGLogical Image

A ready-made, batteries-included Docker image combining Postgres 17 with pglogical.

## Requirements

* Docker
* docker compose

## Instructions

Just run `docker compose up -d` in this directory to get a postgres server running on the default port (5432).
Feel free to edit the port number in `docker compose.yml`.

Depending on your setup, you may find it helpful to set some postgres-related environment variables like so:

```
export PGHOST=localhost
export PGPORT=5432
export PGUSER=postgres
```

With the above variables, you should be able to simply run `psql` to connect to the containerized postgres instance.

## Switching Postgres versions

The base `postgres` image declares an implicit data volume (`/var/lib/postgresql/data`). Even though this
project's `docker-compose.yml` doesn't mount it explicitly, Docker persists it as an anonymous volume across
rebuilds. If you bump the Postgres major version (e.g. 14 -> 17), the old data directory will still be
attached and the new server will refuse to start with:

```
FATAL:  database files are incompatible with server
```

Fix by removing the volume along with the container before bringing it back up:

```
docker compose down -v
docker compose up -d --build
```
