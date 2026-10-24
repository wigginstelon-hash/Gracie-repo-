# GracieAi

Download [GracieAi for Windows](GracieAi-2026-10-23.zip?raw=true), extract the whole ZIP, and run `Start-GracieAi-Local.bat` for local mode. Requires Node.js 24 LTS, Ollama, and the installed `qwen3.5:4b` base model. First launch installs npm dependencies. This is a source application with a built interface, not a standalone EXE.

Local setup creates `gracie-assistant:latest` from existing local weights with Gracie's instructions and conservative resource settings. It preserves an existing profile. Gracie owns its desktop interface, persisted memory, project tools and app previews; its intelligence still comes from pretrained model weights. It is not a newly trained foundation model.

Local mode uses loopback Ollama, filters cloud aliases, blocks cloud inference and model downloads, disables web research/reference URLs and OpenAI voice, and remembers its local model selection separately. Explicit browser actions and project scripts can still access the network; this is not an operating-system network sandbox. Local microphone/transcription/speech generation is not implemented.

## Verification

From the extracted GracieAi folder: `npm ci`, `npm test`, `npm run build`. `npm run doctor` checks local runtime/model availability. `npm run package` builds, tests, and creates the ZIP and SHA-256 checksum in the parent folder. Packaging excludes credentials, chats, model weights and dependencies. The Windows workflow checks the distributed ZIP's checksum, tests and build.

156 automated tests pass locally. Live checks separately exercised streamed chat, structured output, vision where supported, real read-only project tools, cancellation, remembered preferences after restarting the desktop app, generated JavaScript syntax, and a trusted fixture's interactive Electron preview. Mocked helper tests do not establish that every model can reliably edit or execute projects.

## Model findings on the tested 8 GB GPU / 16 GB RAM PC

- `gracie-assistant:latest`, standard Qwen 3.5 4B/9B and the two smaller abliterated Qwens passed their targeted checks. Small models remain fallible.
- Installed `huihui_ai/qwen3.5-abliterated:4B` (about 3.3 GB) and `huihui_ai/qwen3-abliterated:4b` (about 2.5 GB). These fit this system better than the 27B model. Publisher sources: [Qwen 3.5](https://ollama.com/huihui_ai/qwen3.5-abliterated:4B), [Qwen 3](https://ollama.com/huihui_ai/qwen3-abliterated:4b).
- Qwen 3.8 abliterated answered correctly through Gracie in about 65 seconds. Disabling speculative draft generation for large local models resolved this tested request. It is slow on this hardware and is not the default.
- Qwen 2.5 Coder 7B failed a structured arithmetic check and emitted tool-shaped text without a real tool call. Gracie now warns that no tool ran. Do not rely on this model for automatic actions.
- Llama 3.2 Vision and Gemma 4 26B had runtime/model loading failures. Application fixes cannot guarantee compatibility of installed model artifacts.

## Changes

Added a dedicated local assistant setup/launcher, offline controls and diagnostics. Fixed output/context budgeting, early cancellation, large-model draft settings, file-content versus concurrency-hash instructions, truthful tool execution warnings and sanitized vision-projector errors. Included previously omitted project-agent tests and reproducible packaging.

See [the complete readable source patch](GracieAi-fixes.patch) and the README inside the ZIP. SHA-256 is in `GracieAi-2026-10-23.sha256`. Existing user data and installed models are not included or overwritten by this download.
