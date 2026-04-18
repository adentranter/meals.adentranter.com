# Mealie deploy repo for Dokploy / Launchpad

This is a thin deploy repo for running **Mealie** in Dokploy using Docker Compose.

## What this repo is for

This repo is meant to be:

- pushed to GitHub / Gitea / Git
- connected to Dokploy as a **Compose** app
- exposed on its own subdomain, for example:
  - `mealie.adentranter.com`

It is **not** meant to be hosted at a subpath like:

- `launchpad.adentranter.com/mealie`

## Files

- `docker-compose.yml` — the Compose stack Dokploy will deploy
- `.env.example` — example variables
- `.gitignore` — ignores local secrets and junk

## Suggested domain

Use a dedicated subdomain:

- `mealie.adentranter.com`

Point that DNS record at the server that runs Dokploy.

## Dokploy setup

1. Create a new **Compose** application in Dokploy.
2. Connect this repo from GitHub / Gitea / Git.
3. Set the compose path to:

```text
./docker-compose.yml
```

4. Add your domain in the **Domains** tab:

```text
mealie.adentranter.com
```

5. Add environment variables in Dokploy matching the names in `.env.example`.
6. Deploy.

## Important note about environment variables in Dokploy

Dokploy writes variables to a `.env` file, but they only get used if the compose file references them as `${VAR}`.

This repo already does that.

## Minimum variables to set

At minimum, set these:

```env
BASE_URL=https://mealie.adentranter.com
DEFAULT_EMAIL=you@adentranter.com
```

You can usually leave the rest as-is for a first deployment.

## Network assumption

This compose file expects Dokploy's shared network to already exist as:

```text
dokploy-network
```

That is the normal pattern for Dokploy-managed compose apps.

## Storage

This uses a named Docker volume:

```text
mealie-data
```

That keeps your Mealie data persistent across restarts and redeploys.

## Image version

The image is pinned through:

```env
MEALIE_VERSION=v3.16.0
```

You can bump that later by editing the env value and redeploying.

## If you want Postgres later

This repo is intentionally the simple SQLite version.
That is the easiest first deployment.

If you later want Postgres, add a `postgres` service or point Mealie at a managed Postgres instance.
# meals.adentranter.com
