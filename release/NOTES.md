### Verbindungstool 2026.11.09.1 – neue Werkseinstellung, Handrad ausgeblendet, ohne Firmenname und Anschrift

- Neue Werkseinstellung der Tasten und LEDs für die farbigen Controller (V3.3, V3.4, V5.1): Raffis aktuelle Belegung
  (Stand 08.11.2026) ist als Vorgabe eingebettet (`Quelltext/Vorgaben/Tasten_V3.xml`). Sie gilt für neue Platinen,
  „Werkseinstellung“ je Taste und „Alle Tasten auf Werkseinstellung“; bestehende Konfigurationen bleiben unverändert.
  Fehlt die Vorgabe, gilt die bisherige Werkseinstellung.
- Werkseinstellung im Reiter „Allgemein“ (außer EdingCNC-Pfaden) ebenfalls nach Raffis Werten: Hintergrundfarbe Weiß,
  Haltezeit 1000 ms, Vorschub-Poti 50–150 % mit Raststelle 100 % ± 5 %, Spindel-Poti 50–200 %, Verfahren langsam/mittel/
  schnell 10/50/80 %, Startwert „langsam“, Lieblingsfarben. Gilt nur für neue Installationen.
- Folien-Editor: Standardbeschriftung JOG/FUNKTION passend zur neuen Tasten-Werkseinstellung.
- Handbücher: Belegung und LED-Farben der Werkseinstellung neu, Abschnitt „Potis für Vorschub und Spindel“
  (Empfehlung 10 kΩ linear, elektrische Daten je Controller), Maßzeichnungen und Einbaumaße der Tastenmodule;
  Handrad-Abschnitte werden nur gebaut, wenn das Handrad freigegeben ist (`build.py` liest `Version.cs`).
- Handrad vorerst ausgeblendet (noch nicht freigegeben): Reiter „Handrad“, Handrad-Betrieb (kein Zugriff auf den
  Empfänger), Handrad-Anzeige in der Statuszeile sowie „W-Home (nur Handrad)“ und die LED-Quelle „Handrad aktiv“ in den
  Auswahllisten sind nicht mehr sichtbar. Der Code bleibt erhalten; Freigabe über `AppInfo.HandradFreigegeben` in
  `Version.cs`.

- Auf Wunsch von Raffi (09.11.2026) stehen im Verbindungstool, im Folien-Editor und in allen Dokumenten nur noch Name
  und E-Mail (Raphael Kostka, raphael.kostka@web.de): kein „Kostka Engineering“ und keine Anschrift mehr (Kopfzeile,
  Hilfe/Support, Protokoll-Reiter, Diagnose, Handbücher, Lizenz/Datenschutz/Sicherheitshinweise, Herausgeber im Setup).
- Zertifikat-Skripte suchen das Signatur-Zertifikat jetzt nach „Raphael Kostka“ (passt auch zum bisherigen Zertifikat);
  ein neu erstelltes Zertifikat heißt nur noch „Raphael Kostka“.

SIGNATUR: 1FA733F4D2421D6A001A3B53CF283AA186C3614BE492CC80C9715B848661EFF5F1F7C56813572B92B6B5F26753907F5F16F803CE345393DB95405D16826EFDD8
