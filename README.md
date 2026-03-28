# Nexus Architecture Check

> GitHub Action CI quality gate — automated architecture analysis on every PR.

[![Nexus](https://img.shields.io/badge/powered%20by-Nexus-purple)](https://github.com/camilooscargbaptista/nexus)

## Usage

```yaml
name: Nexus Architecture Check

on:
  pull_request:
    branches: [main, develop]

permissions:
  contents: read
  pull-requests: write

jobs:
  nexus-review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: camilooscargbaptista/nexus-action@v1
        with:
          threshold: 70
          fail-on-critical: true
          comment-on-pr: true
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `threshold` | Minimum architecture score to pass (0-100) | `70` |
| `fail-on-critical` | Fail build on critical findings | `true` |
| `comment-on-pr` | Post analysis summary as PR comment | `true` |
| `working-directory` | Directory to analyze | `.` |

## Outputs

| Output | Description |
|--------|-------------|
| `score` | Architecture score (0-100) |
| `findings-count` | Total findings |
| `critical-count` | Critical findings |
| `passed` | Whether quality gate passed |

## What It Does

1. Installs `@nexus/cli` (or builds from local monorepo)
2. Runs `nexus analyze` on the workspace
3. Posts a formatted PR comment with score bar, findings, and status
4. Fails the build if score is below threshold or critical findings exist

## PR Comment Example

```
## ✅ Nexus Architecture Review — PASSED

**Score: 82/100** | 3 finding(s) | 0 critical

`████████████████░░░░` 82%
```

## License

MIT — [Girardelli Tecnologia](https://girardellitecnologia.com)
