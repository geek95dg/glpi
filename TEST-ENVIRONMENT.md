# GLPI 11.0.4 plugin test environment

A reproducible **GLPI 11.0.4** test environment for the `offboarding`
plugin lives in the companion repository, not here:

> **geek95dg/offboard → [`test-env/`](https://github.com/geek95dg/offboard/tree/claude/glpi-test-environment-1p4ty3/test-env)**
> (`cd test-env && ./setup.sh`)

## How this repository is used by that environment

This repo's working tree tracks the **`11.0/bugfixes`** branch (currently
`11.0.6-dev`). The test environment needs *exactly* GLPI **11.0.4**, so it
does **not** run this working tree. Instead `setup.sh` pins the released
version in a separate, detached git **worktree**:

```bash
git fetch --depth 1 origin tag 11.0.4
git worktree add --detach ../glpi-1104 11.0.4      # GLPI_VERSION = 11.0.4
```

That worktree is then built (composer deps, compiled `.mo` locales,
front-end assets) and served natively by PHP while MariaDB runs in Docker,
with the plugin symlinked in. This branch is left untouched by the process —
this file is the only change, documenting the relationship so the pinned
`11.0.4` tag isn't mistaken for a regression against `11.0.6-dev`.

See the offboard repo's `test-env/README.md` for the full design, the
sandbox constraints it works around, and usage.
