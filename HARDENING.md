<!-- markdownlint-disable -->

# Hardening Report: denoland--setup-deno/v2.0.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **denoland--setup-deno/v2.0.4** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses `actions/checkout@v5` (a mutable tag reference) in all 7 `uses:` steps instead of a pinned 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file. Each occurrence should be replaced with a full SHA pin, e.g. `actions/checkout@<40-char-sha> # v5`.

Locations:

- `.github/workflows/test.yml:22`
- `.github/workflows/test.yml:57`
- `.github/workflows/test.yml:72`
- `.github/workflows/test.yml:87`
- `.github/workflows/test.yml:101`
- `.github/workflows/test.yml:115`
- `.github/workflows/test.yml:130`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` key and none of its 7 jobs (test, test-version-file, test-binary-name, test-setup-cache, test-cache, lint, build-diff) define a job-level `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or to each job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 7 occurrences of `actions/checkout@v5` by pinning to the full commit SHA `fbc6f3992d24b796d5a048ff273f7fcc4a7b6c09` with the tag preserved as a comment. Added a top-level `permissions: contents: read` block to the workflow to enforce least-privilege token permissions across all 7 jobs.

