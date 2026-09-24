# publish-action

A GitHub Action that publishes packages to [pkg.vc](https://pkg.vc) and automatically manages a single PR comment with installation instructions for all published packages.

## Features

- 📦 Publish packages by calling the action multiple times
- 💬 Automatically creates and updates a single PR comment listing all packages
- 📝 On push and other non-PR workflows, writes a job summary with the commit install URL
- 🚀 Provides multiple installation options (commit, branch, PR number)

## Usage

Call the action once for each package you want to publish. Use `@2` to track the latest v2 release, or pin `@2.0.0` for an exact version.

v2 requires the Node 24 action runtime (self-hosted runners **v2.327.1** or newer; macOS 13.4 and older and ARM32 self-hosted runners are not supported). `1.0.19` and earlier run on Node 20, which GitHub removed from Actions runners on 2026-09-23.

```yaml
name: Publish to pkg.vc
on:
  pull_request:
    types: [opened, synchronize]

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      
      - name: Publish core package
        uses: pkg-vc/publish-action@2
        with:
          directory: "packages/core"
          organization: "your-org"
          secret: ${{ secrets.PKG_VC_SECRET }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
          
      - name: Publish utils package
        uses: pkg-vc/publish-action@2
        with:
          directory: "packages/utils"
          organization: "your-org"
          secret: ${{ secrets.PKG_VC_SECRET }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
          
      - name: Publish UI package
        uses: pkg-vc/publish-action@2
        with:
          directory: "packages/ui"
          organization: "your-org"
          secret: ${{ secrets.PKG_VC_SECRET }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

## Inputs

| Input | Description | Required |
|-------|-------------|----------|
| `directory` | Path to your module | Yes |
| `organization` | Organization name on pkg.vc | Yes |
| `secret` | Secret key for pkg.vc | Yes |
| `github-token` | GitHub token for commenting on PRs | Yes |

## Outputs

| Output | Description |
|--------|-------------|
| `url_commit` | URL of the published module for commit |
| `url_branch` | URL of the published module for branch |
| `url_pr` | URL of the published module for PR |
| `command` | Command to install the published module |
