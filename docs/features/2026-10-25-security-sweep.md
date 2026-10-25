# Feature: security sweep fixes

**Branch:** security/sweep-2026-10-25
**Date:** 2026-10-25

## Summary
Bumps `body-parser` and `nodemon` past known high-severity advisories, pins the
dependency-review workflow's actions, and fixes the misnamed `.gitignore`.

## Motivation
`osv-scanner` and `npm audit` reported 3 high advisories in the lockfile.
`zizmor` flagged two floating action tags. The ignore file was named
`.gitinore`, so git ignored nothing: a local `.env` or `node_modules/` would be committed.

## What changed
- `body-parser` 2.3.0 → 2.4.0 (lockfile only, GHSA-27r3-jxmh-p828, DoS on compressed bodies). `qs` 6.16.0 → 6.16.1 because body-parser 2.4.0 needs it.
- `nodemon` ^2.0.19 → ^3.0.0, locked at 3.0.0 (dev only). This pulls `semver` 7.8.5 and `simple-update-notifier` 2.0.0 and clears GHSA-c2qf-rxjj-qqgw (semver ReDoS).
- `actions/checkout` and `actions/dependency-review-action` pinned to commit SHAs, `persist-credentials: false`.
- `.gitinore` renamed to `.gitignore`.

## Notes
body-parser 2.4.0 was published 2026-10-22. It is the only 2.x fix, it is the version the advisory names, and it was published by the expressjs trusted-publisher workflow with provenance.
