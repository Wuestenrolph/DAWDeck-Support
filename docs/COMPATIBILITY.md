# Compatibility

Status for release **1.0.0**. "Verified" means checked against the real Cubase files or a running Cubase; it does not mean every feature was exercised on every version.

## Cubase versions

| | Cubase 12 | Cubase 13 | Cubase 14 | Cubase 15 |
|---|---|---|---|---|
| MIDI Remote API | 1.0 | 1.1 (13.0.0) / 1.2 (13.0.50+) | not documented by Steinberg (≥ 1.2 expected) | 1.3 from 15.0.20 (earlier 15.x not documented) |
| Key commands used by the script (55 + 2 plug-in focus) | ✅ all found | ✅ all found | ✅ all found | ✅ all found |
| API members used by the script | ⚠️ not verified (Cubase 12 not installed on the test system) | ⚠️ not verified | ✅ verified against installed API | ✅ verified against installed API |
| Live test (bidirectional, 21 checks + meters) | — | — | — | ✅ passed |
| Control Room feedback | Key-command fallback | ✅ native | ✅ native | ✅ native |
| Quick Controls (Focus + Track, Focus Lock) | API members not verified (Cubase 12 not installed) — feature-detected | API members not verified — feature-detected | ✅ API verified | ✅ live-tested (Waves, FabFilter plug-ins) |
| True stereo meters | Feature-detected: stereo if the build offers per-channel meters, otherwise one summed level on both bars (not verified) | same as Cubase 12 (not verified) | ✅ per-channel meter API present | ✅ per-channel meter API present |

**Safety net for older versions:** the Cubase script checks every version-sensitive API member before using it. If a Cubase build lacks one, only that single key function stays inactive — the rest of the surface keeps working. This follows Steinberg's guidance to use feature detection across API versions.

The API version is tied to the installed Cubase build. It only changes when Cubase itself is updated (e.g. Cubase 13.0.0 → 13.0.50 through the Steinberg Download Assistant). Recommend buyers install the latest maintenance update of their Cubase version.

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
