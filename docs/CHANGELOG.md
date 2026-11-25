# Changelog

All notable changes to DAWDeck. Versions follow the Stream Deck manifest (`major.minor.patch.build`).

## Unreleased

### New: DAWDeck for Yamaha CC1 (beta, experimental)
- Standalone desktop app for Windows and macOS (Apple Silicon) that drives the Yamaha CC1 directly over USB. No Stream Deck and no Yamaha ControlCenter needed.
- Works with Cubase & Nuendo, REAPER and Ableton Live: 12 LCD keys with DAWDeck pages, motorized fader on the selected track with Param-Ride (hold W), pan, Quick Controls, AI knob (AI / Lock / Jog), automation read/write, track select and jog, plus a 60-second calibration.
- Cubase & Nuendo script: new controls on MIDI channels 8–9 for the CC1 (no change for Stream Deck users; the CC1 and the Stream Deck plugin can run together). Pan reset lands on exact center.
- Releases include a `DAW-Scripts.zip` for CC1 users without a DAWDeck Stream Deck plugin. Setup: [Yamaha CC1 guide](YAMAHA-CC1.md).

### Rename
- New umbrella brand **DAWDeck**: CubaseBridge is now **DAWDeck for Cubase & Nuendo** (`com.dawdeck.cubase`), ReaperBridge is now **DAWDeck for REAPER** (`com.dawdeck.reaper`). Plugin UUIDs, action UUIDs, profiles, the MIDI Remote script (`Local/DAWDeck/StreamDeckXL/DAWDeck_StreamDeckXL.js`), the Colorize PLE presets (*DAWDeck Color 01–16*) and the REAPER OSC pattern (`DAWDeck.ReaperOSC`) are renamed.
- Upgrading a beta install: remove the old plugin in the Stream Deck app and place the keys again (new UUIDs). The Setup Assistant disables a leftover `CubaseBridge` MIDI Remote script (renamed to `.js.disabled`) so Cubase does not load two drivers; re-run **Install Colorize presets** and, in REAPER, select the `DAWDeck` pattern in the OSC surface.
- Support repo renamed to `DAWDeck-Support`; buyer docs gained a REAPER guide (`release/REAPER.md`) and an Ableton Live guide (`release/ABLETON.md`).

### Features
- 36 extended Studio Commands on MIDI channel 5: Add Track (Audio, Audio Mono, Instrument, MIDI, Group, FX, Folder, Duplicate Tracks), Zoom (In/Out, Full, Selection, Tracks In/Out), Quantize grid (1/4, 1/8, 1/16, 1/32, Triplet, Dotted), Normalize, Reverse, Fade In/Out, Remove Fades, Direct Offline Processing, Bounce, Glue, MixConsole (window and Lower Zone), Pool, MediaBay, Key/Score/Drum Editor, Studio Setup. All names verified against Cubase 15 Key Commands; available in the Studio Command and Studio Macro actions.
- Control Room: Cue 1–4 on/off and direct Monitor A–D selection with LED feedback on Cubase 13–15 (new SysEx `0x0D`), key-command fallback on Cubase 12; Downmix presets 1–4.
- Colorize · Color 1–16 commands (Project Logical Editor presets *DAWDeck Color 01–16*) and a Setup Assistant installer for those presets.
- Installation guide: Stream Deck Mobile (iPhone/iPad) section.

### Licensing

### Protocol
- MIDI channel 4 reserved for the upcoming Channel Strip, channels 6–7 for the command catalog.

### Experimental

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
