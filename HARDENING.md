<!-- markdownlint-disable -->

# Hardening Report: r0adkll--upload-google-play/v1.1.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **r0adkll--upload-google-play/v1.1.5** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference external actions using mutable tags or version strings instead of pinned full 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced tag is moved or overwritten. Failing references in pr-validation.yml: `actions/checkout@v6`, `actions/setup-node@v6`, `tj-actions/verify-changed-files@v20`. Failing references in release.yml: `actions/checkout@v6`, `rickstaa/action-create-tag@v1`.

Locations:

- `.github/workflows/pr-validation.yml:18`
- `.github/workflows/pr-validation.yml:21`
- `.github/workflows/pr-validation.yml:30`
- `.github/workflows/release.yml:9`
- `.github/workflows/release.yml:11`

### missing-permissions (severity: medium)

Neither workflow file defines a top-level `permissions:` block, and neither job within them defines a job-level `permissions:` block. Without explicit permissions, workflows run with the default (potentially broad) token permissions, violating the principle of least privilege. Both `pr-validation.yml` and `release.yml` are affected.

Locations:

- `.github/workflows/pr-validation.yml:1`
- `.github/workflows/release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files:

pr-validation.yml:
- Added `permissions: contents: read` top-level block
- Pinned actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6
- Pinned actions/setup-node@v6 → @249970729cb0ef3589644e2896645e5dc5ba9c38 # v6
- Pinned tj-actions/verify-changed-files@v20 → @a1c6acee9df209257a246f2cc6ae8cb6581c1edf # v20

release.yml:
- Added `permissions: contents: write` top-level block (write needed to push/force-push tags)
- Pinned actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6
- Pinned rickstaa/action-create-tag@v1 → @a1c7777fcb2fee4f19b0f283ba888afa11678b72 # v1

All SHAs were resolved via lookup_action_sha and are real commit SHAs.

