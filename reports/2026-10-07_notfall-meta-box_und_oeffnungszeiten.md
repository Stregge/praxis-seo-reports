# 07.10.2026 – Notfall Website-Ausfall (Meta Box) + Öffnungszeiten + Gruppe-B-Bilder

## 1. Notfall: HTTP 500 auf allen Seiten (ca. 10:52–10:55)

**Symptom:** Startseite, /kontakt/, /wp-login.php und /wp-admin/ lieferten 500 („Es ist ein kritischer Fehler aufgetreten“).

**Fehlermeldung (error_log, Wortlaut):**
```
PHP Fatal error:  Uncaught Error: Class "RWMB_Block_Bindings_Registry" not found in
.../wp-content/plugins/meta-box/inc/functions.php:292
#0 .../plugins/meta-box-aio/vendor/meta-box/mb-settings-page/mb-settings-page.php(62): rwmb_get_registry()
#1 .../wp-includes/class-wp-hook.php(341): mb_settings_page_load()
```
- Erster Fatal: 10:52:09. Letzter: 10:54:52.

**Ursache:** Versionskonflikt nach dem Update von **Meta Box AIO auf 3.12.0** (10:52).
- AIO bringt den Meta-Box-Kern 5.15.1 mit, der eine „Block Bindings“-Registry kennt.
- Zusätzlich war das separate Plugin **Meta Box 5.12.0** (Stand 29.05.2026) aktiv. Es lädt zuerst seinen älteren Kern, der diese Registry nicht kennt; das neue `mb-settings-page` ruft sie trotzdem auf.

**Weitere Updates im selben Zeitfenster:** fluentformpro 10:39, creame-whatsapp-me 10:40, wp-rocket 10:48, database-cleaner 10:49 und meta-box-aio 10:52. Rank Math war schon um 02:33 aktualisiert worden. WordPress-Core steht auf 7.0.7, Bricks auf 2.4.2. Bricksforge ist nicht installiert (kein Plugin-Ordner); das vermutete Update 3.1.8.5 → 4.0.0 trifft auf diese Installation also nicht zu.

**Behebung (kleinster Eingriff):**
- Ordner `wp-content/plugins/meta-box` umbenannt in `meta-box_off` (nicht gelöscht). Zustand vorher: Ordner `meta-box` aktiv, Version 5.12.0, Dateien vom 29.05.2026.
- AIO bleibt aktiv und nutzt jetzt seinen eigenen Kern 5.15.1.
- Kein Datenbank-Restore, kein UpdraftPlus. Rolands Bricks-Änderung (Öffnungszeiten auf /kontakt/) ist erhalten.

**Ergebnis:**
- Startseite, /kontakt/, /impressum/, /ratgeber/, /faszien-ratgeber/ und /therapie/spagyrik/ liefern 200; /wp-login.php liefert 200; /wp-admin/ liefert 302 (Login-Weiterleitung, normal).
- Logo (Header und Footer), Telefon, E-Mail und Adresse sind da; sie kommen aus der Meta-Box-Einstellungsseite „kundendaten“. Header, Footer und Bricks-Elemente sind vorhanden, keine PHP-Warnungen im HTML.
- Seit der Umbenennung keine neuen Fatal Errors.

**Offen / Hinweise:**
- WordPress wird das Plugin „Meta Box“ beim nächsten Aufruf der Plugin-Seite in wp-admin als „Datei nicht vorhanden“ deaktivieren. Das ist gewollt; AIO ersetzt es. Den Ordner `meta-box_off` später löschen, wenn alles stabil bleibt.
- Im Log taucht nach dem Update ein Datenbankfehler von Rank Math auf: `Table 'k75670_nhp.sh_rank_math_analytics_ga' doesn't exist`. Er betrifft nur das Analytics-Modul, nicht das Frontend. Prüfen, ob Rank Math → Analytics neu verbunden werden muss.
- Die genaue PHP-Version der Domain ist im chrooted SSH nicht auslesbar. Laut Fehlerformat läuft PHP 8.x.
- Backup der Plugin-Liste: `/root/praxis-seo/backups/active_plugins_20261007-105435.sql`

## 2. Öffnungszeiten

Roland hat den sichtbaren Text auf /kontakt/ im Bricks-Editor selbst geändert. Technisch angepasst habe ich drei Stellen:

| Stelle | Vorher | Nachher |
|---|---|---|
| RankMath `opening_hours` (JSON-LD `openingHours`, alle Seiten) | Mo 08:30-19:00 · Tu,Th 08:30-13:00 · We 12:30-18:00 · Fr 08:30-17:30 | Mo 08:00-12:00 · Mo 13:00-19:30 · Tu,Th 07:30-12:15 · We,Fr 07:30-12:00 · We,Fr 13:00-17:30 |
| Snippet #12 `openingHoursSpecification` (Startseite) | 5 Einträge, alte Zeiten | 8 Einträge: Mo 08:00–12:00, Mo 13:00–19:30, Di 07:30–12:15, Mi 07:30–12:00, Mi 13:00–17:30, Do 07:30–12:15, Fr 07:30–12:00, Fr 13:00–17:30 |
| Snippet #20 (bleibt **inaktiv**) | 5 Einträge, alte Zeiten (u. a. Di 08:30-16:00) | dieselben 8 Einträge |
| /kontakt/ sichtbarer Text (durch Roland) | Mo 08:30–19:00 · Di 08:30–16:00 · Mi 12:30–18:00 · Do 08:30–13:00 · Fr 08:30–17:30 | Montag 08:00–12:00 und 13:00–19:30 · Dienstag 07:30–12:15 · Mittwoch 07:30–12:00 und 13:00–17:30 · Donnerstag 07:30–12:15 · Freitag 07:30–12:00 und 13:00–17:30 · Samstag & Sonntag geschlossen |

**Vorgehen:**
- RankMath: Rundweg-Test bestanden (serialize(unserialize) byte-gleich); nur `opening_hours` geändert, die übrigen 319 Schlüssel bleiben gleich. Zurückgelesen: identisch mit dem vorbereiteten Wert.
- Snippets: Nur die Zeitzeilen ersetzt (bei #20 auch der Kommentar „5“ → „8 Einträge“); PHP-Syntaxcheck ok; zurückgelesen: identisch.
- Bei Snippet #12 war `original_code` eine ältere Fassung, ohne den FAQ-Block „Leaky Gut Test“ und mit Dienstag 16:00. Ich habe beide Felder auf den aktuell ausgeführten Code mit neuen Zeiten gesetzt, damit ein späteres Speichern im WPCodeBox-Editor nichts zurückdreht. Die alte Fassung ist gesichert.

**Ablauf mit Ausfall:**
- Die Änderungen fielen zeitlich mit dem Ausfall zusammen. Ich habe sie deshalb vorsorglich zurückgerollt; das brachte keine Besserung, weil Meta Box die Ursache war.
- Nach der Behebung habe ich sie mit neuem Rundweg-Test gegen den aktuellen Stand wieder eingespielt.

**Live (nach WP-Rocket-Cache-Leerung):**
- Startseite: `openingHours` und `openingHoursSpecification` stimmen überein.
- /kontakt/ und /impressum/: `openingHours` neu.
- /kontakt/ sichtbarer Text: neu (siehe Tabelle).

**Backups:**
- `/root/praxis-seo/backups/rankmath-options-titles_20261007-103915.sql` und `.serialized`
- `/root/praxis-seo/backups/wpcb_snippets_12_20_20261007-103915.sql`
- `/root/praxis-seo/backups/wpcb_snippet12_20261007-103915.php`
- `/root/praxis-seo/backups/wpcb_snippet12_original_code_20261007-103915.php`
- `/root/praxis-seo/backups/wpcb_snippet20_20261007-103915.php`

Die DB-Zugangsdatei und alle Temp-Dateien auf dem Hosting sind entfernt.

Nicht angefasst: Bricks-Felder, SEOPress-Rest, FAQ 479, Terminlinks und Lapsula-Widget.

## 3. Gruppe-B-Bilder (Runde 3)

- Alle 7 sind gesetzt (Media 33910–33918) und per REST verifiziert. Die Alt-Texte stimmen; Inhalt, Titel und Meta der Beiträge sind unverändert. Auf /ratgeber/ zeigen 7 von 7 Kacheln das neue Bild.
- `og:image` ist bei 5 von 7 Beiträgen neu.
- **Ausnahme:** Bei **20423** /behandlung-bei-rueckenschmerzen/ und **10649** /ganzheitliche-arthrose-therapie/ ist in RankMath ein eigenes Facebook-Bild hinterlegt (alte Bilder `ganzheitliche-behandlung-bei-rueckenschmerzen-1.png` und `arthrose1-1.jpg`). Es überschreibt das Titelbild in `og:image`. Nicht geändert; Freigabe nötig.
- Protokoll: `/root/praxis-seo/backups/ratgeber-runde3_gesetzt_2026-10-07.json`
