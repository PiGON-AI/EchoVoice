# DISCLOSURES — every byte, every kink, in one place

This page itemizes everything EchoVoice can send or receive over the
network, everything it stores on your machine, and the platform quirks you
might hit. It describes **this release as shipped** — each release's
disclosures describe that release. If you find this page and the code in
disagreement, that's a bug: [tell us](https://github.com/PiGON-AI/echotools/issues).

## Network — the complete list

EchoVoice contains no telemetry or analytics code. The table below is the
entire network surface. If it's not listed here, it doesn't happen.

| what | when | size | where from | verification |
|---|---|---|---|---|
| Kokoro model + selected voices (the three Halloween voices are three more half-megabyte files from the same release; their end sounds ship inside the package, nothing to download) | Once, only if you pick a Kokoro voice, only after you say yes to a consent dialog | ~92 MB model + ~0.5 MB per voice | `github.com/PiGON-AI/Echotools-Runtime` (our release, mirrored from [onnx-community/Kokoro-82M-v1.0-ONNX](https://huggingface.co/onnx-community/Kokoro-82M-v1.0-ONNX), Apache-2.0) | SHA-256 **and** exact byte size pinned in the extension source; mismatches are discarded |
| Piper engine (Windows and Linux; not offered on macOS) | Once, only if you pick a Piper voice, only after a consent dialog naming the sizes | ~39 MB | `github.com/rhasspy/piper` (pinned release `2023.11.14-2`) | SHA-256 pinned per platform archive |
| Piper voices | Same consent flow | 63 MB (medium) or 121 MB (high) per voice you pick | `huggingface.co/rhasspy/piper-voices` (pinned revision, never a moving branch) | SHA-256 pinned per voice + config |
| Voice input pack: speech-to-text engine (whisper.cpp) + English base model | Once, only when you first hold EchoAvatar's talk button or run *Prepare voice input*, only after you say yes to a consent card naming the size | ~150 MB: 147,964,211-byte model + 2.6 MB engine (Windows), 4.5 MB (Linux) or 4.6 MB (Mac) | `github.com/PiGON-AI/Echotools-Runtime`, release `whisper-v1`: the engine built in the open by that repository's own workflow from whisper.cpp commit `927cfce` (v1.9.4); the model re-hosted from [ggerganov/whisper.cpp](https://huggingface.co/ggerganov/whisper.cpp), MIT | SHA-256 **and** exact byte size pinned in the extension source; mismatches are discarded |
| ElevenLabs synthesis | Every spoken reply, **only** while you've selected ElevenLabs with your own API key | the request | `api.elevenlabs.io` over HTTPS | — |
| Get help from Milo / Send Feedback / Suggest an idea / What changed buttons | Only when you click one | Get help from Milo opens Milo's office in his own window when EchoAvatar is installed (the office page itself comes from echotools.dev; EchoAvatar's DISCLOSURES covers what it shares), otherwise a VS Code browser tab (your browser if the editor has none); the others open your browser | `echotools.dev/#milosoffice` for Get help from Milo (his office on our website, the same page anyone can visit); otherwise `github.com/PiGON-AI/echotools` (the suite's one public home for reports and ideas) — the feedback chooser (https-only; non-https values of `echovoice.feedbackUrl` are ignored), the fixed idea template, or the CHANGELOG (on `github.com/PiGON-AI/EchoVoice`) from the after-update toast | — |

**What the ElevenLabs request contains, exactly:** the prepared text of the
reply being spoken — code blocks are stripped *before* sending — plus your
API key (in a header) and normal API metadata. Nothing else. ElevenLabs'
handling of that request is governed by [their privacy policy](https://elevenlabs.io/privacy),
not ours.

**With system voices, Kokoro, or Piper selected, synthesis happens on your
machine and no text goes anywhere.**

**Voice input, when you turn it on in EchoAvatar, is transcribed on your
machine and EchoMemory receives text only; what EchoAvatar and EchoVoice
download, and what a spoken answer sends if you chose ElevenLabs, is in their
own DISCLOSURES.** EchoVoice's part is the download and its fingerprints:
EchoVoice never opens your microphone and never handles audio of your voice.
EchoAvatar records the clip and runs the engine on it; where that clip lives
and when it is removed is in EchoAvatar's DISCLOSURES.

**Milo's own lines** (a summary, a greeting, an answer from your notes) are spoken
by whatever voice you gave Milo. If that voice is an ElevenLabs voice, the
text of Milo's line goes to ElevenLabs with your key, exactly as a partner's
reply does.

**Your log stays yours.** EchoVoice's Output log never leaves VS Code: no
command hands it to another extension, and nothing sends it anywhere.

## Storage — what's on your disk and how to remove it

| what | where | remove it |
|---|---|---|
| ElevenLabs API key | VS Code **SecretStorage** (your OS keychain) — not in any settings file | "EchoVoice: Clear ElevenLabs API Key" |
| Kokoro / Piper models | the editor's global storage folder for this extension | delete the folder after uninstall, or before it via your OS file manager |
| Voice input pack (engine, model, and its MIT licence text) | the same global storage folder, under `whisper/` | delete that folder; the next hold of EchoAvatar's talk button asks again before downloading |
| Your taught words | the `echovoice.pronunciations` setting in your user settings (synced if you use Settings Sync) | *Teach Milo a word* with an empty second answer, or edit the setting |
| Temporary audio | your OS temp folder, deleted after playback | automatic |
| Spoken-reply claim ledger | `~/.echovoice/spoken` (tiny text ledger so two editors don't speak the same reply twice) | delete the folder any time |

EchoVoice reads the transcript files your AI coding tools already write to
your own disk. It doesn't copy them, upload them, or retain them — it
watches, extracts the newest reply, and speaks it.

## Platform notes — the kinks, up front

- **macOS:** Piper is **not offered**. The upstream Mac build is defective
  (the "Apple Silicon" archive holds Intel binaries and neither Mac archive
  ships the libraries the engine needs), so EchoVoice never downloads it on a
  Mac; the menus show Kokoro, ElevenLabs and System, and a Mac whose settings
  still say Piper speaks with Kokoro and is told so once — the setting is left
  alone, so a Windows or Linux machine sharing the account keeps Piper.
  **Kokoro runs natively on Apple Silicon** and is the free voice there.
- **Windows:** ElevenLabs MP3 playback uses Media Foundation, which some
  Windows 11 installs ship without. EchoVoice detects this and points you to
  the fix (Settings → Apps → Optional features → "Windows Media Player
  Legacy"). Kokoro, Piper, and system voices don't need it.
- **Linux:** the system voice uses `spd-say` (package: `speech-dispatcher`);
  ElevenLabs playback uses `mpv`. If a binary is missing, EchoVoice names it
  instead of failing silently. The voice input engine needs glibc 2.35 or
  newer (Ubuntu 22.04, Debian 12, Fedora 36 and later); we tested it in a
  clean Ubuntu 22.04 container, not yet on a Linux desktop.
- **Voice input** is built for Windows x64, Linux x64 and Apple silicon
  Macs (tested by ear on a Mac Studio, M3 Ultra). On a Mac, once the pack is
  verified, EchoVoice removes any "downloaded from the internet" mark from
  the engine (the engine is ad-hoc signed, not notarized by Apple, and macOS
  refuses a marked copy) and runs it once on a second of silence, on this
  machine, so its slow first launch happens during the download. On any
  other machine the menu says so in one sentence and downloads nothing.
- **The suite:** EchoAvatar requires EchoVoice, and EchoMemory requires both.
  VS Code won't uninstall EchoVoice while either is installed, and names which
  one. Muting EchoVoice, from the status bar or per partner, is always
  available.
- **Mute is per window, and windows cover for each other.** Open windows on
  one machine, across editors too, agree so each reply is spoken exactly once.
  A muted window steps back, so an unmuted window speaks instead. Codex
  conversations aren't tied to one repository, so any unmuted window may
  speak a Codex reply. To silence it everywhere, mute each open window, or
  mute Codex alone (*Mute specific partners*) in each editor, since VS Code
  and Antigravity keep separate settings.
- **Remote sessions (SSH / WSL / Dev Containers):** EchoVoice runs on your
  local machine by design (`extensionKind: ui`) — where your speakers and
  your transcripts actually are.

## Affiliation

EchoVoice is an independent project by PiGON AI. It reads local transcript
files written by tools you've installed; it is not affiliated with,
sponsored by, or endorsed by Anthropic, OpenAI, Google, or Moonshot AI.
Product names are used only to state compatibility.

## Provenance

EchoVoice is built as a human–AI partnership — see `llms.txt` for the
briefing we ship for AI models, and `AI-PARTNER.md` for the guide your own
AI assistant can use to help you set up. Contact: milo@echotools.dev (read by
both partners).
