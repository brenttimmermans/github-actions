# github-actions

Shared GitHub Actions workflows for my sites.

## Cloudflare deploy

Verifies, builds and deploys a site to Cloudflare Workers. Add this as `.github/workflows/deploy.yml`:

```yaml
name: Deploy

on:
  push:
    branches: [main]
  pull_request:
  workflow_dispatch:

jobs:
  deploy:
    uses: brenttimmermans/github-actions/.github/workflows/cloudflare-deploy.yml@v1
    secrets: inherit
```

What the repo needs:

- `.node-version`
- `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` repository secrets
- With a `package.json`: npm (`package-lock.json`) and `lint` and `build` scripts. `typecheck` and `test` run when present.
- Without a `package.json`: nothing else, the repo is deployed as-is.

Pull requests run every step except the deploy, which only runs on the default branch. A newer run cancels an older one on the same branch.

### Inputs

| Input | Use |
|---|---|
| `build-env` | Extra build variables, one `KEY=value` per line, e.g. `PUBLIC_KEY=${{ vars.PUBLIC_KEY }}`. Not for secrets. |
| `cache-path` | Build output to cache between runs. |
| `cache-key-files` | Space-separated paths whose change discards the cache. |
| `cache-content-files` | Space-separated paths whose change rebuilds on top of the previous cache. |
| `wrangler-version` | Wrangler version for repos without it as a dependency. |

## Releasing

Callers pin `@v1`. After merging a change, move the tag:

```sh
git tag -f v1 && git push -f origin v1
```
