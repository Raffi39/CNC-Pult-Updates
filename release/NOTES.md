### Verbindungstool 2026.10.31.2 – Funk-Handrad XHC WHB04B-6, Schaltart für Kühlung

- **Neuer Reiter „Handrad“** für das Funk-Handrad XHC **WHB04B-6** (USB-Empfänger 10CE:EB93, HID ohne Treiber;
  Kennung im Reiter änderbar). Abbildung des Handrads mit Anzeige (Position X/Y/Z bzw. A/B/C, F, S), Tasten,
  Achswahl, Stufenschalter und Rad; gedrückte Tasten rot, laufende Sicherheitszeit orange, Rohdaten zur Fehlersuche.
  **Tasten belegen** durch Anklicken in der Abbildung (Haupt- und Fn-Belegung MACRO-1 … MACRO-10), dieselben
  Funktionen wie die Pult-Tasten inkl. Sicherheitszeit; Dauer-Verfahren über Tasten ist am Handrad gesperrt.
  **Simulation** auf derselben Seite (Betrieb „Simulation“): Tasten, Schalter und Rad in der Abbildung bedienen.
- **Rad**: Verfahren über den **Handradbetrieb von EdingCNC** (`CncStartHandweelTracking` /
  `CncSetTrackingHandwheelCounter` / `CncStopTracking`) mit denselben Werten wie Edings eigene Anwendung
  `WirelessPendant.exe` (Achs-Höchstgeschwindigkeit aus `CncGetJointConfig`, Schritte/Umdrehung und Stufenwert aus
  `CncGetHandwheelConfig`, Wegfaktor 0,1/1/10/100 für 0,001/0,01/0,1/1 mm; ×25,4 bei Zoll für X/Y/Z).
  Je Stellung des Stufenschalters einstellbar: Schrittweite, Vorschub- oder Spindel-Override (Schritt je Rastung
  einstellbar) oder nichts. Kein Handradbetrieb während ein Programm läuft oder bei Not-Halt; Achswahl OFF,
  Abziehen des Empfängers, Betriebswechsel und Programmende beenden ihn. Achsumkehr (Reiter Allgemein) gilt auch für das Rad.
- **Display des Handrads** wird beschrieben (3 Feature-Reports, Werkstück- oder Maschinenkoordinaten wählbar).
- Warnung, wenn gleichzeitig „MektriX x EdingCNC“ oder `WirelessPendant.exe` läuft.
- `Eding.cs`: neu `CncGetWorkPosition`, `CncGetMachinePosition` (Rückgabe über versteckten Zeiger, „ret 4“),
  `CncGetActualFeed`, `CncGetActualSpeed`, `CncInMillimeterMode`, Handrad-Funktionen (Parametergrößen aus „ret n“ geprüft).
- **Kühlung Flut / Nebel mit Schaltart**: umschalten (wie bisher, Vorgabe), nur einschalten (M8/M7) oder nur
  ausschalten (M9 – schaltet in EdingCNC alle Kühlungen aus). Bestehende Belegungen bleiben „umschalten“.
- Neue Funktionen für alle Tasten: „Programm Start / Pause (umschalten)“ und „Spindel ein/aus (M3/M5)“.
- Selbsttest (`/selbsttest`): Handrad in Simulation, Bild des Handrad-Reiters, Prüfung der Anzeige-Kodierung.
- Noch nicht mit echtem Handrad getestet (Tastencodes nach LinuxCNC-Treiber `xhc-whb04b-6`).

SIGNATUR: 501F619ECAEE9C5DCB80AFBF31B1FFF3ED894169F16E598DC844C58C157845DDEF947F065DD569DBA2B68DD2B3353FA25102C3DA66E8F4694F605134F1C6FB2B
