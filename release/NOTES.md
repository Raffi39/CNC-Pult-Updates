### Verbindungstool 2026.11.01.1 – LED je Achse/Richtung, Poti-Kalibrierung

- **LED „Achse wird verfahren“ / „Handrad aktiv“ mit Achswahl**: Hinter der Quelle lässt sich jetzt
  „alle Achsen“, „X (beide Richtungen)“, „X+“, „X–“ … bis „C–“ wählen. Die Richtung wird aus der
  Maschinenposition ermittelt (alle 100 ms, solange EdingCNC Verfahren bzw. Handrad meldet) – damit
  wirkt es auch beim Verfahren über die EdingCNC-Oberfläche. Beim Dauer-Verfahren vom Pult leuchtet die
  LED sofort. Nach dem Stillstand ca. 0,3 s Nachleuchten. Bestehende Einstellungen bleiben „alle Achsen“.
- **Poti-Kalibrierung je Platine**: Reiter Platinen → „Potis kalibrieren …“ zeigt die Rohwerte live;
  „0 % übernehmen“ / „100 % übernehmen“ lernen die Anschläge der Potis dieser Platine ein (Ausgleich von
  Bauteiltoleranzen, Sicherheitsabstand 6 von 1023, verkehrt angeschlossene Potis werden umgedreht).
  Gilt nur im Echtbetrieb; „Duplizieren“ übernimmt die Kalibrierung nicht. Firmware unverändert.

SIGNATUR: E57FBBB534BD9A4869BCD9C7EE34EA0779F684B90D23B61522BFDBD9C57A06CD5D91F9769576986DA895B7106773D1208EE22B03BC8827E4A00FD99F45EB56EE
