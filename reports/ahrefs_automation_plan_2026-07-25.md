# Plan: Ahrefs-Automation für ahrefs_tool.py
**Stand: 25. Juli 2026 – noch kein Code geschrieben, nur Plan zur Freigabe**

Alle Endpunkte unten wurden per echtem Testaufruf gegen die Ahrefs-API verifiziert (nicht geraten). Tatsächliche Pfade nutzen Schrägstriche, nicht Bindestriche wie im Ausgangs-Prompt vermutet.

---

## 1. `gsc_audit_report` – Wöchentlicher Site-Audit-Report
- **Endpunkte:** `site-audit/projects` (Health Score, Fehler/Warnungen/Hinweise-Zahlen) + `site-audit/issues` (Problemliste, jedes Issue mit `change`, `added`, `new`, `removed`, `missing`)
- Bestätigt: Projekt 9546763, Health Score 87, 380 Seiten, 51 Fehler / 108 Warnungen / 78 Hinweise
- Report zeigt: Health-Score-Verlauf (Vergleich zum letzten gespeicherten Lauf, den ich lokal in einer JSON-Verlaufsdatei ablege, zusätzlich zu Ahrefs' eigenen `change`/`added`/`removed`-Feldern), Top-Probleme nach Wichtigkeit sortiert
- Nur Issues mit `crawled > 0` auflisten (von 100 Issue-Typen sind die meisten mit 0 betroffenen Seiten – die will keiner sehen)
- Geschätzte Kosten: ~50 Units/Lauf (deine Angabe, unverändert)

## 2. `ahrefs_orphan_watch` – Orphan-Page-Wächter
- **Endpunkt:** `site-audit/page-explorer?project_id=9546763&issue_id=c64d7e96-d0f4-11e7-8ed1-001e67ed4656`
- Bestätigt: exakt 33 Seiten betroffen (Testabfrage lief bereits)
- Felder: `url`, `title`, `content_nr_word` (Wortzahl – exakter Feldname, nicht "word_count"), `traffic`
- **Verlinkungsvorschlag:** Ahrefs liefert dafür kein Feld – das baue ich als eigene Heuristik: einfacher Titel-/Themen-Abgleich der Waisen-Seite gegen die Top-Ranking-Seiten der Website (über den bereits vorhandenen `gsc_alle_seiten`-Datenbestand bzw. eine neue leichte Ahrefs- oder Titel-Wortabgleich-Logik), plus als Fallback immer der Hinweis "von der jeweiligen Themen-Übersichtsseite (z.B. /faq/) verlinken". Das ist ein Vorschlag, keine Garantie für thematische Passgenauigkeit – klar so gekennzeichnet im Report.

## 3. `ahrefs_schema_check` – Schema-Validierungs-Check
- **Endpunkt:** `site-audit/page-explorer` mit `select=url,jsonld_schema_types,jsonld_validation_kinds`
- Beide Felder bestätigt vorhanden
- Report gruppiert nach Fehlerart (`jsonld_validation_kinds`), darunter die betroffenen URLs mit Schema-Typ

## 4. `ahrefs_performance_report` – Performance & Core Web Vitals
- **Endpunkt:** `site-audit/page-explorer` mit `select=url,psi_lighthouse_score,psi_crux_lcp_percentile,psi_crux_cls_percentile,psi_crux_inp_percentile,loading_time,time_to_first_byte`
- Alle 6 Felder bestätigt vorhanden
- Zusätzlich: `issue_id=c64d8113-d0f4-11e7-8ed1-001e67ed4656` ("Image file size too large") – bestätigt exakt 15 betroffene Seiten
- Damit ersetzt dieser Report ein separates PageSpeed-Tool wie besprochen

## 5. `ahrefs_ai_visibility` – KI-Sichtbarkeits-Monitor (monatlich)
- **Endpunkt:** `site-explorer/ai-responses-count?target=naturheilpraxis-straehuber.de&mode=subdomains&country=de&select=chatgpt,perplexity,gemini,google_ai_overviews,google_ai_mode,copilot,grok`
- Alle 7 Plattform-Felder bestätigt gültig (deine Liste war exakt richtig)
- Zusätzlich: `allowed_training_bots` aus `site-audit/page-explorer` – prüft, ob ChatGPT & Co. überhaupt crawlen dürfen. Falls blockiert: Ergebnis klar im Report als "Blocker Nr. 1" markieren, mit Empfehlung zur robots.txt-Anpassung (Textvorschlag, keine automatische Änderung)
- Verlauf wird in einer lokalen JSON-Historie festgehalten (Monat für Monat), damit der Report zeigt, seit wann sich was ändert
- Geschätzte Kosten: ~105 Units/Lauf (deine Angabe, unverändert)

---

## Ausführung
- Jede Funktion einzeln aufrufbar: `python3 ahrefs_tool.py audit_report` / `orphan_watch` / `schema_check` / `performance_report` / `ai_visibility`
- Sammel-Lauf: `python3 ahrefs_tool.py --alle` (führt 1–5 nacheinander aus)
- Jeder Report: eigene Markdown-Datei mit Datum im Namen in `/root/praxis-seo/output/`, danach automatischer Aufruf von `push_reports.sh` (das bestehende Script von letzter Woche, direkt-auf-main-Push für Reports)

## Cron-Vorschlag (noch NICHT eingerichtet)
```
# Woechentlich Montags 06:00 - Punkte 1-4
0 6 * * 1  cd /root/praxis-seo && python3 ahrefs_tool.py audit_report && python3 ahrefs_tool.py orphan_watch && python3 ahrefs_tool.py schema_check && python3 ahrefs_tool.py performance_report

# Monatlich am 1. um 06:30 - Punkt 5
30 6 1 * *  cd /root/praxis-seo && python3 ahrefs_tool.py ai_visibility
```
Geschätzter Gesamtverbrauch: ~50+X+X+X Units/Woche (Punkte 2-4 sind reine Datenabfragen ohne extra Ahrefs-Kosten laut deiner Aufstellung, nur Punkt 1 und 5 haben separate Unit-Kosten) – bei 96% freiem Kontingent unkritisch.

---

**Nichts davon ist umgesetzt.** Sag "ok", dann schreibe ich den Code in `ahrefs_tool.py`.
