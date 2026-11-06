### Verbindungstool 2026.11.06.2 und Firmware 4.7 / 5.5 / 10.4 / 15.3 – ruhige Potis [in Arbeit]

- **Fehler (gemeldet von Raffi am 06.11.2026, 10-kΩ-Poti am Controller V3.3, Kabel ca. 10 cm)**: Der Rohwert des
  Potis sprang am Anschlag zwischen etwa 10 und 40. Die Firmware sendete je 50 ms einen einzelnen ADC-Wert; die
  Schwelle von 4 griff dadurch nie, der Override in EdingCNC zitterte um etwa ±2 %.
- **Firmware (alle Controller, gleiche Datei `pult_pot.h`)**: je Poti und Zyklus eine Messung nach dem Kanalwechsel
  verwerfen, 16 Messungen, die 2 kleinsten und 2 größten weglassen, Rest mitteln; danach gleitender Mittelwert
  (1/4 je Zyklus, ca. 0,2 s), bei einer Änderung von mehr als 32 Schritten (Poti wird gedreht) sofort folgen.
  Gesendet wird bei Änderung um mehr als 2 Schritte und weiter alle 500 ms. Protokoll unverändert.
  Rechnertest mit nachgebildetem Rauschen (±15 und 2 % Störspitzen um ±120): Ausgabe ruhig ±2–3 Schritte,
  keine Meldungen im Stillstand, Drehen 0→1000 in 1 s folgt ohne Verzögerung.
- **Verbindungstool**: Hysterese auf den Prozentwert – ein neuer Override-Wert gilt erst, wenn das Poti um mehr
  als 0,6 % von der aktuellen Stufe weg ist; an den Anschlägen sofort. Kein Pendeln zwischen zwei Nachbarwerten.
- **SICHERHEIT – Achse fuhr weiter (gemeldet von Raffi am 06.11.2026)**: Y− im Dauerbetrieb halten, schnell X−
  dazu drücken, loslassen → Tastenmodul dunkel und ohne Reaktion, die Maschine fuhr einige Sekunden weiter, danach
  LEDs wieder an und Stillstand. Controller blieb verbunden. **Ursache**: Der Ablauf des Verbindungstools (ein Thread
  für Tasten, EdingCNC, LEDs und Lebenszeichen) hing einige Sekunden – vermutlich in einem Aufruf an EdingCNC.
  Ohne Lebenszeichen schaltete die Firmware (ab 4.6) nach 1,5 s die LEDs ab; das Loslassen der Taste und die
  0,4-s-Prüfung wurden erst nach dem Hängen verarbeitet. **Messung (Protokoll Raffi, 20:49)**: CncStopJog dauert
  in EdingCNC etwa 200 ms, CncStartJog2 bis 850 ms – die Aufrufe warten, bis EdingCNC sie verarbeitet hat.
  **Behebung**:
  - Eigener Verfahr-Ablauf: Der Hauptablauf legt je Achse nur noch den Wunsch fest (fahren mit Richtung/Tempo oder
    stehen) und wartet nie auf EdingCNC. Der Verfahr-Ablauf bringt EdingCNC auf den jeweils neuesten Wunsch;
    Stopps haben Vorrang (vor jedem Start werden fällige Stopps gesendet), ein überholter Start wird nicht mehr
    gesendet. Schritte der Reihe nach, höchstens 3 offen. Gilt für Tasten, Eilgang/Tempowechsel und Handrad-Dauerbetrieb.
  - Lebenszeichen, LEDs, Loslassen und die 0,4-s-Prüfung laufen dadurch ohne Unterbrechung weiter.
  - Sicherheits-Thread: hängt der Hauptablauf trotzdem länger als 400 ms, während eine Achse fährt, wird über den
    Verfahr-Ablauf alles gestoppt („SICHERHEIT: Ablauf hängt …“); weiter nur mit neuem Tastendruck.
  - Diagnose: Verfahrbefehle, die länger als 500 ms dauern, stehen mit Dauer im Protokoll.
  - Beim Beenden des Programms werden alle Achsen direkt gestoppt.
  Bleibt in Prüfung, bis Raffi den Ablauf an der Maschine bestätigt hat. Not-Halt ist hart verdrahtet und unabhängig.
- **Raststelle (neu, Wunsch Raffi)**: Reiter **Allgemein** → **Override-Potis**: je Poti (Vorschub/Spindel)
  abschaltbar „mit Raststelle bei … % ± … %“ (Vorgabe aus, 100 % ± 3 %). Im Bereich gilt genau der eingestellte
  Wert. Auch der Simulationsregler zeigt den Wert mit Raststelle. Alte Einstellungen: Raststelle aus.
- Die neuen Firmwares sind im Programm enthalten und werden beim Verbinden zum Update angeboten.
- Auf echter Hardware noch zu bestätigen (V3.3 mit Poti).

### Verbindungstool – Update-Quelle wird nicht mehr angezeigt [in Arbeit]

- Reiter **Allgemein** → **Updates**: Der Hinweis lautet nur noch „Vor jedem Update werden die Einstellungen in den
  Ordner „Sicherungen“ kopiert.“ – die Angabe „Quelle: github.com/…“ entfällt (Wunsch Raffi, 06.11.2026).
  Die Update-Prüfung selbst ist unverändert (`MainForm.cs`).

### Verbindungstool – Treiberanleitung für den DFU-Bootloader (Controller V3.x) [in Arbeit]

- Neue Anleitung `07_Verbindungsprogramm/TREIBER_DFU_Controller_V3.txt` (für Tester mit Controller V3.3):
  WinUSB-Treiber für „ATm32U4DFU“ (03EB:2FF4) einmalig je PC mit Zadig oder QMK Toolbox, Fehlerbehebung.
- `ANLEITUNG.txt`: neuer Abschnitt „Treiber für den DFU-Bootloader“, Firmware-Update V3.x ohne RESET-Taste
  (ab 4.5), Hinweis zu „Tool change area violation“ (Meldung von EdingCNC, tritt auch ohne Pult auf),
  Stand 06.11.2026. Kommt mit dem nächsten Setup ins Programmpaket (ANLEITUNG.txt ist im Setup enthalten).

SIGNATUR: 27EBFEB75B677555598DFAA7C0A8FCD78CE5BA1B08F762FB22DEB604BA1FC60DEF2DA6BD6393B36D79B94D6B883E10AFA333DF835F21203E325B84217C0DBCC0
