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
