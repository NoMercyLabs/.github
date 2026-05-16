# NoMercyLabs — org-level community health files

This repo provides the `.github/` defaults applied across every repository in the
[NoMercyLabs](https://github.com/NoMercyLabs) organization — workflow templates,
issue templates, contributor guides, and shared maintenance jobs.

## Reusable workflows

| Workflow | What it does |
|---|---|
| [`reusable-cleanup-runners.yml`](.github/workflows/reusable-cleanup-runners.yml) | Removes offline self-hosted runners registered to the org. |
| [`reusable-cleanup-runs.yml`](.github/workflows/reusable-cleanup-runs.yml) | Sweeps old workflow runs across every repo: cancelled/skipped after 1 day, failed after 7 days, keeps the last successful run per workflow. |

Call them from any repo's workflow:

```yaml
jobs:
  cleanup:
    uses: NoMercyLabs/.github/.github/workflows/reusable-cleanup-runs.yml@master
    secrets: inherit
```

## Scheduled maintenance

[`daily-maintenance.yml`](.github/workflows/daily-maintenance.yml) runs at 04:00 UTC
daily and fans out to both reusable workflows above. Disable individual jobs by
editing that file.

## Secrets

Both reusable workflows expect an org-level `PAT` secret with `admin:org` and `repo`
scopes so they can enumerate runners and delete workflow runs across the org.
