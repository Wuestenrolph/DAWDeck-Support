# DAWDeck for Ableton Live (beta)

**DAWDeck for Ableton Live** is the Ableton Live edition of DAWDeck. It is a separate Stream Deck plugin built from the same code and talks to Live through a small bundled **Remote Script** (a Live control surface) over local UDP/OSC. You need no virtual MIDI ports, no loopMIDI/IAC Driver and no Max for Live.

> Status: **beta / experimental.** Tested with Ableton Live 12.2.5–12.2.7 on Windows. macOS is not tested yet. Please report anything that does not work in the support repo.

---

## Setup (about three minutes)

**Before you start**
- Ableton Live 12 on Windows or macOS
- Elgato Stream Deck app 7.1 or newer

1. **Install the plugin.** Download **DAWDeck for Ableton Live** (the `.streamDeckPlugin` file) from the [DAWDeck-Support page](https://github.com/Wuestenrolph/DAWDeck-Support#download-the-free-beta), double-click it and confirm the profile for your Stream Deck (XL, MK.2, Neo, + or Mini).
2. **Install the Remote Script.** Click any DAWDeck for Ableton Live key in the Stream Deck app. In the Setup Assistant at the top of its settings, click **Install Remote Script**. It copies the `DAWDeck` script folder into your Live User Library:
   - Windows: `Documents\Ableton\User Library\Remote Scripts\DAWDeck\` (OneDrive-redirected Documents folders are detected)
   - macOS: `~/Music/Ableton/User Library/Remote Scripts/DAWDeck/`
   - If you moved your User Library in Live (*Settings → Library*), copy the folder there by hand.
3. **Restart Live** if it was open, then select the control surface: *Settings → Link, Tempo & MIDI → Control Surface*: **DAWDeck**, Input **None**, Output **None**.
4. **Check.** The "Live OSC link" row in the Setup Assistant turns green within a few seconds. Select a track in Live: the meter key shows its name, color and level.

---

## What works

- Transport with feedback: Play, Stop, Arrangement Record, Session Record, Overdub, Loop, Metronome, Punch In/Out, Capture MIDI
- Bar.Beat display exactly like Live's position display (also in 6/8, 7/8 and other time signatures)
- Auto-Follow: the selected Live track (name, true RGB color, stereo meter, Rec Arm, Mute, Solo)
- 3-state Monitor key (Off / Auto / In); per key either cycle Off → Auto → In or toggle Auto ↔ In
- 8-track bank + Main with names, colors and stereo meters; Live's red session box follows the bank
- Meters update at about 30 Hz while audio plays
- Cue points (add/delete, previous/next, jump to 1–8), Undo/Redo, Quantize, add Audio/MIDI/Return track, duplicate track, Colorize
- Quick Controls on the first 8 parameters of the Blue Hand device (or the selected track's instrument), with live names and values, Focus Lock, device power and previous/next device; Stream Deck + dial support
- **Clip Slot** and **Scene** actions (Live only): launch clips and scenes with name, color and state (empty, stopped, queued, playing, recording); long press on a clip stops the track; scene up/down, Stop All, Arranger ↔ Session view, Back to Arranger, Re-Enable Automation
- `e · Device` key shows and hides Live's Device View with LED feedback
- 5 Auto-Profiles (XL, MK.2, Neo, +, Mini) with page navigation
- Studio Macros

## Not available in Ableton Live

These Cubase features have no equivalent in Live's Remote Script API and are hidden in the Ableton Live edition:

- Control Room (Talkback, DIM, Mono, Monitor A–D, Cue clicks, Downmix)
- Track Versions, Cubase comping tools, VariAudio, Constrain Delay Compensation
- Pre-/Post-Roll, Lock Punch, Retrospective Audio Record
- Zoom, quantize grid presets, offline processing and Cubase window commands

**Count-In is display only.** Live does not let control surfaces change the Count-In setting. The key shows the current value (Off / 1 / 2 / 4 bars); pressing it shows a hint in Live's status bar. Change it in Live's metronome menu.

---

## Troubleshooting

**"Live OSC link" stays red / keys show no names**
- Check that **DAWDeck** is selected as a Control Surface in Live (Input/Output: None) and that Live was restarted after installing the script.
- DAWDeck uses UDP ports `11420` (Live) and `11421` (plugin) on `127.0.0.1`. Another tool on these ports blocks it. AbletonOSC (ports 11000/11001) does not collide.
- Click **Reconnect** in the Setup Assistant.
- Live's log file shows whether the script loaded: look for `DAWDeck: listening on 127.0.0.1:11420` in `Log.txt` (Windows: `%APPDATA%\Ableton\Live 12.x.x\Preferences\`, macOS: `~/Library/Preferences/Ableton/Live 12.x.x/`).

**"DAWDeck" missing in Live's Control Surface list**
- The folder must be `Remote Scripts\DAWDeck\` with `__init__.py` directly inside it. Restart Live after copying.
- If you moved your User Library, the script must be in that location.

---

*Unofficial integration for Ableton Live, not affiliated with or endorsed by Ableton AG. Ableton and Ableton Live are trademarks of Ableton AG. Elgato and Stream Deck are trademarks of Corsair Memory, Inc.*
