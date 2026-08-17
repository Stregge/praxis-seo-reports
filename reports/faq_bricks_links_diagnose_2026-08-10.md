# FAQ-Links in Bricks-Seiten (Kontakt/Ablauf/Über mich): Diagnose
**Stand: 10. August 2026**

## Ergebnis: nicht sicher automatisierbar mit aktuellem Zugriff

Kein Link wurde eingefügt – bewusst, aus Sicherheitsgründen. Details unten.

## Strukturprüfung (Schritt 1 des Auftrags)

Geprüft für alle drei Seiten (`kontakt`, `ablauf`, `ueber-mich`):

| Prüfung | Ergebnis |
|---|---|
| Standard-Content-Feld (`post_content`) | leer (0 Zeichen) – Bricks rendert komplett am WP-Content vorbei |
| `_bricks_page_content_2` über `meta`-Objekt (REST) sichtbar? | Nein – Meta-Objekt enthält nur `_joinchat`, `footnotes` |
| Eigener Bricks-REST-Endpunkt für Content lesen/schreiben? | Nein – `bricks/v1/*` und `bricksforge/v1/*` bieten nur Editor-Hilfsfunktionen (Templates, Formulare, Query-Builder, Rendering-Vorschau), keinen generischen Content-CRUD-Endpunkt |
| WP-CLI / SSH / DB-Zugang auf diesem Server hinterlegt? | Nein |

**Grundursache:** WordPress schützt Meta-Felder mit führendem Unterstrich (`_bricks_...`)
automatisch vor dem REST-API-Zugriff, sofern das Plugin sie nicht explizit freigibt. Das hat
Bricks hier nicht getan – das ist kein Bricks-Bug, sondern WordPress-Kernverhalten.

## Warum ich keinen Testversuch gemacht habe

Bei Gutenberg-Content (wie den FAQ-Seiten) ist ein fehlgeschlagener Schreibversuch harmlos –
entweder er greift, oder er tut schlicht nichts. Bei Bricks steckt hinter dem Feld eine
serialisierte PHP-Datenstruktur, die das komplette visuelle Layout der Seite beschreibt. Ein
unvollständiger oder falsch strukturierter Schreibversuch riskiert nicht "nichts passiert",
sondern eine kaputte Seite (leere/fehlerhafte Darstellung) auf einer der wichtigsten
Praxis-Seiten. Dieses Risiko steht in keinem Verhältnis zum Nutzen von 11 zusätzlichen
Backlinks, deshalb wurde bewusst nichts ausprobiert – auch kein "kleiner, harmloser" Test.

## Was stattdessen möglich ist

1. **Copy-Paste-Liste** (bereits geliefert, siehe `faq_verlinkung_ergebnis_2026-08-05.md`) –
   einzige sichere Option ohne zusätzlichen Zugang.
2. **WP-CLI per SSH**, falls der Hoster das erlaubt – damit ließe sich der Bricks-Post-Meta-Wert
   kontrolliert über `wp post meta get/update` auslesen und zurückschreiben (mit Backup vorher).
   Das bräuchte SSH-Zugangsdaten zum WordPress-Hosting, die aktuell nicht hinterlegt sind.
3. Ohne (2) sehe ich keinen Weg, der das Risiko einer kaputten Seite ausschließt.

## Vorher/Nachher

Kein Vorher/Nachher – es wurde nichts verändert. Die 32 automatisch gesetzten FAQ-Links aus
dem vorherigen Lauf sind unverändert aktiv.
