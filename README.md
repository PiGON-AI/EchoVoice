# EchoVoice™ — hear your AI partner

**Milo speaks every reply, from every terminal agent, in his own window.** Claude Code, Codex CLI, Gemini or Kimi finishes an answer in the terminal; EchoVoice reads it aloud, each partner in its own voice, so your eyes stay on the code while your partners talk. Free local voices, no account, no telemetry. Your words go nowhere.

Built for **Claude Code**, **Codex CLI**, **Gemini / Antigravity**, and **Kimi Code** — each in its own voice, so you can run several partners at once and always know who's talking. Part of the [EchoTools](https://echotools.dev) suite by PiGON AI. **No telemetry — nothing about you or your code is collected.** Network use is limited to things you choose: a local engine's one-time, integrity-verified download, and ElevenLabs synthesis if you bring your own key.

[![EchoVoice — click for the full tour, narrated by Milo](images/tour-teaser.gif)](https://echotools.dev/#echovoice)

*▶ **[Watch the full tour — with Milo's voice](https://echotools.dev/#echovoice)** — or hear it inside the extension: **EchoVoice: Play Intro**.*

**Better together:** install **[EchoAvatar](https://marketplace.visualstudio.com/items?itemName=PigonAI.echoavatar)** and every voice plays through Milo — a living avatar with mouth-sync, a dance, and an ear tuned to your voice. Add **EchoMemory** and Milo remembers. The three are one companion and install as a ladder: EchoVoice works on its own; EchoAvatar brings EchoVoice with it; EchoMemory brings both. VS Code keeps the ladder whole, so it won't uninstall EchoVoice while EchoAvatar or EchoMemory needs it, and it names which one.

## Features

- 🔊 **Speaks new responses automatically** — watches your partners' conversation transcripts and reads each new reply aloud.
- 🎙️ **Four voices to choose from.** Best sound: ElevenLabs, with your own key. Best free and private, and the default we recommend: Kokoro. On a Mac the choices are Kokoro, ElevenLabs and the system voices; Piper is Windows and Linux.
  - **Kokoro** (recommended) — free, local, and the most natural of the free options. Twenty-nine voices (US / UK, male and female), plus three Halloween voices with a sound at the end (below). They share one model that downloads once, 92 MB, and EchoVoice asks before spending a byte; after that it's offline, and each extra voice is half a megabyte. Runs the same on Windows, macOS (Intel and Apple Silicon), and Linux. **It works your CPU**: on a modern machine it flows; on an older or smaller one, long replies can pause between sentences while the next one is made — see *Kokoro and your machine* in the FAQ before you decide it's broken. It isn't; it's the machine.
  - **Piper** (Windows and Linux) — free, local, *neural*, and much lighter on the machine: about 150 MB of memory while it speaks against Kokoro's 600 MB to 1 GB, and a sentence is made in a fraction of the time. Ten voices (US / UK / Scottish); the engine is 39 MB and each voice you pick is 63 to 121 MB, so on disk it is *not* the smaller choice — see *What it costs* below. The right pick for a slower machine. **Not offered on macOS:** the published Mac build never ran there (it is missing the libraries it needs), so a Mac speaks with Kokoro, and a Mac's own system voices are the light option.
  - **System voices** — free, offline, works out of the box (robotic on some systems). Also the automatic fallback if a local engine can't run, so you still hear your partner.
  - **ElevenLabs** — bring your own API key and voice ID for premium/cloned voices. The key is stored in VS Code's encrypted SecretStorage, never in settings files.
- 🎭 **A voice per partner** — give Claude Code, Codex, Gemini, and Kimi Code each their own voice, so you know who's speaking without looking.
- 🤖 **Milo's own voice** — the lines Milo speaks himself (a summary, a greeting, "Codex finished…") have their own row. By default he speaks in your computer's own voice, so he works everywhere with no download; give him any Kokoro, Piper, system or ElevenLabs voice, and he keeps it whatever engine your partners use. Kokoro on the partners and ElevenLabs on Milo works fine. He has his own mute row too.
- 🎨 **One glance, one speaker** — while someone talks, the status bar shows their mark and colour: Milo's robot, Claude Code's sparkle, Codex's terminal, Gemini's telescope, Kimi's rocket, in the same tints Milo's body glows in EchoAvatar. The name stays beside the mark, so colour is never the only cue.
- 🎤 **Voice input for EchoAvatar's push-to-talk** — hold the button in Milo's window, speak, and Milo answers. EchoVoice provides the speech-to-text pack (about 150 MB, once, after one card that names the size); EchoAvatar listens; what you say is transcribed on your machine. *Prepare voice input* in the menu downloads it ahead of time.
- 📖 **Teach Milo a word** — a name the voices say wrong, fixed in two questions from the menu; Milo says it back so you hear it before you keep it.
- ✂️ **Sentence cap** — off by default, so a spoken reply is read to the end; set N to hear only the first N sentences of long answers. (Which replies are spoken at all is the speak mode: *important* by default, which skips progress chatter.)
- 🔇 **One-click mute** — status bar toggle, always visible. It mutes this window until you reload it; to keep EchoVoice quiet for good, turn off `echovoice.enabled` in Settings.
- 📋 **Copy last response** — the full text, straight to your clipboard.
- 📄 **Export transcript** — turn any saved Claude Code conversation into a clean Markdown file.

## Halloween voices

Three voices for the season, under *Halloween* at the top of *Per-partner voices*: the **Witch** (thin and sharp, a flutter at the edges), the **Pumpkin** (low and hollow, with a growl) and the **Ghost** (wavering in a cold hall). Give one to a partner, or to Milo himself. Each is a blend of two Kokoro voices with its effect applied as it speaks, and each ends every reply with its sound: the Witch cackles, the Pumpkin laughs, the Ghost leaves a haunted hush. `echovoice.halloween.endSound` turns the sound off and keeps the voice. They were tuned by ear in a listening lab, not by numbers.

## The free voices, and the work behind them

Kokoro and Piper are open models anyone can download. What you get here is not the download; it is the listening in between. We did not build a new voice — we took an open one and taught it to read developer text, our ROAR-U way: *repurpose, optimize, adjust, recycle, upgrade* before building anything new. Every line below carries a number because we measured it on real replies, not because it sounded good in a meeting.

- **A dictionary built for Kokoro.** The pronouncing dictionary that ships with the free engine knew 126,000 words and none of `async`, `TypeScript`, `linter` or `middleware`. Kokoro's is now built from the very transcriptions the model was trained on — misaki's, used under their Apache-2.0 licence, with thanks — over CMUdict: **254,000 words**, every one checked against the model's own alphabet, plus a hand-written list of the names developers actually say: Supabase, Vercel, Kubernetes, nginx, Postgres, Vite, Prisma.
- **Words it does not know, read as words it does.** "EchoVoice" used to come out as "etch-uh-voice" and `changelog` as "chain-jel-og". A word missing from the dictionary is now read as two that are in it — echo and voice, hand and off, screen and shot, un and install — with the stress where English puts it.
- **Reading lessons from 400 real replies.** We surveyed what tripped the voices and taught them one lesson at a time: acronyms spelled or said (`CPU`, `README`), numbers with their units, commit hashes cut to seven characters, UUIDs as "an ID", filenames with versions, domains with their dots, plural acronyms (`LLMs`), `Date.now()`, and curly apostrophes, which had been turning "I'll" into "ill". A fourth round followed: words inside paths and members (`src/ui` is "source slash U I", `JSON.parse` is "jason dot parse"), a number with its unit read the way English says it ("a 30 second timeout"), initialisms like IIRC and AFAIK spelled, and 24 developer words (iterable, gRPC, zlib, mojibake…) each heard and kept by ear before it went in. On those replies, the words the engine had to guess at fell from **one in 37 to one in 330**.
- **Pauses, measured.** On a machine that synthesizes slower than it speaks, long replies paused between sentences. We measured the pipeline instead of guessing: Kokoro now uses more of a big machine's cores, starts from a short first sentence and keeps two ahead. On our test machine, dead air across a three-minute reply went from **9.8 to 2.6 seconds** and the first word arrives 1.3 seconds sooner. Every reply still writes its own receipt to the log.
- **Piper reads the same lessons** through its own engine, and stays the light choice for a slower Windows or Linux machine.

None of this is a switch you flip. It is in the box, it is free, and every number above was measured before it was written down; ask us for the receipt behind any of them.

## EchoMemory: Milo remembers

EchoMemory is Milo's memory. Save notes for yourself, project by project, and Milo remembers them: ask him what you noted, by voice or by typing, and he answers with your own words, where they came from, and when, in his own voice through EchoVoice. Ask him to sum up what you just told him, or one of your notes, and his version waits in your Inbox for your OK. Your notes are plain files in your project; the folder keeps itself out of git, and no AI coding tool is connected to them. When you talk to Milo, what you say and the notes he reads go to the brain you chose: your Copilot, Ollama on your own computer, or Ollama's cloud with your key. EchoMemory installs with EchoAvatar and EchoVoice, because the three make one companion.

## Quick start

1. Install EchoVoice.
2. Open a Claude Code session in VS Code and ask it anything.
3. When the response lands, EchoVoice speaks. That's it.

Click the **🔊 EchoVoice** item in the status bar to mute or unmute this window (a reload brings back your Settings choice, `echovoice.enabled`). Unmuting also clears an "off" saved in your Settings by an older version, so EchoVoice doesn't start muted again.

**Take the guided tour** — a five-step walkthrough with a narrated intro by
Milo (just under three minutes, full transcript included). It opens by
itself on a fresh install; to revisit it any time, open the Command Palette
and run **"Welcome: Open Walkthrough…" → Get Started with EchoVoice** — or
jump straight to the narration with **"EchoVoice: Play Intro"**.

## Using your own ElevenLabs voice

1. Run **EchoVoice: Set ElevenLabs API Key** from the Command Palette and paste your key (input is masked; stored encrypted). If an `ELEVENLABS_API_KEY` environment variable is present, it is used as a fallback.
2. Set `echovoice.elevenlabs.voiceId` in Settings to the voice you want.
3. Set `echovoice.provider` to `elevenlabs`.

If ElevenLabs is unreachable or misconfigured, EchoVoice falls back to your system voice instead of going silent.

## Commands

| Command | What it does |
| --- | --- |
| EchoVoice: Toggle Voice On/Off | Mute / unmute (same as the status bar click) |
| EchoVoice: Speak Last Response | Replay the most recent response |
| EchoVoice: Stop Speaking | Cut the current speech immediately |
| EchoVoice: Copy Last Response | Copy the full last response to the clipboard |
| EchoVoice: Export Conversation Transcript | Pick any saved conversation and save it as Markdown |
| EchoVoice: Set ElevenLabs API Key | Store your key in encrypted SecretStorage |
| EchoVoice: Clear ElevenLabs API Key | Remove the stored key |
| EchoVoice: Prepare Voice Input | Download the speech-to-text pack for EchoAvatar's push-to-talk, once (about 150 MB, after one card that names the size) |
| EchoVoice: Teach Milo a Word | Fix how every voice says a word: the word as written, then how it sounds; Milo says it back |

## Settings

| Setting | Default | Meaning |
| --- | --- | --- |
| `echovoice.enabled` | `true` | Speak new responses automatically |
| `echovoice.provider` | `system` | `system`, `kokoro`, `piper`, or `elevenlabs` |
| `echovoice.speakMode` | `important` | What deserves voice: `important` (skip progress chatter — the default), `everything`, or `questions-only` |
| `echovoice.toolCues` | `false` | Short spoken cues when your partner uses tools, in the free system voice |
| `echovoice.scope` | `workspace` | Speak only this window's project (`workspace`) or every session on the machine (`all`) |
| `echovoice.sources.claudeCode` | `true` | Speak Claude Code sessions |
| `echovoice.sources.codex` | `true` | Speak Codex CLI sessions |
| `echovoice.sources.antigravity` | `true` | Speak Gemini / Antigravity sessions |
| `echovoice.sources.kimi` | `true` | Speak Kimi Code sessions |
| `echovoice.maxSentences` | `0` | Sentences spoken per response (0 = all, the default) |
| `echovoice.pronunciations` | `{}` | Teach voices your words: `{ "Zustand": "zoo shtand" }` |
| `echovoice.readSymbols` | `false` | Speak code symbols as words (`=>` → "arrow") |
| `echovoice.announceUpdates` | `true` | One small toast after an update, naming what changed — never a release page |
| `echovoice.piper.voice` | `en_US-amy-medium` | Which of the ten Piper voices to speak with |
| `echovoice.piper.speed` | `1` | Piper speaking speed (0.5–2) |
| `echovoice.kokoro.voice` | `af_heart` | Which of the 29 Kokoro voices to speak with |
| `echovoice.kokoro.speed` | `1` | Kokoro speaking speed (0.5–2) |
| `echovoice.kokoro.threads` | `0` | CPU threads Kokoro may use; `0` = automatic (up to 8, leaving room for your editor). See *Kokoro and your machine* in the FAQ |
| `echovoice.systemVoice` | (OS default) | System voice name |
| `echovoice.rate` | `0` | System voice rate, −10…10 (Windows) |
| `echovoice.elevenlabs.voiceId` | — | Your default ElevenLabs voice ID |
| `echovoice.elevenlabs.modelId` | `eleven_turbo_v2_5` | ElevenLabs model |
| `echovoice.kokoro.voices` | `{}` | Per-partner Kokoro voices — easiest from the menu → *Per-partner voices*. The key `milo` is Milo's own voice: he keeps one, in whichever engine's list holds it, and the menu clears the others when you pick |
| `echovoice.halloween.endSound` | `true` | The Halloween voices end every reply with their sound; off keeps the voice without the sound |
| `echovoice.piper.voices` | `{}` | Per-partner Piper voices, e.g. `{ "codex": "en_US-bryce-medium" }` |
| `echovoice.elevenlabs.voices` | `{}` | Per-partner ElevenLabs voice IDs |
| `echovoice.system.voices` | `{}` | Per-partner system voice names |
| `echovoice.voice.<partner>` | — | **Legacy** (`claudeCode`, `codex`, `antigravity`, `kimi`). Held one voice for whichever engine was active when you set it. Still honored, then **moved automatically** into that engine's own list above the next time that engine speaks. Pick the engine first, then the partner's voice |

## How it works (and what it doesn't do)

Coding partners save conversations as transcripts on disk. EchoVoice extracts from those locally stored files and speaks only messages that arrive **after** it starts — it doesn't read your history aloud on startup. Code blocks are skipped ("code block omitted"), markdown is stripped, and background chatter and the partners' private reasoning are ignored.

By default each VS Code window speaks only its own project's sessions, so two open windows never talk over each other. Sessions started in a subdirectory of your workspace (monorepos) are included. Set `echovoice.scope` to `all` if you want one window to voice everything.

EchoVoice runs locally by design (`extensionKind: ui`) — in SSH, WSL, or Dev Container sessions it stays on your machine, where your speakers and your Claude Code transcripts actually live.

**Platform notes:**

- **Windows / macOS** — works out of the box (SAPI / `say`). On macOS the voices offered are Kokoro, ElevenLabs and System; Piper is not offered there.
- **Linux** — system voice needs `spd-say` (install your distro's `speech-dispatcher`); ElevenLabs playback needs `mpv`. If a binary is missing, EchoVoice tells you which one instead of failing silently. The voice input engine needs glibc 2.35 or newer (Ubuntu 22.04, Debian 12, Fedora 36 and later).
- **Voice input** is built for Windows x64, Linux x64 and Apple silicon Macs. On a Mac the first download takes a little longer to say it's ready: EchoVoice runs the new engine once, so your first words aren't kept waiting. On other machines the menu says so in one sentence instead of downloading anything.

EchoVoice contains **no telemetry and no analytics code** — that's checkable in this package, and [DISCLOSURES.md](DISCLOSURES.md) itemizes every byte that can ever leave your machine. The complete network surface is: (1) the one-time Kokoro or Piper model download from pinned, SHA-256-verified sources — only if you choose that voice, and only after you agree to it; (2) the one-time voice input pack (a speech-to-text engine and its model), from the same pinned, verified release — only when you hold EchoAvatar's talk button or run *Prepare voice input*, and only after you agree; (3) the synthesis request to ElevenLabs — only if you choose ElevenLabs with your own key — carrying the prepared text (code blocks are stripped before it is sent), your key, and normal API metadata. System voices make no network calls at all. Voice input itself never leaves your machine: EchoAvatar runs the engine locally and EchoMemory receives text only.

## What it costs

Measured, not guessed — on a 24-core laptop running Windows 11, on 2026-09-23, with the same runner the extension uses. A smaller machine is slower, not different; every number below has a receipt, and we will show it if you ask. EchoAvatar's README has the same section for Milo's window.

**Disk**

| What | Size | When |
|---|---|---|
| EchoVoice itself | 8.2 MB to download, about 23 MB on disk — 13.5 MB of it is the neural runtime, 6 MB is Kokoro's 254,000-word pronouncing dictionary | always |
| Kokoro model | 92 MB, once | when you pick Kokoro and agree to the download |
| each Kokoro voice | 0.5 MB | when you pick it |
| Piper engine (Windows and Linux) | 39 MB, once | when you pick Piper and agree |
| each Piper voice | 63 MB (medium quality), 121 MB (high) | when you pick it |
| Voice input pack | about 150 MB, once: a 148 MB English speech model plus a 2.6 MB engine (4.5 MB on Linux) | when you first hold EchoAvatar's talk button, or run *Prepare voice input*, and agree |
| System voices, ElevenLabs | nothing | — |

Plus a few kilobytes of bookkeeping: which replies have already been spoken (forgotten after a day) and how far each conversation was read.

**Memory**

| Engine | While speaking | Between replies |
|---|---|---|
| Kokoro | about 620 MB when it wakes, about 1 GB after a few paragraphs | held for five idle minutes, then released |
| Piper | 130 to 170 MB, in a fresh process per sentence | nothing |
| System, ElevenLabs | your OS's own, or a network request | nothing |

The extension itself is a file watcher and a small pipeline; your editor will not notice it.

**CPU and time**

- **Kokoro** made a 25-second paragraph in 19 seconds — 0.75× real time — on 8 threads, and is ready about a second after it wakes (model plus dictionary). It uses up to 8 threads and leaves your editor a core on any machine with more than two. On a machine that synthesizes *slower* than it speaks, long replies pause between sentences; the FAQ entry *Kokoro and your machine* explains the receipt it leaves in the log.
- **Piper** (Windows and Linux) made a 28-second paragraph in 2.6 seconds including starting its process — 0.10× real time. That is why it is the pick for a slower machine there; on a Mac the light pick is the system voice.
- **On a small machine** (we tested a mini PC) the same work is slower: Kokoro ran at about 0.86× real time, so a reply can take 5 to 10 seconds to start, and Piper's high-quality voices (like Ryan) are heavier too. There, Piper's **Amy** voice, or your system voice, is the light choice.
- **System voices** cost what your operating system's own voice costs, which is effectively nothing.
- **Voice input** transcribed a 7.5-second spoken sentence word for word in about one second on the same laptop, model load included. The work runs in EchoAvatar's process while you talk and stops when you let go.

**Network**

Nothing, apart from the downloads you agree to and, if you bring a key, ElevenLabs. For budgeting that: across 400 real replies from a coding partner, the typical reply was 600 characters (median), 1,200 on average and 3,600 at the long end, and ElevenLabs bills per character on your plan.

## A quick look

**Everything lives in the status bar** — one click opens the menu, in four groups: *Speaking* (mute, Stop, Replay with Copy inside), *Voices* (provider, per-partner voices, mute partners, how much to read), *Words and voice input* (Teach Milo a word, Prepare voice input) and *Help* (Get help from Milo, Show the EchoVoice log, Report a problem, Suggest an idea):

<img src="images/quick-menu.png" width="760" alt="The EchoVoice quick menu, opened from the highlighted status-bar item" />

**A voice per partner** — know who's talking without looking:

<img src="images/per-partner-voices.png" width="760" alt="Per-partner voice picker: Claude Code, Codex, Gemini, and Kimi Code each with their own voice" />

**Kokoro's 29 free local voices** — one 92 MB download, asked first, offline after:

<img src="images/kokoro-voices.png" width="700" alt="The Kokoro voice picker listing free local neural voices" />

**Milo's narrated intro** — audio plus a full transcript, works with the sound off:

<img src="images/meet-echovoice.png" width="760" alt="The Meet EchoVoice panel: audio player, speed controls, and full transcript" />

**The Get Started walkthrough** — five steps, each with its own guide page:

<img src="images/walkthrough.png" width="760" alt="The Get Started with EchoVoice walkthrough, open on the Pick a voice page" />

**Settings, filtered to Kokoro** — speed, threads, voice, per-partner voices:

<img src="images/settings.png" width="760" alt="VS Code settings filtered to echovoice kokoro: Speed, Threads, Voice and per-partner Voices" />

## Tips

- **Give each partner its own voice** (status-bar menu → *Per-partner voices*) so you always know who's talking without looking.
- **Want every word?** — EchoVoice speaks the important parts by default (`echovoice.speakMode`); set it to `everything` to hear progress chatter too.
- **Teach it your words** — menu → *Teach Milo a word*: the word as written, then how it sounds ("zoo shtand"); Milo says it back. It's stored in `echovoice.pronunciations` and works with every voice.
- **Mute the noisy ones** — menu → *Mute specific partners* to hear just one or two.
- **Calmer Piper** — raise `echovoice.piper.sentencePause` for more room between sentences.

## FAQ

**Does my code leave my machine?** Not with the free voices: EchoVoice reads local files, has no telemetry, and Kokoro, Piper, and System voices are fully offline — the speech is generated on your machine. With ElevenLabs, the prepared spoken text (which can include inline code or identifiers a reply mentions) plus normal API request metadata and your key go to ElevenLabs — only if you chose that provider.

**Is it free?** Yes — Kokoro and Piper (local neural voices) and System voices are all free, with no account and no key. ElevenLabs is optional and uses your own account.

**It only read a few sentences — why?** A sentence cap is set. The default reads everything; check the status-bar menu → *How much to read*. Settings are per editor.

**Nothing speaks.** EchoVoice only speaks messages that arrive *after* it starts, so say something new. Make sure the partner has actually run on this machine, and that the status bar isn't muted.

**Does it read my code aloud?** No — code blocks are skipped ("code block omitted").

**Kokoro and your machine — why does it sometimes pause between sentences?** Kokoro is a neural voice that runs entirely on your CPU, and how smoothly it flows depends on that CPU. EchoVoice speaks a reply in sentence-sized pieces and synthesizes the next piece while the current one plays. On a machine that synthesizes *faster* than it speaks, that hides the work and the reply flows; on an older or smaller machine that synthesizes *slower* than it speaks, each piece takes longer to make than the last one took to play, and the difference shows up as pauses between sentences on long replies. That isn't something we can fix in software beyond what's already there — it's the machine doing the work — so we tell you rather than let you wonder: every reply writes one line to the Output channel (*View → Output → EchoVoice*), `kokoro: pace — …`, that says how long the first word took, how long it spoke, how long it waited, and the engine's own speed as a multiple of real time. Under `1×` you're fine and any pauses are our chunking, which we keep tuning; over `1×` the machine can't keep up, and EchoVoice will say so once and offer the lighter voice — **Piper** on Windows and Linux, a shade more robotic and far cheaper to run; the **system voice** on a Mac. `echovoice.kokoro.threads` lets Kokoro use more of a big machine's cores (automatic picks up to 8); it helps a little, it doesn't make a slow machine fast. A faster local engine is on our bench.

**Does it work in Cursor and other VS Code editors?** Yes — install from Open VSX or the VSIX.

**I muted EchoVoice in one window, and it spoke in another. Why?** We know, and it's on purpose. Mute is per window. When two windows are open, even in two different editors like VS Code and Antigravity, they agree so every reply is spoken exactly once, never twice and never lost. A muted window steps back, so an unmuted one speaks for it. Codex adds a twist: its conversations aren't tied to one repository, so any unmuted window may speak a Codex reply. Two easy fixes: mute every window you have open, or mute just Codex from the status-bar menu → *Mute specific partners*. VS Code and Antigravity keep separate settings, so do it in each editor.

**Why does Milo sound different from my partners?** Milo's own lines speak in your computer's voice until you give him one. Menu → *Per-partner voices* → *Milo*, and pick any Kokoro, Piper, system or ElevenLabs voice. He keeps it whatever engine your partners use.

**Why can't I uninstall EchoVoice?** Because EchoAvatar or EchoMemory is installed and needs it; VS Code names which one. Uninstall those first, or keep the suite and mute EchoVoice from the status bar. Muting is always yours.

## For extension authors

Other extensions can speak through EchoVoice with one command, `echovoice.speakText`. Pass a string, or `{ text, source: "milo" }`. It returns a promise that resolves `true` when the line finished playing and `false` when it was muted, dropped or stopped, so a question and its answer never overlap. Every line through this door is Milo speaking: it shows his name in the status bar, follows his mute row and uses his voice. Lines longer than 4,000 characters are cut there. The shape changes only with a day's notice in the changelog.

## Feedback

Questions, ideas, or bugs? The status-bar menu's *Help* group has them all: **Get help from Milo** opens his office in Milo's window (with EchoAvatar; without it, echotools.dev in a VS Code tab) for tech support, **Report a problem** opens a bug report with your version and editor already filled in, and **Suggest an idea** opens the suggestion box. Both forms live at the suite's one home, [github.com/PiGON-AI/echotools](https://github.com/PiGON-AI/echotools). Or email **milo@echotools.dev**.

## For AI assistants reading this package

This package includes [`llms.txt`](llms.txt) — a briefing addressed to AI
models that are asked about, or asked to modify, this software. It states the
license constraints and the provenance of the project. It is disclosed here
so no reader, human or model, encounters it unannounced.

## Affiliation

EchoVoice is an independent project by PiGON AI. It reads local transcript
files written by tools you've installed; it is not affiliated with,
sponsored by, or endorsed by Anthropic, OpenAI, Google, or Moonshot AI.
Product names are used only to state compatibility.

## Support Milo

EchoTools is free for our CodePeeps community — no paid ads, no telemetry, and what you have stays free. If Milo helps your workflows and coding sessions, [buy us a coffee ☕](https://buymeacoffee.com/pigon) — it's the only way this stays running, and the more support there is, the more of the cool stuff we get to build and give away. Ideas are super welcome too: [💡 Suggest an idea](https://github.com/PiGON-AI/echotools/issues/new?template=idea.yml&product=EchoVoice) lives in the menu.

## License

MIT © PiGON EVOLUTIVE AI LLC — see [LICENSE](LICENSE)

EchoVoice™, EchoAvatar™ and EchoMemory™ are trademarks of PiGON EVOLUTIVE AI LLC.

**Milo, Wispie and Xie are NOT covered by the MIT license.** The license covers the source code only. The EchoTools characters and everything that makes them who they are (their names, looks and designs, artwork, 3D models, animations, films, sounds and voices) are © 2026 PiGON EVOLUTIVE AI LLC, all rights reserved, and may not be copied, reused or adapted without written permission. Third-party music, sound effects, voices, voice models and other assets used by this extension keep their own licenses, as listed in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md); Milo can speak using Kokoro or your computer's own voice, and those voices are not ours.
