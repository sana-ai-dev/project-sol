# Deployment

No site is deployed from this repository yet. This page describes the intended path, not a proven deployment.

## Branch flow

1. Work on `feature/*`, `fix/*` or `docs/*` from `staging`.
2. Squash PR into `staging`.
3. Release PR `staging` → `main` using a merge commit.
4. Tag `main` with `vX.Y.Z`.

## Optional static docs

If enabled later, GitHub Pages can serve `docs/` from `main`. It is not enabled in this build, and no Pages URL is claimed.

## Local guard

A local pre-push hook blocks direct pushes to `main`/`staging`, branch deletion and non-fast-forward pushes on this machine. GitHub-side branch protection is advisory on free private repos and must be checked separately.
