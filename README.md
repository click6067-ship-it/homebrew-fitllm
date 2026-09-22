# homebrew-fitllm

Homebrew tap for [**fitllm**](https://github.com/click6067-ship-it/fitllm-engine) — checks whether a local LLM fits on your GPU or Apple Silicon Mac, using architecture-aware memory math.

```bash
brew tap click6067-ship-it/fitllm
brew trust click6067-ship-it/fitllm   # required: Homebrew will not load a third-party formula without it
brew install fitllm

fitllm "Gemma 4 31b" --gpu "RTX 4090"
fitllm --top --detect
```

## Why a tap and not homebrew-core

homebrew-core does not accept prebuilt binaries, and its notability bar for a self-submitted project is 225 stars / 90 forks / 90 watchers. This project does not meet that yet, so a tap is its honest home today rather than a workaround being hidden.

The `brew trust` line is not optional. Current Homebrew refuses to load a formula from a third-party tap until you trust it — without that line `brew install` stops with "Refusing to load formula from untrusted tap". This is verified on every release by a macOS CI job that runs all three commands.

## What you are installing

A self-contained binary — no Node required. Each release attaches a `.sha256` next to every artifact and the formula pins those digests, so Homebrew verifies what it downloads.

The binary embeds its JavaScript runtime, which makes it 60–94 MB: much larger than an equivalent Rust or Go tool. That is the cost of not forking the calculation engine into a second language, where the two copies would drift.

The formula is generated from the release manifest by [`scripts/gen-packaging.mjs`](https://github.com/click6067-ship-it/fitllm-engine/blob/master/scripts/gen-packaging.mjs) — the URLs and checksums are never hand-written.

Engine source, issues and the memory math: [click6067-ship-it/fitllm-engine](https://github.com/click6067-ship-it/fitllm-engine) · MIT
