# Running CI for this repo

Automatic workflow triggers in this repository are **gated**: pushing does not
start a GitHub-hosted run any more. Checks run on local hardware, and the
workflows that remain are started deliberately.

Why: GitHub Actions was costing the org $563/month, almost all of it hosted
compute for checks that run just as well on hardware we already own.

Starting a gated workflow needs the [`gh` CLI](https://cli.github.com) and push
access. `--ref` matters - the workflow file is read from that branch, so a
workflow that only exists on your feature branch must be dispatched against it.

Full cross-repo runbook: `CI-Local-CICD/RUNBOOK.md` (regenerate with
`ci-local docs`). This file is generated - do not hand-edit.

---

Default branch: `master`

### Test locally

```bash
ci-local run --repo systeminformation
```

Equivalent to:

```bash
npm ci
npm run --silent test
```

### Run a check workflow on GitHub

**CodeQL** — `codeql.yml`

```bash
gh workflow run codeql.yml --repo companionintelligence/systeminformation --ref master
```

**Test** — `test.yml`

```bash
gh workflow run test.yml --repo companionintelligence/systeminformation --ref master
```

### Cut a release

**Release** — `release.yml`

```bash
gh workflow run release.yml --repo companionintelligence/systeminformation --ref master
```
