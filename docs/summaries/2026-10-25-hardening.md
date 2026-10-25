# Session: supply-chain hardening 2026-10-25

**Branch:** security/hardening-2026-10-25
**Date:** 2026-10-25

## Prompts
1. "PHASE 2 from coordinator (owner approved): after you finish the sweep for all your repos and write your _done file, do NOT stop. Read HARDENING.md and do it for each of your repos: Dependabot config with 7-day cooldown, package-manager cooldown, CI lockdown (npm ci, SHA pins, least permissions, zizmor job, gitleaks job on private repos). One more PR per repo, same review and merge rules."
2. "UPDATE from coordinator: HARDENING.md changed. (a) New section 5: add the auto-merge job from templates/merge-when-clean.yml to every repo you harden. (b) Do NOT add dependabot[bot] to CodeRabbit ignore lists. (d) Repos whose branch rule needs 1 approval (… graph_express …): keep PRs open and clean; the owner is fixing that rule, then they merge."

3. "UPDATE from coordinator: templates/merge-when-clean.yml is now v2 … replace it with v2, unchanged."
4. "UPDATE from coordinator: Delete .github/workflows/dependabot-auto-merge.yml in every hardening PR (it merges Dependabot PRs with no review; merge-when-clean v2 covers Dependabot now)."

## Steps taken
- Confirmed keys: npm `min-release-age` (npm 11.20.0 `@npmcli/config` definitions; `npm config get min-release-age` prints 7 here), Dependabot `cooldown.default-days` and `monthly` (GitHub docs), zizmor-action v0.7.1 inputs.
- Local `zizmor`: 0 findings. `actionlint`: clean.

- Replaced merge-when-clean with template v3 (sha256 b175f011…) and deleted `dependabot-auto-merge.yml`.

## Decisions
- Branched from `master` while PR #18 is open, and copied its `dependency-review.yml` pin verbatim instead of stacking on it.
- No gitleaks job (public repo). No CI install step exists, so nothing to switch to `npm ci`.
