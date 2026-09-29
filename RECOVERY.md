# Personal recovery fork

Recovered 27 September 2026 for andycowan after the upstream repositories became private.
Source: DanWlker/kulala-core at 772a506. Original licences and attribution are retained.

Upstream workflows are preserved in `.github/upstream-workflows` but are not active; they assume upstream publishing infrastructure.

The initial Core release is `0.37.0-andycowan.1`, built from recovered source, not a claim that the source matches upstream 0.37.0. Only macOS Apple Silicon is initially built and tested. Other platforms need separate builds and validation.

## Build on macOS Apple Silicon

```sh
VERSION=0.37.0-andycowan.1 bun install --frozen-lockfile
bun run build:darwin-arm64
```

Output: `packages/core/dist/kulala-core-darwin-arm64`. Built using Bun 1.3.10.
The recovery adds `KULALA_CORE_DATA_DIR` support to persistence, matching the plugin bridge.
Validation: 65 parser/request/body tests passed; the compiled binary passed local GET and JSON POST using http-client.env.json.

## Windows and Linux assessment

The recovery code change is not specific to Apple Silicon: `KULALA_CORE_DATA_DIR`
is read before the existing OS-specific fallback is selected. No source-code port is
needed for Windows or Linux. The repository already defines Bun targets and vendored
curl/jq downloads for Windows x86_64 and Linux x86_64/aarch64.

The active `Fork platform builds` workflow installs, lints and tests on Linux, then
builds and uploads all three Windows/Linux artifacts. This deliberately does not
publish npm packages or create GitHub releases. A successful workflow run is the
required platform validation before distributing those artifacts; only macOS arm64
has been manually validated so far.

| Platform | Build command | Artifact |
| --- | --- | --- |
| Linux x86_64 | `bun run build:linux-x64` | `packages/core/dist/kulala-core-linux-x86_64` |
| Linux aarch64 | `bun run build:linux-arm64` | `packages/core/dist/kulala-core-linux-aarch64` |
| Windows x86_64 | `bun run build:windows-x64` | `packages/core/dist/kulala-core-windows-x86_64.exe` |
