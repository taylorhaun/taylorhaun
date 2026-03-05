# Soundtrap & BandLab Research

*Research compiled March 2026. Relevant because Taylor worked at Soundtrap/Spotify for 6 years and these are the closest existing products to what we're building.*

---

## Soundtrap

### Company History

- **Founded**: April 2012 in Stockholm, Sweden
- **Founders**: Bjorn Melinder, Fredrik Posse, Gabriel Sjoberg, Per Emanuelsson
- **Acquired by Spotify**: November 2017 (~$30M estimated)
- **Sold back to founders**: June 2023 (undisclosed amount)
  - ~100 Spotify employees offered to join independent Soundtrap
  - Per Emanuelsson and Bjorn Melinder re-acquired
  - Spotify's second spin-out (also sold SoundBetter back in 2021)
- **Why Spotify sold**: Strategic shift away from music creation; AI tools crowding the space; BandLab reaching 60M+ users; pressure from major labels about upload volume
- **Current**: ~89 employees, 4 continents, $35M annual revenue (Aug 2025)

### Technology Stack

**Core web technologies:**
- **Web Audio API** — the foundation of everything
- **Web MIDI API** — MIDI controller support
- **MediaRecorder API** — audio recording
- **MediaStream API** — mic/input access
- Built-in: multi-track recording, software instruments, audio effects, reverbs, filters, guitar amp simulation — ALL via web standards

**Backend:**
- Google Cloud (App Engine, Cloud Dataflow)
- MySQL
- NumPy (audio processing)

**Key technical challenge: Latency**
- Audio latency is the #1 technical problem for browser DAWs
- "Monitoring" = real-time feedback from what you record
- Pipeline: mic → Web Audio processing → speakers, with latency at every step
- Latency varies dramatically across OS, browser, and audio stack
- This was presented at a W3C/SMPTE workshop by Soundtrap's Ulf Hammarqvist

### Features (2025-2026)

- **AI Vocal Cleanup**: Eliminates background noise (classmates, traffic) without compromising original audio
- **AI Beatmaker**: Auto-generative drum pattern creation
- **Smart Drummer**: MIDI drum patterns across genres
- **Vocal Tuner**: Real-time pitch correction to specified key/scale
- **Interactive Transcription**: Auto-generated text transcripts from voice recordings
- **Antares Auto-Tune**: Built-in
- **Patterns BeatMaker**: Step sequencer
- **Cultural Soundpacks**: Sitar, tabla, taiko, xalam, timbales + genre packs (Senegal Sounds, Taal, Impact, World Percussion)
- **68 new vocal presets** (recent)
- **LMS integrations**: Clever platform for schools

### Education Focus (2026)

Soundtrap published "2026: The Year of the Student Creator":
- AI floods schools with generic content → real skill is creative expression
- Students who create beats, record podcasts, produce songs develop: creative decision-making, iterative refinement, collaborative problem-solving, authentic storytelling, technical literacy
- ELL students build language skills through music composition
- Positioned as antidote to passive AI consumption

### What We Can Learn From Soundtrap

1. **Web Audio API + Web MIDI + MediaRecorder is proven at scale** — Soundtrap proves a full DAW runs in the browser
2. **Latency is the hardest problem** — plan for it, don't ignore it
3. **Google Cloud backend** — not strictly necessary for our scale
4. **The education angle is validated** — Soundtrap serves 50K+ schools
5. **AI features are additive, not core** — their AI (Vocal Cleanup, Smart Drummer) enhances the DAW, doesn't replace it
6. **Taylor's 6 years there = deep institutional knowledge** of what works and what doesn't

---

## BandLab

### Company Overview

- **Founded**: 2015
- **CEO**: Meng Ru Kuok
- **Employees**: 201-500
- **Valuation**: $425M (Series B1, $25M round)
- **Users**: 100 million registered
- **Parent company**: BandLab Technologies (also owns Cakewalk, ReverbNation, Airbit)

### Technology Stack

- 53 technologies in their stack (per Himalayas)
- Browser-based Mix Editor (Chrome, Edge, Firefox, Chromium-based)
- No third-party VST support in browser (web limitation)
- Cloud-native: auto-save, cross-device sync

### Features

**DAW:**
- Up to 16 tracks per project
- Dozens of virtual instruments (drums, bass, synth, piano, strings)
- 385+ VST Instruments total
- Professional effects: EQ, compression, reverb, delay, distortion, modulation
- Free vocal pitch correction, drum machine, sampler, synths, guitar amp sims
- Up to 50 collaborators per project

**AI Tools:**

1. **SongStarter** — AI idea generator (built with Google/TensorFlow)
   - Generates beats, melodies, chord progressions from mood input
   - Updated 2025: faster generation, more mood variations, better melody variety

2. **Smart Tools** — Extend, Recompose, Layer
   - Layer generates basslines, chords, drum patterns
   - Can swap sounds across 385+ virtual instruments

3. **Audio-to-MIDI** — Vocal → MIDI, Instrument → MIDI, Drums → MIDI

4. **Splitter (Stem Separation)** — 2-stem (free) or 4-stem, 6-stem for members
   - Can convert separated stems to editable MIDI

5. **Voice Cleaner** — Noise Remover, DeReverb, AutoEQ

6. **FX Preset Generator** — Text prompt → FX chain

7. **Palette** — Genre + key + BPM + instruments → matching loops from 250K+ samples

8. **AutoMix** — AI-adjusted volume and panning

9. **Voice Changer** — 17 AI voice transformations

**Spatial Audio:**
- Partnership with Sony (360 Reality Audio)
- Free spatial audio production for all 100M users
- Announced April 2025

### BandLab vs Soundtrap

| | Soundtrap | BandLab |
|---|---|---|
| **Users** | 10M+ | 100M+ |
| **Revenue** | $35M/yr | Undisclosed |
| **AI features** | Moderate (Vocal Cleanup, Smart Drummer) | Extensive (9+ AI tools) |
| **Business model** | Freemium + Education plans | Freemium + Membership |
| **Platform** | Browser | Browser + Mobile + Desktop (Cakewalk) |
| **Collaboration** | Real-time | Up to 50 collaborators |
| **Unique edge** | Education market, school integrations | Scale, AI depth, Sony partnership |
| **Ownership** | Independent (re-acquired from Spotify) | BandLab Technologies |

### What We Can Learn From BandLab

1. **Audio-to-MIDI is a killer feature** — we should implement this (Basic Pitch / Essentia.js)
2. **Stem separation is expected** — users want to isolate drums, bass, melody
3. **Text-to-FX is clever** — "describe your effect" → AI builds FX chain. Very achievable with Claude.
4. **SongStarter's approach** — generate from mood/genre/key, not just text prompts. Good UX pattern.
5. **Free is powerful** — BandLab hit 100M users by being free. Worth considering for growth.
6. **AI as creative assistant, not replacement** — every AI feature helps the user create, not replaces them
7. **The DAW-to-GAW shift** — BandLab frames it as "Generative Audio Workstation." That's essentially what we're building, but focused on education/practice rather than production.

---

## Implications for Our Build

### What Soundtrap/BandLab prove is possible in the browser:
- Multi-track recording and editing
- Real-time audio effects processing
- Software instruments and synthesizers
- MIDI controller input
- Audio-to-MIDI conversion
- Stem separation
- AI-powered analysis and generation
- Collaboration
- Pitch correction

### Where we differentiate:
- **They're DAWs. We're a practice partner.** They help you produce music. We help you get better at playing it.
- **Our "killer feature" is analysis + intelligent feedback.** Neither Soundtrap nor BandLab tells you "you rushed bars 3-4, your ii-V-I voice leading was choppy, here's an exercise to fix it."
- **Claude as the brain** gives us something neither has: a genuine musical conversation about what you just played.
- **MIDI-first input** is simpler than their full DAW approach. We don't need 16 tracks. We need one input → smart analysis.

### What we should steal:
- Audio-to-MIDI (from BandLab)
- Text-to-FX concept (from BandLab, via Claude)
- Smart Drummer patterns (from Soundtrap, via Tone.js)
- The education-first framing (from Soundtrap)

---

## Sources

- [Soundtrap Wikipedia](https://en.wikipedia.org/wiki/Soundtrap)
- [Spotify sells Soundtrap back to founders (Music Ally)](https://musically.com/2023/06/09/spotify-sells-its-music-creation-tool-soundtrap-back-to-its-founders/)
- [Soundtrap audio latency (W3C)](https://www.w3.org/2021/03/media-production-workshop/talks/ulf-hammarqvist-audio-latency.html)
- [Soundtrap DAW features](https://www.soundtrap.com/content/product/online-daw-features)
- [Soundtrap product updates](https://edu.soundtrap.com/product-updates-and-releases/)
- [2026: Year of the Student Creator](https://edu.soundtrap.com/2026-the-year-of-the-student-creator/)
- [BandLab AI Tools](https://www.bandlab.com/products/ai-tools)
- [BandLab Smart Tools](https://blog.bandlab.com/smart-tools-bandlab-ai-music-production/)
- [BandLab SongStarter](https://blog.bandlab.com/bandlab-ai-tools-best-ai-music-generator/)
- [BandLab Complete Guide (Audeobox)](https://www.audeobox.com/learn/bandlab/)
- [BandLab Wikipedia](https://en.wikipedia.org/wiki/BandLab)
- [From DAW to GAW (Making a Scene)](https://www.makingascene.org/from-daw-to-gaw-how-bandlab-studio-is-using-ai-to-redefine-music-production/)
- [BandLab Spatial Audio (Sony)](https://musictech.com/features/sony-bandlab-spatial-audio-production/)
