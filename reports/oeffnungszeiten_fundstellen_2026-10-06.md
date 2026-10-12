# Öffnungszeiten – Fundstellen (Schritt 1, nur gelesen)
_Stand: 06.10.2026 · nichts geändert_

Soll (laut Google-Unternehmensprofil, von Roland bestätigt):
Mo 08:00–12:00 und 13:00–19:30 · Di 07:30–12:15 · Mi 07:30–12:00 und 13:00–17:30 · Do 07:30–12:15 · Fr 07:30–12:00 und 13:00–17:30 · Sa/So geschlossen

## Fundstellen, die geändert werden müssen

| # | Ort | Wirkt auf | Aktueller Wortlaut |
|---|---|---|---|
| 1 | RankMath Local SEO, Option `rank-math-options-titles` → `opening_hours` | JSON-LD `openingHours` auf **allen** Seiten (Home, Kontakt, Impressum, Über mich, Ablauf, Datenschutz … geprüft) | Monday 08:30-19:00 · Tuesday 08:30-13:00 · Wednesday 12:30-18:00 · Thursday 08:30-13:00 · Friday 08:30-17:30 → live: `["Mo 08:30-19:00","Tu,Th 08:30-13:00","We 12:30-18:00","Fr 08:30-17:30"]` |
| 2 | WPCodeBox-Snippet **#12** „Schema-Markup – BlogPosting + MedicalWebPage (Arthrose)“, aktiv, Zeilen 43–49, Block `MedicalBusiness` (nur Startseite) | JSON-LD `openingHoursSpecification` auf der Startseite | Monday 08:30–19:00 · Tuesday 08:30–13:00 · Wednesday 12:30–18:00 · Thursday 08:30–13:00 · Friday 08:30–17:30 |
| 3 | Kontakt-Seite (Post 111), Bricks `_bricks_page_content_2`, Element #23 `iguraf` (Text) unter der Überschrift „Öffnungszeiten:“ | Sichtbarer Text auf /kontakt/ | `Montag 08:30–19:00` · `Dienstag 08:30–16:00` · `Mittwoch 12:30–18:00` · `Donnerstag 08:30–13:00` · `Freitag 08:30–17:30` · `Samstag & Sonntag geschlossen` (Wochentage jeweils in `<span class="wochentag">`) |

**Abweichung zum Auftrag:** Auf der Kontakt-Seite steht beim **Dienstag 08:30–16:00**, nicht 08:30–13:00. Der Stand vom 16.09. war dort offenbar nicht vollständig angekommen (letzte Änderung an Post 111: 28.05.2026). Die Zeile wird durch die neuen Zeiten ohnehin ersetzt.

## Fundstellen, die anders formulieren oder nicht aktiv sind (melden, nicht anfassen)

| # | Ort | Wortlaut / Befund |
|---|---|---|
| 4 | FAQ (Post 479) „Vergeben Sie auch Termine am Wochenende oder spät abends?“ | „Montags ist die Praxis länger geöffnet, sodass hier auch arbeitende Menschen mit Regelarbeitszeit die Möglichkeit haben, die Praxis zu besuchen.“ – keine Uhrzeiten; stimmt auch mit den neuen Zeiten (Mo bis 19:30). |
| 5 | Kontakt-Seite, Element #6 `pheyje` | „… Während der Öffnungszeiten stehe ich Ihnen auch unter den folgenden Kontaktdaten zur Verfügung.“ – keine Uhrzeiten. |
| 6 | WPCodeBox-Snippet **#20** „Rank Math Lokales SEO – Geschäftsart + Öffnungszeiten + E-Mail“, **inaktiv** | Alte Zeiten hartcodiert (u. a. Di 08:30-16:00). Nicht aktiv, wirkt nicht. Achtung: Wird es je aktiviert, überschreibt es die RankMath-Zeiten mit alten Werten. |
| 7 | Option `seopress_pro_option_name` (SEOPress, Plugin **nicht aktiv**) | Enthält bereits Zeiten im neuen Muster (Mo 08:00–12:00/13:00–19:30, Di/… 07:30 …). Altlast, wirkt nicht. |
| 8 | Meta-Box-Einstellungsseite „kundendaten“ (Feldgruppe Post 117) | Ein Feld „Öffnungszeiten“ (`offnungszeiten`) ist definiert, aber **leer** (kein Wert in der Option `kundendaten`). Wird nirgends sichtbar ausgegeben. |

## Ohne Treffer
Startseite (sichtbarer Text), Footer- und Header-Template (Bricks 31/33), Impressum, Über mich, Ablauf, Datenschutz, alle übrigen Beiträge, Seiten und CPTs (Volltextsuche in `post_content` und allen Postmeta inkl. `_bricks_page_content_2`, ohne Revisionen).

## Technischer Stolperstein: WP-CLI ist nicht verfügbar
Im chrooted SSH-Zugang (hosting122431) gibt es nur PHP 7.2 (`php`) und PHP 7.4 (`php.os`) ohne Phar- und ohne mysqli-Erweiterung. `/tmp/wp-cli.phar` startet deshalb nicht (`Class 'Phar' not found`), und WordPress 7.0.6 lässt sich per CLI nicht laden. Die Schreibwege „WP-CLI mit Rundweg-Test“ für Bricks **und** für die RankMath-Option sind damit gerade nicht nutzbar.
