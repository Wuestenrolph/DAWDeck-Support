# DAWDeck for Yamaha CC1 (beta)

**DAWDeck for Yamaha CC1** is a small desktop app for Windows and macOS that turns the Yamaha CC1 into a DAWDeck controller for **Cubase & Nuendo, REAPER and Ableton Live**. The app talks to the CC1 directly over USB. You need **no Stream Deck, no Stream Deck app and no Yamaha ControlCenter**.

> Status: **beta / experimental.** Built against the documented CC1 USB protocol and tested with a hardware simulator. It has **not been tested on a real CC1 by us yet**. Feedback from beta testers with a CC1 is very welcome.

---

## What you get

- **12 LCD keys** show DAWDeck pages with live state, the same as on a Stream Deck. Examples for Cubase: *Tracking & Punch*, *Marker & Nav* and *Comping & Takes*. Switch pages with the page buttons.
- **Motorized fader:** volume of the selected track. The fader follows when you select another track.
- **Param-Ride:** hold **W** for about half a second and the fader controls a parameter instead:
  - Cubase & Nuendo: the parameter under the mouse
  - REAPER: the first parameter of the focused plug-in
  - Ableton Live: the first Quick Control parameter of the selected device
- **Pan encoder** for the selected track. Push it to reset pan to center.
- **Quick Control encoders** for Quick Controls 1–4. Push to switch to 5–8.
- **AI knob** with three modes, switched with its push button: AI (Cubase: parameter under the mouse), Lock and Jog.
- **R / W buttons** for automation read/write, plus previous/next track, transport and jog.
- **Built-in calibration** (60 seconds) for the fader and keys.

## Before you start

- Yamaha CC1 connected by USB
- Windows 10/11 or macOS on Apple Silicon (an Intel Mac build is not available yet)
- **Quit Yamaha ControlCenter.** The app needs the CC1's USB port for itself. While DAWDeck for Yamaha CC1 is running, ControlCenter cannot use the device. Quit DAWDeck first if you want to use ControlCenter again.

## Setup

1. **Download** the installer from the beta release: `DAWDeck-for-Yamaha-CC1-…-Windows-Setup.exe` or `…-macOS-AppleSilicon.dmg`. Also download `…-DAW-Scripts.zip` if you have no DAWDeck Stream Deck plugin installed.
2. **Install and start the app.** The installers are not code-signed yet, so your system asks once:
   - Windows: SmartScreen → **More info** → **Run anyway**
   - macOS: right-click the app → **Open** → **Open**
3. **Pick your DAW** at the top of the app window: *Cubase / Nuendo*, *REAPER 7* or *Ableton Live 12*. The CC1 keys change to the pages for that DAW.
4. **Set up the DAW side.** If you already use a DAWDeck Stream Deck plugin for that DAW, this is done: the app uses the same script and ports. Otherwise, follow the section for your DAW below.
5. **Calibrate** once with **Calibrate 60s** in the app and follow the steps.

### Cubase & Nuendo

1. Create two virtual MIDI ports named exactly `SDXL-To-Cubase` and `Cubase-To-SDXL` (Windows: loopMIDI, macOS: IAC Driver). See the [installation guide](INSTALLATION.md) for details. On Windows 11, quit loopMIDI completely after creating the ports and start it again.
2. Copy `Cubase-Nuendo/DAWDeck_StreamDeckXL.js` from the scripts zip to:
   - Windows: `Documents\Steinberg\Cubase\MIDI Remote\Driver Scripts\Local\DAWDeck\StreamDeckXL\`
   - macOS: `~/Documents/Steinberg/Cubase/MIDI Remote/Driver Scripts/Local/DAWDeck/StreamDeckXL/`
   - Nuendo: the same path with `Nuendo` instead of `Cubase`
3. In Cubase or Nuendo: **Studio → MIDI Remote Manager → ↻** (Reload Scripts). Untick **In 'All MIDI Inputs'** for `Cubase-To-SDXL` in *Studio → Studio Setup → MIDI Port Setup*.

The CC1 uses its own MIDI channels (8 and 9), so it can run **together with DAWDeck for Cubase & Nuendo** on a Stream Deck.

### REAPER

1. Copy `REAPER/DAWDeck.ReaperOSC` from the scripts zip into `<REAPER resource path>/OSC/` (Windows: `%APPDATA%\REAPER\OSC\`, macOS: `~/Library/Application Support/REAPER/OSC/`).
2. Add the OSC control surface as described in the [REAPER guide](REAPER.md): pattern config **DAWDeck**, device IP `127.0.0.1`, device port `9000`, local listen port `8000`.

REAPER sends feedback to one OSC device only. Use **either** the CC1 app **or** DAWDeck for REAPER on a Stream Deck with REAPER, not both at once.

### Ableton Live

1. Copy the `Ableton-Live/DAWDeck` folder from the scripts zip into your Live User Library under `Remote Scripts` (Windows: `Documents\Ableton\User Library\Remote Scripts\`, macOS: `~/Music/Ableton/User Library/Remote Scripts/`).
2. Restart Live, then *Settings → Link, Tempo & MIDI → Control Surface*: **DAWDeck**, Input and Output **None**. Details: [Ableton Live guide](ABLETON.md).

Use **either** the CC1 app **or** DAWDeck for Ableton Live on a Stream Deck with Live, not both at once (both use UDP port `11421`).

---

## Troubleshooting

**The app does not find the CC1**
- Quit Yamaha ControlCenter (also from the system tray / menu bar) and unplug and replug the CC1.
- Use a direct USB port instead of a passive hub.

**Keys show "NO MIDI", "NO REAPER" or "NO LIVE"**
- The app cannot reach the DAW. Check the DAW-side setup above for the DAW selected in the app.
- REAPER / Ableton Live: quit DAWDeck for REAPER or DAWDeck for Ableton Live in the Stream Deck app, or switch the CC1 app to another DAW.

**The fader does not follow or jumps**
- Run **Calibrate 60s** again.

Still stuck? Open a [bug report](https://github.com/Wuestenrolph/DAWDeck-Support/issues/new/choose) and pick *DAWDeck for Yamaha CC1*.

---

*Unofficial integration, not affiliated with, endorsed or sponsored by Yamaha Corporation. Yamaha is a trademark of Yamaha Corporation.*
