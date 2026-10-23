# GracieAi

Download [GracieAi for Windows](GracieAi-2026-10-23.zip?raw=true), extract the entire ZIP, and read the included README.md.

Requires Node.js LTS and Ollama. First launch installs dependencies; this is not a standalone executable. The ZIP includes source and the built interface, and excludes API keys, private chats, model weights and dependencies.

SHA-256 checksums are included in GracieAi-2026-10-23.sha256.

## Development and verification

The editable source is inside the ZIP. From its GracieAi folder, run `npm ci`, `npm test` and `npm run build` using Node.js 24 LTS. Every Electron test file is discovered, including project-agent checks. Run `npm run package` to rebuild, test, and regenerate the ZIP and checksum in the parent folder.

The Gracie checks workflow verifies the ZIP checksum, extracts the downloadable source and runs its tests and build on Windows for pushes and pull requests. Tests use mocked model responses; live Ollama inference, microphone/voice, and desktop interaction require separate manual testing.

## Fixes in this update

Local chat context now reserves room for the requested answer. Compact Qwen hybrid models can use a 12,288-token completion window, while other models retain the 8,192-token cap. Short replies can still use a 2,048-token window. Larger windows use more memory; resource estimates remain advisory and Ollama owns allocation.

Tests now reflect short model residency, small inference batches, omitted unsupported thinking controls, advisory memory estimates, and no automatic reload after a runner crash. Resume-test mocks correctly handle metadata requests. Project-agent tests are included in the default suite.

See [the source patch](GracieAi-fixes.patch) for the changes within the ZIP.
