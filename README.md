# Agentic

Agentic is a proprietary coding-agent distribution maintained by Vector Workshop and derived from the MIT-licensed [OpenCode](https://github.com/anomalyco/opencode) project. It keeps OpenCode-compatible providers, plugins, configuration, OAuth, Zen, and Go service boundaries while adding an independent Agentic product identity, release channel, desktop distribution, and selected workflow improvements.

This page is the canonical public entry point for Agentic-specific behavior. For upstream-compatible configuration and APIs, use the [OpenCode documentation](https://opencode.ai/docs).

## Current release

Agentic 1.1.11 is a release candidate undergoing formal acceptance and has not been published yet. Agentic 1.1.10 remains the current public release reconciled against npm, both GitHub release channels, source tags, and the public installer.

| Product | Version | Published platform |
|---|---:|---|
| CLI / npm | `@chunklib/agentic@1.1.11` | Release candidate; npm and GitHub assets are not published yet |
| Agentic VS Code Extension | `1.1.11` | Release candidate for the CLI Release asset; Marketplace/Open VSX not claimed |
| Agentic Desktop | `1.1.11` | Release candidate for macOS arm64 ad-hoc signed DMG and ZIP packages |
| Upstream baseline | OpenCode `v1.18.18` | Agentic adopts stable-release integration points in the same release while preserving upstream opt-in/default boundaries |

The candidate platform list describes the intended 1.1.11 scope. It is not a publication claim or a claim that other operating systems or architectures passed the same release gates.

Agentic 1.1.11 follows the OpenCode v1.18.18 stable baseline and keeps the strictly monotonic, channel-bound package-manager upgrade safety delivered in 1.1.10. Routine successful upgrades no longer print the managed executable's absolute filesystem path; the same exact entrypoint is still verified after installation, and its path remains available in the actionable mismatch error when multiple installations conflict. The Desktop v2 background CLI remains at the same upstream opt-in boundary: the default and production Desktop path is the v1 Node sidecar, and the v2 CLI resource remains limited to upstream-equivalent development packaging. The npm package, platform-limited formal CLI GitHub Release, VSIX asset and macOS arm64 Desktop release will use the same source version after publication. The VSIX is not published to Marketplace or Open VSX.

## Install

Install the npm CLI:

```bash
npm install --global @chunklib/agentic
agentic --version
```

The package name changed at the standalone-repository baseline. An existing `agency-agentic@1.0.10` executable cannot discover the new scope through `agentic upgrade`; migrate once with the same npm installation prefix, then future npm-channel upgrades use `@chunklib/agentic`:

```bash
npm uninstall --global agency-agentic
npm install --global @chunklib/agentic@1.1.10
agentic --version
```

The CLI GitHub binary channel is separate from npm. Agentic 1.1.10 remains available in the [current platform-limited formal Agentic CLI Release](https://github.com/chunklib/agentic-releases/releases/tag/v1.1.10) while 1.1.11 completes formal acceptance; npm remains the portable installation path.

Desktop packages are published in [Agentic Desktop Releases](https://github.com/chunklib/agentic-desktop-releases/releases). Check the release notes, checksum, signing, notarization, architecture, and operating-system scope before installing.

The Agentic 1.1.10 VSIX remains available as a checksum-protected asset in the current formal CLI GitHub Release. The 1.1.11 VSIX is not a publication claim until the candidate release completes. It is not published to Marketplace or Open VSX. JetBrains IDEs that expose ACP configuration can launch Agentic with command `agentic` and argument `acp`; no separate JetBrains plugin is required.

## Agentic-specific behavior

Agentic intentionally keeps its fork surface narrow. Current product-specific or explicitly retained capabilities include:

- Agentic command, configuration, data, application, protocol, visual identity, and independent release channels.
- CLI, TUI, version-matched Web UI, and Desktop product surfaces.
- Persisted-tab recovery, keyed titlebar and prompt controls, attachment deduplication, and updated toast/review navigation through the OpenCode v1.18.14 baseline.
- Provider allowlists enforced before dynamic discovery hooks; Modal discovery credentials restricted to approved HTTPS Modal inference origins.
- `AGENTS.md` instruction discovery across global, project-root, and nested directory scopes, with closer instructions applied as files are accessed.
- Upstream model-specific prompt strategies plus a thin generic engineering discipline covering diagnosis, sensitive information, minimal changes, and truthful verification.
- Agentic Desktop aligned with the official Electron `utilityProcess` and Node server-sidecar lifecycle.
- Session recovery when a persisted working directory was deleted but the same project's valid worktree still exists.
- Optional Agentic Flow orchestration through the separately versioned `@chunklib/agentic-flow` plugin.

Agentic does not replace OpenCode service identities, provider IDs, protocol headers, package names, OAuth endpoints, Zen, Go, Share, or plugin SDK compatibility identifiers with invented Agentic services.

## Runtime surfaces

```text
CLI
  Agentic stable CLI runtime
    ├─ providers, sessions, tools and standard plugins
    └─ version-matched local Web UI

Desktop
  Electron main process
    └─ Node utility-process sidecar
         └─ the same Agentic server and plugin boundary

Browser
  Web UI connected to an Agentic server
  Plugins and MCP servers run on that server, not in the browser
```

CLI, Desktop, and Web can operate at the same time, but each server process owns its own live session lifecycle. Shared external services, such as a memory daemon, must define their own concurrency, identity, storage, and migration behavior.

## Configuration and project instructions

Agentic's native user configuration is stored under:

```text
~/.config/agentic/agentic.json
~/.config/agentic/agentic.jsonc
```

Project configuration can use `.agentic/`; compatible `.opencode/` configuration and required OpenCode ecosystem fields continue to be read where supported. Agentic-specific configuration takes precedence when both forms are present.

Project rules use the upstream-standard filename `AGENTS.md`. Agentic does not introduce an `AGENTIC.md` alias. A project can combine global instructions, a root `AGENTS.md`, and nested `AGENTS.md` files for directory-specific guidance.

For the complete upstream schema, providers, agents, commands, permissions, MCP, plugins, and SDK behavior, consult [OpenCode Docs](https://opencode.ai/docs).

## Flow

Agentic Flow is not enabled implicitly. Install and configure the separately released `@chunklib/agentic-flow` plugin only when its orchestration behavior is wanted; ordinary Agentic sessions should not pay its routing cost by default.

## Agentic docs versus OpenCode docs

Use this repository for:

- Agentic versions, release artifacts, installation, checksums, and supported platforms.
- Agentic CLI/Desktop/Web architecture and product-specific behavior.
- Agentic Flow integration boundaries.
- Agentic branding, feedback, and distribution questions.

Use [OpenCode Docs](https://opencode.ai/docs) for:

- Upstream-compatible configuration fields and schema.
- Providers, models, agents, commands, tools, permissions, MCP, plugins, and SDK APIs.
- OpenCode OAuth, Console, Zen, Go, Share, and other OpenCode-operated services.

Do not infer an Agentic-specific capability solely from OpenCode documentation, and do not treat an Agentic product difference as an upstream OpenCode guarantee.

## Distribution and security

Agentic release artifacts declare `UNLICENSED`; OpenCode's MIT license and applicable third-party notices remain bundled with the distribution. Do not mirror or redistribute Agentic packages without explicit permission.

Verify release checksums before installation. Signing and notarization are platform-specific release properties and are disclosed per release rather than inferred from whether a release is marked stable.

## Feedback

Report Agentic installation, packaging, Desktop, branding, or Agentic-specific behavior issues in [Agentic Releases issues](https://github.com/chunklib/agentic-releases/issues).

When a problem reproduces in upstream OpenCode without an Agentic-specific change, consult the [OpenCode repository](https://github.com/anomalyco/opencode) and its documentation instead.
