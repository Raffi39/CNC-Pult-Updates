### Verbindungstool 2026.11.08.1 und Folien-Editor – Mehrfachauswahl, Icons, Schriftgröße A−/A+, Logo

- **Tasten und LEDs: mehrere Tasten auf einmal einstellen** (Wunsch Raffi): im Modul-Dialog Strg+Klick oder mit der
  Maus einen Rahmen um die Tasten ziehen (Strg = zur Auswahl hinzu). Jede Änderung rechts – Funktion, LED-Quelle,
  Darstellung, Farben, Helligkeit, Haltezeit, Blinken beim Drücken – wird auf alle gewählten Tasten übertragen; dabei
  nur der jeweils geänderte Wert, die übrigen Einstellungen jeder Taste bleiben. Der Name bleibt je Taste (Feld bei
  Mehrfachauswahl gesperrt). „Werkseinstellung“ setzt alle gewählten Tasten zurück. Türkis umrandet = gewählt.
- **Bei „Reset nötig“ nur wirksame Tasten an** (Wunsch Raffi): neues Häkchen im Tasteneditor unter „Funktion beim
  Drücken“, gilt für die angezeigte Platine (jede Platine/jedes Modul einzeln, z. B. nur die Funktionsplatine) und
  wird wie jede Änderung mit Testen/Übernehmen wirksam und gespeichert. Solange EdingCNC einen Reset braucht (nach dem Start, bei/nach
  Not-Halt, nach Fehler oder Abbruch), gehen alle Tasten-LEDs aus, die dann nichts bewirken – auch kein Aufleuchten beim
  Drücken. Hell bleiben Reset, Tastenkürzel und LEDs, die genau diesen Zustand zeigen (Reset nötig, Not-Halt, Fehler,
  Abgebrochen, EdingCNC verbunden); so blinkt z. B. nur noch der Reset-Taster. O8-Lastausgänge schalten unverändert.
- **Vorschläge beim Wählen einer Funktion** (Wunsch Raffi): Mit der Funktion stellen sich passende Bezeichnung und
  LED-Logik ein, z. B. „Programm Start / Fortsetzen“ → Bezeichnung START, LED „Programm läuft“: Status EIN Hintergrund,
  Status AUS grün (= hier kann gestartet werden); Pause blinkt gelb bei Pause, Stopp rot während die Maschine arbeitet,
  Reset blinkt rot bei „Reset nötig“, Achse X+ leuchtet beim Verfahren in X+, Overrides gelb bei ≠ 100 %, Kühlung blau,
  Ref-Fahrt blinkt orange bis referenziert usw. Eigene Einstellungen bleiben: die Bezeichnung wird nur ersetzt, wenn sie
  leer, die Beschriftung oder der Vorschlag der vorigen Funktion ist; die LED nur, wenn sie keine Status-Quelle hat oder
  noch dem vorigen Vorschlag entspricht. Helligkeiten bleiben. Bei Mehrfachauswahl nur LED (Bezeichnung je Taste).
- **Taste löschen** (Wunsch Raffi): Knopf „Taste löschen“ oben rechts im Tasteneditor und Entf-Taste im Modul-Dialog
  (nicht beim Schreiben in einem Eingabefeld) – nach Rückfrage werden alle gewählten Tasten geleert: keine Bezeichnung,
  keine Funktion, keine Haltezeit, kein Icon, LED komplett aus (keine Bedingung, Status EIN und AUS „Aus“, also
  keine Hintergrundbeleuchtung, kein Aufleuchten beim Drücken) – die Taste tut nichts. O8: Eingang nur Funktion, Lastausgang nur
  die Bedingung. Beim Verschieben eines O8-Eingangs bleibt die Einstellung des Lastausgangs jetzt am Platz.
- **Tasten verschieben** (Wunsch Raffi): im Modul-Dialog mit Umschalt + Ziehen eine Taste auf eine andere ziehen – alle
  Einstellungen (Bezeichnung, Funktion, LED, Haltezeit, Icon) wandern mit, die Ausgangstaste wird leer (auch ohne Bezeichnung). Ist die Zieltaste
  belegt, Rückfrage: tauschen, überschreiben oder abbrechen. Hardware-Angaben der Taste (LED angeschlossen,
  Anzeigefarbe einfarbiger Platinen) bleiben am Platz; O8-Eingänge nur untereinander. Wirksam wie jede Änderung
  erst mit Testen/Übernehmen.
- Fehler behoben: Ein im Tasteneditor gewähltes Icon wurde beim Übernehmen nicht in die Einstellungen geschrieben – der
  Knopf blieb auf „Übernehmen“ und nach dem Speichern war das Icon weg. „Werkseinstellung“ entfernt jetzt auch das Icon.
- **Eigene Icons bleiben unverändert** (Wunsch Raffi): Das hinzugefügte Bild wird nicht mehr zugeschnitten oder in eine
  Maske umgerechnet, sondern so gespeichert, wie es ist (als PNG, sehr große Bilder auf höchstens 1024 Punkte
  verkleinert). Gezeichnet wird es nur skaliert und seitenrichtig – im Verbindungstool, in der Icon-Auswahl und im
  Folien-Editor; beim Farbdrucker in Farbe, beim Schwarz-Weiß-Drucker in Graustufen. Bereits hinzugefügte Icons
  (Masken) bleiben nutzbar; wer das Original will, löscht sie und fügt das Bild neu hinzu.
- Folien-Editor: Icon frei platzieren und hineinzoomen (Wunsch Raffi): „Icon-Lage“ ◀ ▲ ▼ ▶ (0,5 mm) und „Mitte“,
  in der Vorschau Umschalt + Ziehen auf der gewählten Taste; Icon-Größe bis zum 4-Fachen des Rahmens (Umschalt +
  Mausrad). Gedruckt wird nur, was im Icon-Rahmen liegt (ohne Text: die Taste, mit Text: der Platz neben dem Text).
- Folien-Editor: Icon-Größe ohne Text jetzt bis zur ganzen Taste (Ränder gelten nur für „auto“); Bilder werden an den
  runden Tastenecken abgeschnitten.
- **Folien-Editor:**
  - Icon-Größe je Taste mit „−“ / „+“ (0,5-mm-Schritte, Anzeige der Kantenlänge, höchstens so groß wie der Platz auf
    der Taste = „auto“); gilt für alle gewählten Tasten, „Wie alle Tasten“ setzt sie zurück.
  - Standard-Schriftgröße jetzt 3,2 mm Versalhöhe (einzeilig, nur durch die Tastenbreite begrenzt; mehrzeilig
    passt die Schrift weiter ins Band). Standardfarben in jedem Fall weiße Taste / schwarze Schrift.
  - Baufehler behoben: `Timer` war mehrdeutig (System.Threading / Windows.Forms).
  - Fenstersymbol (oben links, Taskleiste) jetzt das Kostka-Logo „Nullpunkt“ wie beim Verbindungsprogramm.
  - Schriftgröße je Taste mit „A −“ / „A +“ statt mm-Eingabe: ändert die Versalhöhe in 0,2-mm-Schritten, ausgehend von
    der tatsächlich gedruckten Größe; daneben steht die aktuelle Größe („2,4 mm (auto)“). Die Breite der Taste
    begrenzt die Schrift weiterhin. Die globale Schrifthöhe „alle Module“ ist entfallen.
  - Mehrere Tasten wählen: Strg+Klick, Rahmen ziehen oder Strg+A in der Vorschau. Tastenfarbe, Schriftfarbe, A−/A+
    und „Wie alle Tasten“ gelten dann für alle gewählten Tasten; der Text wird je Taste eingegeben.
- **LED-Einstellungen zweigeteilt** (Wunsch Raffi): Karte „LED reagiert auf“ (Auslöser, mit Hinweis) getrennt von der
  Karte „Darstellung: Status EIN / AUS“ (Art, Farben, Helligkeit, Takt, Aufleuchten beim Drücken). Der Knopf
  „Darstellung auf andere Tasten kopieren …“ sitzt jetzt in der Darstellungs-Karte und überträgt **nur** die Darstellung
  (Status EIN/AUS, Aufleuchten, Anzeigefarbe) – worauf die LED reagiert und „LED angeschlossen“ bleiben bei jeder Taste.
  Bisher wurde mit „LED auf andere Tasten kopieren …“ auch der Auslöser überschrieben.
- **Druckpunkt-Rückmeldung sofort** (Wunsch Raffi): „beim Drücken hell aufleuchten“ leuchtet jetzt gleich beim Drücken,
  auch bei Tasten mit Haltezeit (bisher erst nach Ablauf der Haltezeit). Die Funktion löst weiterhin erst nach der
  Haltezeit aus.
- **Neue LED-Bedingung „Reset nötig (Maschine nicht bereit)“** (Wunsch Raffi, z. B. Reset-Taster blinkt): EIN, solange
  EdingCNC einen Reset braucht – Zustand IDLE/POWERUP (nach dem Start), Not-Halt aktiv, Fehlerzustand oder ABORTED, und
  dabei kein Programm läuft oder pausiert. Am Pult mit Status EIN = blinken einstellen. Am Muster prüfen, ob EdingCNC nach
  Not-Halt bzw. Abbruch genau diese Zustände meldet (Anzeige auf der Seite Simulation).
- **O8 im Tasten-Editor getrennt** (Wunsch Raffi): Die Kachel bzw. der Modul-Dialog einer O8 zeigt oben die 8 **Eingänge**
  (E, nur Funktion beim Drücken – keine LED-Einstellungen) und darunter die 8 **Lastausgänge** (A). Ein Klick auf einen
  Lastausgang zeigt nur „schaltet ein bei“ (bisher „LED reagiert auf“) und den Zustand EIN/AUS; Bezeichnung und Funktion
  sind dort ausgeblendet. Die Ausgänge zeigen ihren Schaltzustand in Farbe, die Eingänge sind neutral. Datenmodell
  unverändert (Eingang i und Lastausgang Ai gehören weiter zu einem Eintrag), alte Einstellungen bleiben gültig.
- **Icons für Tasten** (Wunsch Raffi), eigenes Icon-Set (41 Symbole: Start, Pause, Stopp, Reset, Einzelsatz, Pfeile,
  Eilgang, Schrittweite, Spindel, Rechts-/Linkslauf, Kühlung, Home, Nullpunkt, Werkzeug, Messtaster, Licht, Makro, MDI …).
  Bewusst nicht die Symbole von EdingCNC (Rechte bei EdingCNC B.V., als kleine Pixelbilder im Druck unscharf); die
  eigenen sind Vektor-Umrisse und drucken scharf.
  - Verbindungstool, Tasten-Editor: Zeile „Icon“ unter der Bezeichnung (Auswahl im Raster, „Icon oben/unten“). Die
    Tasten im Modul-Dialog und die Kacheln zeigen das Icon. Gilt auch für die Mehrfachauswahl.
  - Folien-Editor: Knopf „Icon …“ und „Icon oben, Text unten / Text oben, Icon unten“ je Taste (auch für mehrere Tasten).
    Ohne Text füllt das Icon die Taste (mit Randabstand), mit Text steht der Text im Band oben bzw. unten.
    Icons werden wie Schrift ausgespart (Schriftfarbe, Weiß = unbedruckt).
  - **Eigene Icons** (Wunsch Raffi): im Icon-Auswahlfenster „Eigenes Icon hinzufügen …“ – ein Bild (PNG/JPG/BMP/GIF, dunkles
    Motiv auf hellem oder durchsichtigem Grund) wird zugeschnitten, als Maske gespeichert und steht dann auf diesem PC
    immer zur Auswahl, in Verbindungstool und Folien-Editor. Ablage `%ProgramData%\CNC-Pult-Verbindung\Icons\<Name>.png`
    („Ordner öffnen“), Rechtsklick auf ein eigenes Icon: löschen. Auf einem anderen PC fehlt ein eigenes Icon (Taste ohne Icon).
  - „Namen aus Verb.-Tool“ übernimmt auch Icon und Lage; Tasten mit Icon und leerer Bezeichnung werden nur-Icon.
  - Technik: `Icons.cs` (Zeichnen, Auswahl) und `IconsDaten.cs` (Umrisse, erzeugt von `icons_erzeugen.py`, Übersicht
    `icons_vorschau.png`) – beide werden auch in den Folien-Editor kompiliert.
- **Folien-Editor, Karte „Schrift“** (Wunsch Raffi):
  - „2. Zeile an den unteren Tastenrand“: bei mehrzeiligem Text steht die letzte Zeile unten an der Taste, die übrigen
    oben – gleicher Randabstand, alle Zeilen gleich groß.
  - „Randabstand“ oben/unten einstellbar (0,3–2,5 mm, Standard 0,8 mm statt bisher 0,6 mm); seitlich bleibt fest 1,0 mm.
  - Gemeinsame „Schrifthöhe (alle Module)“ entfernt: sie wirkte nur auf Tasten ohne eigene Größe und wurde oft von der
    Tastenbreite begrenzt, daher kaum sichtbar. Ersatz: Strg+A und A−/A+. Alte Dateien mit gemeinsamer Schrifthöhe werden
    beim Öffnen auf die Tasten übertragen, sie sehen gleich aus.
- **Folien-Editor: Standardfarben** jetzt weiße Tasten mit schwarzer Schrift (alle Module, Grund bleibt dunkel) –
  gilt für neue Folien und den Knopf „Standardfarben“; gespeicherte .cncfolie-Dateien behalten ihre Farben.
- **Folien-Editor läuft nur einmal** (Wunsch Raffi): Ist er schon offen, holt ein weiterer Aufruf (z. B. im
  Verbindungstool „Frontfolien“ → „mit den Tastennamen von …“ oder Doppelklick auf eine .cncfolie) das offene Fenster
  nach vorn und übernimmt dort die Tastennamen bzw. öffnet die Datei. Gibt es ungespeicherte Änderungen, fragt der
  Editor vorher „Jetzt speichern?“ (Ja / Nein = verwerfen / Abbrechen = nichts übernehmen). Technik: benannter Mutex je
  Sitzung, der zweite Start reicht seine Parameter über eine benannte Pipe weiter und beendet sich.
- **Fehler behoben:** Beim Öffnen des Modul-Dialogs über eine Kachel war oben der Knopf des geöffneten Moduls (JOG,
  FUNKTION, MAKRO, M22 …) nicht markiert – die Kachel stammte aus einer früheren Modulliste und wurde nicht
  wiedererkannt. Jetzt ist das geöffnete Modul sofort hervorgehoben.
- **Modul-Dialog: „Übernehmen“ schließt nicht mehr** (Wunsch Raffi): speichert, das Fenster bleibt offen und zeigt
  „✓ Übernommen und gespeichert“. Ohne Änderungen heißt der Knopf „Schließen“ und schließt den Dialog. „Abbrechen“
  verwirft die Änderungen seit dem letzten Übernehmen.
- **Status AUS mit Lieblingsfarben** (Wunsch Raffi): dieselbe Favoritenleiste wie bei Status EIN (Klick übernimmt die
  Farbe für Status AUS, Rechtsklick speichert/ändert den Favoriten) und daneben „frei …“ mit der aktuellen Farbe.
- **Auswahllisten alphabetisch** (Wunsch Raffi): „Funktion beim Drücken“ (auch Handrad) und „LED reagiert auf“ sind
  nach Anzeigetext sortiert, „– keine … –“ bleibt oben. Gespeichert wird weiter die Kennung, alte Einstellungen bleiben
  gültig. Zwei Bezeichnungen angepasst, damit Zusammengehöriges nebeneinander steht: „Abgebrochen“ → „Programm
  abgebrochen“, „Zustand: Bereit“ → „Bereit (EdingCNC wartet auf Befehle)“.
- Anleitung, Hilfe (Verbindungstool.html) und LIESMICH des Folien-Editors ergänzt.
- Nicht kompiliert/getestet in Claudes Umgebung (kein C#-Compiler): Raffi baut mit `_bauen_signieren.cmd` und prüft.

### Verbindungstool 2026.11.08.1 und Firmware 15.5 / Modul 1.6 – Firmware-Update der Erweiterungsmodule über den Bus

- **Modul-Firmware über den RS-485-Bus aktualisieren** (Entscheidung Raffi „Modul-Updates über den Bus vom Tool aus“):
  Platinen → Netzwerk und Module → „Modul-Firmware aktualisieren …“ (Controller V15). Das Programm zeigt je Modul die
  gemeldete und die enthaltene Version („neu: 1.6“), aktualisiert die Module nacheinander mit Fortschrittsanzeige und
  Abbruch; die übrigen Module arbeiten weiter, das Modul im Update schaltet seine Ausgänge ab (O8: Lasten aus).
  - Programm (`ModuleUpdate.cs`): Abbild `fw_E8/E16/O8.bin` (verschlüsselt eingebaut wie die Controller-Firmware),
    Textbefehle `MU/MD/ME/MX` an den Controller, 64-Byte-Blöcke mit Bestätigung, CRC32 über das Abbild.
  - Controller-Firmware 15.5: reicht das Abbild in 24-Byte-Rahmen weiter (Bus-Befehle UPD_BEGIN/DATA/END/STAT/ABORT,
    `pult_bus.h`), abwechselnd mit dem normalen Umlauf, prüft Modultyp und Modul-Firmware ≥ 1.6, meldet „FERTIG <FW>“
    erst, wenn sich das Modul nach dem Neustart neu identifiziert.
  - Modul-Firmware 1.6: speichert das Abbild im Dateisystem (LittleFS, 2 MB; Flash-Aufteilung 2 MB/2 MB), prüft CRC32 und lässt es beim Neustart
    vom OTA-Lader des Arduino-Pico-Cores einspielen (PicoOTA, stromausfallsicher); LED BUS blinkt schnell während des Updates.
    Erstes Aufspielen (bzw. 1.5 → 1.6) weiterhin per SWD (neue Flash-Aufteilung mit Dateisystem).
  - `firmware_bauen.ps1`: Module mit Dateisystem bauen, `.bin` ablegen und einbauen; `Werkzeug.exe` kennt E8/E16/O8;
    `build.cmd` nimmt `fw_E8/E16/O8.bin` auf.
  - Host-Simulation: Test 11 (Update 70 kB mit nachgebildeten Flash-Zeiten, andere Module laufen weiter, Neustart mit
    neuer Firmware) und Test 12 (CRC-Fehler, falscher Typ, Abbruch) bestanden.
  - Unabhängig geprüft (Code und Arduino-Pico-Core-Quelltext 6.3.2, Simulation): umgesetzt wurden
    - Flash-Aufteilung 2 MB Programm / 2 MB Dateisystem (`flash=4194304_2097152`; 1 MB gibt es für generic_rp2350 nicht),
    - „FERTIG“ erst von der neuen Firmware (Modul beantwortet nach der Prüfung kein IDENT mehr, Controller wartet ≥ 1 s),
      das Programm vergleicht die gemeldete Version, `picoOTA.commit()` wird geprüft,
    - Eingänge des Moduls gelten beim Update-Beginn und Neustart als losgelassen (Meldung „K … 0“ an den PC),
    - Kennung „CNCPULT-MOD:<Typ>:<Version>“ im Abbild: das Modul spielt nur ein Abbild seines Typs ein, `Werkzeug.exe`
      und das Programm prüfen sie ebenfalls (Schutz gegen E8-Firmware auf einem O8),
    - nach Fehler/Abbruch: Modul gilt als nicht identifiziert, O8 mit Anlaufsperre (Lasten erst nach Quittung), O8 mit
      gesperrten Ausgängen wird nicht aktualisiert, Quittungen werden beim Neu-Identifizieren verworfen,
    - Wiederholung verlorener Aufforderungen, END-Wiederholung, Selbstabbruch des Moduls nach 20 s ohne Daten,
      Watchdog 4 s während des Updates, Dateisystem schon beim Start eingehängt, UART nach Flash-Vorgängen geleert.
  - **Am Muster zu prüfen** (noch keine V15-/Modul-Hardware): OTA-Lader im RP2350-Abbild und der ganze Ablauf.

SIGNATUR: 16856B94E68BFD3A8985E271A41217A7C71D1CFAA2DBFA81C31BCCE54A440D8B5F04897615B701D0514B87D2E3E70F323058D18EFB0B4BF059DAD91672668981
