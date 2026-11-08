### Verbindungstool 2026.11.08.2 – Makro-Taste zeigt an, solange ihr Makro läuft

- **Makro-Tasten: „Funktion dieser Taste aktiv“ = Makro läuft** (Wunsch Raffi): Die LED ist EIN, solange das von dieser
  Taste gestartete Makro läuft – auch wenn es weitere Unterprogramme aufruft und während es auf eine Eingabe wartet
  (z. B. Werkzeugnummer beim Werkzeugwechsel user_13). Ende, wenn EdingCNC wieder 0,7 s lang „Bereit“ ist (kurze
  Bereit-Momente zwischen zwei Schritten zählen nicht), oder bei Abbruch, Fehler, Not-Halt, Reset nötig und Trennung.
  Läuft das Makro nicht binnen 3 s an (z. B. von EdingCNC abgelehnt), endet die Anzeige ebenfalls.
- **LED mit mehreren Bedingungen** (Wunsch Raffi): Unter „LED reagiert auf“ lässt sich die Bedingung mit „nicht“
  umkehren, und mit „+ weitere Bedingung“ kommen bis zu drei weitere hinzu – je mit „und“/„oder“ und „nicht“, von oben
  nach unten verknüpft. Beispiel Spindelstopp M5: „Spindel an“ UND NICHT „Programm läuft“. Weitere Bedingungen können
  Zustände ohne Zusatzangabe sein (also nicht Ausgang/Eingang/Achse/Variable). Gilt auch für Mehrfachauswahl; „LED
  kopieren“ überträgt weiter nur die Darstellung.
- Fehler behoben: Reset am Pult bei ausgeschalteten Motortreibern ließ kurz alle LEDs ausgehen. EdingCNC braucht für
  diesen Reset länger, das Programm wartete und pingte die Platinen nicht – nach 1,5 s ohne Lebenszeichen schaltet die
  Firmware die LEDs ab. Jetzt pingt der Schutz-Ablauf die Platinen weiter, solange der Hauptablauf blockiert ist.
- Tasteneditor: In Zahlenfelder getippte Werte (z. B. Helligkeit 25 %) gelten sofort – „Übernehmen“ erscheint gleich,
  ohne erst in ein anderes Feld zu klicken; Enter übernimmt ohne Windows-Fehlerton.
- Vorschlag beim Wählen von „Makro ausführen“ (außer home_all): LED „Funktion dieser Taste aktiv“, Status EIN blinkt
  grün, Status AUS Hintergrund.
- Zu prüfen an EdingCNC: ob der Zustand während der Eingabeaufforderung eines Makros nicht „Bereit“ meldet (sonst endet
  die Anzeige dort zu früh).

SIGNATUR: A237FECC960FC15EFDAEC4AA5471A014B452FCA0B782F809B9F29FAE6B9223786B646CB0E14A62F69F0024E9ADD4C89A4C899A9AB1BEFC5D18BF29BCCA04002E
