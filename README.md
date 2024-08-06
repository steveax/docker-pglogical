# Postgres/PGLogical Image

A ready-made, batteries-included Docker image combining Postgres 14 with pglogical.

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
