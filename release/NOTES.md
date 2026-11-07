### Verbindungstool 2026.11.07.2 und Firmware 4.8 / 5.6 / 10.5 / 15.4 / Modul 1.5 – Neues Design, Pulsieren, Platinenübersicht

- **Pulsieren in der Firmware** (LED-Modus 3, `pult_puls.h` in allen Sketch-Ordnern gleich): Helligkeit läuft weich
  zwischen 10 % und 100 %, wie die Vorschau im Programm.
  - Firmware 4.8 (Controller V3.x) und 5.6 (V5): RGB-LEDs der Tastenmodule; geschaltete Ausgänge J8/J9: Pulsieren = ein.
  - Firmware 10.5 (V10) und 15.4 (V15, eigene 12 LEDs): einfarbige LEDs als Pulsdichte im 2-ms-Takt (etwa eine Periode
    der Helligkeits-PWM), Untergrenze 25 % statt 10 % (sonst sichtbare 50-Hz-Blitze am Tiefpunkt); die DRV8860-Kette wird
    nur dann alle 2 ms geschrieben, wenn eine LED pulsiert. Am Muster bei kleiner Helligkeit auf Schimmern prüfen.
  - Modul-Firmware 1.5 (E8/E16): V15 sendet die Helligkeit je LED im IO-Rahmen (nur an Module ab 1.5, sonst leuchten
    sie); O8-Lastausgänge bleiben ein/aus. Host-Simulation um Test 10 erweitert (bestanden).
  - Verbindungsprogramm: sendet Modus 3 nur an Firmware ab 4.8 / 5.6 / 10.5 / 15.4 (`Engine.CanPulse`), sonst leuchten;
    einfarbige LEDs pulsieren jetzt auch in der Vorschau. Firmware V3 (alt) bekommt kein Pulsieren.
  - Unabhängig geprüft (Code-Durchsicht aller Sketche, Host-Simulation Bus): umgesetzt wurden Rechenzeit am ATmega32U4
    (16-Bit-Mischung, Pulshelligkeit je Periode nur einmal), Untergrenze einfarbig, V15 bleibt am Scheitel im 2-ms-Takt.
  - **Offen (Entscheidung Raffi, eigener Schritt):** Firmware-Update der Erweiterungsmodule über den RS-485-Bus vom
    Verbindungsprogramm aus – Bus-Befehl und Bootloader in den Modulen fehlen noch, bis dahin Aufspielen per SWD.
- **Platinenübersicht mit Pin-Hinweisen** (Knopf „Platinenübersicht anzeigen“ unter Tasten und LEDs, „Übersicht“ unter
  Platinen, Hilfe → Steckerbelegung): Bild der Platine mit allen Steckern; Maus über einen Pin zeigt seine Belegung,
  rechts die ganze Belegung des Steckers (Pin, Bedeutung, unbelegte Pins grau) und Anschluss-Hilfen (LED-Kette bei
  fehlenden Modulen, Taster mit LED, Bus der Erweiterungsmodule). Für V3.3, V3.4, V5, V10, V15 und – beim
  Controller V15 umschaltbar – E8, E16, O8 (neue Bilder). Fenstergröße und -lage werden gemerkt. Daten aus den
  Platinendateien (`08_Werkzeuge_Platinen/pin_hinweise.py`, prüft jeden Text gegen das Netz). Unabhängig gegen die
  Schaltpläne geprüft (jedes Netz bis zum Baustein): kein sachlich falscher Funktionstext; umgesetzt wurden Anzeige J3 Pin 4,
  O8-Ausgänge „abgesichert 3 A“ statt „kurzschlussfest“, BOOT-Bedienung (BOOT halten + RESET), gemeinsame Polyfuse bei
  V15/E8/E16/V5, JP1 ab Werk offen, J7-Hinweise (V5, E8/E16) und O8-Summenstrom.
- **Größe der Oberfläche:** Textfelder werden jetzt auch in der Breite mit vergrößert (vorher nur Lage und Höhe,
  dadurch z. B. der EdingCNC-Pfad unter Allgemein zu schmal). Simulation: V10-/V15-Tasten etwas kleiner und die rechte
  Spalte 380 breit, damit alle vier Klemmen-Spalten ohne Querscrollen sichtbar sind.
- **Folien-Editor im gleichen Design** (`05_Frontfolien/Folien-Editor`): Kopfzeile mit Logo „CNC-PULT FOLIEN“ und
  Modulwahl JOG / MAKRO / FUNKTION als Navigation, Seitenkopf mit Dateiname, Zustand „● ungespeichert“ und den Knöpfen
  Datei ▾ / Öffnen / Speichern / Druckvorschau / Drucken, links Karten (Ausgewählte Taste mit Farbfeldern, Ganzes Modul,
  Schrift, Drucken mit Drucker-Chips Farbe / Schwarz-Weiß), rechts die Vorschau als Karte, Statuszeile unten,
  Anleitung als gestalteter Dialog, Menü im Farbschema. Dunkel/Hell und Größe folgen der Einstellung des
  Verbindungsprogramms (Datei ▾ → Darstellung: wie das Verbindungsprogramm / Dunkel / Hell). Fenstergröße und -lage
  werden gemerkt. Gewählte Taste in der Akzentfarbe statt Rot. Alle Funktionen und Einstellungen unverändert.
  `Theme.cs` wird dafür mitkompiliert (unabhängig vom Verbindungsprogramm: `ISelfColored`, `WinPlace.Dir`,
  `ThemeMenuRenderer`). Selbsttest `CNC-Pult-Folien.exe /selbsttest <Ordner>` (Bilder folien0–3.png); der Selbsttest
  des Verbindungsprogramms ruft ihn mit auf.
- **Neues Design, Stufe 1** (Richtung „C“, Logo „Nullpunkt“ von Kostka Engineering):
  - **Dunkel/Hell umschaltbar** (Allgemein → Darstellung, wirkt sofort, Einstellung `Design`). Neu `Theme.cs`:
    Farbschema, Karten statt Rahmengruppen, flache Schaltflächen und Eingabefelder, dunkle Titelleiste und
    Bildlaufleisten (Windows 10/11). Dialoge (Assistent, Poti-Abgleich, Tastatur anlernen, Update …) werden mit eingefärbt.
  - **Kopfzeile in einer Zeile** (Entwurf C): Logo, „CNC-PULT VERBINDUNG“, Navigation und „SIMULATION AKTIV“; die
    Statuszeile (Platinen, EdingCNC, Zustand, Overrides, Version) steht unten. „SIMULATION AKTIV“ gelb statt rot (Rot bleibt Not-Halt/Gefahr vorbehalten).
  - **Tasten und LEDs**: Platine wählen, dann die Module als Kacheln (V3.x/V5: JOG, FUNKTION, MAKRO, M22; V10: Klemmen
    J20–J35 in vier Kacheln; V15: Controller und je Erweiterungsmodul eine Kachel) – alle im gleichen Maßstab
    (Tastenraster 22 mm), damit gleich große Tasten gleich groß aussehen. Klick öffnet den **Modul-Dialog**: Tasten in
    großem, gleichem Maßstab, rechts der bekannte Editor (Funktion, LED, Haltezeit …).
  - **LED-Vorschau wie in echt**: Die Tasten zeigen die LED mit der eingestellten Helligkeit (Status und
    Hintergrundbeleuchtung), so wie sie am Pult wirkt; dunkle Tastenkappe, „keine LED“ dunkelgrau.
  - **Farbauswahl** mit Farbfeldern ohne Rot (EN 60204-1: Rot = Not-Halt/Gefahr) und „Eigene Farbe …“ (bei Rot Rückfrage).
  - **Platinenübersicht** hinter dem Knopf „Platinenübersicht anzeigen“ (Stufe 2: Stecker mit Pin-Hinweisen).
  - Programmsymbol aus dem neuen Logo (`Setup/setup.ico`, auch für das Setup). Mindestgröße des Fensters 1280 × 800.
  - **Modul-Dialog nach Entwurf C**: randloser Dialog über dem abgedunkelten Hauptfenster, Modulwechsel im Kopf
    (JOG / FUNKTION / MAKRO / M22 bzw. Klemmen/Module), rechts der kompakte Editor (gleicher Umfang wie bisher:
    alle Funktionen, „LED reagiert auf“ mit allen Quellen, Status EIN/AUS, Druckpunkt-Rückmeldung, Anlernen, Kopieren).
    **Testen / Übernehmen / Abbrechen**: Änderungen wirken erst mit „Testen“ (am Pult ausprobieren, noch nicht
    gespeichert) bzw. „Übernehmen“ (wirksam und gespeichert); „Abbrechen“ stellt den Stand vor dem Öffnen wieder her.
    Ungespeicherte Änderungen stehen links neben dem Schließen-Kreuz; beim Schließen über ✕ (oder Esc) Rückfrage
    Übernehmen / Verwerfen / zurück zum Dialog.
  - **Lieblingsfarben 1–8**: frei belegbar (Rechtsklick auf ein Farbfeld oder nach „Farbe frei wählen“), Farbe bleibt
    jederzeit frei wählbar (Einstellung `FavColors`).
  - **Helligkeit je Taste auch für „Hintergrundbeleuchtung“** (Status EIN/AUS, neues Feld `BgBrightness`; ohne
    Eintrag gilt wie bisher die Hintergrund-Helligkeit der Platine).
  - **Pulsieren** als Darstellung wählbar (Bildschirm pulsiert). Die Firmware kann es noch nicht: bis zur neuen
    Firmware leuchtet die LED dauerhaft.
  - **LED-Einstellung je nach Hardware**: RGB-Tasten mit Farben; einfarbige LEDs und Ausgänge (V10/V15, M22 an
    OUT1–8 ab V3.4) nur ein/aus/blinken ohne Farben; M22-Eingänge an Platinen ohne Ausgänge (V3.3) ohne LED-Einstellung.
  - Kacheln: „Bearbeiten →“, Zusammenfassung (belegt / mit Haltezeit), Rahmen orange = Haltezeit, gestrichelt =
    nicht belegt; Platinenwahl als Auswahlliste neben der Überschrift.
  - **Größe der Oberfläche** einstellbar (Allgemein → Darstellung: 100 / 115 / 125 / 150 %, Vorgabe 125 %, wirkt nach
    Neustart, Einstellung `UiZoom`). Schrift, Felder, Tasten und Handrad-Abbildung werden mit vergrößert.
  - **Fenstergröße und -lage werden gemerkt** (Hauptfenster und Modul-Dialog, auch maximiert; Datei `Fenster.txt` im
    Einstellungsordner). Der Modul-Dialog ist ein normales, verschieb- und vergrößerbares Fenster (Schließen-Kreuz mit
    Rückfrage wie oben). Die Handrad-Abbildung passt sich der Fensterhöhe an.
  - Auswahllisten werden im Farbschema gezeichnet (auch gesperrt nicht mehr hellgrau).
  - Listen (Platinen, Assistent): gewählte Zeile dunkel hinterlegt mit Akzentstrich, der Text behält seine Zustandsfarbe und bleibt lesbar.
- **Neues Design, Stufe 2/3 – alle Seiten nach Entwurf C** (Einstellungen und Einstellungsdatei unverändert, nur neu angeordnet):
  - **Allgemein**: Seitenkopf mit Einrichtungsassistent und Speichern, Karten in zwei Spalten (EdingCNC, Verfahren,
    Override-Potis, Beleuchtung und Bedienung, Programmstart, Updates, Darstellung, Rechtliches, Tasten); Achsen-
    umkehr und Programmstart als Auswahl-Pillen.
  - **Platinen**: links die Platinen als Karten mit Zustand (verbunden / nicht verbunden / Simulation / aus), darunter
    „Gefunden“; rechts Kopf der gewählten Platine (Version, Verbindung, Firmware, Zustand, Platinenübersicht,
    Speichern) und Unterreiter Allgemein / Verbindung / Netzwerk und Module / Firmware.
  - **Handrad**: Seitenkopf mit Zustand des Funkempfängers; Abbildung und Einstellungen wie bisher.
  - **Simulation**: Seitenkopf, Platinenwahl, rechts Karte „EdingCNC“ und Protokoll der Simulation.
  - **Protokoll**: Karte „Hilfe und Support“, Filter (Alle, Warnungen, Platinen, EdingCNC, Tasten), Suche,
    Warnungen farbig hinterlegt; die Diagnose enthält weiterhin das ganze Protokoll.
  - **Neu: Frontfolien** – Folien-Editor öffnen, auf Wunsch mit den Tastennamen einer Platine (Folien-Editor:
    neuer Aufruf `/namen "<Konfiguration>" "<Platine>"`), Vorschau der drei Folien mit den Tastennamen.
  - **Neu: Hilfe und Unterlagen** – Benutzerhandbuch, Anleitung, Steckerbelegung, Sicherheitshinweise, Treiber,
    Windows-Warnung, Folien-Editor, Lizenzen, Datenschutz, Sicherheitslücke melden, Drittsoftware; Suche; Kontakt
    und „Problem melden“.
  - **Setup** installiert zusätzlich Benutzerhandbuch, Verbindungstool-Anleitung, Datenschutzhinweise (neu
    `07_Verbindungsprogramm/DATENSCHUTZ.txt`) und den Folien-Editor (`CNC-Pult-Folien.exe`, signiert, wird von
    `build.cmd` mitgebaut) mit Startmenü-Einträgen; die Deinstallation entfernt sie wieder.
  - **Begleittexte als gestaltete Seite**: Sicherheitshinweise, Treiber, Windows-Warnung, Lizenzen, Datenschutz,
    Drittsoftware öffnen sich aus dem Programm als HTML-Seite im Stil des Programms (Logo, Abschnitte als Karten,
    Warnabschnitt hervorgehoben, nummerierte Schritte, Links anklickbar, druckbar) im Standardbrowser. Neu
    `DocHtml.cs`; die TXT-Dateien bleiben die Quelle (Setup, Startmenü).
- **EdingCNC-Version**: Das Programm ist mit EdingCNC **5.3.2** getestet (`AppInfo.TestedEding`). Bei einer anderen
  Version erscheint eine Warnung – im Einrichtungsassistenten (orange unter der Auswahl), im Reiter Allgemein neben
  der Version und beim Verbinden im Protokoll: „nicht geprüft … bitte zuerst in der EdingCNC-Simulation prüfen“.
  Bisher wurde bei anderen Versionen nur die Versionsnummer angezeigt, ohne Hinweis.
- **Setup**: enthält jetzt auch `TREIBER_DFU_Controller_V3.txt` und den neuen `HINWEIS_Windows-Warnung.txt`
  (SmartScreen „Trotzdem ausführen“, Benutzerkontensteuerung, Download-Warnung in Edge/Chrome, Norton-CyberCapture
  und Ausnahmen, Windows-11-Intelligente-App-Steuerung, Prüfen der Signatur „Kostka Engineering“). Beide im
  Programmordner und im Startmenü; das Deinstallieren entfernt sie (und jetzt auch die Lizenzbedingungen).
  Den Hinweis zur Windows-Warnung bitte zusätzlich zusammen mit dem Setup an Tester geben.
- **Neutrale Texte**: keine Hinweise mehr auf GitHub (Fehlermeldungen des Updaters: „Update-Server“, ANLEITUNG) und
  auf eigene Dateien des Herstellers (Makro, Firmware-Ordner). Die Entwickler-Abschnitte der ANLEITUNG
  (Kompilieren, Veröffentlichen, Protokoll Pult↔PC) stehen jetzt in `Quelltext/ENTWICKLER.txt` und gehen nicht
  mehr ins Setup. ANLEITUNG: Voraussetzungen mit getesteter EdingCNC-Version und aktueller Firmware.
- **Einrichtungsassistent**: zusätzlicher Tipp, wie man die richtige Makrodatei findet (die Datei, in der das „sub …“
  eines funktionierenden Unterprogramms steht).
- Risikobeurteilung (`09_Recht_Konformitaet/02_Risikobeurteilung.md`): G1, G4 aktualisiert, neu G16 (Achse fuhr
  weiter, 06.11.) mit Maßnahmen und Prüfnachweis.
- **Keine irreführenden Sicherheitsbegriffe** (Pult und Programm sind kein Sicherheitsbauteil): „Sicherheitszeit“ heißt
  jetzt **„Haltezeit“** (Reiter Tasten, Allgemein, Handrad, Protokollmeldung), Protokoll „SICHERHEIT: Ablauf hängt …“
  → **„SCHUTZ: …“**, Handrad-Tooltip „Schutz gegen Nachlaufen“, ANLEITUNG „Schutz bei Verbindungsabbruch“ und neuer
  Abschnitt „Sicherheitshinweise“: Schutzmaßnahmen des Programms sind keine Sicherheitsfunktionen im Sinne der
  Maschinennormen. Einstellungsdatei unverändert (alte Einstellungen gelten weiter).
- **Rechtliches im Programm**: Reiter Allgemein → „Rechtliches und Sicherheitshinweise“ mit den Knöpfen
  „Sicherheitshinweise“ (neu `07_Verbindungsprogramm/SICHERHEITSHINWEISE.txt`) und „Drittsoftware-Lizenzen“
  (`09_Recht_Konformitaet/THIRD_PARTY_NOTICES.txt`, jetzt mit Herstellerangaben, Arduino-Pico 6.3.1 und den
  vollständigen BSD-3-/MIT-Texten). Beide Dateien kommen mit dem Setup in den Programmordner, Sicherheitshinweise
  auch ins Startmenü. `SECURITY.md`: Meldeadresse eingetragen.
- Neu `09_Recht_Konformitaet/10_Software_Ergonomie.md`: Regeln für die Programmgestaltung (ISO 9241, Farben nach
  EN 60204-1/IEC 60073, Begriffe, DSGVO, Windows) mit Checkliste für das neue Design. Logo „Nullpunkt“ in `11_Logo/`.
- Bestätigt von Raffi (07.11.): Schrittbetrieb, Eilgang-/Tempowechsel während der Fahrt (kurzer Halt, dann neue
  Geschwindigkeit – EdingCNC übernimmt die Geschwindigkeit nur beim Start). Mehrere Achsen gleichzeitig bleiben erlaubt.

SIGNATUR: 0A72830D9EA7D231FF8BD463ADF0BE03603C32C91F72D23FDCD69FC588044A4CC87BBA3F12363F8C0E67A8AEA9DA4ABE3FD3B577CD7466DE35EC158CE2914A12
