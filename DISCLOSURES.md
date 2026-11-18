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
| Fish Audio synthesis | Every spoken reply, **only** while you've selected Fish Audio with your own API key | the request | `api.fish.audio` over HTTPS | — |
| OpenAI live voice | Every spoken reply, **only** while you've selected OpenAI with your own API key | the request | `api.openai.com` over a secure WebSocket (`wss://`), one short connection per piece of a reply | — |
| Get help from Milo / Send Feedback / Suggest an idea / What changed buttons | Only when you click one | Get help from Milo opens Milo's office in his own window when EchoAvatar is installed (the office page itself comes from echotools.dev; EchoAvatar's DISCLOSURES covers what it shares), otherwise a VS Code browser tab (your browser if the editor has none); the others open your browser | `echotools.dev/#milosoffice` for Get help from Milo (his office on our website, the same page anyone can visit); otherwise `github.com/PiGON-AI/echotools` (the suite's one public home for reports and ideas) — the feedback chooser (https-only; non-https values of `echovoice.feedbackUrl` are ignored), the fixed idea template, or the CHANGELOG (on `github.com/PiGON-AI/EchoVoice`) from the after-update toast | — |

**What the ElevenLabs request contains, exactly:** the prepared text of the
reply being spoken — code blocks are stripped *before* sending — plus your
API key (in a header) and normal API metadata. Nothing else. ElevenLabs'
handling of that request is governed by [their privacy policy](https://elevenlabs.io/privacy),
not ours. **The Fish Audio request** is the same: the prepared text (code blocks
stripped), your key in a header, the model you chose, the voice ID, and normal
API metadata; [Fish Audio's terms](https://fish.audio/terms) and
[privacy policy](https://fish.audio/privacy) govern it. **The OpenAI request**
carries the same prepared text with your key, the voice and the model, in one
of two ways (`echovoice.openai.longReplies`). By default (`summarize`), a reply
over about 1,200 characters is sent whole, in one request, with an instruction
to say a short summary of it; EchoVoice checks the summary that comes back
(it must start "In short:" and stay short) and asks once more if it doesn't;
if the second misses too, the better of the two plays.
Shorter replies, and every reply in `read` mode, are sent in pieces of a few
sentences with an instruction to read them exactly as written; a piece that
comes back with words missing is asked for once more. Either way a retried
request is billed too, and the Output log counts it.
[OpenAI's terms](https://openai.com/policies/terms-of-use) govern the request.
OpenAI's voices are AI-generated, and EchoVoice says so when you choose one.

**What "code blocks are stripped" covers:** every code block a CommonMark
editor would show as one, found by the markdown-it parser bundled in this
package: fenced blocks (three or more backticks or tildes, inside lists and
quotes too), indented code, and a block still being written when the reply
arrives, which is withheld to the end of its quote or list. Line endings
(LF, CRLF or a lone CR, even mixed) are read the way the parser reads them. A
triple-backtick span inside a sentence is withheld too, and if the parser
ever failed on a reply, the whole reply would be withheld. Inline code (a
single name in backticks) stays, because it is part of the sentence: a reply
that mentions a file name or a command says it.

**Raw-text HTML is withheld the same way:** a `<pre>`, `<script>`, `<style>`
or `<textarea>` element a reply writes out. One that opens at the start of a
line is withheld to its closing tag, or to the end of the reply if it is never
closed. One that opens in the middle of a sentence is withheld with the
paragraphs it runs through; if it is never closed, only its own paragraph is,
so a reply that merely mentions the tag, without putting it in backticks,
loses that one paragraph and not everything after it. A tag in backticks is
just a word. **Not covered:** any other HTML a reply writes out (a `<div>`, a
`<code>` element, a table) is not code to CommonMark, so its text is spoken,
and sent to a cloud voice you chose, as text.

**ElevenLabs, Fish Audio and OpenAI are third-party services.** When you choose one,
your partners' replies go to that company's servers with your own key, under
that company's terms. Please read them before you choose: it is your choice,
and it is between you and that service. PiGON stores nothing and sees nothing
of it, and is not responsible for the service you use. Kokoro, Piper (Windows
and Linux) and the system voice stay on your computer. EchoVoice says this
once, the first time a reply goes to each service, with a button to its terms.

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
by whatever voice you gave Milo. If that voice is an ElevenLabs, Fish Audio or OpenAI voice,
the text of Milo's line goes to that service with your key, exactly as a
partner's reply does.

**Your log stays yours.** EchoVoice's Output log never leaves VS Code: no
command hands it to another extension, and nothing sends it anywhere.

## Storage — what's on your disk and how to remove it

| what | where | remove it |
|---|---|---|
| ElevenLabs API key | VS Code **SecretStorage** (your OS keychain) — not in any settings file | "EchoVoice: Clear ElevenLabs API Key" |
| Fish Audio API key | VS Code **SecretStorage** (your OS keychain) — not in any settings file | "EchoVoice: Clear Fish Audio API Key" |
| OpenAI API key | VS Code **SecretStorage** (your OS keychain) — not in any settings file | "EchoVoice: Clear OpenAI API Key" |
| Kokoro / Piper models | the editor's global storage folder for this extension | delete the folder after uninstall, or before it via your OS file manager |
| Voice input pack (engine, model, and its MIT licence text) | the same global storage folder, under `whisper/` | delete that folder; the next hold of EchoAvatar's talk button asks again before downloading |
| Your taught words | the `echovoice.pronunciations` setting in your user settings (synced if you use Settings Sync) | *Teach Milo a word* with an empty second answer, or edit the setting |
| Temporary audio | your OS temp folder, deleted after playback | automatic |
| Spoken-reply claim ledger | `~/.echovoice/spoken` (tiny text ledger so two editors don't speak the same reply twice) | delete the folder any time |
| Window notes | `~/.echovoice/windows`: one small file per open editor window with the folders it has open, when you last used it, and which partners it would speak, so a Codex or Gemini reply is spoken in the window that has its folder open. Never sent anywhere; a closed window's file is removed, a crashed one's after a minute; a damaged or oversized file is ignored | delete the folder any time |

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
  A muted window steps back, so an unmuted window speaks instead. A Codex or
  Gemini conversation speaks in the window that has its folder open; when no
  window has it, in the window you used last. One exception to "windows
  cover for each other": if that home window has the partner muted, no other
  window speaks it. To silence a partner everywhere, mute it (*Mute specific
  partners*) in each editor, since VS Code and Antigravity keep separate
  settings.
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
