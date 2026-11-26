# DAWDeck for REAPER (beta)

**DAWDeck for REAPER** is the REAPER edition of DAWDeck. It is a separate Stream Deck plugin built from the same code and talks to REAPER over REAPER's built-in **OSC control surface**. You need no virtual MIDI ports, no extension and no ReaScript.

> Status: **beta / experimental.** The OSC protocol was tested against REAPER 7.86. Please report anything that does not work in the support repo.

---

## Setup (about three minutes)

**Before you start**
- REAPER 7 (Windows or macOS), started at least once so its resource folder exists
- Elgato Stream Deck app 7.1 or newer

1. **Install the plugin.** Download **DAWDeck for REAPER** (the `.streamDeckPlugin` file) from the [DAWDeck-Support page](https://github.com/Wuestenrolph/DAWDeck-Support#download-the-free-beta), double-click it and confirm the profile for your Stream Deck (XL, MK.2, Neo, + or Mini).
2. **Install the OSC pattern.** Click any DAWDeck for REAPER key in the Stream Deck app. In the Setup Assistant at the top of its settings, click **Install OSC pattern**. It copies `DAWDeck.ReaperOSC` into `<REAPER resource path>/OSC/`. An existing, different file is kept as `.bak`.
   - Windows: `%APPDATA%\REAPER\OSC\`
   - macOS: `~/Library/Application Support/REAPER/OSC/`
   - Portable install: REAPER → *Options → Show resource path in explorer/finder*, then copy the file there by hand.
3. **Add the control surface in REAPER.** *Options → Preferences → Control/OSC/web → Add*:
   - Control surface mode: **OSC (Open Sound Control)**
   - Device name: `DAWDeck for REAPER`
   - Pattern config: **DAWDeck**
   - Mode: **Configure device IP + local port**
   - Device IP `127.0.0.1` · Device port `9000` · Local listen port `8000`
   - OK → Apply
4. **Check.** The OSC row in the Setup Assistant turns green within a few seconds. Select a track in REAPER: the meter key shows its name and level.

---

## What works

- Transport with feedback: Play, Stop, Pause, Record, Repeat (Cycle), Metronome, Bar.Beat display
- Auto-Follow: the followed track is REAPER's last touched track (name, meter, Mute, Solo, Rec Arm, Monitor)
- 8-track bank + master with names, stereo meters and per-track controls
- Markers and common edit commands (via REAPER actions)
- Quick Controls on FX/instrument parameters, including the Stream Deck + dial; Focus follows the focused FX window
- **FX Slot** action (REAPER only): FX name, ON/BYPASS, window. Press = open/close window, hold = bypass. On Stream Deck + the dial controls wet/dry, a parameter or presets.
- 5 Auto-Profiles (XL, MK.2 with an FX page, Neo, +, Mini) with page navigation
- Studio Macros

## Not available in REAPER

These Cubase features have no REAPER equivalent over OSC and are hidden in the REAPER edition:

- Control Room (Talkback, DIM, Mono, Monitor A–D, Cue clicks, Downmix)
- Track Versions, Cubase comping tools, VariAudio, Constrain Delay Compensation
- Post-Roll, Count-In, Lock Punch, Retrospective Audio Record
- Colorize presets and the extended Cubase key commands
- Exact track colors (REAPER does not send track colors over OSC)

---

## Troubleshooting

**OSC row stays red / keys show no names**
- Check that the control surface in REAPER uses pattern **DAWDeck** and the ports exactly as above (device port `9000`, listen port `8000`).
- Another OSC device on port `8000` or `9000` (TouchOSC, another surface) blocks DAWDeck. Change or remove it.
- A firewall prompt for REAPER must be allowed (local traffic only, `127.0.0.1`).
- Click **Reconnect** in the Setup Assistant. REAPER sends a full refresh on reconnect.

**"REAPER resource folder not found"**
- Start REAPER once. For portable installs copy `DAWDeck.ReaperOSC` by hand (see step 2).

**Pattern "DAWDeck" missing in REAPER's list**
- Restart REAPER after installing the pattern, or check that the file is in the `OSC` folder of the resource path REAPER actually uses.

**Upgrading from the earlier beta (ReaperBridge)**
- Remove the old plugin in the Stream Deck app, install DAWDeck for REAPER and place the keys again.
- In REAPER, switch the OSC surface's pattern config from `CubaseBridge` to **DAWDeck**.

---

*Unofficial integration for REAPER, not affiliated with or endorsed by Cockos Incorporated. REAPER is a trademark of Cockos Incorporated. Elgato and Stream Deck are trademarks of Corsair Memory, Inc.*
