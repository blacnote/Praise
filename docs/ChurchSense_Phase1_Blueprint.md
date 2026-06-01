# ChurchSense — Phase 1 Product Blueprint

**A worship-service operating system for the local church.**
*By DLGSENSE*

> **Core principle:** ChurchSense follows worship. Worship does not follow ChurchSense.

---

## 1. Product Summary

ChurchSense is a worship-service operating system that helps a church **plan, run, and control** its praise-and-worship services from one place.

Most music software treats a service like a backing track: press play, and the song runs start to finish on a timeline. Real worship does not work that way. The Holy Spirit may lead the worship leader to **hold a moment, pray, meditate, repeat a chorus, vamp on a bridge, or extend a song** well past what was planned. ChurchSense is built around that reality.

ChurchSense acts as the **brain** of the worship service. It builds the worship set, plays back separated instrument stems, generates the click and guide cues the team needs in their ears, keeps the house mix clean, and stays in step with ProPresenter for lyrics and slides — while always leaving the worship leader free to follow where the Spirit leads.

Phase 1 is intentionally focused: a dependable foundation that a worship team can trust on a Sunday morning, without custom hardware and without forcing worship into a rigid timeline.

---

## 2. Phase 1 Features

### 2.1 Worship Set Builder
- Add songs to a service set.
- Arrange and reorder the worship order.
- Calculate **total estimated worship time** for the set.
- Track **elapsed time** and **remaining time** live during the service.
- Jump directly to a specific song (e.g., "go to Song 2 of 3").

### 2.2 Song Data
Each song stores:
- Title
- Artist / origin
- Key
- Tempo / BPM
- Lyrics
- **Sections** — intro, verse 1, chorus, verse 2, bridge, vamp, outro, tag, etc.
- Estimated length per section and per song

### 2.3 Stem Playback System
ChurchSense plays back **separated instrument stems**, not a single fixed track:
- Drums
- Bass
- Guitar
- Piano / keys
- Pads / ambience
- FX
- Background vocals
- Percussion (when needed)

**No lead-vocal stem by default** — the worship leader and lead singer sing **live**. The team can mute, solo, or balance any stem so the live musicians and the tracks blend as one.

### 2.4 Click + Guide Track
ChurchSense generates and manages:
- **Click track** (the metronome the band plays to)
- **Count-ins** before songs and sections
- **Guide cues** spoken/labeled for musicians and singers, such as:
  - "Intro" · "Verse one" · "Chorus" · "Bridge" · "Vamp" · "Outro" · "Repeat chorus" · "Ending"

**Non-negotiable:** the congregation / house mix must **never** hear click or guide. These exist only for the worship team's ears.

### 2.5 Audio Routing (concept-level for Phase 1)
ChurchSense plans for these outputs:
- **House stereo mix** — what the congregation hears (no click, no guide)
- **Click output** — separate, isolated
- **Guide output** — separate, isolated
- **Optional stem group outputs** — for boards that can take more channels
- **Stereo bounce output** — a clean L/R feed that can drop straight into a live console such as a **PreSonus StudioLive 64**

ChurchSense is the brain — **not** custom in-ear hardware in Phase 1.

### 2.6 Monitor / In-Ear Direction
- Route click and guide into the **church's existing monitor / in-ear system**.
- Musicians, background singers, and lead singers hear click and guide in their ears.
- Phase 1 uses what the church already owns — **no custom in-ear hardware required**.

### 2.7 ProPresenter Integration (concept-level for Phase 1)
ChurchSense is designed to work alongside ProPresenter for:
- Lyrics
- Slide cues
- Song sections
- Worship moments / Scripture (deeper in later phases)
- Following the live worship flow so slides match what's actually happening

### 2.8 Spirit Flow Mode — **REQUIRED in Phase 1**
The feature that sets ChurchSense apart. When the worship leader is led to linger, Spirit Flow Mode lets them:
- **Hold** the current section indefinitely
- **Loop** a chorus, bridge, vamp, or prayer pad seamlessly
- Keep **click, guide, and stems aligned** while holding or looping
- Keep **lyrics on the right section** in ProPresenter
- **Pause automatic transitions** so nothing moves on without permission
- Let the worship leader **pray or meditate longer** with the pad/atmosphere still under them
- **Resume the planned set** smoothly when ready
- **Recalculate service time live** as moments stretch or shorten

(See Section 7 for detailed behavior.)

---

## 3. What Is NOT in Phase 1

To keep ChurchSense focused and trustworthy on day one, Phase 1 **does not** include:
- ❌ Custom in-ear / personal-monitor **hardware**
- ❌ Per-member personal monitor mixing (each player dialing their own blend)
- ❌ Building our own stem-separation / AI source-separation engine (stems are prepared/imported)
- ❌ Lighting, ProPresenter media production, or video switching control
- ❌ Recording / multitrack capture of the live service
- ❌ Mobile remote-control apps for the whole team
- ❌ Cloud song marketplace or large song-sharing library
- ❌ Automatic transcription or AI lyric generation
- ❌ Multi-campus / multi-site sync

These are noted for the roadmap, not for the first release.

---

## 4. Suggested User Flow

**Before the service (preparation):**
1. Worship leader / tech creates a new **Service Set**.
2. Add songs from the song library (or create them).
3. For each song: confirm key, BPM, sections, lyrics, and load its stems.
4. Arrange the **worship order**; ChurchSense shows total estimated time.
5. Confirm routing — house, click, guide, monitor sends — for the room/board.

**During the service (live):**
6. Open the set in **Live / Run view**.
7. Count-in plays into the team's ears; the house hears only music + live vocals.
8. As each song plays, the band hears click + guide; ProPresenter shows the right lyrics.
9. Worship leader watches elapsed / remaining time.
10. **When the Spirit moves:** tap **Spirit Flow** → Hold or Loop the current section. Click, stems, guide, and lyrics stay locked. Pray, repeat, vamp as long as needed.
11. **Resume** to return to the planned flow; service time recalculates live.
12. Jump to another song if the order changes in the moment.

**After the service:**
13. Save the set (with any notes on what changed) for reuse next time.

---

## 5. Suggested Screen / Page List

1. **Home / Dashboard** — recent sets, upcoming service, quick start.
2. **Song Library** — list, search, add/edit songs.
3. **Song Editor** — title, artist, key, BPM, lyrics, sections, lengths, stems.
4. **Set Builder** — drag-and-reorder worship order, total time, per-song time.
5. **Routing / Audio Setup** — assign house, click, guide, stem, and monitor outputs.
6. **Live / Run View** — the main service screen: current song, current section, elapsed/remaining time, transport, **Spirit Flow** controls, jump-to-song.
7. **Spirit Flow Panel** — Hold, Loop section, prayer-pad, Resume (can live inside Live View).
8. **ProPresenter Sync Status** — connection and current-slide indicator.
9. **Settings** — devices, outputs, click sound, count-in, defaults.

---

## 6. Audio Routing Concept

```
                         ┌─────────────────────────────┐
                         │         ChurchSense          │
                         │      (the worship brain)      │
                         └─────────────────────────────┘
                                       │
          ┌───────────────┬────────────┼────────────┬────────────────┐
          ▼               ▼            ▼            ▼                ▼
   HOUSE STEREO MIX   CLICK OUT    GUIDE OUT   STEM GROUPS     STEREO BOUNCE
   (congregation)    (team ears)  (team ears) (optional)      (L/R to board)
          │               │            │            │                │
          │               └────┬───────┘            │                │
          ▼                    ▼                     ▼                ▼
   ┌─────────────┐     ┌────────────────┐    ┌──────────────┐  ┌──────────────┐
   │ FOH / House │     │  Monitor / IEM  │   │ Live console  │  │ StudioLive 64│
   │   speakers  │     │ system (existing)│   │  channels     │  │  or similar  │
   └─────────────┘     └────────────────┘    └──────────────┘  └──────────────┘
```

**Rules of the road:**
- **House mix never carries click or guide.** This is enforced as a hard rule.
- Click and guide ride only on outputs that feed the team's monitors / in-ears.
- The **stereo bounce** is a safe, simple fallback: one clean L/R pair into any board (e.g., StudioLive 64) for churches not ready for multi-output stems.
- Optional **stem group outputs** let larger setups bring stems into the console as separate channels for the FOH engineer to mix.

---

## 7. Spirit Flow Mode — Behavior

Spirit Flow Mode is what makes ChurchSense a worship tool and not a playback app. It is **required in Phase 1**.

**States:**

| State | What happens |
|---|---|
| **Following** (default) | The set runs as planned; sections advance on time; everything is in sync. |
| **Hold** | The current section is sustained. Automatic transitions are paused. Pads/atmosphere continue; click and guide stay aligned. Lyrics stay on the held section. |
| **Loop** | A chosen section (chorus, bridge, vamp, or a prayer pad) repeats seamlessly at the song's tempo. Click, guide, stems, and lyrics loop together cleanly with no gap. |
| **Prayer / Meditate** | A sustained pad/atmosphere bed continues under the leader while they pray or wait on God. The set clock keeps recalculating. |
| **Resume** | ChurchSense returns to the planned flow from where it left off (or to a chosen next section), transitions back in tempo, and re-syncs lyrics. |

**Guarantees while in Spirit Flow:**
- Click, guide, and stems **stay locked together** — no drift, no restart glitch.
- ProPresenter **stays on the right lyric/section**.
- **No automatic transition fires** until the leader resumes.
- **Service time recalculates live**, so the team and tech can see how the set is shifting.
- Entering and leaving Spirit Flow is **one clear action** the worship leader can trigger without stopping the music.

**The point:** the leader is never fighting the software. If the Spirit says linger, ChurchSense lingers. When it's time to move, ChurchSense picks the planned flow back up.

---

## 8. ProPresenter Integration Concept

ChurchSense and ProPresenter stay in step so the screen reflects what is actually happening in the room.

Phase 1 goals:
- **Lyrics follow the song and section** ChurchSense is currently in.
- **Slide cues** advance with section changes.
- During **Spirit Flow Hold/Loop**, ProPresenter **stays on the current lyric** instead of running ahead.
- On **Resume**, ProPresenter catches up to the planned flow.

Approach: ChurchSense sends section/cue signals; ProPresenter reflects them. The integration is **loose and resilient** — if the link drops, ChurchSense keeps running audio and the operator can still drive slides by hand. Deeper Scripture / worship-moment cues come in later phases.

---

## 9. Future Phases (Roadmap)

- **Phase 2 — Personal monitor mixing:** each musician, background singer, and lead singer controls their own in-ear blend.
- **Phase 3 — Deeper ProPresenter & worship moments:** Scripture cues, prayer screens, themed worship moments tied to the flow.
- **Phase 4 — Custom in-ear / hardware exploration:** dedicated ChurchSense monitor hardware, if the church needs it.
- **Phase 5 — Stem preparation tools:** in-app help to import, organize, and possibly separate stems.
- **Phase 6 — Service recording & review:** capture the live service and what changed for next time.
- **Phase 7 — Multi-site / shared library:** sets and songs shared across campuses, with team roles and permissions.
- **Phase 8 — Team mobile companion:** remote view/control for the worship team on their devices.

---

## 10. Risks / Technical Unknowns

- **Seamless looping & holding without audio glitches** — keeping stems, click, and guide perfectly in sync when a section repeats or sustains is the hardest technical problem. This must feel invisible.
- **Low-latency multi-output audio** — driving house, click, guide, and stems simultaneously on church hardware without lag or dropouts.
- **Hard isolation of click/guide from the house** — guaranteeing the congregation never hears them, even during fast routing changes.
- **ProPresenter sync reliability** — the integration surface and how gracefully it degrades if the connection drops.
- **Stem sourcing** — where prepared stems come from and what format/quality they arrive in (Phase 1 assumes stems are imported, not generated).
- **Hardware variety** — every church's board, interface, and monitor system is different; routing must be flexible and forgiving.
- **Tempo/section data quality** — accurate BPM and section markers are essential for clean transitions and loops.
- **Operator trust under pressure** — the Live view must be calm, clear, and impossible to break mid-service.

---

## 11. First MVP Recommendation

Build the **smallest version that a worship team can actually trust on a Sunday**, and prove the one thing that matters most: **Spirit Flow.**

**MVP scope:**
1. **Set Builder** — add songs, set order, see total / elapsed / remaining time, jump to a song.
2. **Song data** — title, key, BPM, lyrics, sections, section lengths.
3. **Stem playback** — play prepared stems together; mute/solo; live vocal sung over the top.
4. **Click + guide** — generate click, count-ins, and section guide cues into the team's ears only.
5. **Routing baseline** — **house stereo mix** + **isolated click** + **isolated guide** + **clean stereo bounce** to a board like the StudioLive 64. (Stem-group outputs optional.)
6. **Spirit Flow Mode** — Hold and Loop a section with click/guide/stems staying locked; Resume; live time recalculation. **This is the heart of the MVP — not an add-on.**
7. **Basic ProPresenter sync** — lyrics follow the current section and stay put during Hold/Loop.

**Deliberately deferred in the MVP:** personal monitor mixing, custom hardware, recording, multi-site, stem generation, and deep ProPresenter Scripture cues.

**Definition of success:** a worship leader can run a real service, and when the Spirit says *"stay here and pray,"* the team holds together in perfect sync — and when it's time, the service picks back up without anyone touching a glitchy timeline.

> ChurchSense follows worship. Worship does not follow ChurchSense.
