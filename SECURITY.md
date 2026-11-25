# Security policy

## Scope

`project-sol` publishes curated summaries, not raw operational logs. Raw evidence lives in `.buddy/` and is git-ignored.

## Rules

- No secrets, private keys, tokens, host credentials or personal file paths in published files.
- No private LAN addresses, internal hostnames or desktop captures.
- External repositories and tools must pass scan, approval and exact-version pinning before clone or install.
- Publishing is blocked on any secrets finding; history rewriting is never done without explicit owner approval.

## Reporting

If you find a secret or unsafe material here, open a private issue or contact the owner directly. Do not post the secret value in a public issue.

## Current status

gitleaks 8.30.1 scanned the working tree and git history on 2026-11-25 with no findings. Dependency audit was not applicable (no dependency manifest). Dependency licence review was skipped (no tool for this ecosystem). See [verification](docs/verification.md).
