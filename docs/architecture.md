# Architecture

This is a documentation-and-curation repository. There is no runtime service; the components below are files and folders, not processes.

## Components

```mermaid
flowchart LR
  README[README.md] --> Docs[docs/]
  Docs --> Scout[scout-summary.md]
  Docs --> Verify[verification.md]
  Docs --> Arch[architecture.md]
  Hub[projects/] --> Candidates[redacted project subfolders]
  CI[.github/workflows/ci.yml] --> Structure[required-file checks]
  Local[.buddy/] -. local only .-> Evidence[raw logs and scout report]
```

Derived from: `README.md`, `docs/`, `projects/README.md`, `.github/workflows/ci.yml`, `.buddy/scout-report.md`. The dotted edge is deliberately local and git-ignored.

## Data flow

```mermaid
sequenceDiagram
  participant W as Local workspace / GitHub metadata
  participant B as GitHub Buddy gate
  participant H as project-sol docs
  participant S as Sana approval
  W->>B: scout + verify + redact
  B->>H: write only verified summaries
  B->>S: review report at Stage 9
  S-->>B: public / flagship decision
  B->>H: publish approved material
```

No automatic path bypasses the approval step.

## Deployment layout

```mermaid
flowchart TB
  Feature[feature/*] -->|squash PR| Staging[staging]
  Staging -->|merge-commit release PR + tag| Main[main]
  Main --> GitHub[github.com/sana-ai-dev/project-sol]
  Main -. optional, not enabled .-> Pages[static docs site]
```

`main` is released, `staging` is integration. No force push, history rewrite or direct push to either protected branch.

## Diagram sources

- Mermaid blocks above are the always-available source of truth.
- Excalidraw export was skipped: no recognised CLI was present. No `.svg` is claimed.
