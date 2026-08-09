# DISCLOSURES — every byte, every kink, in one place

This page itemizes everything EchoVoice can send or receive over the
network, everything it stores on your machine, and the platform quirks you
might hit. It describes **this release as shipped** — each release's
disclosures describe that release. If you find this page and the code in
disagreement, that's a bug: [tell us](https://github.com/pigon-ai/echovoice/issues).

## Network — the complete list

EchoVoice contains no telemetry or analytics code. The table below is the
entire network surface. If it's not listed here, it doesn't happen.

| what | when | size | where from | verification |
|---|---|---|---|---|
| Kokoro model + selected voices | Once, only if you pick a Kokoro voice, only after you say yes to a consent dialog | ~92 MB model + ~0.5 MB per voice | `github.com/PiGON-AI/Echotools-Runtime` (our release, mirrored from [onnx-community/Kokoro-82M-v1.0-ONNX](https://huggingface.co/onnx-community/Kokoro-82M-v1.0-ONNX), Apache-2.0) | SHA-256 **and** exact byte size pinned in the extension source; mismatches are discarded |
| Piper engine | Once, only if you pick a Piper voice, only after a consent dialog naming the size | ~30 MB | `github.com/rhasspy/piper` (pinned release `2023.11.14-2`) | SHA-256 pinned per platform archive |
| Piper voices | Same consent flow | ~22 MB for the set | `huggingface.co/rhasspy/piper-voices` (pinned revision, never a moving branch) | SHA-256 pinned per voice + config |
| ElevenLabs synthesis | Every spoken reply, **only** while you've selected ElevenLabs with your own API key | the request | `api.elevenlabs.io` over HTTPS | — |
| Send Feedback button | Only when you click it | opens your browser | `github.com/pigon-ai/echovoice/issues` (https-only; non-https values of `echovoice.feedbackUrl` are ignored) | — |

**What the ElevenLabs request contains, exactly:** the prepared text of the
reply being spoken — code blocks are stripped *before* sending — plus your
API key (in a header) and normal API metadata. Nothing else. ElevenLabs'
handling of that request is governed by [their privacy policy](https://elevenlabs.io/privacy),
not ours.

**With system voices, Kokoro, or Piper selected, synthesis happens on your
machine and no text goes anywhere.**

## Storage — what's on your disk and how to remove it

| what | where | remove it |
|---|---|---|
| ElevenLabs API key | VS Code **SecretStorage** (your OS keychain) — not in any settings file | "EchoVoice: Clear ElevenLabs API Key" |
| Kokoro / Piper models | the editor's global storage folder for this extension | delete the folder after uninstall, or before it via your OS file manager |
| Temporary audio | your OS temp folder, deleted after playback | automatic |
| Spoken-reply claim ledger | `~/.echovoice/spoken` (tiny text ledger so two editors don't speak the same reply twice) | delete the folder any time |

EchoVoice reads the transcript files your AI coding tools already write to
your own disk. It doesn't copy them, upload them, or retain them — it
watches, extracts the newest reply, and speaks it.

## Platform notes — the kinks, up front

- **macOS, Apple Silicon (M-series):** the upstream Piper build for Mac is
  Intel-only, so Piper needs **Rosetta 2**
  (`softwareupdate --install-rosetta`). Or skip the kink: **Kokoro runs
  natively everywhere** and is the better voice.
- **Windows:** ElevenLabs MP3 playback uses Media Foundation, which some
  Windows 11 installs ship without. EchoVoice detects this and points you to
  the fix (Settings → Apps → Optional features → "Windows Media Player
  Legacy"). Kokoro, Piper, and system voices don't need it.
- **Linux:** the system voice uses `spd-say` (package: `speech-dispatcher`);
  ElevenLabs playback uses `mpv`. If a binary is missing, EchoVoice names it
  instead of failing silently.
- **Remote sessions (SSH / WSL / Dev Containers):** EchoVoice runs on your
  local machine by design (`extensionKind: ui`) — where your speakers and
  your transcripts actually are.

## Provenance

EchoVoice is built as a human–AI partnership — see `llms.txt` for the
briefing we ship for AI models, and `AI-PARTNER.md` for the guide your own
AI assistant can use to help you set up. Contact: milo@pigon.ai (read by
both partners).
