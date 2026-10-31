# github-actions

Shared GitHub Actions workflows.

## Cloudflare deploy

Lints, typechecks, tests, builds and deploys a site to Cloudflare Workers. Deploys only from the default branch.

```yaml
# .github/workflows/deploy.yml
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

The repo needs:

- `.node-version`
- `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` secrets
- With `package.json`: npm, plus `lint` and `build` scripts. `typecheck` and `test` run when present.

Optional inputs (`build-env`, `cache-*`, `wrangler-version`) are described in the workflow file.
