# Installation Guide

> Using REAPER or Ableton Live? See [DAWDeck for REAPER](REAPER.md) or [DAWDeck for Ableton Live](ABLETON.md) instead. This guide covers **DAWDeck for Cubase & Nuendo**.

Setting up DAWDeck takes about five minutes. You need two virtual MIDI ports, the Cubase script and the Stream Deck profile.

**Before you start**
- Cubase Pro 12, 13, 14 or 15 (latest maintenance update recommended)
- Elgato Stream Deck app 7.1 or newer
- Save your Cubase project — you will restart Cubase once.

---

## 1. Install the plugin and profile

1. Install **DAWDeck** from the Elgato Marketplace (or double-click the `.streamDeckPlugin` file).
2. The Stream Deck app asks whether to install the bundled profiles — **confirm**.
3. In the Stream Deck app, select the **DAWDeck** profile for your device (XL, MK.2, Neo, + or Mini).

> **Stream Deck +:** the profile pre-fills the keys. For Quick Controls on the dials, open the last page (*Quick Controls*), drag the **Quick Control Dial** action from the DAWDeck category onto each of the four dials — no further settings needed.

> The profile only works with the View keys (page navigation) when it was installed this way. Importing a `.streamDeckProfile` file by hand creates a copy the plugin cannot navigate.

---

## 2. Create the two virtual MIDI ports

The names must match exactly:

| Port | Direction |
|---|---|
| `SDXL-To-Cubase` | Stream Deck → Cubase (key presses) |
| `Cubase-To-SDXL` | Cubase → Stream Deck (names, colors, meters, states) |

### Windows 10/11 (loopMIDI)
1. Download and install **loopMIDI** by Tobias Erichsen (free).
2. Start loopMIDI, type `SDXL-To-Cubase` into *New port-name* and click **+**. Repeat for `Cubase-To-SDXL`.
3. **Important on Windows 11:** quit loopMIDI completely (right-click the tray icon → **Exit**) and start it again. On current Windows 11 builds, ports created while loopMIDI is running often show up in every app but carry no data until loopMIDI restarts. loopMIDI remembers your ports.
4. Optional but recommended: in loopMIDI's settings, enable *Start minimized / autostart* so the ports exist before Cubase starts.

**Alternative on Windows 11: built-in loopbacks.** Windows 11 PCs with *Windows MIDI Services* enabled can create MIDI loopbacks without loopMIDI, in Microsoft's **MIDI Settings** app (part of the Windows MIDI Services SDK Runtime and Tools package). Create two loopbacks and make sure the port names contain `SDXL-To-Cubase` and `Cubase-To-SDXL`. DAWDeck and the Cubase script only look for those name parts, so nothing else needs to change. A built-in loopback is a bidirectional A/B pair: what is sent to side A arrives on side B. So give both sides of a pair the same name part, for example `SDXL-To-Cubase A` / `SDXL-To-Cubase B`. loopMIDI remains the recommended, tested setup.

### macOS 12+ (IAC Driver)
1. Open **Audio MIDI Setup** (Applications → Utilities).
2. **Window → Show MIDI Studio**, then double-click **IAC Driver**.
3. Tick **Device is online**.
4. Add two ports (**+**) and rename them `SDXL-To-Cubase` and `Cubase-To-SDXL`. Click **Apply**.

---

## 3. Install the Cubase / Nuendo script

1. In the Stream Deck app, click any DAWDeck key to open its settings. The **Setup Assistant** appears at the top.
2. Click **Install / Update Script**. It copies the script into every Steinberg host it finds:
   - Cubase: `Documents/Steinberg/Cubase/MIDI Remote/Driver Scripts/Local/DAWDeck/StreamDeckXL/`
   - Nuendo: `Documents/Steinberg/Nuendo/MIDI Remote/Driver Scripts/Local/DAWDeck/StreamDeckXL/`

   A host counts as found when its `Documents/Steinberg/<Cubase|Nuendo>` folder exists (it is created the first time you start that host). If neither exists yet, the script goes to the Cubase folder. OneDrive-redirected *Documents* folders on Windows are detected automatically.

   Nuendo 12–15 uses the same MIDI Remote API as Cubase, so all steps below apply to Nuendo as well.

---

## 4. Connect Cubase

1. Start (or restart) Cubase and open a project.
2. Go to **Studio → MIDI Remote Manager** and click **↻** (Reload Scripts). The surface **DAWDeck – StreamDeckXL** appears with status *Connected*, using `SDXL-To-Cubase` as input and `Cubase-To-SDXL` as output. If it does not appear, click **Add Surface**, choose vendor *DAWDeck*, model *StreamDeckXL* and select the two ports.
3. Go to **Studio → Studio Setup → MIDI Port Setup** and untick **In 'All MIDI Inputs'** for the **`Cubase-To-SDXL`** input (unticking *Visible* is even better). `SDXL-To-Cubase` is handled by Cubase automatically.

---

## 5. Check

- In the Setup Assistant, click **Refresh / Resync** — all three indicators should be green (MIDI In, MIDI Out, Cubase script).
- Select a track in Cubase: the Auto-Follow keys show its name and color.
- Press Play on the Stream Deck: the transport keys and Bar.Beat display follow Cubase.
- Open a plug-in window in Cubase, click into it, and go to the **Quick Controls** page: the keys show its parameter names and values. For third-party plug-ins, pick the parameters you want with a right-click → **Add '…' to Quick Controls** (see [TROUBLESHOOTING.md](TROUBLESHOOTING.md#quick-controls-show-the-wrong-parameters-of-a-plug-in)).

Something not working? See [TROUBLESHOOTING.md](TROUBLESHOOTING.md).

---

## Stream Deck Mobile (iPhone / iPad)

DAWDeck actions also run on **Stream Deck Mobile**. The phone or tablet connects to the Stream Deck app on your studio computer, so the plugin, the MIDI ports and Cubase stay exactly as set up above.

1. Install Stream Deck Mobile and pair it with the Stream Deck app on the computer that runs Cubase.
2. Select the Mobile device in the Stream Deck app and drag DAWDeck actions (Studio Command, Transport, Channel, Macro …) onto its keys. Feedback such as track names, colors, meters and LEDs works the same as on hardware.
3. The free Mobile app offers 6 keys. Larger layouts, for example an 8×4 grid on an iPad as a remote in the recording room, need a **Stream Deck Mobile Pro** subscription.

> The bundled profiles and the View (page navigation) keys are built for the physical Stream Deck models. On Mobile, build your own pages from the actions; a dedicated Mobile profile is planned once it has been tested on real devices.

---

## Colorize presets (optional)

The **Colorize · Color 1–16** commands color the selected tracks, events or parts with one key press. They run small Project Logical Editor presets named *DAWDeck Color 01–16*. When the plugin ships these presets, the Setup Assistant shows a **Colorize Presets** row: click **Install Colorize Presets**, then restart Cubase once so it picks them up. The presets are copied into the user preset folder that all Cubase versions share, `Documents/Steinberg/Cubase/User Presets/Project Logical Editor` (Nuendo: `Documents/Steinberg/Nuendo/...`), on Windows and macOS.

---

## Updating
After a plugin update, open any key's settings: if the Setup Assistant reports *Update available* for the Cubase script, click **Install / Update Script** and reload scripts in Cubase/Nuendo.

## Uninstalling
1. Remove the plugin in the Stream Deck app (plugin list → uninstall). Delete the DAWDeck profile if you no longer need it.
2. In Cubase's MIDI Remote Manager, remove the *DAWDeck – StreamDeckXL* surface.
3. Delete the folder `Documents/Steinberg/Cubase/MIDI Remote/Driver Scripts/Local/DAWDeck` (and the same folder under `Steinberg/Nuendo` if you use Nuendo).
4. Optionally remove the two virtual MIDI ports.
