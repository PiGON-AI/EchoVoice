# EchoVoice — Troubleshooting

First stop, always: **View → Output → pick "EchoVoice"** in the dropdown. EchoVoice logs every decision — which folders it watches (and whether they exist), every spoken utterance (`speak: source=… chars=… cap=…`), every fallback and its reason. Most mysteries end there.

## No sound at all
- Is the **🔊 EchoVoice** item in the status bar? Click it — is it muted?
- Does the Output channel exist? If there's no "EchoVoice" channel at all, the extension never activated — see [Installed but never activates](#installed-but-never-activates).
- EchoVoice only speaks messages that arrive **after** it starts. Say something new to your agent.
- The agent must have actually run **on this machine** — EchoVoice reads local transcript files.

## It only reads a few sentences
By design: the default **sentence cap is 3**. Status-bar menu → **Sentence cap… → Read everything**.
⚠️ Settings are **per editor** — a cap set in VS Code does nothing in Antigravity/Cursor, and vice versa. The log line shows the effective cap on every utterance (`cap=3`).

## One agent is silent, the others speak
- Check its toggle: `echovoice.sources.*` in Settings.
- Check the log's startup lines: `source <name>: watching <path>` vs `MISSING`.
- Kimi/Codex only speak if their CLIs have produced sessions on this machine.
- **Antigravity comes in two products** — "Antigravity" and "Antigravity IDE" — with separate settings, separate extension installs, and different transcript filenames (`overview.txt` vs `transcript.jsonl`). Both filenames are supported since 0.9.5; make sure EchoVoice is installed in the product you actually use.

## The same message plays twice
Fixed in 0.9.4 by a cross-instance ledger (every message spoken exactly once per machine) — but **all** open editors must run ≥ 0.9.4. One old install anywhere reintroduces the echo.

## ElevenLabs keeps falling back to another voice
ElevenLabs needs **two** things, both **per machine and per editor**: the API key (encrypted SecretStorage) *and* a voice ID. Run **EchoVoice: Set ElevenLabs API Key** — it walks you into the voice ID too. The warning toast tells you which half is missing.

## Piper sounds robotic or garbled
- Pick a better voice: menu → **Choose free Piper voice** → **Ryan (high quality)**.
- Pacing: raise `echovoice.piper.sentencePause` (0.35 → 0.5) for a calmer read; `echovoice.piper.speed` for tempo.
- Emoji/symbols being read aloud was fixed in 0.9.4 — update.
- Per-agent voices under Piper must be **Piper keys** (like `en_US-bryce-medium`); an ElevenLabs ID in `echovoice.voice.*` is ignored under the Piper provider and that agent falls back to the default voice.

## Installed but never activates
(Especially in VS Code forks.) In order of likelihood:
1. **Engine gate** — Help → About: the app must report VS Code compatibility ≥ 1.90. Forks with `update.mode: none` can sit on old builds; the extension installs but the host silently refuses to load it.
2. **Activation crash** — Help → Toggle Developer Tools → Console: a red stack trace naming the extension is the murder weapon. Please file it as an issue with the trace.
3. **Remote/WSL** — EchoVoice deliberately runs on your local machine (`extensionKind: ui`): that's where the transcripts and the speakers are. In remote setups, install it locally, not in the remote.
4. **Managed devices** — corporate policy can block third-party VSIX loading in some editors while allowing it in others. Check the Extension Host output for policy warnings.

## Where things live
- Settings: per editor (`%APPDATA%\<Editor>\User\settings.json` / `~/Library/Application Support/<Editor>/User/settings.json`)
- ElevenLabs key: per editor, encrypted SecretStorage (never in files)
- Piper engine + voices: the extension's private storage, downloaded on first use
- Spoken-once ledger: `~/.echovoice/spoken` (safe to delete; it re-creates)

*This guide was distilled from real multi-machine debugging — including forensic and architectural diagnosis contributed by the AI team that builds EchoVoice.*
