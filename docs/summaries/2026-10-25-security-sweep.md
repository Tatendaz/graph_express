# Session: security sweep 2026-10-25

**Branch:** security/sweep-2026-10-25
**Date:** 2026-10-25

## Prompts
1. "You are worker sec-w7 in the 2026-10-25 security sweep. Read BRIEF.md now and follow it exactly. Your repos: graph_express onemind dental-scan-viewer yapui."
2. "Pick old, safe versions, never latest: bump only the named package, to the lowest fixing version, published on or before 2026-10-18."

## Steps taken
- IOC grep, commit authors, deploy keys, webhooks, secrets, branch protection: nothing unexpected.
- gitleaks (history + tree): no leaks. osv-scanner + npm audit: 3 high advisories.
- Bumped only the flagged packages with `npm install --package-lock-only --ignore-scripts --before=2026-10-18T23:59:59Z`, then reviewed the lockfile diff: only body-parser, qs, nodemon, semver, simple-update-notifier changed.
- `npm ci --ignore-scripts`, `npm audit` (0), `osv-scanner` (0). Ran the server and queried `/graphql`, plain and gzip bodies.

## Decisions
- nodemon 3.0.0 is a major bump, but it is a dev-only file watcher and `nodemon --version` and the server run the same. No 2.x release fixes semver.
