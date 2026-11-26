# Xara toolbelt architecture

This page describes the verified pattern, not a shipped runtime. All blocks are Mermaid because no Excalidraw CLI was available.

## Components

```mermaid
flowchart LR
  V[Voice request] --> I[Intent match]
  I --> G{ACT mode?}
  G -- no --> P[Plan-only reply]
  G -- yes --> T[Bounded tool loop]
  T --> F[File and note tools]
  T --> B[Browser tools]
  T --> C[Clipboard and screenshot]
  T --> A[Allowlisted app launch]
  T --> O[OpenCode delegation and ping]
  T --> U[Windows UI automation]
  F --> R[Redacted spoken summary]
  B --> R
  C --> R
  A --> R
  O --> R
  U --> R
  R --> N[Completion notify]
```

Derived from the slice 1, slice 2, session-ping, permission-notify and desktop UIA proofs.

## Trust boundary

```mermaid
flowchart TB
  subgraph LocalOnly[Local-only evidence]
    Proofs[Proof files]
    Logs[Harness logs]
    State[Session and outbox state]
    Captures[Screenshots and restores]
  end

  subgraph Guards[Enforced guards]
    Paths[Allowed roots and blocked names]
    URLs[Public http/https only]
    Apps[App allowlist and no shell]
    Refs[Snapshot-scoped refs with TTL]
    Redact[Output redaction and caps]
  end

  Guards --> Writeup[Redacted public write-up]
  LocalOnly -. never copied .-> Writeup
  Writeup --> Gate[GitHub Buddy review gate]
```

The dotted edge is the deliberate boundary: private evidence informs the claims but is not published.

## Execution flow

```mermaid
sequenceDiagram
  participant S as Sana / local user
  participant X as Voice assistant
  participant L as Tool loop
  participant G as Guard
  participant E as Local effect
  participant N as Notify route

  S->>X: spoken request
  X->>L: intent matched, ACT confirmed
  L->>G: validate path, URL, app or ref
  G-->>L: allow or refuse
  L->>E: bounded side effect
  E-->>L: result
  L->>X: short redacted summary
  X->>N: completion notice
```

## Diagram sources

- Tool names, ACT gate and notify flow: slice 1 and slice 2 proofs.
- Ping path: session-ping proof.
- Redaction, URL filtering and ref TTL: desktop UIA proof.
- Publication boundary: `docs/scout-summary.md` and this hub's approval gate.
