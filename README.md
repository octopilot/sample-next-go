# sample-next-go

**One repo: Next.js frontend + Go API.** Use this if your stack is Next.js + Go.

## What's in this repo

| Part       | Stack        | Build     |
|------------|--------------|-----------|
| **frontend** | Next.js 14   | Dockerfile |
| **api**      | Go (Gin)     | buildpacks |

## Prerequisites

- **Docker**

## Build

**With [OctoPilot pipeline tools](https://github.com/octopilot/octopilot-pipeline-tools) (`op`)** — recommended for local/Mac:

```bash
docker run -d -p 5001:5000 --restart=unless-stopped --name registry registry:2  # once
op build-push
```

Or with Skaffold: `skaffold build`. For CI, use `op build-push --repo <registry>` or `op build`.

## Run

```bash
# Terminal 1 — API
docker run -p 8081:8080 sample-next-go-api

# Terminal 2 — Frontend (default API URL is http://localhost:8081)
docker run -p 8080:8080 sample-next-go-frontend
```

Set **API URL** in the form to `http://localhost:8081` if needed. Open **http://localhost:8080**.

## Deploy

`skaffold build --file-output build.json` or `op push` (set `--default-repo` or use a `.registry` file) → use the image refs with your GitOps tool.
