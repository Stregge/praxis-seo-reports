# Zwei Fixes aus der Diagnose vom 22.08. – Ergebnis
**Stand: 22. August 2026**

## Fix 1: Meta-Description Startseite – erledigt, live verifiziert

- **Neuer Text (1:1 übernommen):** "Naturheilpraxis Strähuber in Dorfen bei Erding: Osteopathie,
  Faszientherapie, Dorn-Methode und Mikronährstoffanalyse. Heilpraktiker Roland Strähuber –
  persönlich, ganzheitlich, erfahren."
- Alter (abgeschnittener) Text vorher gesichert: `/root/praxis-seo/backup/content/pages_12_rank_math_description_*.txt`
- Live verifiziert nach Cache-Leerung: neue Description erscheint vollständig und korrekt im
  `<meta name="description">`-Tag der Startseite

**Technischer Zwischenfall unterwegs:** Der Standard-REST-Weg (wie sonst für Meta-Description
üblich) hat bei dieser speziellen Seite **nicht funktioniert** – ein bislang unbekannter
REST-Lese-/Schreib-Bug speziell für Page-ID 12 (die Startseite). Direkter Datenbank-Check per
WP-CLI zeigte: der abgeschnittene Text stand tatsächlich schon länger unverändert in der
Datenbank (kein Auto-Generierungs-Mechanismus, wie ich am 22.08. zunächst vermutet hatte,
sondern ein einmal so gespeicherter, nie korrigierter Wert). RankMaths eigene
"Homepage"-Sonderoption (`homepage_title`/`homepage_description`) habe ich im Plugin-Quellcode
geprüft – die kommt bei einer statischen Startseite (wie hier) laut Code gar nicht zum Einsatz,
war also nicht die Ursache. Der Fix erfolgte stattdessen zuverlässig direkt per WP-CLI
(derselbe Weg, der sich schon bei den Bricks-Seiten bewährt hat).

**Für dich zur Kenntnis:** Dieser REST-Bug bei Page 12 ist unabhängig vom eigentlichen
Meta-Description-Problem und könnte bei künftigen technischen Änderungen an der Startseite
erneut auftreten – ich werde bei Bedarf direkt den WP-CLI-Weg statt REST nutzen.

## Fix 2: Sitemap-Staleness – erledigt, live verifiziert

**Ursache gefunden (dein zweiter Verdacht lag richtig):** RankMath selbst cached seine
Sitemap-Ausgabe als statische XML-Dateien im Ordner `wp-content/uploads/rank-math/` – nicht
WP-Rocket. Alle 7 Cache-Dateien dort stammten vom 24./25. Juli; der automatische
Invalidierungs-Mechanismus (der bei jeder neuen Veröffentlichung greifen sollte) hat seither
offenbar nicht mehr funktioniert.

**Fix:** Alte Cache-Dateien vorher gesichert (`/root/praxis-seo/backup/content/rankmath_sitemap_cache_backup_*/`),
danach über den offiziellen RankMath-WP-CLI-Befehl `wp rankmath sitemap generate` sauber
neu generiert (kein rohes Löschen, sondern der vom Plugin selbst vorgesehene Weg).

**Live verifiziert:**
- `post-sitemap.xml` zeigt jetzt `lastmod: 2026-08-22` (vorher 24.07.)
- Alle 7 genannten Seiten sind jetzt drin: Mikronährstoffanalyse, Presse, Vitamin-B12-,
  Magnesium-, Zink-, Müdigkeit- und Leaky-Gut-Artikel
- Sitemap insgesamt von 60 auf 71 URLs gewachsen

**Ein Punkt nicht wie gewünscht umsetzbar:** Die aktive Neu-Einreichung bei GSC per API ist
fehlgeschlagen – `HTTP 403: insufficientPermissions`. Der hier hinterlegte Google-Service-Account
hat nur Lese-, keine Schreibrechte für die Sitemap-Submit-Funktion. Das kann ich nicht selbst
beheben (würde erweiterte OAuth-Scopes für den Service-Account in der Google Cloud Console
erfordern). Zur Einordnung: Die Sitemap ist bereits seit 30.05. bei GSC registriert und wird
mit 0 gemeldeten Fehlern regelmäßig automatisch neu abgerufen (letzter automatischer Abruf:
18.08., also schon vor dem heutigen Fix) – Google wird die aktualisierte Version beim nächsten
regulären Abruf ohnehin erfassen. Für eine *sofortige* Neuabfrage müsstest du das einmal manuell
in der GSC-Weboberfläche anstoßen (Sitemaps → bestehenden Eintrag erneut einreichen, dauert
dort etwa 30 Sekunden) – oder mir erweiterte API-Rechte einrichten, falls das öfter gebraucht
wird.

## Zusammenfassung

| Fix | Status |
|---|---|
| 1. Meta-Description Startseite | ✅ erledigt, live verifiziert |
| 2. Sitemap-Regenerierung | ✅ erledigt, live verifiziert (71 statt 60 URLs, alle 7 neuen Seiten drin) |
| 2b. Aktive GSC-Neueinreichung | ⚠️ nicht möglich (fehlende API-Rechte) – manuell nachholen oder Scopes erweitern |
