### Firmware 4.6 (Controller V3.x) und 5.4 (Controller V5) – LEDs aus ohne Verbindungsprogramm [in Arbeit]

- Ohne Lebenszeichen vom Verbindungsprogramm (1,5 s, z. B. Programm geschlossen) bleiben alle LEDs aus.
  Bisher pulsierten sie langsam gedimmt blau. Ausgänge sind wie bisher aus.
- 4.6 enthält alle Änderungen von 4.5 (Update ohne RESET-Taste).

### Verbindungstool – Eilgang nur solange die Taste gedrückt ist [in Arbeit]

- Eilgang-Taste während des Verfahrens drücken → die Achse wird sofort schneller; loslassen → sofort zurück auf die
  eingestellte Stufe. Bisher galt die Geschwindigkeit vom Beginn der Bewegung bis zum Loslassen der Achstaste
  (Eilgang danach gedrückt: keine Wirkung; Eilgang vorher gedrückt und losgelassen: blieb im Eilgang).
- Ebenso wirkt ein Wechsel der Tempostufe (langsam/mittel/schnell) jetzt sofort auf eine laufende Bewegung.
- Technik: EdingCNC übernimmt den Geschwindigkeitsfaktor nur beim Start einer Bewegung, deshalb wird die laufende
  kontinuierliche Bewegung mit dem neuen Faktor neu gestartet (gleiche Achse, Richtung, Taste). Schrittbewegungen
  laufen mit ihrem Faktor zu Ende.

### Verbindungstool – Hintergrund- und Status-Helligkeit getrennt einstellbar [in Arbeit]

- Farbige Platinen (V3.x, V5): Reiter **Platinen** → „Hintergrund (%)“ stellt nur noch die Hintergrundbeleuchtung ein.
  Unter **Tasten und LEDs** hat „Status EIN“ und „Status AUS“ je Taste ein eigenes Feld „Hell. %“ (für Leuchten und
  Blinken; das Aufleuchten beim Drücken nutzt die Helligkeit von „Status EIN“).
- Technik: Die Firmware läuft bei farbigen Platinen fest mit Höchsthelligkeit (H 120), das Programm dunkelt die
  Farbwerte ab. Keine Firmware-Änderung nötig. Die Bildschirmvorschau zeigt weiter die vollen Farben.
- Alte Einstellungen sehen unverändert aus: Solange nichts neu eingestellt ist, gilt die frühere Platinenhelligkeit
  (z. B. 40 von 120 = 33 %) für Hintergrund und Status.
- Einfarbige Platinen (V10, V15): wie bisher eine gemeinsame Helligkeit (0–120) im Reiter Platinen – die Hardware
  dimmt alle Ausgänge gemeinsam, eine getrennte Status-Helligkeit ist dort nicht möglich.

### Firmware V15 15.2, Modul-Firmware 1.4 (E8/E16/O8) und Verbindungstool – Erweiterungsmodule [in Arbeit]

- **Modul-Firmware 1.4 (06.11.2026) für die geänderte O8-Platine** (Q60/R602, siehe PRUEFBERICHT_O8_V1):
  - /OE der Schieberegister jetzt über den MOSFET Q60: GPIO6 HIGH = Ausgänge frei. Beim Start bleibt GPIO6 LOW
    (Gate-Pull-down R601), erst Nullen schieben, dann freigeben – kein Einschaltimpuls beim Hochlaufen.
    **1.4 nur auf O8 mit Q60 verwenden** (auf einer alten O8 ohne Q60 wären die Ausgänge gesperrt).
  - Lastspannungsüberwachung: 9. Messplatz mit allen DEN aus misst VLOAD über R602 (330 kΩ; R603 entlädt VLOAD, D23 jetzt M7 mit kleinem Sperrstrom). Bewertet wird der Sprung: „fehlt“ bei Abfall um mehr als ca. 12 V gegenüber dem Wert mit Lastspannung, „wieder da“ bei Anstieg um mehr als ca. 16 V gegenüber dem Wert ohne; beide Bezugswerte folgen nur mit ca. 2 mV/s. So täuscht der (langsam veränderliche) Sperrstrom der Klemmdiode D430 keine Lastspannung vor, und auch ein langsames Abklingen nach Not-Halt (C500 über R603, ca. 1 s) wird erkannt (zwei unabhängige Prüfungen). Fehlt die Lastspannung
    (Not-Halt, Sicherung), gehen alle Ausgänge aus, LED FEHLER an, Status Bit 3. Kehrt sie zurück, bleibt alles
    aus (kein Wiederanlauf von selbst), bis „O8-Sperren aufheben“ gedrückt wird oder 3 s lang kein Ausgang
    angefordert ist. Gilt auch nach dem Start des Moduls (Anlaufsperre).
  - Laststrom: der R602-Grundwert (ca. 195 mV) wird abgezogen; 8 statt 4 ADC-Messungen je Platz.
  - **Fehler behoben**: Das erste Einschalten nach dem Start des Moduls galt als „warm“ (Ausblendung 20 statt
    100 ms) – eine Lampe/ein Kondensator konnte den Kanal direkt nach dem Einschalten sperren.
  - E8/E16: unverändert bis auf die Versionsnummer.
- Verbindungstool: zeigt beim O8 „Ausgänge gesperrt: Lastspannung fehlt bzw. Anlaufsperre“ (Status Bit 3);
  „O8-Sperren aufheben“ wirkt auch auf diese Sperre.
- Host-Simulation: O8-Modell mit Q60-Freigabe und R602, neue Tests 6–9 (Lastspannung weg/zurück mit Leckversatz, Start ohne Lastspannung, langsames Abklingen, steigender Leckstrom); alle Tests bestanden.

- **Modul-Firmware 1.3 und V15 15.2 nur zusammen verwenden** (IO-Rahmen hat jetzt 5 Byte mit dem erwarteten Modultyp).
- **Fehler (unabhängige Prüfung 06.11.2026)**: Ein O8, das im Betrieb neu startete (Watchdog, Spannungseinbruch,
  RESET), schaltete beim ersten IO-Rahmen sofort die alten Lastausgänge wieder ein. **Behebung**: Nach dem Start
  schaltet ein Modul nichts, bis der Controller es neu identifiziert hat (Status Bit 2 „nicht identifiziert“);
  der Controller fragt dann sofort IDENT und löscht beim O8 die Sollwerte (das Verbindungsprogramm setzt sie
  innerhalb von 2 s neu).
- **Fehler**: Ein O8 auf der Adresse eines E8/E16 (doppelte oder verstellte Adresse) hätte deren LED-Muster auf die
  24-V-Lastausgänge gelegt. **Behebung**: Der IO-Rahmen enthält den erwarteten Modultyp, ein Modul mit anderem Typ
  verwirft den Rahmen.
- Controller V15: Geht die PC-Verbindung verloren (1,5 s), werden die Sollwerte aller Module gelöscht – sonst
  schaltete die erste Zeile einer neuen Verbindung die O8-Ausgänge mit dem alten Zustand wieder ein. Ein neu
  erkanntes O8 oder ein anderer Modultyp an einer Adresse beginnt ebenfalls mit AUS.
- RS-485: Sender-Einschaltzeit vor dem ersten Byte 15 µs statt 4 µs (THVD1450 bis 10 µs).
- O8: /OE der Schieberegister beim Start erst auf HIGH, dann als Ausgang (kein kurzer LOW-Puls); Fehlerschwelle
  der Strommessung 3,25 V statt 3,15 V (weniger Fehlsperren bei Anlaufströmen um 2,3 A).
- Verbindungstool: fragt die Modulliste alle 5 s neu ab („M?“), damit eine verlorene Meldung kein Modul dauerhaft
  stumm schaltet. Ist ein Controller V15 angeschlossen, aber eine Platine ohne Bus eingestellt, werden keine
  Modul-Indizes (≥ 16) geschaltet und Modul-Eingänge nicht als Tasten ausgewertet.
- Modul-Firmware: Beschreibung, SWD-Flashskript (`modul_flashen.cmd`) und Host-Simulation (`Firmware_Modul/test`:
  Controller + bis zu 10 Module am nachgebildeten Bus, Fuzz-Test des Rahmen-Parsers; alle Tests bestanden).

### Verbindungstool – Firmware-Update über den Atmel-DFU (Controller V3.x) [in Arbeit]

- **Fehler**: Auf Controller V3.3 mit Werks-DFU-Bootloader bricht das Update über das Verbindungstool mit
  „Treiber fehlt“ ab, obwohl der WinUSB-Treiber installiert und gestartet ist (gemeldet 05.11.2026).
- **Diagnose eingebaut**: Beim Öffnen des DFU-Bootloaders wird jetzt jeder Schritt (Registry, Schnittstellen-GUID,
  Gerätesuche, Öffnen, WinUSB-Start) mit Windows-Fehlercode ins Protokoll („DFU-Diagnose“) und in die
  Fehlermeldung geschrieben.
- **Ursache gefunden**: Diagnose „GUIDs: 1; Pfade: 0“ – der installierte Treiber (libwdi/Zadig) trägt die
  Schnittstellen-GUID ohne geschweifte Klammern ein, dadurch legt WinUSB keine eigene Schnittstelle an und das
  Programm fand den Bootloader nicht. **Behebung**: Das Programm sucht zusätzlich über die allgemeine
  USB-Geräteschnittstelle, die Windows für jedes USB-Gerät anlegt – unabhängig davon, womit der Treiber
  installiert wurde.
- **Protokoll kopierbar**: Im Reiter „Protokoll“, im Protokoll der Simulation und im Update-Fenster lassen sich
  Zeilen markieren und kopieren (Strg+C, Strg+A, Rechtsklick-Menü). Solange Zeilen markiert sind, springt die
  Liste nicht mehr ans Ende.
- **UF2-Update (V5/V10/V15) geprüft statt blind**: Vor dem Schreiben wird die Prozessor-Kennung der Firmware
  geprüft (RP2040 bzw. RP2350); beschrieben wird nur ein neu erschienenes Update-Laufwerk (ein schon vorhandenes
  nur nach Rückfrage); bleibt das Laufwerk nach dem Schreiben stehen, wird ein Fehler gemeldet; Schreibsperren
  (Gruppenrichtlinie, BitLocker To Go) werden verständlich gemeldet.
- **Erfolg erst nach Bestätigung**: Nach jedem Firmware-Update wartet das Programm, bis sich die Platine wieder
  meldet, und vergleicht die gemeldete Firmware-Version. Erst dann „aufgespielt“ (vorher immer, ohne Prüfung).
- Befehl an die Platine wird bis zu sechsmal wiederholt, falls Windows den Anschluss nach dem Trennen noch nicht
  freigegeben hat; jeder Schritt (U, UJ, 1200-Baud, Rückkehr der Platine) steht im Protokoll.

### Firmware V5 – Kommentar zur neuen Freigabe der Ausgänge (05.11.2026)

- Platine V5.1 (Layout ab 05.11.2026): ENABLE des DRV8860 hängt an GPIO20 (LED „PC“) mit Pull-down statt fest an
  3,3 V. Die Firmware passt ohne Änderung (Ausgänge nur bei Verbindung, Daten jede ms neu); nur der Kommentar im
  Quelltext wurde angepasst, kein neuer Build.

### Firmware 4.5 – Update über das Verbindungstool ohne RESET-Taste (Controller V3.x mit Werks-DFU) [in Arbeit]

- **Fehler**: Nach dem Befehl „U“ meldete sich eine Platine mit Werks-DFU-Bootloader nicht mehr, erst RESET half.
- **Ursache**: Nach einem Watchdog-Neustart bleibt beim ATmega32U4 der Watchdog (15 ms) eingeschaltet, solange
  das Reset-Flag WDRF steht. Die Firmware schaltete ihn nicht ab und startete deshalb endlos neu.
- **Behebung**: Ganz am Anfang des Starts (.init3) wird die Reset-Ursache gesichert, WDRF gelöscht und der
  Watchdog abgeschaltet. „U“/„UJ“ setzen jetzt beide Kennwörter (Arduino-Bootloader und Atmel-DFU) und lösen
  einen Watchdog-Neustart aus; bei Werks-DFU springt die Firmware dann aus dem Grundzustand in den Bootloader
  (bewährter Weg, wie QMK). Platinen mit Arduino-Bootloader verhalten sich wie bisher.

SIGNATUR: 96C97E5A762E8304DC292D266D055D95D65B2CF611C8A06EA89ACC91492B15D19101807C8D3FC775ADFD59819E8D4DDCE266B3E794DE4E6E2A5C8B6C1603E5A9
