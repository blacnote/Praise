# ChurchSense — Current Status

**Product:** ChurchSense by DLGSENSE — a worship-service operating system for churches.
**Build pattern:** Single self-contained HTML file (vanilla HTML/CSS/JS + Web Audio API). No npm/build step.
**Core rule:** ChurchSense follows worship. Worship does not follow ChurchSense.
**Source of truth:** `docs/ChurchSense_Phase1_Blueprint.md`.

---

## Canonical location
`/Users/ddregriffin/Desktop/DLG Ideas/ChurchSense` (on the Mac).
Standalone DLGSENSE project — NOT associated with PodSense, DreLovesGod-site, 1DROP, SingSense,
HARMONY, ASCEND, SUMMIT, CLARITY, or any other app/repo. See `docs/SAFETY_RULES.md`.

> Note: any `/home/user/churchsense` copy in a cloud container is **temporary only** (ephemeral).

## Structure
```
ChurchSense/
├── README.md
├── churchsense_v1.html        ← working build
├── docs/  (Blueprint, CURRENT_STATUS, ROADMAP, SAFETY_RULES)
├── prototype/                 ← experimental builds
└── notes/  (STRATEGIC_NOTES)
```

## v1 — what works (browser proof-of-concept)
- [x] Set Builder: add songs, reorder, jump to a specific song (Song 2 of 3)
- [x] Total worship time + live elapsed / remaining
- [x] Song data: title, artist, key, BPM, lyrics, sections + per-section length
- [x] Click track via Web Audio (metronome at BPM) + count-in
- [x] Guide cues: visual section labels + spoken guide (SpeechSynthesis)
- [x] **Spirit Flow Mode:** Hold, Loop section, Prayer/Pad, Resume — with live time recalculation
- [x] House mix never carries click/guide (enforced in logic)
- [x] Routing concept screen + ProPresenter sync placeholder

## v1 — faked / not real yet (honest)
- Stems are **synthesized tones**, not real separated audio files.
- True multi-output routing needs a desktop layer (browsers can't address multiple interfaces).
- ProPresenter integration is a **status placeholder**, not a live link.

## Git status
- No repo created yet. **No commit, no push.** ChurchSense will get its OWN repo when approved.

## Next (await approval before deeper building)
1. Real multi-stem audio file playback (replace synth tones).
2. Glitch-free Spirit Flow hold/loop with real stems — the critical bet.
3. Real ProPresenter network sync.
4. Desktop layer for true multi-output routing.
