### Verbindungstool 2026.10.30.7 und Firmware 4.2 / 5.2 / 10.2 – Sicherheit und Lizenzen

- **Updates ohne Zugangsschlüssel**: Das Update-Repository Raffi39/CNC-Pult-Updates ist öffentlich; der frühere
  Lese-Schlüssel (`UpdateToken.cs`, `token_eintragen.py`) entfällt. `build.cmd` löscht eine noch vorhandene
  `UpdateToken.cs`.
- **Updates sind unterschrieben**: `release.py` unterschreibt jede Version mit dem Update-Schlüssel des Herstellers
  (ECDSA P-256, privat nur in `_lizenz\Update-Schluessel\update_privat.blob`) und schreibt `SIGNATUR: …` in die
  Release-Beschreibung. Das Programm installiert nur Versionen mit gültiger Unterschrift (öffentlicher Teil in
  `UpdateKey.cs`). Unterschrieben ist `CNCPULT-UPDATE1:<Version>:<SHA-256 der Setup-Datei>`.
- **Hersteller-Werkzeug** `Quelltext\Werkzeug\Werkzeug.exe` (baut `build.cmd`, nur PC): Update-Schlüssel anlegen,
  Updates unterschreiben, Firmware verschlüsselt einbauen. Neues Skript `06_Firmware\firmware_bauen.ps1` baut alle
  Firmwares mit arduino-cli und baut sie ins Programm ein.
- **Netzwerk geschützt (Controller V5/V10, Firmware 5.2 / 10.2)**: Ethernet ist ab Werk aus. Im Reiter Platinen
  „Netzwerkbetrieb freischalten“ erzeugt das Programm einen Kopplungsschlüssel und überträgt ihn per USB (`NK`).
  Jede Netzwerkverbindung meldet sich mit HMAC-SHA256 an (`Y …`, beide Seiten prüfen sich); unangemeldete
  Verbindungen bekommen keine Daten und können eine bestehende Verbindung nicht mehr verdrängen.
  `N?` meldet zusätzlich, ob das Netzwerk freigeschaltet ist. Ältere Firmware wird im Netzwerk abgelehnt.
- **Firmware 4.2 / 5.2**: eigener WS2812-LED-Treiber (`ws2812_avr.h`, `ws2812_pio.h`) statt der Bibliothek
  „Adafruit NeoPixel“ (LGPL-3.0). Firmware 10.2: nur Netzwerkschutz.
- Die im Programm enthaltenen Firmware-Dateien werden erst mit `firmware_bauen.ps1` auf 4.2 / 5.2 / 10.2
  aktualisiert (braucht den Firmware-Schlüssel auf dem PC).

SIGNATUR: E2F19A717A175931B18ACCD54D8775FFD142B559F02EBC3F551E0231195C3CF6FE99AAF5E297FB2D0337A71ED6AF79628C3CD68461064266D0E37B9AF8CE0C14
