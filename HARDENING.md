<!-- markdownlint-disable -->

# Hardening Report: r0adkll--upload-google-play/v1.1.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **r0adkll--upload-google-play/v1.1.3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow files reference actions by mutable tags instead of full 40-character commit SHAs, making them vulnerable to supply-chain attacks if the tag is moved.

- `.github/workflows/pr-validation.yml`: `actions/checkout@v3` (tag), `tj-actions/verify-changed-files@v17` (tag)
- `.github/workflows/release.yml`: `actions/checkout@v2.5.0` (version tag), `rickstaa/action-create-tag@v1` (tag)

All should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/pr-validation.yml:17`
- `.github/workflows/pr-validation.yml:25`
- `.github/workflows/release.yml:9`
- `.github/workflows/release.yml:11`

### missing-permissions (severity: medium)

Neither `.github/workflows/pr-validation.yml` nor `.github/workflows/release.yml` declares a top-level `permissions:` block, and no job in either file has a job-level `permissions:` block. Without explicit permissions, workflows run with the default (potentially broad) repository permissions. A top-level `permissions: {}` or minimal scoped permissions should be added to each workflow.

Locations:

- `.github/workflows/pr-validation.yml:1`
- `.github/workflows/release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files:

**pr-validation.yml**:
- Added top-level `permissions: {}` block
- Pinned `actions/checkout@v3` → `actions/checkout@a37ce9120846195fa4ece8f58b268e6043cb2f26 # v3`
- Pinned `tj-actions/verify-changed-files@v17` → `tj-actions/verify-changed-files@2acec78834cc690f70b3445712363fc314224127 # v17`

**release.yml**:
- Added top-level `permissions: {}` block
- Added job-level `permissions: contents: write` (needed for creating/pushing tags)
- Pinned `actions/checkout@v2.5.0` → `actions/checkout@e2f20e631ae6d7dd3b768f56a5d2af784dd54791 # v2.5.0`
- Pinned `rickstaa/action-create-tag@v1` → `rickstaa/action-create-tag@a1c7777fcb2fee4f19b0f283ba888afa11678b72 # v1`

