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

## G. Next recommended lane

**Full rehearsal stability test:** run a complete song / set start to finish and confirm that
**music, guidance, click, BPM source (Manual/Detected/Planned), and the bar counter stay locked**
from start to finish — across song changes, Spirit Flow, and meter (4/4 ↔ 3/4) switches.

---

## Commit reference

| Commit | Meaning |
|--------|---------|
| `6df7e27` | Click routed through the proven HTMLAudio WAV tick path — **confirmed audible** |
| `5e1c0a9` | Protected checkpoint note (this handoff originated here) |
