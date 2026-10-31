### Verbindungstool 2026.10.31.6 – Handrad: Ebenen nach Farben (WXHC), Fn rastend, Override bei Achswahl OFF, Kopierschutz und Lizenzbedingungen

- **Ebenen nach Farben** (neu, Vorgabe beim WXHC): ohne Fn wirken die blauen Makros, mit Fn die orangen Funktionen
  (Feed±, Spindle±, M-HOME, Safe-Z, W-HOME, S-ON/OFF, Probe-Z). Haken „Ohne Fn = blaue Makros, mit Fn = orange
  Funktionen (WXHC)“; beim Umschalten wandert die Belegung der zweifarbigen Tasten mit. „Belegung wie EdingCNC-Handrad…“
  stellt die Eding-Logik ein (ohne Fn orange, mit Fn Makros). Gespeicherte Belegungen älterer Versionen werden einmalig
  passend getauscht. Abbildung, Tastennamen und Hinweise folgen der Einstellung.
- **Freigabe des Handrads**: Echtbetrieb nur, solange eine **Original-Platine** angeschlossen ist (Original-Prüfung
  bestanden), und noch **1 Stunde nach dem Abziehen**; danach nur Simulation. Keine dauerhafte Freigabe. Die
  Original-Prüfung fragt die Platine jetzt mit einer an den PC gebundenen Frage (SHA-256 aus Windows-Maschinen-ID und
  Zufall). **Testmodus**: Knopf „Testmodus 1 Stunde“ schaltet den Echtbetrieb jeweils für
  eine Stunde frei (beliebig oft); danach wird der Handradbetrieb beendet.
- **Direkttasten**: RESET, Stop, Start/Pause, Macro-10, Continuous und Step haben genau eine Funktion und wirken
  mit und ohne Fn gleich (bisher blieb z. B. das Umschalten STEP/CONTINUOUS bei aktivem Fn ohne Wirkung). Die Fn-Ebene
  gibt es nur noch für die zweifarbigen Tasten; eine Belegung von „Fn + Macro-10“ wird auf Macro-10 übernommen.
- **Fn rastend** (Vorgabe an): einmal drücken = Fn an (Display zeigt „Fn“), nochmal = aus – am echten Handrad wie in
  der Simulation; gehaltenes Fn wirkt weiterhin.
- **Achswahl OFF**: Vorschub-Override, Spindel-Override und Lead (Einstellung des Stufenschalters) wirken jetzt in
  **beiden** Betriebsarten – bisher im Dauerbetrieb (CONTINUOUS) nicht. Dauerbetrieb fährt nur mit gewählter Achse.
- **Selbstprüfung des Programms** (Schutz gegen Veränderung): Das Programm prüft beim Start und regelmäßig seine
  eigene Hersteller-Unterschrift (Authenticode, Aussteller „Kostka Engineering“; ist beim Bauen ein Zertifikat
  vorhanden, wird zusätzlich dessen Fingerabdruck fest eingebaut und geprüft). Ist die Datei verändert oder nicht mehr
  gültig unterschrieben, werden Handrad-Echtbetrieb und automatische Updates gesperrt (Hinweis im Protokoll und im
  Reiter Handrad). Ein selbst gebautes Programm ohne Zertifikat wird nicht gesperrt.
- **Platine im Betrieb erneut geprüft** (nur V5/V10): Die Original-Prüfung (Zufallsfrage, nur von der Original-Firmware
  zu beantworten) wird nicht mehr nur beim Verbinden gestellt, sondern alle 2 Minuten wiederholt. Bleibt eine gültige
  Antwort aus, gilt die Platine als nicht mehr echt und das Handrad wird gesperrt. V4 (ATmega) wird im Betrieb nicht
  erneut geprüft (rechnet zu lange), die einmalige Prüfung beim Verbinden bleibt.
- **Verschleierung** (optional): `build.cmd` verschleiert das Programm vor dem Signieren mit ConfuserEx (anti-ildasm,
  Konstanten, Programmfluss), falls ConfuserEx unter `_lizenz\ConfuserEx\` liegt; sonst wird es übersprungen.
- **Lizenzbedingungen**: Bei der Installation müssen die Bedingungen einmal bestätigt werden (Weitergabe und Verändern
  untersagt, Betrieb nur mit Original-Platine, Gewährleistungs- und Haftungsausschluss, deutsches Recht). Sie sind im
  Programm jederzeit unter Allgemein → Rechtliches → „Lizenzbedingungen anzeigen“ nachlesbar und liegen als
  `LIZENZBEDINGUNGEN.txt` im Programmordner (auch im Startmenü). **Hinweis:** kein absoluter Schutz – ein Programm lässt
  sich mit genügend Aufwand zerlegen; die Maßnahmen erhöhen die Hürde.

SIGNATUR: C35DEEF130D5AFDBE6EEFF06A4430145E135CEEEAC23EB646EADDAF6CF244632D1875FA397E0BD6CD230F1468A0BF28A773AF1F14630A4F49063A1DB4846CBC3
