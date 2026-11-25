# DAWDeck — Support

Help, documentation and issue tracking for **DAWDeck**, the Elgato Stream Deck plugins and the Yamaha CC1 app for bidirectional studio & recording control:

| Plugin | For | Connection | Status |
|---|---|---|---|
| **DAWDeck for Cubase & Nuendo** | Steinberg Cubase Pro 12–15, Nuendo 12–15 | MIDI Remote script + two virtual MIDI ports | Beta |
| **DAWDeck for REAPER** | REAPER 7 | REAPER's built-in OSC control surface | Beta (experimental) |
| **DAWDeck for Ableton Live** | Ableton Live 12 | Bundled Remote Script (Live control surface "DAWDeck") | Beta (experimental) |
| **DAWDeck for Yamaha CC1** | Yamaha CC1 with Cubase/Nuendo, REAPER or Ableton Live | Desktop app, direct USB (no Stream Deck, no Yamaha ControlCenter) | Beta (experimental) |

![DAWDeck on a Stream Deck XL](assets/showcase-xl.png)

> This repository contains documentation and the issue tracker only. The plugins are in beta.

---

## Get help

| I want to… | Go to |
|---|---|
| Set up DAWDeck for Cubase or Nuendo | [Installation guide](docs/INSTALLATION.md) |
| Set up DAWDeck for REAPER | [REAPER guide](docs/REAPER.md) |
| Set up DAWDeck for Ableton Live | [Ableton Live guide](docs/ABLETON.md) |
| Set up DAWDeck for Yamaha CC1 | [Yamaha CC1 guide](docs/YAMAHA-CC1.md) |
| Fix something that doesn't work | [Troubleshooting & known quirks](docs/TROUBLESHOOTING.md) · [REAPER troubleshooting](docs/REAPER.md#troubleshooting) · [Ableton Live troubleshooting](docs/ABLETON.md#troubleshooting) · [Yamaha CC1 troubleshooting](docs/YAMAHA-CC1.md#troubleshooting) |
| Check if my DAW / Stream Deck / OS is supported | [Compatibility](docs/COMPATIBILITY.md) |
| See what changed | [Changelog](docs/CHANGELOG.md) |
| Ask a question | [Discussions → Q&A](../../discussions) |
| Report a bug | [New issue → Bug report](../../issues/new/choose) |
| Suggest a feature | [New issue → Feature request](../../issues/new/choose) |

**Before opening an issue**, please check the troubleshooting guide. The most common setup problems:
1. **Windows 11 (Cubase/Nuendo):** after creating the loopMIDI ports, quit loopMIDI completely (tray icon → Exit) and start it again.
2. **Cubase/Nuendo:** untick **In 'All MIDI Inputs'** for `Cubase-To-SDXL` in *Studio → Studio Setup → MIDI Port Setup*.
3. **REAPER:** the OSC surface must use pattern config **DAWDeck**, device port `9000` and local listen port `8000`.
4. **Ableton Live:** select **DAWDeck** as Control Surface (Input/Output: None) and restart Live after installing the Remote Script.
5. **Yamaha CC1:** quit Yamaha ControlCenter before starting DAWDeck for Yamaha CC1; only one app can use the CC1 at a time.

---

## Quick setup

### Cubase & Nuendo
1. Install **DAWDeck for Cubase & Nuendo** and confirm the profile for your Stream Deck.
2. Create two virtual MIDI ports named exactly `SDXL-To-Cubase` and `Cubase-To-SDXL` (Windows: loopMIDI, macOS: IAC Driver).
3. Open any DAWDeck key's settings in the Stream Deck app and click **Install / Update Cubase Script**. It installs the script for every Cubase and Nuendo found.
4. In Cubase or Nuendo: **Studio → MIDI Remote Manager** → **↻** (Reload Scripts).

Details: [Installation guide](docs/INSTALLATION.md).

### REAPER
1. Install **DAWDeck for REAPER** and confirm the profile for your Stream Deck.
2. Open any key's settings and click **Install OSC pattern** in the Setup Assistant.
3. In REAPER: *Preferences → Control/OSC/web → Add → OSC*, pattern config **DAWDeck**, device IP `127.0.0.1`, device port `9000`, local listen port `8000`.

Details: [REAPER guide](docs/REAPER.md).

### Ableton Live
1. Install **DAWDeck for Ableton Live** and confirm the profile for your Stream Deck.
2. Open any key's settings and click **Install Remote Script** in the Setup Assistant.
3. Restart Live, then *Settings → Link, Tempo & MIDI → Control Surface*: **DAWDeck**, Input and Output **None**.

No loopMIDI, IAC Driver or Max for Live needed. Count-In can only be shown, not changed (Live doesn't allow it). Details: [Ableton Live guide](docs/ABLETON.md).

### Yamaha CC1
1. Quit Yamaha ControlCenter, then install and start **DAWDeck for Yamaha CC1** (Windows `.exe` or macOS `.dmg`).
2. Pick your DAW in the app window. If you already use the DAWDeck Stream Deck plugin for that DAW, the DAW side is ready; otherwise install it from the `DAW-Scripts.zip` of the release.
3. Run **Calibrate 60s** once.

No Stream Deck needed. Details: [Yamaha CC1 guide](docs/YAMAHA-CC1.md).

---

## Upgrading from CubaseBridge / ReaperBridge
DAWDeck is the new name of the earlier betas *CubaseBridge* and *ReaperBridge*. The plugin IDs changed, so remove the old plugin in the Stream Deck app, install the new one and place your keys again. The Setup Assistant switches off the old Cubase script automatically. In REAPER, select the **DAWDeck** pattern in the OSC surface.

---

## Privacy
DAWDeck runs entirely on your computer and collects no data — see the [privacy statement](docs/PRIVACY.md).
When you post an issue or discussion here, it is **public**: please don't include personal data, private project names or contact details.

---

*Unofficial integrations, not affiliated with, endorsed or sponsored by Steinberg Media Technologies GmbH, Cockos Incorporated, Ableton AG or Yamaha Corporation. Steinberg, Cubase and Nuendo are registered trademarks of Steinberg Media Technologies GmbH. REAPER is a trademark of Cockos Incorporated. Ableton and Ableton Live are trademarks of Ableton AG. Yamaha is a trademark of Yamaha Corporation. Elgato and Stream Deck are trademarks of Corsair Memory, Inc.*
