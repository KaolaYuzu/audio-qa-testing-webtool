# Audio QA Testing Web v1.3.1

Browser-based audio QA pre-screening tool. Open `index.html` in any modern browser (Chrome, Firefox, Edge, Safari). No server, no install, no external dependencies.

## Features

| Feature | Details |
|---|---|
| Single-file upload | Drag-and-drop or browse — MP3, WAV, M4A, AAC, OGG |
| Live recording | MediaRecorder API — record from microphone, analyse instantly |
| Batch upload | Drop multiple files; sequential queue with per-file cards |
| Per-card audio player | Play any batch file directly from its result card |
| Per-card waveform | Amplitude preview per file |
| Signal metrics | Peak dBFS, RMS, L/R balance, noise floor estimate, silence gaps |
| QA flags | Clipping risk, volume level, L/R imbalance — colour-coded |
| Single-file export | CSV + JSON with full metrics + QA form fields |
| Batch CSV export | Aggregated CSV — one row per completed batch file |
| QA record form | Tester, device, environment, issue type, severity, judgment |
| Live recording download | Download as original WebM or converted 16-bit PCM WAV |

## How to use

1. Open `index.html` in Chrome, Firefox, Edge, or Safari.
2. **Single file:** drag a file onto the Upload zone or click Browse.
3. **Batch:** drop multiple files onto the Batch Upload zone, or click to browse.
4. Review per-file cards: play audio → check flags → export Batch CSV.
5. Fill in the QA Record form → Export CSV or JSON for single-file records.

## Version history

- v1.3.1 — Per-card audio player with object URL lifecycle management
- v1.3   — Batch upload / multi-file queue / per-file cards / aggregated CSV
- v1.2   — Live recording (MediaRecorder), WebM + WAV download
- v1.1   — Recording download (WebM)
- v0.1   — Single-file upload, signal metrics, QA form, CSV/JSON export

## Architecture notes

- Everything is in a single `index.html` — no build tools, no bundler, no server.
- All analysis runs in the browser via Web Audio API (`AudioContext.decodeAudioData`).
- Batch rendering uses DOM-swap adapters so `renderMetrics` and `drawWaveform` are never modified.
- Object URLs created by the batch player are revoked on Clear Queue and Reset All.
