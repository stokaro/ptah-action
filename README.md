# Ptah Action

Run Ptah migration planning, safety checks, lint, sticky pull request comments,
and a destructive-change Check Run from GitHub Actions.

```yaml
name: Ptah

on:
  pull_request:

permissions:
  checks: write
  contents: read
  issues: write
  pull-requests: read

jobs:
  ptah:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7

      - uses: stokaro/ptah-action@v1
        with:
          dir: ./internal/models
          db-url: ${{ secrets.PTAH_DATABASE_URL }}
          dialect: postgres
          migration-dir: ./migrations
```

## Inputs

| Input | Default | Description |
| --- | --- | --- |
| `version` | `latest` | Ptah release tag to download. |
| `binary-path` | empty | Existing Ptah binary path. Skips release download. |
| `setup-go` | `true` | Set up the Go toolchain before running Ptah. |
| `go-version` | `1.26.5` | Go version passed to `actions/setup-go`. |
| `dir` | `.` | Root directory scanned for Go schema entities. |
| `db-url` | required | Target database URL used to read the current schema. |
| `dialect` | empty | Dialect passed to `ptah migrations lint`. |
| `migration-dir` | `migrations` | Migration directory passed to lint. |
| `schemas` | empty | Comma-separated database schemas to inspect. |
| `comment` | `true` | Whether to write a sticky PR comment. |
| `lint` | `true` | Whether to run `ptah migrations lint`. |
| `lint-fail-on` | `error` | Lint failure threshold: `error`, `any`, or `none`. |
| `allow-destructive` | `false` | Allows destructive plans after review. |
| `output-dir` | temporary | Directory for generated reports. |

## Outputs

| Output | Description |
| --- | --- |
| `plan-path` | Text migration plan report. |
| `safety-path` | JSON safety report. |
| `lint-path` | JSON lint report. |
| `destructive` | `true`, `false`, or `unknown`. |

## Behavior

The action downloads the requested Ptah release binary by default. If a release
asset is not available yet, it falls back to:

```bash
go install github.com/stokaro/ptah/cmd/ptah@master
```

when `version` is `latest`. Use `binary-path` when a workflow builds Ptah from
source before invoking the action.

The action runs:

```bash
ptah migrations plan --report text
ptah migrations plan --report json --check-destructive
ptah migrations lint --format json
```

The text plan is generated without `--check-destructive` so the pull request
comment still contains SQL for review. The separate JSON safety command drives
the destructive-change failure gate and Check Run.

## Provenance

This repository packages the composite action source maintained in
[`stokaro/ptah`](https://github.com/stokaro/ptah) under
`.github/actions/ptah`.
