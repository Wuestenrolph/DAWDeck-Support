# Troubleshooting & Known Quirks

Start with the **Setup Assistant** (click any CubaseBridge key in the Stream Deck app). Its three indicators tell you where the problem is: **MIDI In**, **MIDI Out** and **Cubase script**.

---

## Keys show "NO MIDI"

The plugin cannot find the two ports.
- Check the exact names: `SDXL-To-Cubase` and `Cubase-To-SDXL` (spelling, hyphens).
- Windows: make sure loopMIDI is running (tray icon).
- Click **Refresh / Resync** in the Setup Assistant. The plugin also retries automatically every 3 seconds.

## Ports exist, but nothing happens (no names, keys do nothing)

**Windows 11 — restart loopMIDI after creating ports.**
On current Windows 11 builds (with the *Windows MIDI Services* background service), ports created while loopMIDI is already running can appear in Cubase and the Stream Deck app but pass **no data at all**.
1. Save your project and close Cubase.
2. Quit loopMIDI completely: tray icon → **Exit** (closing the window is not enough).
3. Start loopMIDI again — your ports are restored.
4. Start Cubase.

**loopMIDI disabled the ports (feedback protection).**
loopMIDI switches off a port when it detects a flood of messages, typically caused by a MIDI loop. Fix the loop (next section), then remove and re-add the two ports and restart loopMIDI as above.

## Prevent MIDI loops in Cubase

In **Studio → Studio Setup → MIDI Port Setup**:
- **`Cubase-To-SDXL` (In):** untick **In 'All MIDI Inputs'** (and ideally **Visible**). Cubase does not need to listen to this port. If it stays in *All MIDI Inputs*, a record-armed or monitoring MIDI track can echo CubaseBridge's feedback back out — a loop.
- **`SDXL-To-Cubase` (In):** Cubase removes it from *All MIDI Inputs* automatically once the MIDI Remote surface uses it. If it is still ticked, untick it, otherwise key presses can end up as MIDI notes/CCs in armed MIDI tracks.

## Cubase does not show the "CubaseBridge – StreamDeckXL" surface

- In the Setup Assistant, click **Install / Update Cubase Script** and check that the indicator turns green.
- **Studio → MIDI Remote Manager** → **↻** (Reload Scripts).
- Still missing? Click **Add Surface** → vendor *CubaseBridge*, model *StreamDeckXL*, input `SDXL-To-Cubase`, output `Cubase-To-SDXL`.
- Cubase only lists MIDI ports that existed when it started. If you created the ports later, restart Cubase.

## Surface is "Connected" but keys show no names/colors

- Click **Refresh / Resync** in the Setup Assistant (asks Cubase for a full state update).
- Check the two Windows 11 / loop items above — a silent port looks exactly like this.
- After updating the plugin, re-install the Cubase script (Setup Assistant shows *Update available*) and reload scripts.

## The profile is missing or the View keys do nothing

- The bundled profiles are installed when the plugin is installed from the Marketplace or from a `.streamDeckPlugin` file; the Stream Deck app asks you to confirm.
- A profile imported by hand (double-clicking a `.streamDeckProfile`) is a plain copy: the keys work, but the **◀ View / View ▶** keys cannot switch its pages. Remove it and reinstall the plugin package to get the plugin-owned profile.

---

## Known quirks (by design)

| What you see | Why |
|---|---|
| Punch In/Out, Pre-/Post-Roll, Count-In, Show Lanes, Low Latency, Mono and edit-tool keys can show the wrong state after you change them **in Cubase** | Cubase does not report these states to MIDI Remote scripts. CubaseBridge toggles the key light when you press it; changes made with the mouse in Cubase are not visible. Press the key once more to resynchronise. |
| **Cue 2 Click** does nothing on Cubase 12 or without a second cue channel | Cubase has only one Control Room click key command. On Cubase 13–15 with two cue channels configured in Control Room, Cue 1 and Cue 2 work independently with real feedback. |
| Talkback / DIM / Cue lights on Cubase 12 can drift | Cubase 12 has no Control Room access for scripts; CubaseBridge falls back to key commands and tracks the state itself. Cubase 13–15 report the real state. |
| Both meter bars move identically | Mono tracks always mirror one level to both bars. On Cubase builds without the per-channel meter API (present in Cubase 14 and 15), CubaseBridge shows the summed level on both bars. |
| Umlauts and other special characters in track names show as `?` | Names are transferred as plain ASCII over MIDI. |
| Track names are cut after ~10 characters on meter keys | The 96×96 key has room for about 10 characters. |
| Control Room keys need Control Room to be enabled | Enable it in **Studio → Audio Connections → Control Room**. |

---

## Still stuck?
Ask in [Discussions → Q&A](https://github.com/Wuestenrolph/CubaseBridge-Support/discussions/categories/q-a) or report a bug at [CubaseBridge-Support](https://github.com/Wuestenrolph/CubaseBridge-Support/issues/new/choose). Please include your OS, Cubase version, Stream Deck model and a screenshot of the Setup Assistant.
