# Audio Generation Research

*Research compiled March 2026 for the Music Collaborator custom build.*

---

## AI Full-Track Generation (the Suno-like dream)

### Suno — The Gold Standard

- **Website**: [suno.com](https://suno.com)
- **Current model**: v5 (released September 2025)
- **What it does**: Text prompt → full song with vocals, lyrics, and instrumentals
- **Quality**: Industry-leading. v5 achieves ELO 1,293, dramatically ahead of all competitors
- **Architecture**:
  - Hybrid transformer + diffusion models
  - **Bark** (vocal model) + **Chirp** (instrumental model)
  - Compression/codec models tokenize audio for the transformer
  - Multi-step pipeline: lyric interpretation → melody → arrangement → post-processing
- **v5 capabilities**:
  - 44.1kHz audio (up from 24kHz in v3)
  - 30-second hooks to 8-minute epics
  - Persistent voice & instrument memory across generations
  - 10x faster than previous versions
  - Stem exports (vocals, bass, drums, etc.)
  - "Sample to song" — upload audio, expand into full track
  - Suno Studio (built-in DAW for editing sections)
- **API status**: NO official public API. Options:
  - Third-party providers (sunoapi.org, etc.) — reverse-engineered, legally gray
  - Self-hosted open source (gcui-art/suno-api on GitHub) — browser automation
  - v5 only available on Pro ($8/mo) and Premier ($24/mo) plans
- **Legal**: Settled $500M lawsuit with Warner Music Group (Nov 2025). Now has licensing partnerships with major labels.
- **Founders**: Mikey Shulman (CEO, Harvard Physics PhD), Georg Kucsko, Martin Camacho, Keenan Freyberg — all met at Kensho (financial AI)
- **Funding**: $375M total (Series C Nov 2025), 2M paid subscribers
- **Company history**:
  - Founded by ex-Kensho team, Cambridge MA
  - First released Bark (text-to-speech, 19K GitHub stars, MIT license)
  - Surveyed Bark users → pivoted to music generation
  - Dec 2023: public launch + Microsoft Copilot partnership
  - June 2025: acquired WavTool (web-based DAW)

### Udio

- **Website**: [udio.com](https://udio.com)
- **Current model**: v4 (2026)
- **What it does**: Text prompt → full songs with deep control over lyrics, timing, clarity
- **Quality**: Strong, especially for film scoring and production music. Settled copyright suit with UMG.
- **API**: Official Developer Platform launched 2025
  - Settings > Developer Portal → generate `UDIO_API_KEY`
  - Pro and Enterprise tiers only
  - Official SDKs for Python and Node.js
  - Async polling + webhook endpoints
  - 30-120 second generation time
- **Pricing**: Free tier, Standard $10/mo, Pro $30/mo (commercial rights)
- **New features (late 2025)**: Voice cloning (1 min audio → custom vocal avatar)
- **Best for**: Developers who need an actual API for AI music generation right now

### Soundverse

- **Website**: [soundverse.ai](https://soundverse.ai)
- **What it does**: AI music generation with multitrack stem separation
- **API**: Enterprise API platform launched, REST endpoints, Python/JS SDKs
- **Key features**:
  - Multitrack stem separation (isolate drums, bass, melody post-generation)
  - Autocomplete Intelligence (expand a melody fragment into full composition)
  - Lyrics timestamping, song section detection
  - V4 and V5 generation models
  - 99.9% uptime SLA
- **Pricing**: Tiered plans (indie → enterprise)
- **Recognition**: Ranked #1 AI Music API by ChatGPT, Claude, Gemini, etc.
- **Best for**: Developers who want stem-level control and ethical licensing

### Wondera

- **What it does**: AI music generation API
- **Quality**: Ranked #1 in 3 of 4 Meta music aesthetic metrics
- **Best for**: Comprehensive API-first music generation

---

## AI Music Generation APIs (with actual developer access)

| Service | API Available | Quality | Pricing | Best For |
|---------|:---:|---------|---------|----------|
| **Suno** | Unofficial only | Best overall | $8-24/mo subscription | Full song generation (no real API) |
| **Udio** | Official (Pro+) | Excellent | $10-30/mo | Film scoring, production music |
| **Soundverse** | Official | Very good | Tiered plans | Stem separation, ethical licensing |
| **Mubert** | Official | Good (generative, not composed) | $49/mo trial | Background music, jingles, ambient |
| **AIVA** | Official | Good (orchestral focus) | Tiered | Soundtracks, emotional music |
| **Wondera** | Official | Excellent | TBD | Highest aesthetic quality scores |
| **SOUNDRAW** | Web only | Good | Subscription | Royalty-free, downloadable stems |
| **Beatoven.ai** | Web only | Good | Subscription | Adaptive background music |

### Mubert API Details

- Generates unique music per request (not from a database of tracks)
- Controls: genre, mood, tempo, duration (jingles 5-30s, tracks, mixes up to 25min)
- Modular: regenerate specific elements (drums, melodies) without starting over
- Live streaming via WebRTC
- **Pricing**: No free tier. Trial $49/mo, Startup and Startup+ plans for monetization
- **Restrictions**: Cannot distribute on streaming services or register via Content ID

---

## Browser-Based Audio (for backing tracks without AI)

### Tone.js — RECOMMENDED for browser synthesis

- **Website**: [tonejs.github.io](https://tonejs.github.io/)
- **GitHub**: [Tonejs/Tone.js](https://github.com/Tonejs/Tone.js)
- **What it does**: Full Web Audio framework for synthesis, sequencing, effects
- **Capabilities**:
  - Synthesizers (AM, FM, subtractive, etc.)
  - Sampler (load audio samples, pitch-shift to fill gaps)
  - Sequencing and transport (play/pause/loop with tempo)
  - Effects (reverb, delay, chorus, distortion, EQ, compressor)
  - Polyphonic instruments
- **Limitation**: Sampler rounds to equal temperament (no microtonal)
- **Sound quality**: Synthetic, not "real" sounding. Good for functional backing tracks, not for album-quality production.
- **Best for**: Programmatic music playback, sequenced backing tracks, jam mode

### smplr — RECOMMENDED for realistic browser instruments

- **GitHub**: [danigb/smplr](https://github.com/danigb/smplr)
- **npm**: `smplr`
- **What it does**: Pre-built sampled instruments for Web Audio, zero setup
- **Instruments available**:
  - `SplendidGrandPiano` — high-quality piano samples
  - `DrumMachine` — drum kit samples
  - `Soundfont` — full General MIDI instrument set (MusyngKite or FluidR3_GM)
  - `Sampler` — custom sample loading
  - `Soundfont2Sampler` — load .sf2 files directly
  - Versilian instruments support
- **Pros**:
  - No server needed (samples hosted online)
  - Sounds decent out of the box
  - Modern replacement for soundfont-player
  - Easy to integrate
- **Best for**: Quick realistic-sounding instrument playback in browser

### WebAudioFont

- **GitHub**: [surikov/webaudiofont](https://github.com/surikov/webaudiofont)
- **What it does**: Full GM (General MIDI) instrument set for browser
- **Features**: 5-10 sound variations per instrument, reverb, EQ
- **Best for**: MIDI playback with full instrument coverage

---

## Voice & Singing Synthesis

### Top Models (2026)

| Model | Best For | Notes |
|-------|----------|-------|
| **Synthesizer V** | Most realistic singing | 300% faster rendering than v1, no GPU needed, human-level naturalness |
| **ACE Studio 2.0** | All-in-one AI music (vocals + instruments) | Released Dec 2025, 140+ AI voices, MIDI-to-performance instruments, $398-528 lifetime |
| **VOCALOID:AI** | Industry standard singing synthesis | Massive voicebank library, deep Cubase integration |
| **Fish Speech V1.5** | Open-source multilingual voice | Industry-leading open-source |
| **CosyVoice2-0.5B** | Real-time streaming voice | Ultra-low latency |
| **ElevenLabs** | Voice cloning (speech, not singing) | "Virtually indistinguishable" cloning, not singing-specific |

### ACE Studio 2.0 (Deep Dive)

Released December 2025. Most relevant for this project because it does **both** vocals AND instruments:

- **AI Vocals**: 140+ voice models, 8 languages, Verse25 vocal synth model
- **AI Instruments**: Violin, viola, cello, saxophone, trumpet, duduk — NOT sample libraries, generates performances from MIDI
- **Generative AI Kits**: "Inspire Me", "Music Enhancer", "Add a Layer"
- **DAW Integration**: VST/AU/AAX via ACE Bridge plugin
- **Tools**: Stem splitter, vocal-to-MIDI, lyric extraction
- **Ethics**: Models trained with artist partnerships + royalty shares
- **Pricing**: $398 (Artist) / $528 (Artist Pro) — lifetime license
- **Limitation**: Desktop app, not browser-based. Would need API or server-side integration.

---

## AI Synth & Instrument Models

| Tool | What It Does | Platform | Price |
|------|-------------|----------|-------|
| **FADR SynthGPT2** | Text-to-synth sample generation | Web | $10/mo (FADR Plus) |
| **Sistema (guk.ai)** | Text prompt → synth sounds | VST3/AU (desktop) | TBD |
| **NSynth Sound Maker** | ML-based sound exploration | Web (Google experiment) | Free |
| **Arturia Pigments 5** | 4-engine synth (wavetable, analog, sample, granular) | VST (desktop) | ~$199 |

---

## Recommendation for This Project

### Phase 1: MVP (no cost)
- **MIDI input** via Web MIDI API → exact note data, no generation needed
- **Tone.js** for simple metronome/click track
- **smplr** for realistic piano/instrument sounds in browser
- **Claude API** for the intelligent analysis

### Phase 2: Backing tracks
- **Tone.js + smplr** for programmatic backing tracks (drums + bass + chords)
- Quality: functional but synthetic. Good enough for practice.

### Phase 3: Real-sounding generation
- **Udio API** (official, Pro tier, $30/mo) — best option for actual API access to high-quality generation
- **Soundverse API** — if stem separation is important
- **Suno** — if/when they launch an official API, switch to this immediately

### Phase 4: Dream scenario
- **Suno official API** (when available) for full-track generation
- **ACE Studio** integration for realistic instrument performances from MIDI
- User plays → app analyzes → generates a backing track in their key/tempo/style → they play along

---

## Sources

- [Suno v5 Introduction](https://help.suno.com/en/articles/8105153)
- [Suno AI Deep Dive (eesel.ai)](https://www.eesel.ai/blog/suno)
- [How Suno AI Works (musicgeneratorai.io)](https://musicgeneratorai.io/posts/how-does-suno-ai-create-music)
- [Suno Company Profile (Wikipedia)](https://en.wikipedia.org/wiki/Suno_(platform))
- [Suno Funding (Sacra)](https://sacra.com/c/suno/)
- [Suno API Reality (aimlapi.com)](https://aimlapi.com/blog/the-suno-api-reality)
- [Udio Developer Guide (aitoolsdevpro)](https://aitoolsdevpro.com/ai-tools/udio-guide/)
- [Udio API (musicapi.ai)](https://musicapi.ai/udio-api)
- [Soundverse API Launch](https://www.soundverse.ai/blog/article/soundverse-launches-enterprise-api-platform-for-ai-music-and-song-generation)
- [Mubert API](https://landing.mubert.com/)
- [Best AI Music APIs 2026 (wondera.ai)](https://www.wondera.ai/tools/en/the-best-ai-music-api)
- [Best AI Music Generators 2026 (rokform)](https://www.rokform.com/blogs/rokform-blog/best-ai-music-generation-apps-2026)
- [Tone.js](https://tonejs.github.io/)
- [smplr on GitHub](https://github.com/danigb/smplr)
- [ACE Studio 2.0 Release](https://acestudio.ai/blog/ace-studio-2-released/)
- [Best Open Source Singing Voice Models](https://www.siliconflow.com/articles/en/best-open-source-models-for-singing-voice-synthesis)
- [Best AI Vocal Tools 2026 (Sonarworks)](https://www.sonarworks.com/blog/learn/best-ai-vocal-tools-2025)
