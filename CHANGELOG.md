# Changelog

## 0.11.5

- **The intro panel works with a screen reader and a keyboard.** The audio
  player has a name instead of being announced as an unlabelled player; the
  speed buttons say which one is switched on, and show a focus ring when you
  tab to them; the tip titles are real headings, so you can jump between them
  the way you'd skim any page; and the buttons stay visible in themes that
  don't define their own button colours. The written transcript was always
  there and always will be — it's the audio's text alternative, not a bonus.
- **🐛 Report a problem** — a new item in the 🔊 menu that opens a bug report
  with your extension version, editor and operating system already filled in,
  so you don't have to go digging through the Extensions panel to answer three
  questions about your own setup. If EchoVoice currently can't read one of your
  partners, it says so in the first line for you. Your log is **not** attached —
  it names your sessions and file paths, so it stays yours to trim and paste.
  Nothing is sent from here; it's a door you push, and you see everything
  before you press submit.
- **EchoVoice now tells you when a partner stops making sense.** Your coding
  partners each write their conversations to disk in their own private format,
  and when one of them changes it — usually after that tool updates itself —
  EchoVoice can go quiet with no explanation, which looks like EchoVoice broke.
  Now it notices. If a partner's records stop being anything EchoVoice
  recognizes, it says so once, names the partner, and Milo wears it on his face.
  Silence because nothing is happening finally looks different from silence
  because something is wrong.
- **Your per-partner voices move into their own engine's list.** The old
  `echovoice.voice.<partner>` setting held a single voice for whichever engine
  was active when you set it — which is why giving a partner a voice sometimes
  seemed to do nothing at all. It still works, and now it tidies itself: the
  next time that engine speaks, EchoVoice moves the voice into that engine's
  own per-partner list and clears the old setting. **Nothing is lost** — the
  voice hasn't vanished, it has a proper home. Pick your engine first, then
  give each partner a voice from it.
- **A reply that trails off in whitespace no longer sends an empty request** to
  the voice engine.
- **The sentence cap reads its real default.** A setting that fell back to the
  built-in value was quietly capped at three sentences while Settings showed
  `0` — speak everything.

## 0.11.4

- **Milo's emoji reactions land on cue again.** With the free local voices
  (Kokoro and Piper) a reply is spoken in pieces, and every reaction was
  arriving inside the first piece — so a 😄 halfway down a long answer fired
  at the very start. Each reaction is now dealt to the piece it belongs to
  and timed inside it. ElevenLabs was always right, and is untouched.
- **Per-partner voices explain themselves.** The settings now say a Kokoro
  voice key is welcome too — they only mentioned Piper, ElevenLabs and
  system before. And if a saved voice belongs to a different engine than the
  one you're using, EchoVoice tells you once instead of quietly falling back
  to the default: pick your engine first, then give each partner a voice
  from that engine.
- **💡 Suggest an idea** — a new item in the 🔊 menu that opens the
  suggestion box in your browser. Nothing is sent from here; it's a door you
  push.
- **A quiet word after an update.** When EchoVoice updates, one small toast
  names what changed and offers the full changelog — once per version, asked
  once, and never a release page that takes over your editor. Turn it off with
  `echovoice.announceUpdates`.

## 0.11.3

- EchoVoice wears its mark: ™ on the listing name and readme.
- The one-time review invitation (after 25 spoken replies, asked once,
  never again) now reads the way we actually talk.

## 0.11.2 — Initial public release

EchoVoice gives your AI coding partners a voice inside VS Code. This first
public release includes:

- **Four voice engines**: system voices (instant, offline), Kokoro — 29
  local neural voices from one 92 MB model, Piper — 10 local neural voices,
  and ElevenLabs with your own API key. Local engines download once, with
  your consent, integrity-verified — then work fully offline.
- **A voice per partner**: Claude Code, Codex CLI, Gemini / Antigravity, and
  Kimi Code each get their own voice, so you know who's talking without
  looking.
- **Speaks what matters**: questions, blockers, errors, and final answers by
  default — progress chatter is skipped, code blocks are summarized as
  "code block omitted", and everything skipped stays available via replay
  and Copy Last Response.
- **Exactly-once across windows**: two open editors don't talk over each
  other.
- **Made yours**: pronunciation lexicon, per-engine speeds, sentence cap,
  one-click mute, transcript export to Markdown.
- **Private by construction**: no telemetry or analytics code; every byte
  that can leave your machine is itemized in DISCLOSURES.md.
- **Pairs with EchoAvatar**: install Milo and every voice plays through him,
  mouth-synced.

Changes from here on are listed per release, in plain language.
