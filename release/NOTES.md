### Verbindungstool 2026.10.31.4 – Handrad: richtige Wege, Dauerbetrieb, neue Abbildung

- Gleicher Inhalt wie 2026.10.31.3: Diese wurde versehentlich mit der Versionsnummer 2026.10.31.2 unterschrieben
  (veraltete Hilfsdatei `_signieren.cmd` auf dem PC) und vom Programm zu Recht abgelehnt („Unterschrift ungültig“).
  Jetzt richtig unterschrieben; die Unterschrift wird vor dem Veröffentlichen gegengeprüft.
- **Weg je Rastung korrigiert**: Eding rechnet im Handradbetrieb mit „Schritte je Umdrehung“. Bisher wurde
  `handwheelCountPerRev` aus der server.ini übernommen (bei Raffi 400, gilt für ein Encoder-Handrad am Controller) –
  das WHB04B liefert aber 1 Zählschritt je Rastung (100 je Umdrehung), dadurch fuhr das Rad nur etwa ein Viertel des
  Wegs. Jetzt fest 100 Schritte je Umdrehung: 0,001 / 0,01 / 0,1 / 1 mm je Rastung.
- **Schrittbetrieb exakt** (neu, Vorgabe an): immer Positionsmodus. Bisher galt der Geschwindigkeitsmodus aus der
  Eding-Einstellung (`handwheelX100VelMode = 1`), der bei 1 mm Wege abbricht, sobald das Rad steht.
  Abschaltbar; dazu ein **Wegfaktor** zum Abgleichen (Vorgabe 1,000).
- **Dauerbetrieb (Taste CONTINUOUS)**: die Achse fährt mit 2 / 5 / 10 / 30 / 60 / 100 % der Höchstgeschwindigkeit
  (Stellung des Stufenschalters), solange das Rad gedreht wird; 300 ms ohne Rastung = Halt (Totmann, auch bei
  Funkabbruch). **STEP** schaltet zurück auf Schrittbetrieb. CONTINUOUS/STEP sind dafür fest, ihre Fn-Ebene
  (MACRO-15/16) bleibt belegbar. Stop, Reset und Not-Halt beenden den Dauerbetrieb.
- **Abbildung wie das echte Gerät**: Tasten 4 × 4 in der Reihenfolge der Tastencodes (RESET oben links …
  MACRO-10 unten rechts), orange Haupt- und blaue Fn-Beschriftung (MACRO-1 … MACRO-16), LCD mit WC/MC,
  STP/CONT, Achsstern, F/S; Drehschalter mit Rastmarken, MPG-Rad mit Skala 0–100 und Griffmulde.
- **Programmfenster** öffnet höher (bis 890 Pixel Innenhöhe, begrenzt auf den Bildschirm), damit die
  Handrad-Abbildung ohne Scrollen ganz sichtbar ist.
- **Reiter „Tasten und LEDs“**: unter den Tasten eine gerenderte Ansicht der gewählten Platine (V3.3, V3.4, V5.1, V10:
  Lötstopplack, Pads, Bestückungsdruck, Bohrungen – kein Leiterbahn-Layout). Erzeugt aus den Gerber-Daten mit dem neuen
  Werkzeug `08_Werkzeuge_Platinen\gerber_vorschau.py`, eingebettet aus `Quelltext\Bilder\platine_*.png` (`build.cmd` ergänzt).
- **Controller V5.0 entfernt** (wurde nie gefertigt): Profil gestrichen; Einstellungen und Kennungen mit V5.0
  werden als V5.1 übernommen.
- **Simulation**: Drehschalter und Rad mit gedrückter Maustaste drehen (100 Rastungen je Umdrehung), Klick auf eine
  Schalterbeschriftung stellt den Schalter direkt dorthin.

SIGNATUR: 1FE18EEFC8279F766FE2AEC06C94232E6FCE0E50830AB57E77345E62D2C79C4F62B64481E0281AF776BD1A43E2556FB44402675798E2E3044904A99A466DE639
