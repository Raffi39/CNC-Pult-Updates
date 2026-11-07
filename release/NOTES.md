### Verbindungstool 2026.11.07.1 – Tastenkürzel an offene EdingCNC-Dialoge, Diagnose-Datei und Kontakt [in Arbeit]

- **Fehler (gemeldet von Raffi am 07.11.2026)**: War in EdingCNC ein Dialog offen (z. B. „Nullpunkt ermitteln“) und
  wurde ESC über ein Tastenmodul gesendet, verlor der Dialog den Fokus und reagierte nicht mehr; ESC über die Tastatur
  schloss ihn. **Ursache**: Das Tool holte vor jedem Tastenkürzel das EdingCNC-Hauptfenster nach vorn (mit kurzem
  ALT-Antippen gegen die Windows-Vordergrundsperre). Das ALT ging an den offenen Dialog, danach wurde das
  Hauptfenster aktiviert – das Kürzel kam beim Dialog nie an.
- **Behebung**: Gehört das Vordergrundfenster schon zu EdingCNC (Hauptfenster oder Dialog), wird nichts umgeschaltet
  und das Kürzel direkt gesendet (von Raffi bestätigt). Ist ein anderes Programm vorne (z. B. das Verbindungstool),
  wird das **oberste** sichtbare, bedienbare EdingCNC-Fenster nach vorn geholt – Dialoge liegen immer über dem
  Hauptfenster, auch nicht-modale Makro-Dialoge, die das Hauptfenster nicht sperren (2. Meldung 07.11.: dort kam die
  Taste erst nach einem Mausklick in den Dialog an). Berücksichtigt werden das Hauptfenster, ihm gehörende Fenster
  und Fenster mit Titelleiste, keine Werkzeugfenster. Im Protokoll steht dann „(an offenen EdingCNC-Dialog)“.
- **Neu: Diagnose und Kontakt (Wunsch Raffi, 07.11.2026)** – Reiter **Protokoll** oben: Kontaktdaten (Raphael Kostka,
  Grenzweg 1, 42555 Velbert, raphael.kostka@web.de) und die Knöpfe **„Diagnose speichern …“**, **„Per E-Mail senden …“**
  und **„Protokollordner öffnen“** (`Diagnose.cs`). Die Diagnose ist eine einzige Textdatei: Programm/Windows/.NET/
  Administrator, EdingCNC (bin-Ordner, Makrodatei, Verbindung, letzter Fehler, alle Installationen), je Platine
  Betriebsart, Zustand, Anschluss, Kennung, Firmware, ID, Original-Prüfung, letzter Fehler, Alter der letzten Daten,
  Poti-Rohwerte, Module/Bus-Fehler (V15), serielle Anschlüsse, die Einstellungs-XML (Kopplungsschlüssel `NetKey`
  entfernt), das Bildschirm-Protokoll und die Protokolldatei. E-Mail: Simple MAPI mit Anhang (Outlook, Thunderbird …),
  sonst mailto + Datei im Explorer markiert.
- **Neu: Protokolldatei** – alle Protokollzeilen werden zusätzlich mit Datum in `<Datenordner>\Protokoll.txt`
  geschrieben (ab 1 MB → `Protokoll_alt.txt`), damit sie nach Neustart/Absturz für die Diagnose erhalten bleiben.

SIGNATUR: 4C59FDF20897E2F2289A0B0A4FA9B7E63F3F37ABFA13BA995A9FE813048EBF461B216F09CC2DF17306550F0BCE27F09AF747A93C6E1B48525CBB9190FA7B2C83
