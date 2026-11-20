# Privacy Statement — DAWDeck

_Last updated: 1.0.0 release_

DAWDeck does **not collect, store or transmit any personal data**.

- **No network access.** The plugin communicates only with Steinberg Cubase on the same computer through two local virtual MIDI ports (`SDXL-To-Cubase`, `Cubase-To-SDXL`) and with the Elgato Stream Deck app through its local plugin interface.
- **No accounts, analytics or telemetry.** Nothing is sent to the developer or any third party.
- **Data processed locally.** Track names, track colors, meter levels, mixer and transport states are received from Cubase solely to draw the Stream Deck keys. They are kept in memory while the plugin runs and are never written to disk or sent anywhere.
- **Files written.** The Setup Assistant copies the DAWDeck MIDI Remote script into your Cubase and/or Nuendo *Documents* folder when you click **Install / Update Script**. Key settings are stored by the Stream Deck app as part of your profiles. The Stream Deck SDK writes local diagnostic log files inside the plugin folder.
- **Windows registry (read-only).** On Windows, the plugin reads the location of your *Documents* folder (`User Shell Folders\Personal`) to support OneDrive-redirected folders.

Contact: [DAWDeck-Support](https://github.com/Wuestenrolph/DAWDeck-Support/issues)
