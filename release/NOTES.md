### Verbindungstool 2026.10.31.5 – Handrad wie das Original, Nachlaufbegrenzung, Platinen mit Bauteilen

- **Nachlaufbegrenzung im Schrittbetrieb**: Wird das Rad schneller gedreht, als die Achse fahren kann, liefen die
  Rastungen auf und die Maschine fuhr nach dem Loslassen weiter. Jetzt liest das Programm bei jeder Rastung die
  Maschinenposition und gibt nur so viele Rastungen weiter, dass das Ziel höchstens „Nachlauf höchstens“ (Vorgabe
  1 mm, mindestens eine Rastung) vorauseilt – überzählige Rastungen werden verworfen (Hinweis im Protokoll).
  Langsames Drehen bleibt exakt.
- **Handrad-Abbildung nach dem Original**: Antenne, Display mit großen Ziffern (F/S in Prozent wie am Gerät),
  RESET/Stop gelb, Start/Pause grün, POWER, zweifarbige Tasten (oben blau Macro-n = Fn-Belegung, unten orange
  Funktion), großes Fn, Probe-Z und Macro-10 zwischen den Drehschaltern, Continuous/Step gelb, blaues MPG-Rad mit
  Skala (dreht mit) und heller Griffscheibe. Belegung jeder Taste als Hinweis beim Darüberfahren.
- **Display des Handrads**: F und S zeigen den Vorschub- bzw. Spindel-Override in Prozent.
- **Verhalten wie das EdingCNC-Handrad einstellbar** (Vergleich mit docs.edingcnc.com/hardware/wireless-pendant):
  - neue Funktion **„W-Home wie EdingCNC“**: Achswahl OFF = G0 X0 Y0, Achswahl X…C = Werkstücknull dieser Achse setzen;
  - Haken **„Achswahl OFF: Stufenschalter stellt Vorschub-Override“** (2/5/10/30/60/100 % beim Umschalten);
  - Haken **„CONTINUOUS / STEP schalten die Betriebsart des Rads“** – aus = frei belegbar;
  - **„Einzelsatz“** mit Schaltart umschalten / nur ein / nur aus (wie Kühlung);
  - Knopf **„Belegung wie EdingCNC-Handrad…“**: Stop = Pause, W-HOME wie Eding, Probe-Z = `xhc_probe_z`,
    Fn + Taste = `xhc_macro_1…10`, Override ±5 %, CONTINUOUS/STEP = Einzelsatz aus/an, Achswahl OFF = Vorschub-Override.
    Die CNC-Pult-Werkseinstellung bleibt über „Ganzes Handrad auf Werkseinstellung…“ erreichbar.
- **Platinenbilder mit Bauteilen**: `gerber_vorschau.py` zeichnet jetzt auch die Bauteile aus Stückliste und CPL
  (ICs, Widerstände, Kondensatoren, Dioden, Elko, Spule, Taster, Klemmen, Wannenstecker, USB-C, RJ45); Lage jedes
  Bauteils an Lötpads bzw. Bohrungen abgeglichen.

SIGNATUR: 3D18F35B2253AEBFAB511920FA0140D92CC7EF3FBCD7B6F45584936BA12FEA67E0D5EDF621C0ABC0634E08F8454401220645287DD8C252C82709DF0BA7BF48F4
