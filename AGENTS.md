# Audiveris

> **Workspace:** `../../AGENTS.md` | **Deep context:** `AGENTS-DEEP.md`
> **Fork of:** `Audiveris/audiveris` → `johanngj/audiveris`

Open-source OMR (Optical Music Recognition): PDF → MusicXML. Java, Swing UI, neural net classifier, Tesseract OCR.

**Goals:** Perfect playback (pitches, rhythms, durations) for TTBB choral + piano. Fully automated.

## Fork Workflow

```bash
# Sync with upstream
git fetch upstream && git merge upstream/master

# Push your changes
git push origin <branch>
```

## Structure

```
Audiveris/
├── app/src/main/java/org/audiveris/omr/
│   ├── sig/            # Symbol Interpretation Graph (core data)
│   ├── sheet/          # Sheet processing pipeline
│   ├── score/          # MusicXML export (ProxyMusic)
│   └── ui/             # Swing UI
├── docs/               # Handbook (Jekyll)
└── packaging/          # Cross-platform installers
```

## Where to Look

| Task | Location |
|------|----------|
| Entry point | `Audiveris.java`, `Main.java`, `CLI.java` |
| Domain model | `sig/inter/`, `sig/relation/` |
| Symbol recognition | `classifier/`, `glyph/` |
| MusicXML export | `score/` (ProxyMusic) |
| Processing steps | `step/` |

## Commands

```bash
./gradlew build              # Build
./gradlew run                # Run GUI
./gradlew run -PcmdLineArgs="--help"

# Batch transcribe
./app/build/install/app/bin/Audiveris -batch -export -transcribe input.pdf

# With debug images
./app/build/install/app/bin/Audiveris -batch -debug-images /tmp/debug -export -transcribe input.pdf

# Disable OCR (often improves note detection)
./app/build/install/app/bin/Audiveris -batch -constant org.audiveris.omr.text.tesseract.TesseractOCR.useOCR=false -export -transcribe input.pdf
```

## Anti-Patterns

- ❌ Use `src/main/resources/` (use `app/res/` instead)
- ❌ `class.newInstance()` (deprecated)
- ❌ JGoodies PanelBuilder (legacy)
- ❌ Observer/Observable (use PropertyChangeListener)

For debugging, OCR tuning, lyrics zone issues → see `AGENTS-DEEP.md`
