# Statuscheck Teil 2 – Antwort auf Briefing vom 12.08.2026
**Stand: 13. August 2026 – reine Bestandsaufnahme, nichts ausgeführt/verändert**

## Rücken-Cluster

**1. PDF-Lead-Magnet "5-Minuten-Rückenübungen" – erledigt, aber anders als evtl. angenommen**
Datei ist live (`.../wp-content/uploads/5-minuten-rueckenuebungen.pdf`, Status 200) und auf
**zwei** Seiten eingebunden (`/ruecken-uebungen/` und `/rueckenschmerzen/`) als gestylte
Download-Box mit Klartext-Link. Aber: **direkter Download, kein Newsletter-Gate.** Es gibt keine
E-Mail-Anmeldung davor – wer klickt, bekommt die PDF sofort, ohne Adresse zu hinterlassen. Falls
ein Lead-Magnet-Gate (E-Mail gegen PDF) ursprünglich geplant war, ist das nicht umgesetzt.

**2. Ischias-Selbsttest-Widget – teilweise**
- Klick-Durchlauf-Verifikation: Keine Hinweise auf einen echten interaktiven Test gefunden
  (kein Log, keine spätere Erwähnung). Ich habe damals nur den Code/die Anzeige per Screenshot
  geprüft, nicht den tatsächlichen Klickpfad in einem Browser. Aktuell habe ich auch keinen
  Browser-Zugriff in dieser Session.
- CTA-Button: **immer noch Platzhalter** – verlinkt live weiterhin auf `/kontakt/`, wurde nie
  auf eine spezifischere Ziel-URL geändert.

**3. Facebook-Karussell "Ischias-Check" – unbekannt/nicht auffindbar**
Weder die Datei `facebook-karussell-ischias-check.md` noch irgendein Hinweis darauf finde ich
in meinen aktuellen Unterlagen (weder in `/root/praxis-seo/` noch im Upload-Ordner dieser
Session). Vermutlich nur in einer früheren Chat-Session vorhanden, die nicht Teil meines
aktuellen Kontexts ist. Kann den Stand der 7 Bilder nicht beurteilen.

**4. Marky-MCP-Fähigkeiten – geprüft**
- Mehrbild-Posts: `create_post` akzeptiert `media_urls` als **Array** – mehrere Bilder in einem
  Post sind technisch unterstützt (das wäre die Grundlage für ein Karussell).
- Echte Nutzung geprüft (`list_posts`, 50 aktuellste Einträge): Es gibt bereits einen
  **erheblichen Bestand an echten Marky-Posts** (viele PUBLISHED, einige SCHEDULED/REJECTED,
  laufend seit Ende Juni). Aber: **kein einziger davon hat mehr als 1 Bild** (`media_count`
  überall 0 oder 1) – ein Mehrbild-Post wurde also noch nie tatsächlich erstellt. Und: **kein
  Post mit Bezug zum Ischias-Karussell** in der Liste – dieser spezifische Post wurde über Marky
  nie angelegt.

**5. FAQ-Schema Rücken-Cluster – unverändert offen**
Frisch (gerade eben) per API geprüft: `hexenschuss-was-tun` zeigt weiterhin FAQPage-Schema mit
Rich-Results-Fehler. Die 4 neuen Artikel (ruecken-uebungen, bandscheibenvorfall-lws-syndrom,
ischias-ischiasnerv, rueckenschmerzen) haben weiterhin **kein** FAQPage-Schema. Keine Anzeichen
einer manuellen Bearbeitung in wp-admin seit dem letzten Stand.

## Rechtliche/organisatorische Punkte

**6. Datenschutzerklärung + CleverReach-Passus – erledigt**
Vollständiger, korrekter Absatz "Newsletter-Versand über CleverReach" mit Firmenname, Adresse
und Link zur CleverReach-Datenschutzerklärung ist live auf der Datenschutzseite vorhanden. Das
war offenbar schon erledigt, bevor es aus dem Blick geriet – gute Nachricht.

**7. LaVita-Lektorat (Post-ID 11765) – unbekannt, kein Skript auffindbar**
Kein Skript mit "lavita" im Namen in `/root/praxis-seo/` gefunden. Post 11765
("Warum ich das LaVita Vitalstoffkonzentrat empfehle") wurde zuletzt am 25.07. geändert – ob das
die Lektorat-Anwendung war oder ein unabhängiger Edit, kann ich ohne Vorher-Version nicht
sagen. Ohne das erwähnte Skript kann ich "ausgeführt ja/nein" nicht verlässlich beantworten.

**8. Sonnenschutz-Seite – wahrscheinlich nur Meta-Description**
Seite zuletzt am 03.08. geändert – das Datum fällt genau mit dem automatischen
Alt-Text-Ergänzungs-Lauf (Block 4) zusammen, nicht mit einer inhaltlichen Überarbeitung. Ohne
die ursprünglich geplante Überarbeitungs-Fassung zum Vergleich kann ich nicht zweifelsfrei
sagen, ob eine inhaltliche Überarbeitung je stattfand – die Änderungshistorie deutet aber eher
darauf hin, dass nur die Meta-Description (und ein Alt-Text) angefasst wurden.

## Sonstiges

**9. GitHub-Ordner für Datei-Austausch – nie eingerichtet**
Geprüft: beide GitHub-Repos (`praxis-seo-tools`, `praxis-seo-reports`) haben keine
Austausch-/Exchange-Struktur, nur Code bzw. Reports. Datei-Austausch läuft weiterhin über dich
als Vermittler (Copy-Paste/Upload).

**Nebenfund dabei:** `praxis-seo-tools` enthält nur `ahrefs_tool.py` und `wp_publish.py` – die
neueren Skripte `image_optimize.py`, `link_healing.py` und `faq_linking.py` wurden nie dorthin
gepusht (nur die Reports werden automatisch gepusht, die Tools/Skripte nicht). Kein Datenverlust,
da alles lokal hier liegt – aber falls du diese Skripte auch im Repo als Backup haben willst,
sag Bescheid, das push ich gerne nach.

**10. Prompt "Monatliche Report-Automatisierung" (12.08.) – in Bearbeitung, noch nicht abgeschlossen**
Das war meine unmittelbar letzte Aufgabe vor diesem Statuscheck hier. Stand: Content-Strategie-
Report existiert nicht (Rückfrage an dich/Chat gestellt, was rein soll), E-Mail-Versand für
ai_visibility braucht SMTP-Zugangsdaten (angefragt, noch nicht erhalten). Siehe
`monatliche_reports_klaerung_2026-08-13.md` für Details – wartet auf deine/Chat-Antwort.

---

## Was sich sonst noch getan hat, aber nie zurückgemeldet wurde

Nichts Größeres über die oben schon behandelten Punkte hinaus. Zwei kleine Dinge, die beim
Durchsuchen aufgefallen sind:
- Der GitHub-Tools-Repo-Rückstand (siehe Punkt 9) – kein Bug, aber eine offene Kleinigkeit.
- Der bereits erwähnte, laufende reguläre Marky-Content-Stream (viele automatisch veröffentlichte
  Posts seit Ende Juni) läuft offenbar unabhängig weiter – falls dir das bereits bekannt ist,
  ignorier diesen Punkt, falls nicht, lohnt sich ein Blick ins Marky-Dashboard zur Kontrolle.
