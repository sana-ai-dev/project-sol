# project-sol: notes for opencode

Public hub for sana.ai.dev projects, verified tools and evidence-backed write-ups.

## Tier: open

- `open`: public on purpose. Write docs that teach; never put secrets, private notes or customer data in the repo.
- `vault`: private on purpose, may earn money. NEVER make the repo public, never copy its code or details into any public repo, post or README.
- Tier is stored locally at `.git/buddy-tier`. Never change repo visibility; only the owner does that, through the GitHub Buddy publish gate.

## How to run

TODO: install, run and test commands (keep this exact and tested).

## Branch rules (follow these every time)

- `main` = released and stable. `staging` = integration; everything lands here first.
- Never commit or push straight to `main` or `staging`.
- Start work: `git switch -c feature/<short-name> staging` (use `fix/`, `docs/`, `chore/` too).
- Commit messages: `type: short summary` (feat, fix, docs, chore, refactor, test).
- Finish: push the branch, open a squash pull request into `staging`.
- Release: pull request `staging` -> `main`, merge with a MERGE COMMIT (not squash), then tag `vX.Y.Z` on `main`.
- Urgent fix on live code: branch from `main`, pull request into `main`, then merge `main` back into `staging`.
- Pushing feature branches, opening pull requests and merging into `staging` needs no extra permission.
- Ask only for: public visibility, secrets findings, and which nominated flagship/viral projects go public.
- Never force-push, rewrite history, or delete `main`/`staging`.

## Evidence and docs

- `.buddy/` holds raw local evidence and is git-ignored; only `verification.json` and `docs/verification.md` summaries are published.
- README.md is the front door; longer pages live in `docs/`.
- Diagrams live in `docs/diagrams/` (keep the `.excalidraw` source and any exported `.svg` together; Mermaid is the honest fallback).
