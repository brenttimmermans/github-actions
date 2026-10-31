# github-actions

Shared GitHub Actions workflows.

## Cloudflare CI

Lints, typechecks, tests, builds and deploys a site to Cloudflare Workers. Deploys only from `main`.

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main]
  pull_request:
  workflow_dispatch:

jobs:
  ci:
    uses: brenttimmermans/github-actions/.github/workflows/cloudflare-ci.yml@v1
    secrets: inherit
```

The repo needs:

- `.node-version`
- `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` secrets
- With `package.json`: npm, plus `lint` and `build` scripts. `typecheck` and `test` run when present.

Optional inputs (`build-env`, `cache-path`, `cache-files`) are described in the workflow file.
