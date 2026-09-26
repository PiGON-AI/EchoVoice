# Changelog

## 1.0.0

*Why this is 1.0: EchoVoice now tells you when a partner's format changes
instead of going quiet, Milo has been taught to read developer text, Kokoro
and Piper were rebuilt around what people actually heard, and every behaviour
that matters leaves a receipt in the log.*

- **A reply written while EchoVoice was restarting is spoken, not lost.**
  EchoVoice has always refused to read history aloud — nobody wants a hundred
  old replies on a Monday morning — but that rule had a hole: when the editor
  restarted it for a couple of seconds (an update installing, a reload), a
  reply your partner finished in that gap looked exactly like history and was
  dropped in silence. Now EchoVoice remembers how far it had read each
  conversation and when; on the way back up it speaks what arrived during a
  short gap (up to two minutes) and still skips anything older. Close the
  laptop over lunch and you get silence, as before; blink through a restart and
  you get the reply.
- **Milo reads developer text better on the free voices.** Kokoro and Piper
  never dropped a character — the stumbles were pronunciation and flow. We
  surveyed 400 real replies for what tripped them and taught the reader five
  things: acronyms are spelled when they should be (`CPU`, `PR`, `HTML`) and
  said as words when they are words (`README` → "read me", `OK` → "okay");
  numbers keep their units ("3.4 seconds", "92 megabytes", "0.72 times");
  a commit hash is its first seven characters spelled, not forty letters of
  noise, and a UUID is just "an ID"; long asides in parentheses get a breath
  around them; and dashes, ellipses and symbol runs (`->`, `!=`, `&&`) become
  the pause or the word they mean. ElevenLabs, which already reads these
  well, is untouched.
- **Kokoro knows twice as many words, and reads the ones it doesn't as two it
  does.** The words that still stumbled were not exotic English — they were
  developer words the dictionary lacked (`async`, `TypeScript`, `linter`,
  `middleware`) and words it knew glued together: EchoVoice came out
  "etch-uh-voice", `runtime` as "run-tim", `changelog` as "chain-jel-og".
  Kokoro's dictionary is now built from misaki's — the pronunciations the model
  was actually trained on, used under their Apache-2.0 licence with thanks
  (see THIRD_PARTY_NOTICES.md) — over CMUdict: 254,000 words instead of
  126,000. A word not in it is read as two words that are (`echo` + `voice`,
  `hand` + `off`, `screen` + `shot`, `un` + `install`), possessives get the
  right ending, and a short list of our own names and everyday tools (Supabase,
  Vercel, Kubernetes, nginx, Postgres…) is spelled out by hand. Round two of
  the reading lessons follows the same receipt: plural acronyms (`LLMs`,
  `URLs`), letters with numbers (`MP4`, `S3`), lowercase shorthand (`ps`,
  `src`, `dbt`), filenames with versions (`echovoice-0.11.4.vsix`), dotfiles,
  bare domains (`echotools.dev`), `Date.now()`, and `EventDetailModal`. Round
  three came from the panel that judged this build before release: prices
  (`$0.99`, `$10/month`), ranges (`100-200ms`, `10–20`), `userId`,
  `console.log`, "a 30s timeout" as thirty seconds while "a 90s kid" keeps
  its decade, and wordpress, timeseries and scriptable read as the two words
  they are. Measured on 400 real replies: the words the engine had to guess
  at fell from one in 37 to one in 300 — the rest is in the log, not in your
  ear.
- **Kokoro's pauses, measured and explained.** On some machines Kokoro
  synthesizes slower than it speaks, and long replies pause between
  sentences while the next one is still cooking — the most-reported Kokoro
  complaint. EchoVoice now measures that waiting time on every reply (it's in
  the Output log as `kokoro: pace`), and if it's real and repeated it tells
  you once what's happening and offers the lighter voice — Piper on Windows
  and Linux, your Mac's own voices on a Mac. Kokoro also
  uses more of your CPU when you have it: up to 8 threads instead of 4 on big
  machines, and no longer parks half the cores on a 4-core laptop. A new
  `echovoice.kokoro.threads` setting lets you set it yourself (0 = automatic).
  This helps; it does not make a slow machine fast — that's a bigger job we're
  working toward. And on machines that *are* fast enough, the remaining pauses
  turned out to come from uneven sentence lengths, not speed: a short sentence
  followed by a long one left the engine no time to get ahead. Replies now ramp
  up gently from a quick first sentence and keep two sentences cooking ahead
  instead of one, and Kokoro wakes up the moment your partner starts working
  rather than when the reply arrives — so the first word comes sooner.
- **Piper is Windows and Linux; a Mac gets Kokoro.** Piper's published macOS
  build never ran: the archive labelled for Apple Silicon holds Intel binaries
  and neither Mac archive ships the libraries the engine needs, so every Mac
  that tried it downloaded well over a hundred megabytes to be told so. Our
  Mac test window proved it to the byte, and Piper has left macOS. It is no
  longer in any menu there; a Mac whose settings still say Piper speaks with
  Kokoro and is told so once — the setting itself is left alone, so a Windows
  or Linux machine sharing the account keeps Piper — and the slow-machine
  hint offers the Mac's own system voices instead. Kokoro runs perfectly on Apple Silicon. On Windows and
  Linux Piper stays what it was: the light voice for a slower machine — and
  its download prompt now tells you the real sizes.
- **Three things EchoVoice does now leave a receipt in the Output log.** When
  a code block is skipped ("code block omitted"), when emoji reactions are
  dealt out across a long reply, and when the after-update toast is shown —
  or deliberately not shown, and why. None of this changes what you hear; it
  changes what can be checked. If something ever sounds off, the log now says
  what EchoVoice decided instead of leaving you to guess from memory.

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
