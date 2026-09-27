# emsui-agent

Public build mirror for the private Forgejo repo `Delnegend/emsui-agent` -
workflows only, no source.

## Workflows

| Workflow | Trigger | Does |
|---|---|---|
| `ci` | `workflow_dispatch` from Forgejo | Checks the Forgejo source out and runs `just check` |
| `release` | `workflow_dispatch` from Forgejo | Builds release binaries + container image, publishes to GitHub Releases and GHCR |
| `cleanup` | Daily schedule | Deletes old workflow runs (retains 7 days, min 5 runs) |

Assumption: this repo only ever builds `main` (single-branch flow). `ci`'s
concurrency group is the static key `ci-main` - if multi-branch builds are
ever added, the group must become per-branch or runs will wrongly cancel and
serialize each other.
