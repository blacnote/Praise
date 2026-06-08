# PRAISE — Project Handoff

_Last updated: 2026-06-02 · Protected checkpoint: `5e1c0a9` · Working audible-click build: `6df7e27`_

---

## 🔒 PROTECTED NON-REGRESSION RULE (read first)

> **Click audio confirmed audible by DLG after `6df7e27`. Do not regress. Click must remain on the
> proven HTMLAudio WAV tick path unless a better tested path is approved.**

The click is one of the most important In-Ears functions — without it, musicians and singers cannot
keep time. **Preserve the working click before every new feature.**

---

## A. Project identity

**PRAISE** — a worship-service / rehearsal / in-ear support tool (by DLGSENSE).
It helps a worship team run a service or rehearsal from one place, built around:
- **Music playback** (local track, browser-side)
- **Spoken guidance** (section cues)
- **Click** (tempo reference for the team's ears)
- **Bar counter / meter** (4/4 and 3/4 visual count)
- **Service flow** (set list, Live / Run transport, Spirit Flow, In-Ears page)

Main app is a single self-contained file: `praise_v1.html`.

---

## B. Confirmed working (verified by DLG)

- Music plays.
- Guidance plays.
- **Click is audible.**
- Click is controlled by the existing **Click checkbox** (`optClick`).
- Bar meter works.
- Live Run and In-Ears meters **match** (shared render — one scheduler, no drift).
- **4/4** shows `Bar N` separately with beat cells **`1 2 3 4`**.
- **3/4** shows `Bar N` separately with beat cells **`1 2 3`**.
- Analyze Tempo **auto-applies** the detected BPM to the click.
- Manual BPM **overrides** detected / planned BPM.
- BPM priority **Manual → Detected → Planned** is preserved.

---

## C. Protected non-regression rule

(See the boxed rule at the top — repeated here for emphasis.)

> **Click audio confirmed audible by DLG after `6df7e27`. Do not regress. Click must remain on the
> proven HTMLAudio WAV tick path unless a better tested path is approved.**

---

## D. Click architecture (why it works now)

**What was broken:** previous click attempts used the **Web Audio API** (oscillator + gain
automation, then a baked AudioBuffer through a `clickBus → ctx.destination`). In DLG's browser the
Web Audio **clock advanced** — which is exactly why the bar meter moved correctly on-beat — but the
Web Audio **output produced no audible sound**. Music (HTMLAudioElement) and guidance
(speechSynthesis) used different, proven-audible browser paths, so only the click was silent.

**The working click path (do not replace without approval):**
- `makeTickWav(freq, peak, ms)` generates a short decaying-sine click as a **`data:audio/wav` URI**
  (accent 1500 Hz, normal 1000 Hz). No audio files are committed — the WAV is synthesized at runtime.
- Two preloaded `HTMLAudioElement`s (`clickEl` / `playClickTick`) are played with **`.play()`** — the
  **same browser path the music uses** (`iaAudio`).
- The click fires **inside the same `setTimeout` that renders the visual beat** (`scheduleClick`), so
  it stays in time with the bar meter and follows the BPM scheduler.
- The existing **Click checkbox (`optClick`)** remains the only user-facing control.
- **No Test Click button** — it was removed and must **not** be added back.
- The old Web Audio click nodes (`clickBus`, `getClickBus`, `playClickTone`, `clickBuf`) are removed.
  Do **not** reintroduce a Web-Audio-only click output.

---

## E. Files / current scope

- **Main app file:** `praise_v1.html` (single-file app — HTML + CSS + JS).
- **Handoff file:** `HANDOFF.md` (this file).
- **Do not touch backup folders** (e.g. `Praise_backup_*`).
- **Do not** add stems, DAW routing, hardware routing, StudioLive / Pro Tools / OBS / Core Audio
  integration, multi-output routing, or any unrelated systems.

---

## F. Future-session warnings

- **Do not rebuild PRAISE.**
- **Do not replace the click system unless DLG confirms the replacement is audible** in his real
  browser.
- **Do not add more buttons** to solve click problems. (Adding buttons is not fixing the issue.)
- **Do not change music / guidance / bar meter / BPM behavior** while working on unrelated issues.
- **Preserve the working click before every new feature.**
- Keep changes scoped to `praise_v1.html` unless absolutely necessary.

---

## G. Core Rehearsal Stability Test — PASSED (2026-06-02)

**Core Rehearsal Stability Test passed: music, guidance, click, BPM source, Live Run meter, and
In-Ears meter worked together during the test.**

Scope verified (click audibility is DLG-confirmed and protected; the full rehearsal flow was traced
end-to-end and is intact / non-regressed):
- Load track → Start → music + guidance + audible click together.
- Click controlled by the existing Click checkbox.
- Bar counter correct; Live Run and In-Ears meters match (shared render, one scheduler).
- 4/4 → `Bar N` + cells `1 2 3 4`; 3/4 → `Bar N` + cells `1 2 3`.
- Analyze Tempo auto-applies detected BPM; Manual BPM overrides (Manual → Detected → Planned).
- Pause / Resume / Stop: music, click, and meters recover; Stop resets music to 0, stops the click,
  and resets both meters to `Bar —`.

**Known behavior (not a regression, not changed):** on **Resume**, the click and bar counter restart
from `Bar 1` with a fresh count-in while the music resumes from its paused position. This is existing
count-in behavior. If DLG wants resume to continue the prior bar count instead, that is a separate,
approved change — do not alter it as a side effect of unrelated work.

---

## H. Future Integration Readiness — Studio 64s / Hardware Test Later

**Full hardware integration is NOT certified yet.** DLG expects deeper integration testing to require
the actual **PreSonus StudioLive 64s** hardware. The current build can prepare the lane, but must
**not** claim hardware routing is complete.

When the StudioLive 64s is available, the future hardware test should verify:
1. Output routing
2. Click routing
3. Guide routing
4. Music routing
5. Performer / in-ear mix behavior
6. Latency
7. Drift
8. Start / Pause / Stop recovery
9. No click dropout
10. No guide / click conflict

Until that test is done and approved: no hardware routing, no DAW routing, no stems. PRAISE remains a
separate control/rehearsal layer; the StudioLive 64s stays the live/house authority.

---

## I. Uploaded Song Visibility + Track Control — built (2026-06-08)

The loaded local song now has a real control surface in **In-Ears → Track Test** (operates on the
existing `iaAudio` element only — no new audio path, click untouched):
- **Total duration** + **current elapsed time** — `#iaTrackTime` ("m:ss / m:ss"), updated from
  `iaAudio` events (`loadedmetadata`, `durationchange`, `timeupdate`) via `formatTime()`.
- **Progress / scrub / seek** — `#iaSeek` range; `onSeekInput()` sets `iaAudio.currentTime`. Seeking
  keeps the track playing if playing and paused if paused. A `seeking` flag stops `timeupdate` from
  fighting the handle while dragging.
- **Restart** — `#iaRestartBtn` / `trackRestart()` → returns to 0 (replays if it was playing).
- **Clear / remove** — `#iaClearBtn` / `clearTrack()` → stops the track, revokes the blob URL, clears
  `trackLoaded` / `trackName` / `trackFile` / `detectedBpm`, resets the file input + all displays, and
  disables Analyze Tempo until a new file is loaded. (Manual BPM override is left intact.)
- Existing **filename** (`#iaTrackName`), **play-state** (`#iaTrackPlayState`), and **Play / Pause /
  Stop** behavior are unchanged.

**Not touched:** click path (HTMLAudio WAV tick), `optClick`, bar meters, BPM priority logic. Track
playback remains browser-local — nothing is uploaded or committed.

---

## J. Gate 1 — Uploaded Audio → Set Builder Attachment Status (2026-06-08)

**What was built:** Set Builder now shows, per song, whether it has audio attached and lets DLG attach
the track currently loaded in **In-Ears → Track Test** to a chosen Set Builder song.
- Song objects gained an optional `audio` field: `{ name, url, file }`.
- Set Builder card shows **"Metadata only — no audio attached yet"** or **"🎵 Audio attached — [filename]"**,
  with an **Attach** / **Detach** button per song. `saveSong` preserves the attachment across an edit.
- Live Run order cards show a **read-only** status tag (`🎵 audio attached` / `metadata only`). No Live Run
  player was built (that is Gate 2).

**What remains metadata-only:** the 3 demo songs (and any song) until DLG attaches audio. Nothing is
falsely shown as playable.

**Browser-local / session-local:** attachments use `URL.createObjectURL(trackFile)` — **in-memory only**,
no server upload, no persistence. **Object URLs do not survive a page reload — re-attach after refresh.**
A fresh object URL is minted per attachment so the In-Ears Track Test "Clear" does not break a song's
attachment.

**Not touched (verified):** click path (HTMLAudio WAV tick), `optClick`, bar meters, BPM priority,
Analyze Tempo auto-apply, Track Test controls.

## K. Design Correction — loading a song AUTO-creates a Set Builder song (2026-06-08)

**Why:** the prior pass still required an extra **"Add to Set Builder"** button. DLG's design: the *sole
purpose* of loading a song is for it to enter Praise in the right place — so loading should auto-create
the set song, no extra click.

**What was corrected:**
- **`loadTrack()` now auto-creates the song.** Choose a file → Praise immediately makes a real Set Builder
  song: title from filename (`Pray Together.mp3` → **"Pray Together"**), audio attached (`{name, url, file}`),
  `bpm` = detected BPM if available else `0`/"?" (honest, editable; detected BPM still drives the click
  separately), default editable sections. The In-Ears panel is now **"Load a Song"** with preview controls.
- **The "Add to Set Builder" button was removed** (no longer needed).
- **Duplicate guard:** loading the *same* file (matched by name + size + lastModified) reuses the existing
  set song and refreshes its URL instead of creating a duplicate.
- **Attach / Detach (Gate 1) remains secondary** for attaching a loaded track to an *existing* song.

**Still browser/session-local:** `URL.createObjectURL` (in-memory, no upload, no persistence).
**Re-load after a page reload.** Removing a song revokes its object URL.

**Still NOT connected (next lane):** a set song's attached audio **does not yet play from Live Run**
(Live Run shows it in the order with read-only audio status). That is **Gate 2**.

## L. Demo songs removed from the active set (2026-06-08)

The 3 hard-coded demo songs (Way Maker, Goodness of God, Great Are You Lord — metadata-only, no audio)
were **removed** so the Set Builder only holds real loaded songs and nothing looks playable when it
isn't. `songs` now starts **empty**; the app already guards an empty set (Start alerts "Add a song
first"). The earlier example data remains in git history (pre-`73…`/this commit) if needed for dev.

## M. Lyrics — honest field exists; future lane

Songs already carry a manual **`lyrics`** field (editable in the song editor — `edLyrics`). Lyrics are
**not** fetched/scraped (no fake retrieval). Future lyric lane: paste/import lyrics → align lyrics to
sections → display lyrics in Live Run.

## N. Roles + Personal Mix roadmap (no fake stems)

**Roles** (In-Ears `ROLES`) now include **Organist**: Worship Leader · Drummer · Bass · Keys ·
**Organist** · Guitar · BGV · Tracks Operator. **Guidance** is the main word (the mix source formerly
"Guide" is now **"Guidance"**; "Cues" is now **"Section prompts"** = Intro/Verse/Chorus/Bridge/Vamp/Outro).

**Personal Mix (In-Ears) — concept only, not built as real audio yet:**
- **Immediate target:** each role controls **Music / Click / Guidance** levels.
- **Future (after real stem breakdown):** Drums, Bass, Keyboards, Guitar, Pads, Click, Guide, Talkback,
  Background Vocals, Lead. **No stems exist yet — do not claim stems are available until actually built.**
- **Future:** an "Add custom instrument/category" control (e.g. strings/violin) for sources not listed.

### Gate roadmap
- **Gate 2 (next):** Live Run selected-song playback/control — play/seek a set song's attached audio from
  Live Run (reuse the `iaAudio` / track-control approach; **do not touch the click path**).
- **Gate 3:** In-Ears Personal Mix Controls (immediate: per-role Music/Click/Guidance; stems later).
- **Gate 4:** StudioLive 64s hardware integration — **future / hardware-only, not certified** (see §H).

---

## Commit reference

| Commit | Meaning |
|--------|---------|
| `6df7e27` | Click routed through the proven HTMLAudio WAV tick path — **confirmed audible** |
| `5e1c0a9` | Protected checkpoint note (this handoff originated here) |
| `056c1c4` | Expanded into full project handoff |
| `6b7be5f` | Core Rehearsal pass + Studio 64s integration-readiness lane |
| `e6dbcf7` | Uploaded-song visibility + track control (duration, seek, restart, clear) |
| `c69ddb7` | Gate 1 — uploaded audio → Set Builder attachment status |
| `32e3da9` | Realign — loaded song becomes a Set Builder song (via Add button) |
