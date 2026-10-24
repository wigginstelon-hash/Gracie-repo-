# GracieAi

Download [GracieAi for Windows](GracieAi-2026-10-23.zip?raw=true), extract the whole ZIP and run `Start-GracieAi.bat`. The normal launcher now opens local mode. Node.js 24 LTS, Ollama and installed compact local weights are required. This includes complete source and a built interface, not a standalone EXE. First launch installs npm dependencies.

## Local assistant

Setup creates `gracie-assistant:latest` from installed Qwen 3.5 4B weights and preserves an existing profile. On the tested PC the profile was deliberately rebuilt from `huihui_ai/qwen3.5-abliterated:4B`; Qwen 3 abliterated 4B is a smaller text-only alternative. Gracie owns its interface, persisted memory, project tools and app previews. It still uses pretrained weights; it is not a newly trained foundation model.

Local mode enforces loopback Ollama, filters cloud aliases, blocks cloud inference/model downloads and disables web research/reference URLs and OpenAI voice. Explicit browser tasks and project scripts can still access the internet; this is not an OS network sandbox. `Start-GracieAi-Online.bat` retains the optional online provider.

## Local speech

Run `Setup-Local-Speech.bat` once with 64-bit Python 3.14 installed. Setup downloads pinned Python dependencies and the small English Whisper model. Runtime transcription uses CPU int8 and local files only; no hosted audio API is used. Output uses an installed Windows voice through SAPI, without changing PowerShell execution policy.

The microphone records up to 45 seconds and inserts transcribed text into the composer. Review it before pressing Send. The speaker reads up to 4,000 characters of the latest reply. Stop cancels recording, transcription or playback. Temporary audio files are removed after each request. English transcription is supported. Microphone hardware quality and speaker audibility depend on the user's devices and Windows permissions.

## Fixes and verification

165 automated tests pass, TypeScript and production build pass, and npm audit reports zero vulnerabilities in the tested installation. The Windows workflow verifies the distributed ZIP checksum, extracts its source, installs dependencies, tests and builds it. `npm run package` reproduces the ZIP and SHA-256 checksum; `npm run doctor` checks runtime/model availability.

Fixed output/context budgeting, early cancellation, large-model speculative draft settings, file-content versus concurrency-hash instructions, text-only tool-call warnings, sanitized vision errors and restoration of local-mode settings. Ordinary arithmetic without a selected project advertises no project/app-launch tools. App launching requires an explicit request; canceling a launch halts the task, and its approval dialog observes request cancellation.

Local speech checks covered an actual Windows TTS -> Whisper round trip, real Chromium WAV -> MediaRecorder WebM -> Whisper conversion, and the Desktop microphone UI with generated fixture audio and isolated test data. Reply playback is checked separately with test audio muted; fixture checks do not establish real microphone or speaker hardware quality. Existing project-helper tests use controlled fixtures.

The combined live model-guided edit/command-execution test was rejected by automatic approval review with only “blocked by policy.” That complete workflow remains unverified. Controlled helper, generation, syntax and trusted preview checks are reported separately; they do not substitute for the blocked check.

## Model selection

The tested 8 GB GPU / 16 GB RAM PC works much better with compact 4B models. They passed targeted chat, structured output, vision where supported, actual file reading and cancellation. Qwen 3.8 answered correctly but took 65–325 seconds and caused heavy memory pressure. Installed Llama Vision/Gemma artifacts failed to load and Qwen Coder failed native tools; these choices were retired locally in favor of the verified compact profile. These model files are not shipped or deleted by the downloadable application.

Sources: [Whisper implementation](https://github.com/SYSTRAN/faster-whisper), [Windows voice API](https://learn.microsoft.com/en-us/previous-versions/windows/desktop/ms723597(v=vs.85)), [Qwen 3.5 abliterated](https://ollama.com/huihui_ai/qwen3.5-abliterated:4B), [Qwen 3 abliterated](https://ollama.com/huihui_ai/qwen3-abliterated:4b).

The ZIP excludes private chats, API keys, weights, Python environments and npm dependencies. See the included README and [complete readable source patch](GracieAi-fixes.patch). The matching checksum is in `GracieAi-2026-10-23.sha256`.
