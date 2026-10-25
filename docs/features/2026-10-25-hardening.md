# Feature: supply-chain hardening for CI, npm and Dependabot

**Branch:** security/hardening-2026-10-25
**Date:** 2026-10-25

## Summary
Adds a 7-day cooldown for npm installs and Dependabot updates, a zizmor workflow
that fails on high-severity workflow findings, the shared merge-when-clean
workflow, and removes the
old Dependabot auto-merge workflow.

## Motivation
Phase 2 of the 2026-10-25 security sweep. This month's npm and PyPI worms shipped
as brand-new versions of trusted packages. Waiting 7 days before taking a new
version closes most of that window.

## What changed
- `.npmrc`: `min-release-age=7` (npm 11.20.0 supports it; older npm warns and ignores it).
- `.github/dependabot.yml`: npm and github-actions, monthly, `cooldown.default-days: 7`, minor + patch grouped per ecosystem, at most 3 open PRs each.
- `.github/workflows/zizmor.yml`: zizmor 1.31.1 via `zizmorcore/zizmor-action` v0.7.1 (SHA-pinned), fails on high findings.
- `.github/workflows/merge-when-clean.yml`: the sweep's shared template, unchanged.
- `dependabot-auto-merge.yml`: deleted. It merged patch/minor Dependabot PRs as soon as tests passed, with no review. merge-when-clean (template v4) now merges Dependabot PRs (non-major, reviewed, 0 open threads) instead.
- `dependency-review.yml`: the same SHA pins as PR #18, so the new zizmor job passes on this branch too. The change is identical, so the two PRs merge cleanly in either order.

## Notes
- `master` needs 1 approving review. Neither the owner nor merge-when-clean can satisfy that on the owner's own PRs. The owner is changing that rule.
