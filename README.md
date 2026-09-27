# SFX Editor

A single-file, browser-based sound-effects editor for trimming, cutting, reordering, and merging short audio clips (dialogue stingers, loops, foley, etc.) into one exported file. No build step, no server-side code, no dependencies — just static HTML/CSS/JS running on the Web Audio API.

## Features

- **Manifest-driven clip loading** — reads `audio/manifest.json` (a JSON array of filenames) and loads every listed file from the `audio/` folder on page load.
- **Add files manually** — "+ Add files" lets you load additional local audio files at runtime.
- **Waveform view** — per-clip waveform rendered to canvas, with zoom in/out.
- **Trim** — drag the start/end handles to trim the clip's usable range.
- **Cut** — drag-select a range on the waveform and delete it; multiple cuts per clip are supported and merged automatically.
- **Undo** — `Ctrl+Z` / `Cmd+Z` steps back through trim/cut edits.
- **Transport controls** — play, pause, stop, loop, and jump to previous/next clip.
- **Scrub / seek** — click the waveform, or click-and-drag the marker on the ruler, to move playback to any point; playback (when started) begins from there.
- **Per-clip volume** — adjustable gain per clip, applied both in the live preview and in the final export.
- **Reorder clips** — drag clips in the list to set the export order.
- **Configurable gap** — set a silence gap (ms) inserted between clips on export.
- **Export** — renders the full sequence (respecting trims, cuts, volumes, order, and gap) offline and downloads a merged `.wav` file.

## Project structure

```
.
├── index.html          # entire app: markup, styles, and logic
└── audio/
    ├── manifest.json   # JSON array of audio filenames to auto-load
    ├── clip-one.mp3
    ├── clip-two.mp3
    └── ...
```

To add your own clips: drop the audio files into `audio/` and list their filenames in `audio/manifest.json`, e.g.:

```json
[
  "clip-one.mp3",
  "clip-two.mp3"
]
```

Filenames with spaces or special characters are supported.

## Running locally

The app loads `audio/manifest.json` and the audio files via `fetch()`, which browsers block on the `file://` origin. You need to serve the folder over HTTP. From the project root:

```bash
# Python
python3 -m http.server 3000

# or Node
npx serve -l 3000
```

Then open `http://localhost:3000` in a browser.

## Browser support

Requires a browser with the Web Audio API (`AudioContext`, `OfflineAudioContext`) — current versions of Chrome, Edge, Firefox, Safari, and Brave.

## Notes

- All editing is non-destructive to the source files; trims/cuts/volume/order only affect the in-browser session and the exported file.
- Export format is 16-bit PCM `.wav`.

## License

UNKNOWN — add a license file/section if you intend to publish this publicly.
