# Third-Party Notices

EchoVoice ships some third-party code inside this package and downloads the
rest, at the user's request, from upstream projects. The two are listed
separately below, because the obligations differ.

## Bundled in this package

These files are redistributed inside the VSIX, unmodified. All are permissively
licensed; **no GPL or other copyleft code is bundled**.

- **ONNX Runtime 1.27.0** — [microsoft/onnxruntime](https://github.com/microsoft/onnxruntime),
  MIT License. Ships as `media/kokoro/ort/` (`ort.node.min.js`,
  `ort-wasm-simd-threaded.mjs`, `ort-wasm-simd-threaded.wasm`) and
  `media/kokoro/node_modules/onnxruntime-common`. Licence text:
  `media/kokoro/ort/LICENSE-onnxruntime.txt`; upstream's own third-party
  notices (protobuf, zlib, ONNX, Eigen and others) are reproduced verbatim in
  `media/kokoro/ort/LICENSE-onnxruntime-thirdparty.txt`.
  The same runtime is bundled by EchoAvatar for Milo's wake word.
- **HeadTTS `language-en-us`** — [met4citizen/HeadTTS](https://github.com/met4citizen/HeadTTS),
  MIT License (© 2025 Mika Suominen). Ships as `media/kokoro/g2p/`
  (`language-en-us.mjs`, `language.mjs`, `utils.mjs`). Licence text:
  `media/kokoro/g2p/LICENSE-headtts.txt`. This is the grapheme-to-phoneme
  converter used by the Kokoro voice; it deliberately uses **no espeak-ng**,
  which is why Kokoro adds no copyleft to this package.
- **CMUdict** — the pronunciation dictionary `media/kokoro/g2p/en-us.txt`
  derives from [CMU Pronouncing Dictionary](http://www.speech.cs.cmu.edu/cgi-bin/cmudict)
  0.7 (BSD-style licence, © 1993–2015 Carnegie Mellon University). The full
  copyright header is preserved inside the dictionary file itself.
- **NRL Report 7948** — the letter-to-sound fallback rules derive from
  *Automatic Translation of English Text to Phonetics by Means of Letter-to-Sound
  Rules* (Naval Research Laboratory, 1976). A work of the US Government:
  **public domain** (17 U.S.C. §105). Attributed here so it need not be
  re-audited.
- **Kokoro tokenizer** — `media/kokoro/g2p/tokenizer.json` is data from the
  Kokoro model distribution, Apache-2.0 (see below).

## Downloaded at runtime, at the user's request

Pinned versions, SHA-256-verified before installation (see llms.txt):

- **Kokoro-82M v1.0 (ONNX)** — [onnx-community/Kokoro-82M-v1.0-ONNX](https://huggingface.co/onnx-community/Kokoro-82M-v1.0-ONNX),
  **Apache-2.0**, derived from [hexgrad/Kokoro-82M](https://huggingface.co/hexgrad/Kokoro-82M).
  The model weights and voice tensors are downloaded on first use; a copy of
  the Apache-2.0 licence text is written beside them at install time.
- **Piper** text-to-speech engine — [rhasspy/piper](https://github.com/rhasspy/piper),
  MIT License. Piper embeds espeak-ng (**GPL-3.0**) for phonemization; the
  engine is executed as a separate downloaded program, not linked into or
  shipped with this extension. Choosing the Piper voice therefore places
  GPL-licensed software on the user's disk, under its own licence; it is never
  part of this package.
- **Piper voice models** — [rhasspy/piper-voices](https://huggingface.co/rhasspy/piper-voices);
  per-voice licensing is stated in each model's upstream card.

The optional ElevenLabs tier calls the ElevenLabs API with the user's own
key under the user's own ElevenLabs terms.
