# Changelog

All notable changes to CubaseBridge. Versions follow the Stream Deck manifest (`major.minor.patch.build`).

## 1.0.0 — first public release

### Features
- Bidirectional Cubase 12–15 control over two virtual MIDI ports (`SDXL-To-Cubase`, `Cubase-To-SDXL`).
- Selected-track Auto-Follow: name, exact track color, 30 FPS stereo VU meter with peak hold and clip reset, Rec Arm, Input Monitor, Mute, Solo, VSTi editor, Channel Settings (`e · FX/EQ`).
- 8-channel mixer bank + master with stereo meters, names, colors and per-channel controls.
- Recording commands: Auto Punch In/Out, Pre-/Post-Roll, Count-In, locators, punch points, quick markers, Retrospective Record (Audio/MIDI), Bad Take!, Track Versions, lanes, comping tools, edits, clip gain, Render in Place, VariAudio, Undo/Redo, Save New Version, Constrain Delay Compensation.
- Control Room: Talkback, DIM, Mono, Monitor A/B, Cue 1/2 click — native feedback on Cubase 13–15.
- Studio Macro action: up to 16 steps with per-step delays, 5 templates, 6 color themes, live progress.
- Quick Controls: the 8 Quick Controls of the focused plug-in (with Focus Lock) or the selected track, with live parameter names and values; ▲/▼ with accelerating auto-repeat, plug-in focus switching, a Quick Controls page in every profile (XL: ▲ / value / ▼ for all 8), and a Quick Control Dial action for Stream Deck + (rotate / press = QC 1–4 ↔ 5–8 / touch = source).
- Profiles for Stream Deck XL, MK.2, Neo, + and Mini with page navigation.
- Setup Assistant in every Property Inspector: live MIDI status, 1-click Cubase script install/update, Windows/macOS port guide (incl. the Windows 11 loopMIDI restart and Cubase "All MIDI Inputs" tips).

### Fixes and hardening before release
- Cubase 15: the MIDI Remote script no longer aborts during setup (volume display callback on the correct API object); track names and colors use the correct callback signatures.
- Version-sensitive Cubase API members are feature-detected, so a missing member disables only one key function instead of the whole surface.
- True left/right meters via `getVUChannelMeterByChannelIndex` (Cubase 14+), throttled to ≤ 33 updates/s per channel; silence is always delivered.
- Cue 2 click no longer duplicates Cue 1 when Cubase has no second cue channel, and its key light is driven only by real Cubase feedback.
- Bar.Beat display collapses Cubase's padded position format and shrinks long positions to fit the key.
- Tests: driver harness enforces the real Cubase API shape; optional Python check no longer fails on Windows.
