<!-- markdownlint-disable -->

# Hardening Report: denoland--setup-deno--/v2.0.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **denoland--setup-deno--/v2.0.5** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references `actions/checkout@v5` (a mutable tag) in 7 steps across multiple jobs. These should be pinned to a full 40-character commit SHA to prevent supply-chain attacks. Failing references: `actions/checkout@v5` appears in jobs: test, test-version-file, test-binary-name, test-setup-cache, test-cache, lint, and build-diff.

Locations:

- `.github/workflows/test.yml:27`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and none of its 7 jobs (test, test-version-file, test-binary-name, test-setup-cache, test-cache, lint, build-diff) define job-level `permissions:` blocks. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially write) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Replaced all 7 occurrences of `actions/checkout@v5` with the pinned SHA `actions/checkout@93cb6efe18208431cddfb8368fd83d5badbf9bfd # v5`. (2) Added `permissions: {}` at the workflow top level to enforce least-privilege — the workflow only runs Deno tests and does not require any GITHUB_TOKEN permissions.

