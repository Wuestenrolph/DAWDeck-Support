# Troubleshooting & Known Quirks

> REAPER problems: see the troubleshooting section in [DAWDeck for REAPER](REAPER.md).
> Ableton Live problems: see the troubleshooting section in [DAWDeck for Ableton Live](ABLETON.md).

Start with the **Setup Assistant** (click any DAWDeck key in the Stream Deck app). Its three indicators tell you where the problem is: **MIDI In**, **MIDI Out** and **MIDI Remote script** (one status covering Cubase and/or Nuendo; hover it to see each host's path). Everything in this guide applies to Nuendo too.

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

**Windows 11 — loopMIDI ports do not show up at all.**
With the *Windows MIDI Services* background service, loopMIDI ports created after the service started may be invisible to other apps (Microsoft has confirmed this bug and announced a fix).
1. Close Cubase and the Stream Deck app.
2. Start loopMIDI so the ports exist.
3. Open **Services** (`services.msc`), find the Windows MIDI service, click **Stop**, then **Start** (not *Restart*).
4. Start the Stream Deck app and Cubase again.

**loopMIDI disabled the ports (feedback protection).**
loopMIDI switches off a port when it detects a flood of messages, typically caused by a MIDI loop. Fix the loop (next section), then remove and re-add the two ports and restart loopMIDI as above.

## Prevent MIDI loops in Cubase

In **Studio → Studio Setup → MIDI Port Setup**:
- **`Cubase-To-SDXL` (In):** untick **In 'All MIDI Inputs'** (and ideally **Visible**). Cubase does not need to listen to this port. If it stays in *All MIDI Inputs*, a record-armed or monitoring MIDI track can echo DAWDeck's feedback back out — a loop.
- **`SDXL-To-Cubase` (In):** Cubase removes it from *All MIDI Inputs* automatically once the MIDI Remote surface uses it. If it is still ticked, untick it, otherwise key presses can end up as MIDI notes/CCs in armed MIDI tracks.

## Cubase does not show the "DAWDeck – StreamDeckXL" surface

- **Nuendo:** the script is only installed for Nuendo if `Documents/Steinberg/Nuendo` existed when you clicked *Install / Update Script*. Start Nuendo once, open the MIDI Remote tab, then click the button again.
- In the Setup Assistant, click **Install / Update Script** and check that the indicator turns green.
- **Studio → MIDI Remote Manager** → **↻** (Reload Scripts).
- Still missing? Click **Add Surface** → vendor *DAWDeck*, model *StreamDeckXL*, input `SDXL-To-Cubase`, output `Cubase-To-SDXL`.
- Cubase only lists MIDI ports that existed when it started. If you created the ports later, restart Cubase.

## Surface is "Connected" but keys show no names/colors

- Click **Refresh / Resync** in the Setup Assistant (asks Cubase for a full state update).
- Check the two Windows 11 / loop items above — a silent port looks exactly like this.
- After updating the plugin, re-install the Cubase script (Setup Assistant shows *Update available*) and reload scripts.

## Quick Control keys show "QC 1 … —" without names

- **Focus source:** Cubase reports the Quick Controls of the plug-in window that was **last clicked inside Cubase**. Click once onto the plug-in's surface (not only its title bar). Use **Focus Lock** to keep that plug-in while you click elsewhere.
- **Track source:** the selected track has no Quick Controls assigned (common on audio tracks). Assign them in the Inspector → *Quick Controls*, or switch the **Source** key to *Focus*.
- Long names and values are shortened to 16 characters on the keys.

## Quick Controls show the "wrong" parameters of a plug-in

**Steinberg plug-ins** come with useful Quick Control assignments and work right away. **Third-party plug-ins** get Cubase's default assignment, which is often their global settings. Example: FabFilter Pro-Q 3 starts with *Gain Scale, Output Level, Output Pan, Bypass, Auto Gain …* instead of the EQ bands.

To choose the parameters yourself:
1. Open the plug-in window in Cubase.
2. **Right-click the parameter** you want on the keys (e.g. a band's gain or frequency) and choose **Add '…' to Quick Controls** — or **Add '…' to Quick Controls Slot** to pick the slot and replace one you don't need.
3. Repeat for up to 8 parameters. The DAWDeck keys update immediately.

Verified with FabFilter Pro-Q 3. Cubase offers this right-click option for VST 3 plug-ins that support it.

## The profile is missing or the View keys do nothing

- The bundled profiles are installed when the plugin is installed from a `.streamDeckPlugin` file (later also from the Elgato Marketplace); the Stream Deck app asks you to confirm.
- A profile imported by hand (double-clicking a `.streamDeckProfile`) is a plain copy: the keys work, but the **◀ View / View ▶** keys cannot switch its pages. Remove it and reinstall the plugin package to get the plugin-owned profile.

---

## Known quirks (by design)

| What you see | Why |
|---|---|
| Punch In/Out, Pre-/Post-Roll, Count-In, Show Lanes, Low Latency, Mono and edit-tool keys can show the wrong state after you change them **in Cubase** | Cubase does not report these states to MIDI Remote scripts. DAWDeck toggles the key light when you press it; changes made with the mouse in Cubase are not visible. Press the key once more to resynchronise. |
| **Cue 2 Click** does nothing on Cubase 12 or without a second cue channel | Cubase has only one Control Room click key command. On Cubase 13–15 with two cue channels configured in Control Room, Cue 1 and Cue 2 work independently with real feedback. |
| Talkback / DIM / Cue lights on Cubase 12 can drift | Cubase 12 has no Control Room access for scripts; DAWDeck falls back to key commands and tracks the state itself. Cubase 13–15 report the real state. |
| Both meter bars move identically | Mono tracks always mirror one level to both bars. On Cubase builds without the per-channel meter API (present in Cubase 14 and 15), DAWDeck shows the summed level on both bars. |
| Umlauts and other special characters in track names show as `?` | Names are transferred as plain ASCII over MIDI. |
| Track names are cut after ~10 characters on meter keys | The 96×96 key has room for about 10 characters. |
| Control Room keys need Control Room to be enabled | Enable it in **Studio → Audio Connections → Control Room**. |
| **Monitor C/D** or **Cue 3/4** do nothing | Those keys address the third and fourth monitor/cue channel. Add them in **Studio → Audio Connections → Control Room**; with fewer channels the keys have no target. |
| **Downmix 1–4** light follows your last key press only | Cubase does not report the active downmix preset to scripts. The key shows the preset you last selected from the Stream Deck. |
| **Colorize** keys do nothing | Install the presets in the Setup Assistant (**Install Colorize Presets**) and restart Cubase once. Cubase only picks up new Project Logical Editor presets at start-up. |
| One ▲/▼ press moves a Quick Control only a little | Each press is one Cubase step (fine). Hold the key: the auto-repeat speeds up after about a second. The Stream Deck + dials send every tick for fast sweeps. |
| Stream Deck + dials are empty after installing the profile | The dial action is not pre-assigned by the profile; drag **Quick Control Dial** onto the four dials once (see INSTALLATION). |

---

## Still stuck?
Ask in [Discussions → Q&A](https://github.com/Wuestenrolph/DAWDeck-Support/discussions/categories/q-a) or report a bug at [DAWDeck-Support](https://github.com/Wuestenrolph/DAWDeck-Support/issues/new/choose). Please include your OS, Cubase version, Stream Deck model and a screenshot of the Setup Assistant.
