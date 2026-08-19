<!-- markdownlint-disable -->

# Hardening Report: denoland--setup-deno/v2.0.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **denoland--setup-deno/v2.0.3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All 7 `uses:` references in .github/workflows/test.yml use mutable version tags (@v3 or @v4) instead of full 40-character commit SHA digests. This exposes the workflow to supply-chain attacks if the referenced tag is moved or overwritten. Affected references: actions/checkout@v3 (lines 21, 57, 72), actions/checkout@v4 (lines 88, 103, 118, 133).

Locations:

- `.github/workflows/test.yml:21`
- `.github/workflows/test.yml:57`
- `.github/workflows/test.yml:72`
- `.github/workflows/test.yml:88`
- `.github/workflows/test.yml:103`
- `.github/workflows/test.yml:118`
- `.github/workflows/test.yml:133`

### missing-permissions (severity: medium)

The workflow file .github/workflows/test.yml has no top-level `permissions:` key and none of its jobs (test, test-version-file, test-binary-name, test-setup-cache, test-cache, lint, build-diff) define a job-level `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (write access to contents, packages, etc.).

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Added top-level `permissions: {}` to restrict default GITHUB_TOKEN permissions. (2) Pinned all 3 `actions/checkout@v3` references to SHA f43a0e5ff2bd294095638e18286ca9a3d1956744 (v3.6.0). (3) Pinned all 4 `actions/checkout@v4` references to SHA eef61447b9ff4aafe5dcd4e0bbf5d482be7e7871 (v4.2.1). Original tags preserved as inline comments for readability.

