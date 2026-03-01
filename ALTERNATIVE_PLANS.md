# Alternative Product Plans: Music Education AI

*Backup plans if the AI Practice Companion doesn't pan out.*
*Tailored for: side project pace, revenue-first, music production + piano, hybrid B2C→B2B*

---

## Plan B: AI Mix Coach — "MixMentor"

**One-liner**: "Upload your mix. Learn what to fix and why — like having a mixing engineer mentor on call."

---

### The Problem

Every day, thousands of beginner/intermediate producers finish a beat or mix and hit the same wall: **"How does my mix sound? What am I doing wrong?"**

Their options today:
1. **Post on Reddit** (r/mixingmastering, r/WeAreTheMusicMakers) — slow, inconsistent, often unhelpful
2. **Pay a mixing engineer** for feedback — $50-200/session, too expensive for learning
3. **Use AI mastering tools** (LANDR, Masterchannel, Cryo Mix) — these *do the work for you* but teach you **nothing**
4. **Watch YouTube tutorials** — generic, not tailored to YOUR mix

The critical gap: **existing AI tools master your track FOR you. Nobody teaches you HOW to mix better yourself.**

RoEx's Mix Check Studio comes closest (it analyzes and gives feedback), but it's surface-level — frequency balance charts and loudness meters. It doesn't explain *why* your low end is muddy, what specific frequencies to cut, how compression would help, or what your reference tracks are doing differently.

### The Product

MixMentor is a web app where you upload your mix (and optionally a reference track) and get **AI-powered coaching feedback** — not automated mastering.

#### Core Features (MVP)

**1. Upload & Analyze**
- Upload your mix (MP3/WAV, up to 10 min)
- Optionally upload a reference track ("I want my mix to sound like this")
- AI analyzes: frequency spectrum, dynamic range, stereo width, loudness (LUFS), transient clarity, tonal balance by frequency band

**2. AI Coach Report**
The key differentiator. Instead of just showing you graphs, Claude generates a **coaching report** written like a mentor talking to you:

```
🎧 MixMentor Report: "Late Night Beat v3.wav"

OVERALL: Your track has great energy and the arrangement works well.
The main issues are in the low-mid range and your vocal processing.
Here's what I'd focus on:

LOW END (Score: 6/10)
Your kick and bass are competing between 80-200Hz. The bass synth has
too much fundamental energy sitting right on top of the kick.

→ Try this: High-pass your bass synth at 80Hz and boost around
  800-1200Hz to let it cut through via harmonics instead of
  fundamental. This lets the kick own the sub-bass frequencies.

→ Reference comparison: Your reference track ("Blinding Lights") has
  a much cleaner separation — the bass sits above 100Hz and the kick
  punches through below.

VOCALS (Score: 5/10)
Your vocals sound dry and sit behind the mix instead of on top of it.
They need more presence and space.

→ Try this: Add a gentle boost at 3-5kHz for presence. Use a short
  plate reverb (0.8-1.2s decay) with the wet signal high-passed at
  600Hz so it doesn't mud up the low end.

DYNAMICS (Score: 7/10)
...
```

**3. Side-by-Side Comparison**
- Visual comparison of your mix vs. your reference track
- Frequency spectrum overlay, loudness comparison, stereo width comparison
- "Your track is 4 dB quieter in the 2-5kHz range than your reference — that's why it sounds less bright"

**4. Progress Tracking**
- Upload revisions of the same track → see how you improved
- Track your mixing skills over time across multiple projects
- "Your low-end control has improved 40% over your last 10 mixes"

**5. Learning Modules (v1.5)**
- Based on your common mistakes, MixMentor suggests short learning modules
- "You've struggled with vocal presence in 4 of your last 5 mixes. Here's a 5-minute lesson on vocal EQ and compression"

#### What Makes This Different from Competitors

| Feature | LANDR / Masterchannel | RoEx Mix Check | MixAnalytic | **MixMentor** |
|---------|----------------------|---------------|-------------|---------------|
| Auto-masters your track | Yes | Yes | No | **No** — teaches YOU |
| Shows frequency analysis | Basic | Yes | Yes | Yes |
| Explains WHY in plain English | No | Minimal | Basic | **Deep coaching** |
| Reference track comparison | No | No | No | **Yes** |
| Actionable "try this" steps | No | Generic | Generic | **Specific to YOUR mix** |
| Tracks improvement over time | No | No | No | **Yes** |
| Teaches mixing concepts | No | No | No | **Yes** |

### Technical Architecture

```
Frontend:  Next.js 15 + React 19 + TypeScript + Tailwind
Audio:     Web Audio API (playback/visualization)
Analysis:  Essentia.js (WASM, in-browser) for spectral/loudness analysis
           OR server-side Python (librosa + essentia) for deeper analysis
AI:        Claude API — receives structured analysis data, generates coaching report
Storage:   Supabase (auth, user data, analysis history)
Files:     Supabase Storage or S3 (audio uploads, temp)
Viz:       D3.js or Chart.js (frequency plots, comparisons)
```

**MVP is server-rendered analysis** — no real-time processing needed. Upload → analyze (5-10 sec) → display report. This is extremely lean.

### Monetization

| Tier | Price | Features |
|------|-------|----------|
| **Free** | $0 | 3 mix analyses/month, basic report |
| **Pro** | $9.99/mo | Unlimited analyses, reference comparisons, progress tracking, full coaching reports |
| **Team** | $29.99/mo | 5 seats, shared projects, perfect for producer collectives or small studios |
| **Edu** | $5/student/mo | Bulk licensing for music production programs at schools |

**Why $9.99/mo works**: A single session with a mixing engineer costs $50-200. MixMentor replaces that with unlimited AI coaching for $10/mo. The value proposition is obvious.

### Revenue Projections

| Timeframe | Users (Free) | Paid Subs | MRR | ARR |
|-----------|-------------|-----------|-----|-----|
| Month 3 | 2,000 | 200 | $2K | $24K |
| Month 6 | 8,000 | 800 | $8K | $96K |
| Month 12 | 25,000 | 2,500 | $25K | $300K |
| Month 18 | 50,000 | 5,000 | $50K | $600K |

### Go-To-Market

1. **Launch on ProductHunt** — "Grammarly for your music" angle
2. **Reddit**: r/mixingmastering (92K), r/WeAreTheMusicMakers (2.3M), r/edmproduction (510K), r/BeatMaking (101K) — these are literally communities of people asking "how does my mix sound?"
3. **YouTube content**: "I ran 10 famous songs through MixMentor — here's what it found"
4. **Music production YouTuber partnerships**: Give free Pro accounts to educators
5. **SEO**: "how to EQ vocals," "mixing bass and kick," "how to master a beat" — massive search volume

### Why This Works as a Side Project

- **MVP is tiny**: Upload form + audio analysis + Claude prompt + results page. Could be a working prototype in 2-3 weekends.
- **No real-time audio**: All async/batch processing. Much simpler than live instrument feedback.
- **Clear value from day one**: Even the free tier delivers immediate value.
- **Viral potential**: Producers share their mix reports, driving organic growth.
- **Your Soundtrap background**: You know the production workflow intimately. You know what beginners struggle with.

### Risks & Mitigations

| Risk | Mitigation |
|------|-----------|
| Claude's music analysis might be inaccurate | Combine structured audio analysis (Essentia) with LLM interpretation — Claude interprets data, not raw audio |
| RoEx improves their feedback | Your moat is the coaching + learning angle, not just analysis |
| Users want actual mastering, not coaching | Offer both — "learn mode" and "quick master" as separate features |
| Hard to retain users | Progress tracking + learning modules create ongoing value beyond one-time analysis |

---

## Plan C: AI Song Deconstructor — "SongLens"

**One-liner**: "Point it at any song. Understand exactly how it was made — chords, arrangement, production, theory."

---

### The Problem

Every musician — whether a producer, pianist, or guitarist — has the same experience:
**"I love this song. How do I play it? How did they MAKE it sound like that?"**

Their options today:
1. **Chord/tab sites** (Ultimate Guitar, Chordify) — chords only, often inaccurate, no production info, no theory context
2. **YouTube tutorials** — one person's interpretation, no standardization, takes 15 min for one song
3. **Sheet music** (Musicnotes, Sheet Music Plus) — expensive ($3-5/song), only shows notes, no production analysis
4. **Transcription by ear** — the gold standard but takes years of training
5. **AI chord detectors** (Chordify, Chord AI) — decent at chord detection but that's ALL they do

The gap: **nobody gives you the FULL picture of a song** — chords AND arrangement AND production techniques AND theory context AND a playable arrangement for your instrument, all in one place.

### The Product

SongLens is a web app where you paste a song link (or upload audio) and get a **complete deconstruction** — like having a music theory professor, a producer, and a piano teacher analyze the song together.

#### Core Features (MVP)

**1. Instant Song Breakdown**
Paste a Spotify/YouTube link or upload audio → get a full analysis:

```
🔍 SongLens: "Blinding Lights" by The Weeknd

KEY: F minor (relative major: Ab)
TEMPO: 171 BPM
TIME SIGNATURE: 4/4
ENERGY: High

CHORD PROGRESSION:
Verse:   Fm → Ab → Eb → Bb     (i → III → VII → IV)
Chorus:  Fm → Ab → Eb → Bb     (same progression, different energy)
Bridge:  Db → Eb → Fm           (VI → VII → i)

THEORY INSIGHT: This song uses a four-chord loop in F minor that
never resolves to a major chord — that's what gives it the
"nostalgic but melancholy" feeling. The constant motion between
Fm and Ab creates tension. Compare this to "Take On Me" by a-ha,
which uses the same key but resolves differently...
```

**2. Production Breakdown** (Differentiator #1)
For producers — what's actually happening in the mix:

```
PRODUCTION ANALYSIS:

SYNTHS: The iconic lead synth is a bright, heavily chorused saw wave
with a low-pass filter sweep. You can recreate this in Serum:
→ Oscillator: 2x saw waves, slightly detuned (+7 cents)
→ Filter: Low-pass, cutoff automated from 800Hz to 8kHz
→ Effects: Chorus (rate 0.5Hz, depth 60%), reverb (hall, 30% wet)

DRUMS: The kick is a tight 808 with a short decay (~100ms).
Snare is a gated reverb snare (classic 80s technique).
Hi-hats: 16th note pattern with velocity variation.

BASS: Sub-bass following the chord root, side-chained to kick
(-6dB, fast attack, medium release).

VOCALS: Double-tracked, slight pitch correction, plate reverb,
de-essing around 6-8kHz.
```

**3. Piano/Guitar Arrangement** (Differentiator #2)
For instrumentalists — a playable arrangement at YOUR level:

```
PIANO ARRANGEMENT (Intermediate):

Right hand: Melody + chord voicings
Left hand:  Root + octave bass pattern

   Fm          Ab          Eb          Bb
   ┌───────────┬───────────┬───────────┬───────────┐
RH │ Ab C F    │ C Eb Ab   │ Bb Eb G   │ F Bb D    │
LH │ F . F .   │ Ab . Ab . │ Eb . Eb . │ Bb . Bb . │
   └───────────┴───────────┴───────────┴───────────┘

Simplified (Beginner): Just play root position chords in the right
hand with single bass notes in the left hand.

Advanced: Add the synth melody line in the right hand while
comping chords — here's the voicing...
```

**4. "Songs Like This" Engine**
- "47 other songs use this same i-III-VII-IV progression"
- "Here are 12 songs with a similar production style"
- Creates learning paths: "If you can play Blinding Lights, try these next..."

**5. Theory Deep Dive**
- Every analysis includes contextual theory explanations
- "This chord progression works because..."
- "The bridge uses a deceptive cadence — here's what that means..."
- Adapts to user's theory level (beginner → advanced)

#### What Exists vs. What SongLens Does

| Feature | Chordify | Ultimate Guitar | Musicnotes | Hooktheory | **SongLens** |
|---------|----------|----------------|------------|------------|-------------|
| Chord detection | Yes | User-submitted | Manual | Manual | **AI-powered** |
| Production breakdown | No | No | No | No | **Yes** |
| Theory explanations | No | No | No | Some | **Deep, contextual** |
| Playable arrangements | No | Tabs (guitar) | Sheet music | No | **Multi-level, multi-instrument** |
| "Songs like this" | No | No | No | Yes | **Yes** |
| One place for everything | No | No | No | No | **Yes** |

### Technical Architecture

```
Frontend:   Next.js 15 + React 19 + TypeScript + Tailwind
Audio In:   Upload audio file, or server-side fetch from URL
Analysis:   Basic Pitch (audio → MIDI), Essentia (key, tempo, energy)
            Demucs (stem separation: vocals, drums, bass, other)
            Chord detection: autochord or madmom
AI Layer:   Claude API — interprets analysis data, generates:
            - Theory explanations
            - Production breakdowns
            - Arrangement suggestions
Notation:   VexFlow or Flat.io embed (render sheet music/tabs)
Database:   Supabase (users, saved analyses, progress)
Caching:    Cache song analyses — same song = instant result
```

**Key technical insight**: You DON'T need to analyze raw audio with Claude. The pipeline is:
1. **Structured analysis tools** extract data (chords, key, tempo, stems, spectral features)
2. **Claude receives structured data** and generates human-readable coaching/explanations
3. This is reliable, fast, and cost-effective

### Monetization

| Tier | Price | Features |
|------|-------|----------|
| **Free** | $0 | 3 song analyses/month, basic chord + key detection |
| **Pro** | $12.99/mo ($89.99/yr) | Unlimited analyses, production breakdowns, arrangements, theory deep dives |
| **Studio** | $24.99/mo | Everything + stem separation downloads, export arrangements as MIDI/PDF, API access |
| **Edu** | $6/student/mo | Bulk licensing for music schools, teacher dashboard, assignment integration |

**Additional revenue streams:**
- **Sheet music marketplace**: AI-generated arrangements, $1.99-3.99 per download (competes with Musicnotes at $3-5/song)
- **API licensing**: Other music apps integrate SongLens analysis ($0.05-0.10/analysis)
- **Affiliate**: Link to VST plugins, sample packs, and gear mentioned in production breakdowns

### Revenue Projections

| Timeframe | Users (Free) | Paid Subs | MRR | ARR |
|-----------|-------------|-----------|-----|-----|
| Month 3 | 5,000 | 250 | $3.2K | $39K |
| Month 6 | 20,000 | 1,500 | $19.5K | $234K |
| Month 12 | 60,000 | 5,000 | $65K | $780K |
| Month 18 | 120,000 | 12,000 | $156K | $1.87M |

Higher user counts than MixMentor because the TAM is broader — every musician, not just producers.

### Go-To-Market

1. **SEO / Content goldmine**: "Blinding Lights chords," "how to play [song] on piano," "how was [song] produced" — millions of monthly searches. Each analyzed song becomes an SEO landing page.
2. **TikTok / YouTube Shorts**: "Here's how [viral song] was actually made in 60 seconds" — this format is proven to go viral
3. **ProductHunt**: "Shazam for music education" angle
4. **Piano/guitar teacher communities**: Teachers use this to quickly prep lessons around songs students want to learn
5. **Music production forums**: Producers use the production breakdown to learn sound design

### Why This Works as a Side Project

- **MVP is focused**: Song upload → chord detection + key/tempo + Claude theory explanation. Could be a working prototype in 2-3 weekends.
- **Each analysis creates SEO content**: Every song analyzed becomes a searchable page. Organic growth compounds over time.
- **Viral mechanics built in**: People share "look what this AI found in [song]" — it's inherently shareable content.
- **Bridges your two interests**: Production breakdowns for producers, piano arrangements for pianists.
- **Natural B2B expansion**: Piano teachers and music schools NEED this for lesson prep.
- **Caching = cost efficiency**: Popular songs get analyzed once, served to thousands. Your API costs drop over time.

### Risks & Mitigations

| Risk | Mitigation |
|------|-----------|
| Chord detection accuracy | Combine multiple algorithms (Basic Pitch + autochord + LLM verification). Start with popular songs where accuracy is verifiable. |
| Copyright concerns with audio | Analyze uploaded audio only, don't host/redistribute. Arrangements are "educational use." Follow the Chordify/Ultimate Guitar model. |
| Chordify or Hooktheory add these features | Your moat is the COMBINATION — production + theory + arrangements + AI coaching. No one does all four. |
| Production breakdowns might be inaccurate | Frame as "AI interpretation" not gospel. Users will still find it valuable as a starting point. Improve with user feedback. |

---

## Comparison: All Three Plans

| Factor | Plan A: Practice Companion | Plan B: MixMentor | Plan C: SongLens |
|--------|---------------------------|-------------------|-----------------|
| **MVP Complexity** | Medium (real-time audio) | **Low** (upload → analyze) | **Low** (upload → analyze) |
| **Time to MVP** | 6-8 weekends | **2-3 weekends** | **3-4 weekends** |
| **Market Size** | $4B+ | $862M (DAW) + overlap | $4B+ (all musicians) |
| **Competition** | Yousician, Simply Piano | RoEx, LANDR (different angle) | Chordify, Hooktheory (partial) |
| **Differentiation** | Theory + real-time coaching | Teaching vs. doing | All-in-one deconstruction |
| **Viral Potential** | Medium | Medium | **High** (shareable content) |
| **SEO Potential** | Low | Medium | **Very High** (per-song pages) |
| **B2B Potential** | Strong (schools) | Medium (production schools) | Strong (all music schools) |
| **Revenue Ceiling** | Very High | Medium | High |
| **Side Project Fit** | Hardest (real-time) | **Easiest** | Easy |
| **Your Background Fit** | Strong | **Very Strong** (Soundtrap) | **Very Strong** (both) |

### My Recommendation Order

1. **Plan C (SongLens)** if you want the fastest path to revenue with the broadest market. It has the best viral/SEO mechanics, bridges both your production and piano interests, and the MVP is lean. High ceiling too — every song is potential content.

2. **Plan B (MixMentor)** if you want to stay closer to music production. Easiest MVP, very clear value prop, directly leverages your Soundtrap knowledge. Lower ceiling but faster to profitability.

3. **Plan A (Practice Companion)** if you're willing to invest more upfront for the biggest long-term play. Highest ceiling but hardest MVP due to real-time audio requirements.

**Plot twist**: Plans B and C could also be **features** that eventually fold into Plan A as the platform matures. Start with SongLens (easiest, best organic growth), add MixMentor (production coaching), then layer on real-time practice companion features. This is a crawl-walk-run strategy.
