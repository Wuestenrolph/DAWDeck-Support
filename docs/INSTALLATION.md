# Installation Guide

Setting up CubaseBridge takes about five minutes. You need two virtual MIDI ports, the Cubase script and the Stream Deck profile.

**Before you start**
- Cubase Pro 12, 13, 14 or 15 (latest maintenance update recommended)
- Elgato Stream Deck app 7.1 or newer
- Save your Cubase project — you will restart Cubase once.

---

## 1. Install the plugin and profile

1. Install **CubaseBridge** from the Elgato Marketplace (or double-click the `.streamDeckPlugin` file).
2. The Stream Deck app asks whether to install the bundled profiles — **confirm**.
3. In the Stream Deck app, select the **CubaseBridge** profile for your device (XL, MK.2, Neo, + or Mini).

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

### macOS 12+ (IAC Driver)
1. Open **Audio MIDI Setup** (Applications → Utilities).
2. **Window → Show MIDI Studio**, then double-click **IAC Driver**.
3. Tick **Device is online**.
4. Add two ports (**+**) and rename them `SDXL-To-Cubase` and `Cubase-To-SDXL`. Click **Apply**.

---

## 3. Install the Cubase script

1. In the Stream Deck app, click any CubaseBridge key to open its settings. The **Setup Assistant** appears at the top.
2. Click **Install / Update Cubase Script**. It copies the script to
   `Documents/Steinberg/Cubase/MIDI Remote/Driver Scripts/Local/CubaseBridge/StreamDeckXL/`
   (OneDrive-redirected *Documents* folders on Windows are detected automatically).

---

## 4. Connect Cubase

1. Start (or restart) Cubase and open a project.
2. Go to **Studio → MIDI Remote Manager** and click **↻** (Reload Scripts). The surface **CubaseBridge – StreamDeckXL** appears with status *Connected*, using `SDXL-To-Cubase` as input and `Cubase-To-SDXL` as output. If it does not appear, click **Add Surface**, choose vendor *CubaseBridge*, model *StreamDeckXL* and select the two ports.
3. Go to **Studio → Studio Setup → MIDI Port Setup** and untick **In 'All MIDI Inputs'** for the **`Cubase-To-SDXL`** input (unticking *Visible* is even better). `SDXL-To-Cubase` is handled by Cubase automatically.

---

## 5. Check

- In the Setup Assistant, click **Refresh / Resync** — all three indicators should be green (MIDI In, MIDI Out, Cubase script).
- Select a track in Cubase: the Auto-Follow keys show its name and color.
- Press Play on the Stream Deck: the transport keys and Bar.Beat display follow Cubase.

Something not working? See [TROUBLESHOOTING.md](TROUBLESHOOTING.md).

---

## Updating
After a plugin update, open any key's settings: if the Setup Assistant reports *Update available* for the Cubase script, click **Install / Update Cubase Script** and reload scripts in Cubase.

## Uninstalling
1. Remove the plugin in the Stream Deck app (plugin list → uninstall). Delete the CubaseBridge profile if you no longer need it.
2. In Cubase's MIDI Remote Manager, remove the *CubaseBridge – StreamDeckXL* surface.
3. Delete the folder `Documents/Steinberg/Cubase/MIDI Remote/Driver Scripts/Local/CubaseBridge`.
4. Optionally remove the two virtual MIDI ports.
