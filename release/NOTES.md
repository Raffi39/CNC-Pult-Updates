### Verbindungstool 2026.10.30.5 und Firmware 4.1 / 5.1 / 10.1 – Original-Firmware und Firmware-Update

- **Original-Prüfung ohne Einzel-Freigabe**: Der geheime Firmware-Schlüssel (ECDSA P-256) steckt in jeder
  Original-Firmware; das Programm prüft mit einer Zufallsfrage (`Z` → `Z OK2 <ID> <Version> <Unterschrift>`).
  Gilt für alle Platinen ab Controller V3.0 (neue Firmware **4.1** für ATmega32U4) sowie V5 (**5.1**) und V10 (**10.1**).
  Freigabe-Werkzeug und Einzel-Freigabe (`ZP`/`ZC`) entfallen.
- **Firmware-Update über das Programm**: Firmware verschlüsselt im Programm enthalten, automatische Nachfrage bei
  älterer Firmware (oder Knopf im Reiter Platinen). RP2040 über das UF2-Laufwerk, ATmega32U4 über den
  Arduino-Bootloader (AVR109) oder den Atmel-DFU-Bootloader (WinUSB). Einstellungen werden vorher gesichert.
- Firmware: neue Kennung `… ID <Platinen-ID> FW <Version>`, Befehl `U` (Bootloader starten, V4.1 zusätzlich `UJ`
  für den Atmel-DFU-Bootloader); Firmware 4.1 erzeugt eine eindeutige Platinen-ID im EEPROM.

### Verbindungstool 2026.10.30.4 – Update-Test

- Nur neue Versionsnummer, um das automatische Update von 2026.10.30.3 aus zu prüfen (Release im Update-Repository).

### Verbindungstool 2026.10.30.3 und Firmware V5/V10 – nur Original-Platinen

- **Original-Prüfung**: Jede freigegebene Platine hat einen eigenen geheimen Schlüssel (ECDSA P-256) und ein
  Zertifikat des Herstellers. Das Verbindungsprogramm stellt bei jedem Verbinden eine Zufallsfrage; nur eine
  Original-Platine kann sie richtig beantworten. Andere Platinen werden angezeigt, aber gesperrt (keine Tasten,
  keine Potis) – dann ist nur die Simulation möglich.
- **Firmware V5 und V10**: neue Befehle `Z` (Prüfung), `ZP`/`ZC` (Freigabe, nur über USB); Kennung mit Platinen-ID
  auch bei V5 (`… B5.0 ETH ID <Chip-ID>`). Firmware V3/V4 (ATmega) hat keine Original-Prüfung.
- **CNC-Pult-Freigabe.exe** (nur für den Hersteller): Hauptschlüssel verwalten (Sicherung mit Passwort),
  Platinen über USB freigeben, Freigabeliste `_lizenz\Freigaben.csv`.
- Update-Zugang mit Lese-Schlüssel für das private Repository Raffi39/CNC-Pult-Updates.

### Verbindungstool 2026.10.30.2 – automatische Updates

- Sucht beim Start und täglich nach einer neuen Version (privates Update-Repository, Zugriff nur über das Programm).
- Ein Klick: Einstellungen sichern, Setup herunterladen und prüfen (Größe, SHA256), Programm beenden,
  aktualisieren und neu starten – ohne Browser. Setup hat dafür den Modus `/update` (übernimmt Ordner,
  Startmenü/Desktop/Autostart der bisherigen Installation).
- Allgemein: „Updates“ (ein/aus, jetzt suchen); „Diese Version überspringen“ möglich.

### Verbindungstool 2026.10.30 – Programmfenster beim Start

- Neue Einstellung „Programmfenster beim Start“ (Einrichtungsassistent und Reiter Allgemein): nur im Infobereich
  der Taskleiste, minimiert oder normales Fenster. Im Infobereich: Doppelklick öffnet, X/Minimieren legt zurück,
  Beenden über das Kontextmenü, Tooltip mit Verbindungsstatus.
- Ein zweiter Programmstart holt das laufende Fenster nach vorne (statt der Meldung „läuft bereits“),
  auch wenn das laufende Programm als Administrator läuft.

### Verbindungstool 2026.10.30 – Installation und Einrichtungsassistent

- **CNC-Pult-Setup.exe**: Installation nach `C:\Program Files (x86)\CNC-Pult-Verbindung` mit Startmenü,
  Desktop-Verknüpfung, Autostart (wählbar), Eintrag in Windows „Apps“, Deinstallation (Einstellungen bleiben
  auf Wunsch erhalten), Übernahme der Einstellungen einer früheren Version. Zum Weitergeben genügt die Setup-Datei.
- **Einrichtungsassistent** (erster Start, Reiter Allgemein, Startmenü): findet alle EdingCNC-Installationen
  (Windows-Programmliste, Laufwerke, laufender Server) mit Version und schlägt die laufende vor; Makrodatei mit
  Erklärung, Markierung der von EdingCNC benutzten Datei (server.ini) und Vorschau der Unterprogramme;
  „Später einrichten“ jederzeit möglich.
- Einstellungen liegen jetzt in `C:\ProgramData\CNC-Pult-Verbindung` (alte Datei neben der exe wird einmalig
  übernommen), Sicherung der letzten 20 Stände im Unterordner „Sicherungen“; `portabel.txt` neben der exe
  behält den alten Speicherort.
- Programmversion im Fenstertitel, eigenes Programmsymbol.

### Verbindungstool 2026-10-30 – Nachfrage bei ungespeicherten Änderungen

- Ungespeicherte Änderungen werden zuverlässig erkannt (Vergleich mit dem zuletzt gespeicherten Stand, erfasst
  alle Reiter, auch Pfade und automatisch gelernte Platinen-IDs). Beim Schließen kommt die Nachfrage
  Speichern / Verwerfen / Abbrechen; schlägt das Speichern fehl, bleibt das Programm offen.
- Fenstertitel zeigt „* Änderungen nicht gespeichert“, solange etwas offen ist.

### Verbindungstool 2026-10-30 – Sicherheitszeit

- Neu: **Sicherheitszeit** je Taste einschaltbar (Reiter „Tasten und LEDs“), Dauer global unter Allgemein
  (Standard 500 ms). Die Funktion löst erst aus, wenn die Taste mindestens so lange gedrückt bleibt;
  kürzeres Drücken / Drüberwischen wird ignoriert und protokolliert. Druckpunkt-LED erst nach dem Auslösen,
  oranger Rahmen auf dem Bildschirm während die Zeit läuft. Gilt für echte und simulierte Platinen.
- Korrektur: Der Haken „Sicherheitszeit (… ms)“ zeigt sofort die unter Allgemein eingestellte Zeit.

### Verbindungstool 2026-10-30 – mehrere Platinen

- **Mehrere Platinen gleichzeitig** (verschiedene Versionen, USB und Netzwerk gemischt), jede mit
  eigenem Namen, Version, Betrieb (Echt / Simulation / Aus), Verbindung, Helligkeit, „Poti verwenden“
  und eigener Tastenbelegung. Poti-Bereiche, Farben, Jog und EdingCNC bleiben global.
- Neuer Reiter **„Platinen“** (ersetzt „Platineneinstellungen“): Platinen anlegen, duplizieren,
  entfernen, sortieren; gefundene, nicht zugeordnete Hardware zuordnen oder als neue Platine anlegen;
  Netzwerkeinstellungen gelten für die gewählte Platine.
- Zuordnung: Platinen-ID (ab Firmware V10) → fester COM-Anschluss → „Auto“ (passendes Tastenlayout).
- **Controller V10** wird unterstützt: 64 Taster in Klemmen-Anordnung J20–J35, einfarbige LEDs
  (aus / leuchten / blinken, „LED angeschlossen“, Anzeigefarbe).
- Reiter „Tasten und LEDs“ und „Simulation“ mit Platinen-Leiste; die Simulation zeigt die Platinen mit
  Betrieb = Simulation, die Auswahl „Simuliertes Board“ entfällt. Echte Platinen laufen beim Simulieren weiter.
- Platinen lassen sich ohne Hardware vorkonfigurieren und in der Simulation testen.
- Abwärtskompatibel: alte Einstellungsdateien werden als Platine „Pult 1“ übernommen; die alten Felder
  werden weiter geschrieben (erste Platine), ältere Programmversionen können die Datei lesen.
- Sicherung der Vorversion: `07_Verbindungsprogramm/Sicherung_2026-10-30_vor_Mehrplatinen/`.

### Firmware V10 2026-10-30 (Nachtrag)

- Kennung um eine eindeutige Platinen-ID erweitert: `I CNC-PULT V10 64 64 0 B10.0 ETH MONO ID <Chip-ID>`.

### Firmware V10 2026-10-30

- **Neue Firmware V10** für Controller V10 (64 externe Taster an Schraubklemmen J20–J35),
  Basis Firmware V5 (USB + Ethernet, Netzwerkeinstellungen, Suche per UDP unverändert).
- Taster über 74HC165-Kette (GPIO0–2), LEDs über TPIC6B595-Kette (GPIO3–6) mit Helligkeit per PWM an /G.
- Kennung `I CNC-PULT V10 64 64 0 B10.0 ETH MONO`, Zustandsmeldung `S` mit 16 Hex-Zeichen (64 Taster).
- Einfarbige LEDs: `L`-Befehl wie bisher, LED an, wenn die Farbe nicht 000000 ist. `P` (Ausgänge) wird ignoriert.
- Noch nicht auf Hardware getestet; das Verbindungsprogramm muss die V10 noch unterstützen.

### Verbindungstool 2026-10-25

- **Start nach Vorschub-Halt:** Ist der Job pausiert, fährt die Start-Taste jetzt wie die Start-Taste
  der Eding-Oberfläche erst zur Pausenposition zurück (X/Y zuerst, dann Z) und setzt danach fort
  (`CncSyncFromPauseAndStartAutomatic`). Behebt „S1092: Z not at resume position“.
  Neue Einstellung „Start nach Pause: Rückfahrt … mm/min“ (Standard 1000).
- **Absturz von EdingCNC beim Beenden behoben:** Das Tool meldet sich als reiner Client an
  (`CncConnectServer("")`). Vorher wurde mit Ini-Namen verbunden; dann schickt `CncDisConnectServer`
  beim Beenden einen Shutdown an CncServer.exe und die Eding-Oberfläche hängt sich auf.

