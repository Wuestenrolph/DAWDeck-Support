# Compatibility

> REAPER: see [DAWDeck for REAPER](REAPER.md) (beta, tested against REAPER 7.86).
> Ableton Live: see [DAWDeck for Ableton Live](ABLETON.md) (beta, tested with Live 12.2.5–12.2.7 on Windows).

Status for release **1.0.0**. "Verified" means checked against the real Cubase files or a running Cubase; it does not mean every feature was exercised on every version.

## Cubase versions

| | Cubase 12 | Cubase 13 | Cubase 14 | Cubase 15 |
|---|---|---|---|---|
| MIDI Remote API | 1.0 | 1.1 (13.0.0) / 1.2 (13.0.50+) | not documented by Steinberg (≥ 1.2 expected) | 1.3 from 15.0.20 (earlier 15.x not documented) |
| Key commands used by the script (55 + 2 plug-in focus) | ✅ all found | ✅ all found | ✅ all found | ✅ all found |
| API members used by the script | ⚠️ not verified (Cubase 12 not installed on the test system) | ⚠️ not verified | ✅ verified against installed API | ✅ verified against installed API |
| Live test (bidirectional, 21 checks + meters) | — | — | — | ✅ passed |
| Control Room feedback | Key-command fallback | ✅ native | ✅ native | ✅ native |
| Quick Controls (Focus + Track, Focus Lock) | API members not verified (Cubase 12 not installed) — feature-detected | API members not verified — feature-detected | ✅ API verified | ✅ live-tested: Steinberg plug-ins out of the box; Waves Harmony, FabFilter Pro-Q 3 (parameters assigned via right-click → Add to Quick Controls) |
| True stereo meters | Feature-detected: stereo if the build offers per-channel meters, otherwise one summed level on both bars (not verified) | same as Cubase 12 (not verified) | ✅ per-channel meter API present | ✅ per-channel meter API present |

**Safety net for older versions:** the Cubase script checks every version-sensitive API member before using it. If a Cubase build lacks one, only that single key function stays inactive — the rest of the surface keeps working. This follows Steinberg's guidance to use feature detection across API versions.

The API version is tied to the installed Cubase build. It only changes when Cubase itself is updated (e.g. Cubase 13.0.0 → 13.0.50 through the Steinberg Download Assistant). Recommend buyers install the latest maintenance update of their Cubase version.

## Nuendo

Nuendo 12–15 shares the MIDI Remote API with Cubase (Steinberg lists every API version for "Cubase / Nuendo"), so the same script, ports and protocol are used. The Setup Assistant installs the script into `Documents/Steinberg/Nuendo/MIDI Remote/Driver Scripts/Local/` when that host folder exists.

| | Nuendo 12–15 |
|---|---|
| Script install path | ✅ handled by Setup Assistant and `install-windows.ps1` |
| Key commands used by the script | ⚠️ not verified against Nuendo's key command list (expected identical) |
| Live test | — not yet done |

## Stream Deck

| | Status |
|---|---|
| Stream Deck app | 7.1+ (tested with 7.6.1) |
| Plugin runtime | Node.js 24 (bundled with the Stream Deck app) |
| Stream Deck XL | ✅ live-tested (profile install + plugin) |
| Stream Deck MK.2 / Classic, Neo, + (keys), Mini | Profiles generated and validated; not tested on hardware |
| Stream Deck + dials / touch strip | Quick Control Dial action (rotate / press / touch); dial assignment is manual; not tested on hardware |

## Operating systems

| | Status |
|---|---|
| Windows 11 (x64) | ✅ live-tested with loopMIDI |
| Windows 10 | Expected to work (same MIDI stack); not tested |
| Windows on ARM (arm64) | Native MIDI prebuild included; not tested |
| macOS 12+ Apple Silicon / Intel | Native MIDI prebuilds included; not tested on hardware |

## Virtual MIDI drivers

| | Status |
|---|---|
| loopMIDI (Windows) | ✅ — restart loopMIDI after creating ports on Windows 11 (see TROUBLESHOOTING) |
| IAC Driver (macOS) | Documented; not tested on hardware |
