# MeetOnTrack capture agent instructions

## Distribution

This is the public MeetOnTrack recorder repository (MIT), derived from Amanu
(`gsamat/amanu`). `master` mirrors upstream; MeetOnTrack work lands on `main`
and upstream is merged from `master`. The product-facing name is MeetOnTrack by
aiagentlbs.com. Keep upstream copyright/license attribution in shipped legal
notices; do not use upstream branding in setup, tray or recording UI. Internal
namespaces and persisted paths are compatibility details, not rename targets.
The public `AIAgentLbs/meeting-copilot` repository packages the native capture,
web assistant and embedded runtime together and hosts the releases. Do not
publish to upstream update feeds or use upstream signing. Never commit secrets,
private client data or meeting recordings.

Owner rules shared with `meeting-copilot` (2026-10-20), see its `AGENTS.md`:
no hardcoded AI or speech providers, models or model modes; one settings store
`%USERPROFILE%\.config\meeting-copilot\config.json` /
`~/.config/meeting-copilot/config.json` with one schema
(`meeting-copilot/docs/config.schema.json`) and lock-protected
read-modify-write that preserves keys a component does not own.

## Windows release source

- The current Windows app and release scripts live on `origin/codex/ready-0.6.3`, including the versioned installer implementation merged in PR #29. The branch name reflects its origin, not the version of the next release.
- Before preparing a Windows release, fetch that branch and use a clean checkout based on its latest commit. Until the Windows source is integrated into `master`, do not use the old Windows workflow on `master` or stale untracked `windows/` files in a local macOS checkout.
- Dispatch `windows-beta.yml` with an explicit `--ref` pointing to the prepared Windows release branch. Set its root `VERSION` to the agreed shared release version and commit the release changes before building; local packaging rejects a version that differs from `VERSION`.
- Follow `docs/releasing.md` for the release route and post-publication download-link checks.

## Release installer filenames

- Standalone native Windows installers, if published, must use `MeetOnTrack-<version>-Setup.exe`. The integrated distribution uses the versioned archive named by the main repository's packager.
- Apply this name in Windows packaging and publication, website download links and `/win.exe`, checksums, and package manifests. The Velopack channel can remain `stable`; `stable` alone is not a sufficient installer filename.
- Preserve already published release assets; apply this naming convention when preparing the next Windows release.

## Windows testing

- The user has connected a Windows computer to Codex for Amanu development and testing. Treat it as an available testing environment, but confirm that the host is online and the project is accessible before relying on it.
- For changes to the Windows app, run the relevant build and tests on Windows. When behavior depends on the Windows graphical interface, launch the app there and verify the actual flow with Computer Use when available.
- Mac-only checks or CI results do not establish that the Windows app works. Report which checks ran on the Windows host and any checks that could not run.
- If the current chat runs on another host, use the connected Windows host or arrange a handoff of the chat to it before Windows-specific validation. If the host is unavailable, state the blocker instead of claiming Windows verification.
