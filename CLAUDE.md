# CLAUDE.md — scala-reels

Guidance for Claude Code when working in this repo. This is the **content** for
the **Scala** topic in [graphl-mobile](../graphl-mobile), the technical reels PWA.
The app fetches this content at runtime via raw GitHub; it is **not** bundled into
the app. Repo: `github.com/schemabotview/scala-reels`.

## Structure

```
scenes/   # currently EMPTY — SceneSpec data lives in graphl-mobile/src/data/scenes/<stem>.ts
tts/      # <stem>.tts — plain spoken prose (no markdown/code) for ChatterboxTTS
audio/    # <stem>.wav — generated narration, committed and served via raw GitHub
```

One reel = one `<stem>` shared across folders (e.g. `scala-execution-model.tts`,
`scala-execution-model.wav`). A scene's `audio` field defaults to its `id`.

## Pipeline (who does what)

1. **Scene** — author `graphl-mobile/src/data/scenes/<stem>.ts` and register it in
   `src/data/scenes/index.ts` (feed order = teaching order). `npm run build` is
   the only gate (runs DEV `validateLayout`).
2. **TTS** — write `tts/<stem>.tts` here: ~650–780 words (≈5 min), plain spoken
   prose, no markdown/code. Blank lines become ~300 ms pauses that pace reveals.
3. **Audio** — **the user** generates + pushes the `.wav` (Claude does not run
   the conda/audio/push step):
   ```bash
   # from ~/Apps/graphl-mobile:
   conda run -n chatterbox python scripts/generate_audio.py --topic scala
   ```
   Then commit + push the `.wav` here so it serves via raw GitHub.

## Scene index

Feed order matches the teaching order below. Legend: ✅ scene + tts done ·
🔊 audio generated · 🔲 not started.

| #  | Stem                    | Title                          | Scene | TTS | Audio |
|----|-------------------------|--------------------------------|-------|-----|-------|
| 1  | `scala-execution-model` | How Scala Runs on the JVM      | ✅    | ✅  | 🔲    |
| 2  | `scala-bindings`        | Anatomy of a Binding           | ✅    | ✅  | 🔲    |
| 3  | `scala-control-flow`    | Control Flow                   | ✅    | ✅  | 🔲    |
| 4  | `scala-oop`             | Object-Oriented Programming    | ✅    | ✅  | 🔲    |
| 5  | `scala-encapsulation-polymorphism` | Encapsulation & Polymorphism | ✅ | ✅ | 🔲 |
| 6  | `scala-objects`         | Objects & Companions           | ✅    | ✅  | 🔲    |
| 7  | `scala-functional`      | Functional Programming         | ✅    | ✅  | 🔲    |
| 8  | `scala-collections`     | Collections Library            | 🔲    | 🔲  | 🔲    |
| 9  | `scala-error-handling`  | Error Handling                 | 🔲    | 🔲  | 🔲    |
| 10 | `scala-concurrency`     | Parallel & Async Programming   | 🔲    | 🔲  | 🔲    |
| 11 | `scala-types`           | Type System & Generics         | 🔲    | 🔲  | 🔲    |
| 12 | `scala-contextual`      | Implicits / Givens             | 🔲    | 🔲  | 🔲    |

The OOP arc is a sub-series: `scala-oop` (abstraction + inheritance) → `scala-encapsulation-polymorphism` (the other two pillars) → `scala-objects` (singletons, companions, `apply`/`unapply`).
