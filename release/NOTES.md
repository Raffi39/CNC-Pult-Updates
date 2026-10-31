### Verbindungstool 2026.10.31.1 und Firmware 5.3 / 10.3 – kurzschlussfeste Ausgänge (Platinen V5.1 / V10.1)

- **Verbindungstool**: kennt die Platinen **V5.1** (neues Profil, gleiche Tasten wie V5.0) und **V10.1**
  (Kennung `B10.1`, Profil V10). Die Meldung `F 1`/`F 0` der V10.1 wird im Zustand der Platine angezeigt
  („LED-Treiber meldet Überstrom/unbelegte Klemme“). Die enthaltene Firmware 5.3/10.3 wird **nur auf
  Platinen ab V5.1/V10.1** aufgespielt (andere Treiber und Anschlüsse); meldet eine Platine B5.0/B10.0, wird
  kein Update angeboten und das manuelle Aufspielen abgelehnt.
- **Controller V10.1**: LED-Treiber TPIC6B595 durch **TI DRV8860** ersetzt (8 kurzschlussfeste Low-Side-Ausgänge je
  Baustein, Überstrom-/Übertemperaturabschaltung, Erkennung offener Last). Pegelwandler 74AHCT1G125 entfallen,
  die Kette hängt direkt am RP2040 (DIN GPIO3, CLK GPIO4, LATCH GPIO5). **ENABLE GPIO6 ist jetzt aktiv HIGH**
  (Pull-down, LEDs beim Start aus), Helligkeit per PWM 500 Hz an ENABLE. Neu **nFAULT GPIO7** nur als Hinweis:
  Meldung `F 1` / `F 0` an den PC bei Änderung (höchstens 1× je Sekunde), die LEDs bleiben an – der DRV8860
  meldet an jedem ausgeschalteten, unbelegten Ausgang „offene Last“, nFAULT ist bei nicht voll belegten
  Klemmen also dauerhaft LOW. Die Überstrom-Sperre wird alle 2 s durch kurzes Schreiben von 0 gelöscht
  (ca. 0,4 ms, unsichtbar). Kennung `B10.1` (auch Antwort auf `?`). CLK/LATCH/DIN mit 2 mA Treiberstärke
  (lange Leitungen). Zeiten laut Datenblatt (CLK ≥ 5 µs).
- Vor Neustart/Bootloader werden die Ausgänge abgeschaltet (V5 und V10); V5 bekommt einen 4-s-Watchdog
  (ENABLE liegt bei V5.1 fest an 3,3 V).
- **Controller V5.1 (Layout V9)**: Ausgänge OUT1–8 über **einen DRV8860** statt 74HC595 + 2× TPS4H160, damit
  **masseschaltend wie V10** (Klemmen J8/J9: „+“ = VIN über Polyfuse, „Ln“ = nach GND geschaltet). Die
  **M22-Eingänge J4** werden wie bei V10 gelesen: Taster gegen GND, 4k7/10k/10 nF, **74HC165** an GPIO23; Takt und
  Laden teilen sich CLK/LATCH des DRV8860 (LATCH invertiert auf /PL). Jede Millisekunde ein Zyklus: 8 Bit Ausgänge
  schreiben, dabei 8 Eingänge lesen, dann LATCH. Alle 2 s ein Zyklus mit Ausgängen = 0, damit ein
  kurzgeschlossener Ausgang nach Behebung wieder einschaltet. Zeilen R0–R3 bleiben für die Tastenmodule
  (Tasten 0–55), M22 = Tasten 56–63 wie bisher. Kennung `B5.1`.
- Noch nicht auf Hardware getestet (Platinen V5.1/V10.1 in Fertigung).

SIGNATUR: C449AA34069682F2AD51830AF49F26809698962DA8C4E785B3381D78BA30485D9A866BE8CA240339B64634A99D23DB826AA4937341EE6191903E029C6B183686
