### Verbindungstool 2026.11.10.1 und Drehknopf-Firmware 1.8 – Drehknöpfe, Kopierschutz mit eigenem Schlüssel je Platine, Dialoge mit mehreren Feldern

- **Kopierschutz: eigener Schlüssel je Platine** (Raffi 10.11.2026, „Punkt 2“; Firmware 4.9 / 5.7 / 10.6 / 15.6):
  Die Controller-Firmware enthält keinen gemeinsamen geheimen Schlüssel mehr. Jede Platine erzeugt bei der
  Einrichtung durch den Hersteller (neues Werkzeug `CNC-Pult-Einrichtung.exe`, nur auf dem Hersteller-PC in `_lizenz`,
  Start über `Platine_einrichten.cmd`) ein eigenes Schlüsselpaar; der geheime Teil verlässt die Platine nie, der
  öffentliche wird zusammen mit der Platinen-ID mit dem neuen Hersteller-Schlüssel unterschrieben (Zertifikat, im
  EEPROM, bleibt bei Updates erhalten). Prüfung „Z OK3“: Zertifikat + Antwort der Platine. Nachbauten und kopierte
  Firmware haben kein gültiges Zertifikat; eine 1:1-Kopie des Speichers auf einen anderen RP2040/RP2350 passt nicht
  (Zertifikat und Schlüsselmaske hängen an der Chip-ID). Alte Firmware („Z OK2“) gilt nicht mehr.
  Einrichtungsbefehle „E …“ nur über USB. Das Tool spielt Firmware (auch Modul-Firmware) nur noch auf Original-
  Platinen auf; neue Platinen und Platinen mit alter Firmware laufen einmal durch das Einrichtungs-Werkzeug
  (Firmware aufspielen, Schlüssel erzeugen, unterschreiben, Gegenprobe, Eintrag in `_lizenz/Platinenliste.csv`).
  Neue Geheimnisse: `_lizenz/Hersteller-Schluessel/hersteller_privat.blob` (wird beim ersten Bauen angelegt – sichern!).
  `fw_key.h` wird nicht mehr gebraucht.
- **Dialog mit mehreren Feldern über UI Automation** (Raffi 11.11.2026): EdingCNC 5.3 ist mit Qt 5.15 gebaut, seine
  Dialoge haben keine Windows-Eingabefelder (Diagnose: „Felder 0 … Steuerelemente: keine“), deshalb schloss der Klick am
  Drehknopf den Dialog „Werkzeug ohne gespeicherte Laenge“ sofort. Neu `DialogUia.cs`: Felder (Zahlenfelder, Textfelder,
  Auswahllisten), Fokus und Wert über UI Automation; Klick springt mit Tab ins nächste Feld, erst im letzten Feld Enter.
  Der Wert des Fokusfelds erscheint jetzt auch bei Qt-Dialogen am Drehknopf (eigener Thread, alle 300 ms). Diagnose hinter
  „Dialog: Enter“ zeigt zusätzlich, was UI Automation findet. build.cmd: Verweise UIAutomationClient/-Types, WindowsBase.
- Hersteller-Schlüssel beim ersten Bau angelegt, `HerstellerKey.cs` vom PC übernommen; erste Platine (Controller V3.x,
  Firmware 4.9) eingerichtet.
- **Drehknopf-Firmware 1.8 – CrowPanel 1,46":** Display blieb schwarz/gestreift (Raffi 10.11.2026, erster Test des
  1,46"). Die aktuelle LovyanGFX startet das Panel mit einer Sequenz für ein anderes ST77961-Panel; die Firmware nutzt
  jetzt die Startsequenz aus dem Elecrow-Beispiel für genau diese Platine, dazu spi_3wire/rgb_order wie bei Elecrow und
  einen Reset-Puls nach dem Einschalten. Noch nicht auf dem Gerät bestätigt.
- **Dialog-Erkennung:** Das Hauptfenster von EdingCNC 5.3 („CNC V5.3.2 / Simulation …“) galt fälschlich als Dialog
  (Raffi 10.11.2026). Fenster mit Titel „CNC V…“ gelten jetzt als Hauptfenster, und ein Fenster ohne Besitzer zählt
  nur als Dialog, wenn es das Hauptfenster sperrt. Diagnose im Protokoll hinter „Dialog: Enter“ (Steuerelemente und
  Fokus), um das Weiterspringen in Dialogen mit mehreren Feldern („Werkzeug ohne gespeicherte Laenge“) zu richten.
- Gemeldet von Raffi am 10.11.2026 (erster Test mit dem CrowPanel 1,28"): je Raste wurden 2 Schritte gezählt (2 %),
  teils unruhig.
- **Firmware 1.1:** Der Knopf zählt jetzt ganze Rasten mit einem Zustandsautomaten (gezählt wird erst, wenn A/B
  einen vollständigen, gültigen Ablauf bis zur Ruhelage durchlaufen haben). Prellen und Zittern in der Raste zählen
  nicht mehr. Drehrichtung wie bisher. Für Drehgeber mit halbem Zyklus je Raste gibt es eine Einstellung.
- **Tool:** statt „Zählschritte je Raste“ jetzt „Drehgeber: voller Zyklus je Raste (Standard) / halber Zyklus“.
  Ein Knopf mit Firmware 1.0 wird bis zum Update passend umgerechnet (4 Flanken = 1 Raste).
- „Schnell gedreht“ (grobe Schrittweite) erst, wenn 3 Rasten in Folge schnell kamen – einzelne Ausreißer springen
  nicht mehr um 5 %.
- Reiter „Drehknöpfe“: Knopf **„Speichern“** unter der Vorschau.
- **Programm Start/Pause auf der Vorschubseite** (Firmware 1.6, Option je Knopf, Vorgabe aus; Raffi 10.11.2026):
  kein Programm → 5 s halten = Programm starten (innerer Bogen und „Start in 3/2/1“, Loslassen vorher bricht ab;
  nur wenn EdingCNC bereit, referenziert, kein Not-Halt, keine Störung, nichts läuft, Echtbetrieb erlaubt – sonst
  Meldung im Display). Ob ein Programm geladen ist, kann das Tool vorab nicht abfragen: EdingCNC lehnt den Start dann
  ab, der Knopf zeigt „Start abgelehnt“. Programm läuft → kurz drücken = Pause, pausiert → kurz drücken = weiter
  (gleiche Wege wie die Pult-Tasten); die Seite wechselt dann nicht. „Lang drücken = 100 %“ löst mit der Option erst
  beim Loslassen nach 1–5 s aus, ab 5 s gilt Start. Dialog-Bedienung hat Vorrang. Neue Meldungszeile Tool → Knopf.
  Vorschau: Umschalt+Rechtsklick = 5 s halten.
- **Zweitbelegung der Tasten bei offenem EdingCNC-Dialog** (Wunsch von Raffi, 10.11.2026): je Taste „wie immer“,
  „gesperrt“ oder „Taste senden“ (Pfeile, Enter, ESC, Tab, Bild auf/ab …); Pfeil-/Bildtasten wiederholen sich beim
  Halten (0,4 s, dann alle 100 ms). Erkannt wird ein Dialog wie beim Tastenkürzel-Senden (oberstes bedienbares Fenster
  von EdingCNC über dem Hauptfenster, alle 200 ms); Öffnen/Schließen steht im Protokoll und im Reiter Simulation.
  Läuft beim Öffnen eine Jog-Bewegung einer Taste mit Zweitbelegung, stoppt sie sofort. Knopf „Dialog-Belegung für
  das Jog-Feld vorschlagen“: X−/X+ = ←/→, Y+/Y− = ↑/↓, Eilgang = Enter, oben rechts im Jog-Feld = ESC, übrige
  Verfahrtasten gesperrt.
- **Dialog-Erkennung korrigiert** (gemeldet von Raffi am 10.11.2026: beim Programmstart zeigte der Knopf kurz
  „Dialog: EdingCNC Simulation – D:\OneDrive\…“, obwohl kein Dialog offen war): Das Hauptfenster von EdingCNC
  (Fenster ohne Besitzer, Titel beginnt mit „EdingCNC“) gilt nie als Dialog, auch wenn Windows ein anderes Fenster als
  Hauptfenster meldet. Ein Dialog gilt erst als offen, wenn er bei zwei Abfragen nacheinander (200 ms) oben liegt.
  Das Tool öffnet oder schließt selbst keine Dialoge – EdingCNC zeigt sie wie immer, Knopf und Tasten fernbedienen sie nur.
- **Beim Programmstart auf die erste Seite springen** (Firmware 1.7, Option je Knopf, Wunsch von Raffi 10.11.2026):
  Startet in EdingCNC ein Fräsprogramm (Zustand RUNNING = Job), springt der Knopf auf die erste Seite seiner Liste –
  z. B. ein Knopf auf Vorschub, ein zweiter auf Spindel. Nicht bei MDI, Makros oder Werkzeugwechsel über die
  Oberfläche und nicht beim Fortsetzen nach einer Pause. Protokoll „Programmstart erkannt (EdingCNC: …)“.
  Protokoll Tool → Knopf: Byte SPRUNG (Folgenummer) am Ende des Zustandsrahmens; ältere Firmware ignoriert es.
- **Werkzeugwechsel auf der Statusseite** (Firmware 1.7, Raffi 10.11.2026): läuft ein Werkzeugwechsel (EdingCNC
  arbeitet und das angeforderte Werkzeug #5011 weicht vom aktuellen ab), zeigt die Statusseite „T4 → T28“ (neues
  Werkzeug gelb, Pfeil gezeichnet), auch in der Vorschau. Protokoll: NEUWZ(2) am Ende des Zustandsrahmens.
- **Start/Pause nur auf der Job-Seite** (Raffi 10.11.2026): Klick = Pause/weiter und 5 s = Start wirken nur noch, wenn
  das Häkchen „Start/Pause auf der Vorschubseite“ gesetzt ist **und** Vorschub die erste Seite der Liste ist **und**
  „Beim Programmstart auf die erste Seite springen“ an ist. Sonst blättert ein Klick auf der Vorschubseite wie überall.
- **Dialoge mit mehreren Eingabefeldern** (Wunsch von Raffi, 10.11.2026): Klick am Drehknopf springt zum nächsten Feld
  (Tab), erst im letzten Feld bestätigt der Klick (Enter). Felder sind die sichtbaren, bedienbaren Windows-Eingabefelder
  des Dialogs, von oben nach unten und links nach rechts gezählt; Protokoll „Dialog: nächstes Feld (2 von 3)“. Findet
  das Tool keine lesbaren Felder oder steht der Fokus auf keinem Feld (z. B. auf einer Schaltfläche), bleibt Klick = Enter.
- **Drehknopf bedient EdingCNC-Dialoge** (Firmware 1.5, je Knopf einschaltbar): Display zeigt Dialog-Titel und – wenn
  lesbar (Windows-Eingabefeld mit dem Fokus) – den Wert; drehen = ↑/↓, Klick = Enter, 1 s = ESC. Overrides bleiben
  dabei unverändert.
- **Werkzeugwechsel am Knopf** (Firmware 1.4, Wunsch von Raffi 10.11.2026): auf der Seite Status den Knopf 5 s gedrückt
  halten (weißer Fortschrittsbogen ab 1 s) → Werkzeug wählen (drehen), Klick = einwechseln, 1 s drücken oder 15 s
  nichts tun = abbrechen. Das Tool führt „T<n> M6“ per MDI aus – nur wenn EdingCNC bereit ist (kein Programm, keine
  Pause, kein Fehler, kein Not-Halt), sonst nur Protokollmeldung. Einstellung „Werkzeugwechsel: höchste
  Werkzeugnummer“ (Standard 99, 0 = aus).
- **Texte passen ins runde Display** (Firmware 1.4, Raffi 10.11.2026: „Abgebrochen - Reset“ ragte beim 1,28" über den
  Rand): jeder Text wird gegen die nutzbare Breite auf seiner Höhe geprüft – erst kleiner (bis 75 %), dann zweizeilig,
  notfalls gekürzt; auf der Seite Status rücken Titel und Werkzeugnummer bei zweizeiligem Zustand zur Seite. Vorschau
  im Reiter ebenso. Zustandstext bei Abbruch jetzt „Abbruch, Reset nötig“.
- Firmware 1.3: Anzeige „nicht verbunden“ mit dem Logo (Bildzeichen „Nullpunkt“) groß oben mittig, Schriften darunter
  (Wunsch von Raffi, 10.11.2026); Vorschau im Reiter ebenso.
- Override am Anschlag (z. B. Spindel bei 24 000 U/min, EdingCNC lässt nur 100 % zu): Weiterdrehen zählte im Tool
  weiter hoch, Zurückdrehen wirkte erst nach einigen Rasten (Raffi 10.11.2026). Jetzt gilt der von EdingCNC gemeldete
  Wert, sobald er vom gesetzten abweicht – Zurückdrehen wirkt sofort.
- **LED-Ring „Farbe = Maschinenzustand“ wie die Ampel/Reset-Taste in EdingCNC** (Raffi 10.11.2026; zeigte bei
  laufendem Programm rot): grün = Programm läuft, gelb blinkend = Pause, rot blinkend = Störung bzw. Reset nötig
  (nach Start, Fehler, Abbruch), rot schnell blinkend = Not-Halt, orange = Referenzfahrt fehlt, blau = Verfahren,
  gelb = bereit (Firmware 1.2, wie die EdingCNC-Ampel); nicht verbunden (Tool oder EdingCNC): Ring aus, Hinweis nur im Display. Gleiche Farben im Display (Seite Status) und in der Vorschau.
  Neue Einstellung „LED-Ring: Rot und Grün tauschen“, falls der Ring andere Farben zeigt als das Display.
- Nach dem Bauen den Knopf über „Firmware aktualisieren“ auf 1.1 bringen (erster echter Test des Updates über USB).

### Verbindungstool 2026.11.09.4 und Drehknopf-Firmware 1.0 – Reiter „Drehknöpfe“, Handrad als Beta [in Arbeit, aufgegangen in 2026.11.10.1]

- **Neu: Reiter „Drehknöpfe“** für den Drehknopf mit rundem Display (Elecrow CrowPanel ESP32 Rotary Display 1,28"
  und 1,46", direkt per USB am PC). Mehrere Knöpfe; echte Knöpfe werden beim Anstecken erkannt (Seriennummer) und
  angelegt, dazu Simulation und Duplizieren. Einstellbar je Knopf: Modell, angezeigte Seiten (Vorschub, Spindel,
  Status, Position) mit Reihenfolge, Titel und Startseite, Kopfzeile mit Istwert, Akzentfarbe, Helligkeit,
  LED-Ring (aus / Zustandsfarbe / Override-Balken), Farben umkehren, 180° drehen, Override je Raste fein/schnell,
  Zählschritte je Raste, Drehrichtung, Raststelle 100 %, lang drücken = 100 %. Vorschau wie am Knopf (vereinfacht),
  in der Simulation mit Mausrad/Klick bedienbar. Einstellungen werden sofort an den Knopf übertragen.
- Drehen stellt den Override der angezeigten Seite (Grenzen aus „Allgemein“, wie die Potis; ist ein Poti aktiv,
  wirkt der Knopf nicht auf diesen Override). Gesetzt wird nur im Engine-Ablauf (cncapi.dll nur dort).
  Echtbetrieb wie beim Handrad nur mit angeschlossener Original-Platine (bzw. 1 Stunde danach oder Testmodus).
- Firmware des Knopfs aus dem Tool: Update über das eigene Protokoll (zwei App-Bereiche, bei Abbruch bleibt die
  alte Firmware) und Erstinstallation/Notweg über den ROM-Lader des ESP32-S3 (Espressif Serial Protocol in C#,
  kein esptool nötig). Firmware wird wie die Controller-Firmware verschlüsselt eingebaut (fw_DK.bin, fw_DKV.bin);
  build.cmd baut sie nur ein, wenn sie gebaut ist.
- Pult-Suche (und Bootloader-Suche beim Firmware-Update) lassen Anschlüsse mit USB-Kennung 303A (Espressif) aus –
  deren DTR/RTS-Wechsel würden den ESP32-S3 neu starten.
- Neue Firmware `06_Firmware/Firmware_DK` 1.0 (LovyanGFX, ESP32-Arduino-Core 3.x), Bau mit
  `firmware_bauen.ps1 DK` (Core und Bibliothek werden beim ersten Mal installiert; schlägt das fehl, werden die
  anderen Firmwares trotzdem gebaut). Protokoll in `dk_proto.h`. Lizenzhinweise ergänzt (THIRD_PARTY_NOTICES).
- **Noch nicht an Hardware getestet** (Muster bestellt). Am Muster zu prüfen: siehe `Firmware_DK/BESCHREIBUNG.txt`.
- Reiter „Handrad“ wieder sichtbar als **„Handrad (Beta)“** mit großer Warnung „ACHTUNG: BETA – NICHT GETESTET“
  (Wunsch von Raffi, 09.11.2026); Handrad-Betrieb und Listeneinträge wieder aktiv (`AppInfo.HandradFreigegeben = true`).

### Verbindungstool 2026.11.09.3 und Folien-Editor – Kühlung während des Programms, sichereres Beenden, Bild umkehren [in Arbeit, aufgegangen in 2026.11.09.4]

- Folien-Editor: neues Kästchen „Bild umkehren (hell ↔ dunkel)“ unter „Ausgewählte Taste“ (nur bei eigenen Bildern):
  das Bild wird als Negativ gedruckt – z. B. das EdingCNC-RESET-Logo mit dunkler Schrift auf hellem Grund, damit es
  sich gut hinterleuchten lässt. Wirkt im Farb- und im Schwarz-Weiß-Druck, wird mit der Folie gespeichert
  (Wunsch von Raffi, 09.11.2026).

- Beenden sicherer (Absturz beim Schließen, gemeldet von Raffi am 09.11.2026): Alle Abläufe des Tools (auch der
  Schutz-Ablauf) werden erst beendet, bevor die Verbindung zu EdingCNC getrennt wird. Hängt ein Ablauf noch in einem
  EdingCNC-Aufruf, wird die Verbindung nicht mehr aktiv über cncapi.dll getrennt (das kann cncapi.dll abstürzen lassen).
  Jeder Schritt beim Beenden ist einzeln abgesichert.
- Meldungen beim Beenden landen jetzt im Protokoll.txt (bisher gingen sie verloren, weil der Anzeige-Takt schon stand).
- Unbehandelte Fehler werden mit Ablaufstelle ins Protokoll geschrieben; Fehler in der Oberfläche beenden das Programm
  nicht mehr, sondern zeigen einen Hinweis.

- Kühlung Flut/Nebel per Pult-Taste auch während ein Programm läuft oder pausiert: EdingCNC nimmt dann keine
  MDI-Befehle an („not allowed in state running“). Das Tool schaltet in diesem Fall – wie die Kühlungstasten in
  EdingCNC – direkt den Ausgang FLOOD bzw. MIST. Im Zustand Bereit bleibt es bei M7/M8/M9 (gemeldet von Raffi am 09.11.2026).

SIGNATUR: 154E0342CA109EA203A3A9D2834400E9CE0A99571265D88FA70828B1F0BCE12731D84260FED847CBBFA5F304A5BF189EFAF9E7BC5CF406624B2F9E15D99E8E90
