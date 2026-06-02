# PRAISE — Handoff / Verified Checkpoints

## ✅ Protected checkpoint — Click audio (2026-06-02)

**Click audio confirmed audible by DLG after `6df7e27`. Do not regress. Click must remain on the
proven HTMLAudio WAV tick path unless a better tested path is approved.**

### Why this is a non-regression rule
The click is one of the most important In-Ears functions — without it, musicians and singers
cannot keep time. Multiple Web Audio attempts (oscillator + gain automation, then a baked
AudioBuffer through a clickBus → `ctx.destination`) advanced the AudioContext clock (so the bar
meter moved on-beat) but produced **no audible output** in DLG's browser. The fix routes the click
through the **same proven-audible browser path as the music**.

### The working click path (do not replace without approval)
- `makeTickWav(freq, peak, ms)` — generates a short decaying-sine click as a `data:audio/wav` URI
  (accent 1500 Hz, normal 1000 Hz). No audio files are committed.
- Two preloaded `HTMLAudioElement`s (`clickEl`/`playClickTick`) — played with `.play()`, the same
  path as the music (`iaAudio`).
- Triggered inside the **same `setTimeout` that renders the visual beat** in `scheduleClick`, so the
  click stays in time with the bar meter and follows the BPM scheduler.
- The existing **Click checkbox (`optClick`)** is the only control. No Test Click button.
- The old Web Audio click nodes (`clickBus`, `getClickBus`, `playClickTone`, `clickBuf`) are removed —
  do not reintroduce a Web-Audio-only click output.

### Confirmed working at this checkpoint
Music plays · Guidance plays · **Click audible** · Bar meter works · Bar counter correct ·
Click follows the beat · Click checkbox controls the click · Live Run and In-Ears meters match ·
4/4 shows `Bar N` + cells `1 2 3 4` · 3/4 shows `Bar N` + cells `1 2 3` ·
Analyze Tempo auto-applies BPM · Manual → Detected → Planned BPM priority.

### If the click ever needs to change
Keep the HTMLAudio WAV tick path as the baseline. Only swap it for a path that has been tested
audible in DLG's real browser **and** approved. Verify against this checklist before committing.
