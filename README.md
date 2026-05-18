# Audio QA Testing Web v1.3.2

Browser-based audio QA pre-screening tool. Open `index.html` in Chrome, Firefox, Edge, or Safari. No server, no install, no external dependencies.

## Features

| Feature | Details |
|---|---|
| Single-file upload | Drag-and-drop or browse — MP3, WAV, M4A, AAC, OGG |
| Live recording | MediaRecorder API — record from mic, analyse instantly |
| Download recording | WebM (original) or 16-bit PCM WAV |
| Batch upload | Drop multiple files; sequential queue with per-file cards |
| Per-card audio player | Play any batch file directly from its result card |
| Per-card waveform | Amplitude preview per file |
| Signal metrics | Peak dBFS, RMS, L/R balance, noise floor, silence gaps |
| QA flags | Clipping risk, volume, L/R imbalance — colour-coded |
| Single-file export | CSV + JSON — includes metrics + QA form fields |
| Batch CSV export | Aggregated CSV — one row per completed batch file |
| QA record form | Tester, device, environment, issue type, severity, judgment |

## Layout (v1.3.2)

1. Live Recording
2. Upload
3. Audio Player *(appears after file load)*
4. File Metadata
5. Signal Metrics
6. Waveform Preview
7. **Export — Single File** ← moved here in v1.3.2
8. Batch Upload — Multi-file Queue *(includes Export Batch CSV)*
9. QA Record
10. Limitations & Accuracy Notes

## How to use

1. Open `index.html` directly in a modern browser.
2. **Single file:** drag onto Upload zone or click Browse → review metrics → Export CSV/JSON.
3. **Batch:** drop multiple files onto Batch Upload → per-file cards render → Export Batch CSV.
4. **Record:** click Start Recording → Stop → metrics populate automatically.

## Version history

| Version | Change |
|---|---|
| v1.3.2 | Move single-file Export section to immediately after Waveform Preview |
| v1.3.1 | Per-card audio player with object URL lifecycle management |
| v1.3   | Batch upload / multi-file queue / per-file cards / aggregated CSV |
| v1.2   | Live recording (MediaRecorder), WebM + WAV download |
| v0.1   | Single-file upload, signal metrics, QA form, CSV/JSON export |

## Architecture

- Single `index.html` — no build tools, no bundler, no server required.
- All analysis via Web Audio API (`AudioContext.decodeAudioData`).
- Batch rendering uses DOM-swap adapters; `renderMetrics` and `drawWaveform` are never modified.
- Object URLs are revoked on Clear Queue and Reset All.
