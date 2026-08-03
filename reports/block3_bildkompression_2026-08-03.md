# Block 3 – Automatische Bild-Kompression: Ergebnis
**Stand: 3. August 2026**

## Ergebnis
19 von Ahrefs geflaggte Bilder ("Image file size too large") verarbeitet:

| Status | Anzahl |
|---|---|
| Erfolgreich als Featured Image getauscht (WebP) | 15 |
| Übersprungen (SVG, Vektorformat – Konvertierung nicht sinnvoll) | 1 |
| Nicht automatisch zuordenbar (siehe unten) | 3 |

**Gesamteinsparung: ca. 24,37 MB** (Originale zu WebP, Qualität 82). Typische Einsparung 85–98%, ohne sichtbaren Qualitätsverlust (2 Beispiele vorab visuell geprüft und dir gezeigt).

Alle 19 Originale liegen unverändert gesichert unter `/root/praxis-seo/backup/images/`.

## Erfolgreich getauscht (15)
| Datei | Vorher | Nachher | Ersparnis | Seite |
|---|---|---|---|---|
| faszium_konzept.png | 1353 KB | 25 KB | -98,2% | faszium-konzept |
| ruecken_uebungen.png | 1501 KB | 44 KB | -97,1% | ruecken-uebungen |
| bandscheibe.png | 1475 KB | 48 KB | -96,7% | bandscheibenvorfall-lws-syndrom |
| ruecken_pillar.png | 1659 KB | 63 KB | -96,2% | rueckenschmerzen |
| faszien_muenchen_ost.png | 1615 KB | 70 KB | -95,7% | faszientherapie-muenchen-ost |
| faszien_homoeopathie.png | 2424 KB | 376 KB | -84,5% | homoeopathie-muskel-gelenkbeschwerden |
| faszien_nacken.png | 1507 KB | 44 KB | -97,1% | faszien-nacken |
| wasserfasten.jpg | 1026 KB | 114 KB | -88,9% | wasserfasten-mit-st-leonhardsquellen |
| faszientraining.png | 1452 KB | 36 KB | -97,5% | faszientraining-uebungen |
| natuerlicher-sonnenschutz.png | 1428 KB | 70 KB | -95,1% | natuerlicher-sonnenschutz-ohne-chemie |
| faszien_ratgeber.png | 1768 KB | 113 KB | -93,6% | faszien-ratgeber |
| ischias.png | 1351 KB | 43 KB | -96,9% | ischias-ischiasnerv |
| faszien_ablauf.png | 1584 KB | 54 KB | -96,6% | faszientherapie |
| triggerpunkte.png | 1432 KB | 28 KB | -98,0% | triggerpunkte-loesen |
| ganzheitliche-behandlung-bei-rueckenschmerzen-1.png | 1451 KB | 110 KB | -92,4% | behandlung-bei-rueckenschmerzen |

## Übersprungen (1)
- `ueberblick-hormone.svg` – Vektorformat, WebP-Konvertierung nicht sinnvoll. Falls das trotzdem "zu groß" ist, bräuchte es eine SVG-Minifizierung (anderes Werkzeug) statt Bildkompression.

## Nicht automatisch zuordenbar (3) – gleiche Ursache
- `arthrose-uebungen-zuhause-1024x572.png`
- `stoffwechsel-verstehen-und-optimieren-1-1024x683.png`
- `meine-gefaesse-sind-verkalkt-1024x1024.png`

Alle 3 sind bereits komprimiert und lokal gesichert (88–94% Ersparnis berechnet), aber **nicht live getauscht**. Grund: Die "-1024x572"-Endung ist eine von WordPress automatisch erzeugte Bildgrößen-Variante – die eigentliche Mediathek-Datei heißt vermutlich nur "arthrose-uebungen-zuhause.png" (ohne Maßangabe), und diese 3 Bilder werden nicht als Featured Image, sondern **inline im Artikeltext** eingebunden. Das deckt sich mit dem, was wir vorhin besprochen hatten (Inline-Bild-Ersetzung ist noch nicht gebaut).

## Was noch offen ist
1. **Inline-Bild-Ersetzung** für die 3 obigen Fälle (und generell für künftige Wochenreports) – müsste den Bild-Link direkt im Artikel-Content finden und ersetzen, nicht nur `featured_media`.
2. **Cron-Integration:** Das Skript (`image_optimize.py`) läuft aktuell nur manuell. Soll ich es in den bestehenden Montags-Cron aufnehmen?
3. **Wochenreport-Dokumentation:** `ahrefs_audit_report` müsste künftig automatisch mitmelden, wie viele Bilder optimiert und wie viel gespart wurde – noch nicht verdrahtet.
