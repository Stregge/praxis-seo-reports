# 07.10.2026 – og:image-Overrides, Rank Math Analytics, UpdraftPlus, Auto-Updates

## 1. og:image-Overrides (Social-Bild in Rank Math)

Geprüft wurden alle 16 Beiträge, deren Titelbild in Pilot, Runde 2 und Gruppe B geändert wurde (Meta `rank_math_facebook_image*` und `rank_math_twitter_*`).
- **Override vorhanden nur bei 20423 und 10649.** Die übrigen 14 haben keinen Override; Twitter-Overrides gibt es keine.
- Entfernt (Freigabe Roland): je `rank_math_facebook_image` und `rank_math_facebook_image_id`, insgesamt 4 Zeilen.
  - 20423: zeigte vorher auf `ganzheitliche-behandlung-bei-rueckenschmerzen-1.png` (Media 19893)
  - 10649: zeigte vorher auf `arthrose1-1.jpg` (Media 11498)
- Backup: `/root/praxis-seo/backups/og-override_20423_10649_20261007-113747.sql` (4 INSERT-Zeilen)
- Live nach Cache-Leerung: `og:image`, `og:image:alt` und `twitter:image` zeigen auf das neue Titelbild (praxisraum-liege-kraeuter-… bzw. gartenbank-handschuhe-kraeutertoepfe-…).
- Hinweis: Facebook und Co. cachen Vorschaubilder. Bereits geteilte Links zeigen das alte Bild, bis sie im Facebook-Sharing-Debugger neu eingelesen werden.

## 2. Rank Math Analytics

**Search Console liefert weiter Daten.** Die Tabelle `sh_rank_math_analytics_gsc` hat 2.610 Zeilen, die neuesten Daten sind vom 04.10.2026; die übliche GSC-Verzögerung beträgt 2–3 Tage. Die Inspections laufen (zuletzt 06.10.).

**Warum `sh_rank_math_analytics_ga` fehlt:** Rank Math Pro legt diese Tabelle nur an, wenn Google Analytics verbunden ist (`is_analytics_connected()`). In `rank_math_google_analytic_options` sind `property_id` und `view_id` leer; GA war also nie verbunden. Die Tabelle hat nie existiert, auch nicht vor dem Update.

**Was neu ist:** Seit Rank Math Pro 3.0.122 fragt eine Abfrage („Top-Seiten nach Pageviews“) die Tabelle trotzdem ab. Im Log steht der Fehler heute 3-mal (ab 10:37), in den älteren Logs nicht:
`WordPress database error Table 'k75670_nhp.sh_rank_math_analytics_ga' doesn't exist for query SELECT page, SUM(pageviews) AS pageviews FROM sh_rank_math_analytics_ga …`
Auswirkung: nur ein Log-Eintrag. Das Frontend und die GSC-Daten sind nicht betroffen. Dasselbe gilt für `sh_rank_math_analytics_adsense`.

**Vorschlag (nicht umgesetzt):**
- Option A, empfohlen: nichts tun. Der Fehler ist harmlos und verschwindet vermutlich mit einem Rank-Math-Update.
- Option B, kleinste Reparatur: die leere Tabelle exakt nach dem Schema von Rank Math Pro anlegen (`includes/modules/analytics/workflows/class-analytics.php`), mit `CREATE TABLE IF NOT EXISTS`, ohne etwas zu löschen oder zu überschreiben:
```sql
CREATE TABLE IF NOT EXISTS sh_rank_math_analytics_ga (
  id bigint(20) unsigned NOT NULL auto_increment,
  page varchar(500) NOT NULL,
  created timestamp NOT NULL,
  pageviews mediumint(6) NOT NULL,
  visitors mediumint(6) NOT NULL,
  referrer varchar(500) NOT NULL,
  PRIMARY KEY (id),
  KEY analytics_object_analytics (page(190))
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_520_ci;
```
  Die Kollation vorher an der GSC-Tabelle abgleichen. Backup: Strukturdump der Analytics-Tabellen vorher. Nebenwirkung: Rank Math hält GA danach eventuell für „teilweise eingerichtet“. Zurückdrehen per `DROP TABLE`; die Tabelle ist leer, es gehen keine Daten verloren.

## 3. UpdraftPlus

| | |
|---|---|
| Letztes **vollständiges** Backup (DB, Plugins, Themes, Uploads, Sonstiges) | **04.10.2026, 01:15** – laut Log erfolgreich („The backup succeeded and is now complete“) |
| Ziel | **Google Drive** (Remote). Lokale Reste in `wp-content/updraft`: 437 MB, u. a. eine Uploads-ZIP vom 26.09. |
| Zeitplan | **aktiv**: Dateien wöchentlich, Datenbank wöchentlich, Start 00:05. Nächster Lauf **11.10.2026, 01:05** (Dateien und DB). Zusätzlich täglich inkrementell (nächster Lauf heute 14:45). |
| Aufbewahrung | je 4 Sätze (Dateien und DB) |
| Heute | 5 Backups von DB und Plugins (10:38, 10:39, 10:44, 10:48, 10:51). UpdraftPlus legt sie automatisch vor jedem Plugin-Update an; alle laut Log erfolgreich nach Google Drive hochgeladen. Das letzte (10:51) entstand **vor** dem Meta-Box-AIO-Update. |
| E-Mail-Benachrichtigung | **keine** (keine Adresse hinterlegt) |

Den Inhalt von Google Drive habe ich nicht selbst eingesehen; die Angaben stammen aus den UpdraftPlus-Logs.

## 4. Auto-Updates (nur Bericht, nichts geändert)

- WordPress-Core: Minor-Updates **an**, Major-Updates **aus**. Themes: keine Auto-Updates eingetragen.
- Plugins mit eingeschaltetem Auto-Update (Option `auto_update_plugins`):

| Plugin | Status |
|---|---|
| Fluent Forms (fluentform) | installiert, aktiv |
| Rank Math SEO | installiert, aktiv |
| Rank Math SEO Pro | installiert, aktiv |
| UpdraftPlus | installiert, aktiv |
| Borlabs Cookie | installiert, aktiv |
| MainWP Child | installiert, **inaktiv** |
| ACF, All-in-One WP Migration (+ FTP-Extension), Code Snippets, Custom Post Type UI, Motion.page, WP Grid Builder | **nicht installiert** (Einträge von früher; ohne Wirkung) |

- **Meta Box AIO hat kein Auto-Update.** Das Update von heute kam also aus Rolands manuellem Update-Lauf.
- Wirksam sind somit 5 Plugins: Fluent Forms, Rank Math, Rank Math Pro, UpdraftPlus und Borlabs Cookie.

DB-Zugangsdatei auf dem Hosting nach jedem Schritt entfernt.
