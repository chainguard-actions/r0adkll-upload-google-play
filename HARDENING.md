<!-- markdownlint-disable -->

# Hardening Report: r0adkll--upload-google-play/v1.1.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **r0adkll--upload-google-play/v1.1.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference GitHub Actions using mutable tags or version strings instead of pinned full 40-character SHA commit hashes. This exposes the workflow to supply-chain attacks if the referenced tag is moved or the repository is compromised.

Failing references:
- `.github/workflows/pr-validation.yml`: `actions/checkout@v3`, `tj-actions/verify-changed-files@v9.2`
- `.github/workflows/release.yml`: `actions/checkout@v2.5.0`, `rickstaa/action-create-tag@v1`

All should be replaced with their corresponding full SHA digests (e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`).

Locations:

- `.github/workflows/pr-validation.yml:18`
- `.github/workflows/pr-validation.yml:28`
- `.github/workflows/release.yml:8`
- `.github/workflows/release.yml:10`

### missing-permissions (severity: medium)

Neither `.github/workflows/pr-validation.yml` nor `.github/workflows/release.yml` declares a top-level `permissions:` block, and no individual job within either file declares its own `permissions:` block. Without explicit permissions, workflows run with the default (often broad) token permissions, violating the principle of least privilege. Each workflow should declare minimal required permissions (e.g. `contents: read`) at the top level or per job.

Locations:

- `.github/workflows/pr-validation.yml:1`
- `.github/workflows/release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files:

**pr-validation.yml**:
- Added `permissions: contents: read` top-level block
- Pinned `actions/checkout@v3` → `actions/checkout@a37ce9120846195fa4ece8f58b268e6043cb2f26 # v3`
- Pinned `tj-actions/verify-changed-files@v9.2` → `tj-actions/verify-changed-files@6f40ee1d523d9a9223204ae06919a3b2739702dc # v9.2`

**release.yml**:
- Added `permissions: contents: write` top-level block (write needed to create/push tags)
- Pinned `actions/checkout@v2.5.0` → `actions/checkout@e2f20e631ae6d7dd3b768f56a5d2af784dd54791 # v2.5.0`
- Pinned `rickstaa/action-create-tag@v1` → `rickstaa/action-create-tag@a1c7777fcb2fee4f19b0f283ba888afa11678b72 # v1`

