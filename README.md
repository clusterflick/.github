# .github

Org-level configuration and reusable workflows for the `clusterflick` org.

## Reusable workflows

### `zizmor` — GitHub Actions security audit

[`.github/workflows/zizmor.yml`](.github/workflows/zizmor.yml) runs
[zizmor](https://docs.zizmor.sh) against a repository's workflows to catch
common GitHub Actions security issues (template injection, dangerous triggers,
excessive `permissions`, credential persistence, unpinned actions, …).

It fails the job — and therefore the PR check — on **medium or higher** findings
(via `min-severity: medium`) and annotates them inline on the diff. Low /
informational advisories still appear in the run logs but don't block.

**Add it to a repo** by creating `.github/workflows/zizmor.yml`:

```yaml
name: zizmor

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  workflow_dispatch:

permissions: {}

jobs:
  zizmor:
    name: Audit workflows
    uses: clusterflick/.github/.github/workflows/zizmor.yml@main
    permissions:
      contents: read
```

**Inputs:**

| Input     | Default   | Description                                            |
| --------- | --------- | ------------------------------------------------------ |
| `persona` | `regular` | zizmor persona: `regular`, `pedantic`, or `auditor`.   |

**Policy:** the workflow applies an org-wide zizmor policy (written inline in
the reusable workflow and passed via `--config`) that sets `unpinned-uses` to
`ref-pin` — actions may be pinned to a tag/branch (e.g. `@v6`) rather than a
commit hash. This also permits moving refs like `@latest`, so pin those by hand
where you can. To enforce hashes for a specific source, add a more specific
policy entry (e.g. `chromaui/*: hash-pin`).

**Make it a required check:** in each repo's branch protection / ruleset for
`main`, mark the `Audit workflows` check as required so PRs can't merge while
zizmor reports findings.

**SARIF / Security tab instead of failing the PR:** if you'd rather have
results land in the GitHub Security tab (code scanning) than fail the job,
flip `advanced-security` to `true` in the reusable workflow, remove
`annotations`, and add `security-events: write` to the job permissions. In that
mode the action does not fail on findings, so gate merges with a ruleset that
requires the code-scanning result.
