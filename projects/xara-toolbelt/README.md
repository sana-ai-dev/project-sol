# Xara toolbelt — bounded local computer use

This is a redacted write-up in the `sana.ai.dev` hub. It documents verified patterns and limits; it is not a code package and not a flagship claim. The working material stayed local.

## What it is

A voice assistant can be given a small set of bounded tools that act only in ACT mode. The toolbelt covers file operations, browser launch, clipboard, notes, screenshots, allowlisted apps, OpenCode delegation and local Windows desktop control. Every side effect is guarded, redacted in spoken summaries and reported back with a short completion notice.

## Verified capability groups

| Group | Tools and behaviour | Evidence |
|---|---|---|
| Delegation slice | `grep_files`, `opencode_status`, `delegate_to_opencode`; atomic inbox requests, outbox results and a spoken completion ping | Slice 1 proof, independent verifier PASS |
| File and desktop slice | `create_folder`, `create_file`, `edit_file`, `open_file`, `save_note`, `browser_open`, `browser_search`, `clipboard`, `screenshot`, `launch_app`, `brainstorm`; 18 schemas including `ping_opencode` | Slice 2 and session-ping proofs, independent verifier PASS |
| Windows UI automation | `status`, `apps`, `launch`, `navigate`, `snapshot`, `click`, `type`, `press`; snapshot-scoped refs with a 600-second TTL, redaction, URL filtering and allowlisted keys | Desktop UIA proof, harness 11/11, independent verifier PASS |
| Permission and completion notices | Native permission prompts and task completion are announced through the local voice notify route | Permission-notify proof, independent verifier PASS |

## Guardrails that mattered

- ACT mode is explicit; a plan-mode restart makes the tools inert.
- File writes require a concrete path, reject blocked names and outside-root paths, cap bytes, write through a temporary file and create a timestamped backup before overwrite.
- Browser tools accept only public http/https URLs with no embedded credentials or loopback/private targets.
- App launch is allowlisted, passes no arguments and uses no shell.
- Clipboard, notes and spoken summaries are capped and redacted; file contents, clipboard contents and screenshot bytes are never spoken.
- Desktop UI refs are scoped to one snapshot, expire after 600 seconds and are re-resolved by path and runtime identity.
- `ping_opencode` addresses a registered active session directly and never writes to the delegation inbox.

## Architecture and evidence

- [Architecture and diagrams](docs/architecture.md)
- [Verification summary](docs/verification.md)

## Known limitations

- This is support material, not a product to install. No source package is published here.
- Browser, open-file and app-launch calls were monkeypatched in the harness; one harmless live file-tool loop proved the real execution path.
- No spoken microphone test was run.
- Desktop UI coverage depends on each app exposing an accessibility tree; custom surfaces may expose little.
- The OpenCode lane must be running and the active session registered for the ping path to work.
- Screenshots, outbox records, restore snapshots, private host details and environment-specific state were deliberately excluded.

## License

MIT. See [LICENSE](../../LICENSE).

[Sana](https://sana.ai.dev)
