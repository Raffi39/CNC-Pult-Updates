### Verbindungstool 2026.10.31.8 – periodische Platinenprüfung entfernt

- **Platinenprüfung nur noch beim Verbinden**: Die alle 2 Minuten wiederholte Original-Prüfung
  (nur V5/V10) wurde entfernt. Sie brachte wenig – eine Platine besteht die Prüfung ohne den echten
  Firmware-Schlüssel ohnehin nicht – und barg das Risiko einer Fehlabschaltung mitten im Betrieb,
  wenn Antworten ausbleiben. Die Prüfung beim Verbinden (und bei jedem Neuverbinden) bleibt; alle
  Platinen – auch Controller V3.3/V3.4 – verhalten sich jetzt gleich. Verschleierung und
  Selbstprüfung der Unterschrift bleiben unverändert.

SIGNATUR: 3A181622B4AFA6DEE3D6A3D8F6D922B6D8E1442F27C305899996420D38535FA8339145A74A06FEE9F062D7AC8AF3F421CB1C7DB3B2688AB15E9003BA3BF15AB4
