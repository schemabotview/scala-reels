# scala-reels

Content for the **Scala** topic in [graphl-mobile](../graphl-mobile) — the
technical reels PWA. The app fetches this content at runtime; it is not bundled into the app.

## Structure

```
scenes/   # <stem>.ts (or .json) — SceneSpec data: nodes/edges/grid for one reel
tts/      # <stem>.tts — plain spoken prose (no markdown/code) for ChatterboxTTS
audio/    # <stem>.wav — generated narration, committed and served via raw GitHub
```

One reel = one `<stem>` shared across the three folders (e.g.
`scala-execution-model.ts`, `scala-execution-model.tts`,
`scala-execution-model.wav`). A scene's `audio` field defaults to its `id`.

`.wav` files are generated from `.tts` via local ChatterboxTTS (see
`graphl-mobile/CLAUDE.md`), then committed here so the app can load them.
Target up to ~5 min (~650–780 words) per scene — cover a concept and its parts in depth.

## Scene index

Feed order matches the teaching order below. Legend: ✅ scene + tts done · 🔊 audio generated · 🔲 not started.

| # | Stem | Title | Scene | TTS | Audio |
|---|------|-------|-------|-----|-------|
| 1 | `scala-execution-model` | How Scala Runs on the JVM | ✅ | ✅ | 🔲 |
| 2 | `scala-bindings` | Anatomy of a Binding | ✅ | ✅ | 🔲 |
| 3 | `scala-control-flow` | Control Flow | 🔲 | 🔲 | 🔲 |
| 4 | `scala-oop` | Object-Oriented Programming | 🔲 | 🔲 | 🔲 |
| 5 | `scala-functional` | Functional Programming | 🔲 | 🔲 | 🔲 |
| 6 | `scala-collections` | Collections Library | 🔲 | 🔲 | 🔲 |
| 7 | `scala-error-handling` | Error Handling | 🔲 | 🔲 | 🔲 |
| 8 | `scala-concurrency` | Parallel & Async Programming | 🔲 | 🔲 | 🔲 |
| 9 | `scala-types` | Type System & Generics | 🔲 | 🔲 | 🔲 |
| 10 | `scala-contextual` | Implicits / Givens | 🔲 | 🔲 | 🔲 |

## Generating audio

```bash
# from ~/Apps/graphl-mobile:
conda run -n chatterbox python scripts/generate_audio.py --topic scala
```

Then commit + push the `.wav` files in this repo so they serve via raw GitHub.
