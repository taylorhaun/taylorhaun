# Browser Audio Analysis Libraries Research

*Research compiled March 2026 for the Music Collaborator custom build.*

---

## Pitch Detection Libraries

### Pitchy — RECOMMENDED for MVP

- **What**: Simple pitch detection using McLeod Pitch Method
- **GitHub**: [ianprime0509/pitchy](https://github.com/ianprime0509/pitchy)
- **npm**: `pitchy` (v4.1.0, MIT license)
- **How it works**: `PitchDetector.findPitch(input, sampleRate)` returns detected pitch in Hz + clarity score (0-1)
- **Pros**:
  - Dead simple API — one function call
  - Fast enough for real-time use (designed for tuners)
  - Pure JavaScript, no WASM dependencies
  - ESM-only (v4+), modern
  - Lightweight
- **Cons**:
  - Only detects single pitch (monophonic)
  - No chord detection, no tempo, no key — just pitch
  - ESM-only may need dynamic import for CommonJS
- **Best for**: Real-time single-note pitch detection (tuner-style), simple MVP
- **React Native variant**: `react-native-pitchy` exists (different algorithm)

### Essentia.js — RECOMMENDED for full analysis

- **What**: Full audio analysis library (WASM port of Essentia C++)
- **GitHub**: [MTG/essentia.js](https://github.com/mtg/essentia.js/)
- **Developed by**: Music Technology Group, Universitat Pompeu Fabra, Barcelona
- **Capabilities**:
  - Onset detection, beat tracking, tempo estimation
  - Pitch extraction (PitchMelodia algorithm)
  - Key and chord estimation
  - Melody extraction
  - Loudness metering
  - Spectral features (MFCCs, etc.)
  - Genre/mood classification (with pre-trained models)
- **Pros**:
  - Most comprehensive browser audio analysis library available
  - WASM-powered = near-native performance
  - Real-time analysis via AudioWorklet
  - Academic-grade algorithms (published research papers)
  - TypeScript API available
  - Supports both real-time and offline analysis
- **Cons**:
  - Heavier than Pitchy (WASM bundle)
  - Under rapid development, APIs may change
  - Some algorithms are slow (pYIN pitch: up to 55% of audio duration)
  - MFCCs can be slow (up to 29% of audio duration in worst case)
  - Steeper learning curve
- **Performance**: Most algorithms run in 1.5-6.8% of audio duration. Some (MFCCs, pYIN) significantly slower.
- **Best for**: Serious audio analysis — when you need more than just pitch

### aubio.js

- **What**: JavaScript port of aubio (C library for audio analysis)
- **Capabilities**: Pitch detection, onset detection, tempo estimation
- **Pros**: Well-established algorithms (aubio is battle-tested in C)
- **Cons**: Less actively maintained than Essentia.js, smaller feature set
- **Best for**: If you want aubio's specific algorithms in the browser

### Meyda.js

- **What**: Audio feature extraction library
- **Capabilities**: RMS, ZCR, spectral features, MFCCs, chroma
- **Pros**: Simple API, good for visualizations, lightweight
- **Cons**: Lower-level than Essentia — gives you features, not musical analysis
- **Best for**: Audio visualizations, feeding features into your own analysis

---

## Web MIDI API

### Browser Support (2026)

| Browser | Support |
|---------|---------|
| Chrome (desktop & Android) | Full support (v43+) |
| Edge | Full support (v79+) |
| Firefox | Full support (v109+) |
| Opera | Full support (v30+) |
| **Safari (desktop & iOS)** | **NOT SUPPORTED** |
| Firefox Android | NOT supported |

- **Compatibility score**: 63/100
- **Safari**: Apple explicitly refused to implement Web MIDI due to fingerprinting concerns (announced 2020). This is unlikely to change.
- **Workaround for Safari**: Jazz-Plugin v1.4+ (requires user install)

### What MIDI Gives You

- **Note On/Off**: Exact note with velocity (0-127)
- **Control Change (CC)**: Knobs, sliders, mod wheel, sustain pedal
- **Pitch Bend**: Pitch wheel data
- **Program Change**: Instrument/patch selection
- **Timing**: Precise timestamps on all events

**Key insight**: MIDI gives you exact note data. No pitch detection needed. This is dramatically simpler than mic-based analysis for the "I play something, it tells me what I played" demo.

### WEBMIDI.js — RECOMMENDED

- **GitHub**: [djipco/webmidi](https://github.com/djipco/webmidi)
- **Website**: [webmidijs.org](https://webmidijs.org/)
- **npm**: `webmidi`
- **What it does**: Wraps the low-level Web MIDI API with human-friendly functions
  - `playNote()`, `sendPitchBend()`, etc.
  - Event listeners: `noteon`, `pitchbend`, `controlchange`
  - No need to parse MIDI bytes manually
- **Pros**:
  - Massively simplifies MIDI in the browser
  - Works in browser and Node.js (v3+)
  - Well-documented, active development
- **Best for**: Any project using MIDI controllers in the browser

---

## Music Notation Rendering

### VexFlow — RECOMMENDED

- **What**: TypeScript library for rendering music notation & guitar tab
- **GitHub**: [vexflow/vexflow](https://github.com/vexflow/vexflow) (~3.9k stars)
- **Output**: HTML5 Canvas & SVG
- **Current version**: VexFlow 5
- **Approach**: Programmatic API (EasyScore for high-level, Factory for full control)
- **Pros**:
  - Fine-grained control over complex scores
  - 10+ years of development
  - MIT license
  - Works in browser and Node.js
  - Can render notation from programmatic input (perfect for "show what you played")
- **Cons**:
  - Steeper learning curve (API-driven, not text-based)
  - No built-in MIDI playback
- **Best for**: Rendering notation from detected/MIDI notes programmatically

### abcjs

- **What**: Renders ABC notation (text-based music format) to sheet music
- **Website**: [abcjs.net](https://www.abcjs.net/)
- **GitHub**: ~2.2k stars
- **Output**: SVG
- **Approach**: Text-based (write ABC notation string, renders to score)
- **Pros**:
  - Much simpler to get started
  - Built-in MIDI playback
  - Plugins for Obsidian, VSCode
  - Lower learning curve
- **Cons**:
  - Less control over complex layouts
  - ABC notation is its own format to learn
- **Best for**: Quick text-to-score rendering, educational contexts

### OpenSheetMusicDisplay (OSMD)

- **What**: Renders MusicXML in the browser (built on VexFlow)
- **Best for**: If you have MusicXML data (e.g., from notation software)

### Bridge: abcjs-vexflow-renderer

- Combines abcjs parser with VexFlow renderer
- Gets you ABC notation input with VexFlow's rendering quality
- Works in React Native too

---

## Audio-to-MIDI

### Basic Pitch (Spotify)

- **What**: Audio-to-MIDI conversion model
- **Created by**: Spotify (open source)
- **Capabilities**: Converts audio recordings to MIDI note data
- **Limitation**: Primarily a Python model — browser version would need WASM port or server-side processing
- **Best for**: "Show me what I played" from audio files (not real-time)

---

## Recommended Stack for This Project

### Phase 1 (MVP — MIDI-first)

| Need | Tool | Why |
|------|------|-----|
| MIDI input | **WEBMIDI.js** | Wraps Web MIDI API, gives exact note data, no pitch detection needed |
| Notation display | **VexFlow** | Programmatic = easy to render from MIDI note events |
| Basic pitch detection (for mic later) | **Pitchy** | Simple, fast, good enough for single notes |

### Phase 2 (Full audio analysis)

| Need | Tool | Why |
|------|------|-----|
| Comprehensive analysis | **Essentia.js** | Key detection, chord estimation, tempo, melody — the whole package |
| Audio-to-MIDI | **Basic Pitch** (server-side) | Convert recordings to MIDI for notation display |

### Architecture

```
MIDI Keyboard → Web MIDI API → WEBMIDI.js → Note events (exact data)
                                              ↓
                                        VexFlow (notation display)
                                              ↓
                                    Structured text → Claude API
                                              ↓
                                    Intelligent feedback to user

Microphone → Web Audio API → Pitchy/Essentia.js → Pitch/chord/key data
                                                        ↓
                                                  (same pipeline as above)
```

---

## Sources

- [Essentia.js](https://mtg.github.io/essentia.js/)
- [Pitchy on GitHub](https://github.com/ianprime0509/pitchy)
- [Pitchy on npm](https://www.npmjs.com/package/pitchy)
- [WEBMIDI.js](https://webmidijs.org/)
- [Web MIDI API on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_MIDI_API)
- [Web MIDI API browser support](https://caniuse.com/midi)
- [VexFlow](https://www.vexflow.com/)
- [abcjs](https://www.abcjs.net/)
- [Audio Analysis with Essentia.js (ISMIR)](https://transactions.ismir.net/articles/10.5334/tismir.111)
