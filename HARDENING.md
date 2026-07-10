<!-- markdownlint-disable -->

# Hardening Report: azure--docker-login/v2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **azure--docker-login/v2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow steps use mutable tag references instead of pinned full SHA commit digests, making the workflow vulnerable to supply-chain attacks if the tag is moved. Failing references: 'actions/stale@v9' (lines 11 and 22) and 'actions/checkout@v4' (line 15).

Locations:

- `.github/workflows/defaultLabels.yml:11`
- `.github/workflows/defaultLabels.yml:22`
- `.github/workflows/unit-tests.yml:15`

### missing-permissions (severity: medium)

Neither workflow file has a top-level 'permissions:' key, and no job in either file defines its own 'permissions:' block. Without explicit permissions, workflows run with the default (potentially broad) token permissions. Both 'defaultLabels.yml' and 'unit-tests.yml' are affected.

Locations:

- `.github/workflows/defaultLabels.yml:1`
- `.github/workflows/unit-tests.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files: (1) Pinned actions/stale@v9 to SHA 5bef64f19d7facfb25b37b414482c7164d639639 in both steps of defaultLabels.yml, and actions/checkout@v4 to SHA 34e114876b0b11c390a56381ad16ebd13914f8d5 in unit-tests.yml — original tags preserved as comments. (2) Added top-level permissions blocks: defaultLabels.yml gets 'issues: write' and 'pull-requests: write' (minimum needed by the stale action); unit-tests.yml gets 'contents: read' (minimum needed by checkout).

