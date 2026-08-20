<!-- markdownlint-disable -->

# Hardening Report: r0adkll--upload-google-play/v1.1.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **r0adkll--upload-google-play/v1.1.4** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in both workflow files use mutable tags or version strings instead of full 40-character SHA commit digests, making the workflows vulnerable to supply-chain attacks if the referenced action tags are moved or compromised.

In `.github/workflows/pr-validation.yml`:
- Line 18: `uses: actions/checkout@v6`
- Line 21: `uses: actions/setup-node@v6`
- Line 34: `uses: tj-actions/verify-changed-files@v20`

In `.github/workflows/release.yml`:
- Line 9: `uses: actions/checkout@v6`
- Line 11: `uses: rickstaa/action-create-tag@v1`

All should be pinned to full SHA digests, e.g. `actions/checkout@<40-char-sha> # v6`.

Locations:

- `.github/workflows/pr-validation.yml:18`
- `.github/workflows/pr-validation.yml:21`
- `.github/workflows/pr-validation.yml:34`
- `.github/workflows/release.yml:9`
- `.github/workflows/release.yml:11`

### missing-permissions (severity: medium)

Neither `.github/workflows/pr-validation.yml` nor `.github/workflows/release.yml` declares a top-level `permissions:` key, and neither of their jobs declares job-level `permissions:`. Without explicit permissions, workflows run with the default (often broad) token permissions, violating the principle of least privilege. Each workflow should declare the minimal set of permissions required (e.g. `permissions: contents: read`).

Locations:

- `.github/workflows/pr-validation.yml:1`
- `.github/workflows/release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 5 unpinned `uses:` references by pinning them to full 40-character SHA digests (with original tags preserved as comments). Added top-level `permissions:` blocks to both workflow files: `contents: read` for pr-validation.yml (read-only operations) and `contents: write` for release.yml (needs to create/push tags).

