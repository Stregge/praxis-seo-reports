# Ahrefs-Automation – Abschlussbericht
**Naturheilpraxis Strähuber | Stand: 25. Juli 2026**

Zusammenfassung der gesamten Session: Plan, Umsetzung, Tests, gefundene Probleme, Cron-Einrichtung.

---

## Was gebaut wurde

`ahrefs_tool.py` wurde um 5 neue Befehle erweitert (Site-Audit-Projekt 9546763, Health Score 87/100, 380 Seiten):

| Befehl | Zweck | Ergebnis beim Testlauf |
|---|---|---|
| `audit_report` | Wöchentlicher Health-Score- und Problem-Report, mit Verlaufsvergleich zum letzten Lauf | 16 aktive Probleme (33 Orphan-Seiten, 15 zu große Bilder, 64 Rich-Results-Fehler u.a.) |
| `orphan_watch` | Seiten ohne eingehende interne Links, inkl. automatischem Verlinkungsvorschlag | 33 betroffene Seiten |
| `schema_check` | Google-Rich-Results- und schema.org-Validierungsfehler, gruppiert | 67 betroffene Seiten (64 + 3) |
| `performance_report` | Core Web Vitals + zu große Bilder | 15 Bilder-Seiten; Lighthouse-Teil aktuell leer (siehe unten) |
| `ai_visibility` | Sichtbarkeit in ChatGPT/Perplexity/Gemini/Google AI/Copilot/Grok + Crawler-Blocker-Check | alle 7 Plattformen aktuell 0; keine echte Crawler-Blockade |

Ausführung: einzeln oder gesammelt über `python3 ahrefs_tool.py --alle`. Jeder Lauf speichert eine datierte Markdown-Datei in `/root/praxis-seo/output/` und pusht automatisch über `push_reports.sh` ins öffentliche Reports-Repo.

## Alle Ahrefs-API-Endpunkte wurden per Testaufruf verifiziert, nicht geraten
Die tatsächlichen Pfade weichen von der ursprünglichen Annahme ab (Schrägstrich statt Bindestrich): `site-audit/projects`, `site-audit/issues`, `site-audit/page-explorer`, `site-explorer/ai-responses-count`. Alle verwendeten Felder und Issue-IDs wurden gegen die echte API geprüft und lieferten exakt die von dir genannten Zahlen zurück (87 Health Score, 380 Seiten, 33 Orphan-Seiten, 15 Bilder-Seiten, 64+3 Schema-Fehler).

## Zwei Bugs beim Testen gefunden und sofort gefixt
1. Das `title`-Feld kommt von Ahrefs als Liste zurück, nicht als Text – hätte den Verlinkungsvorschlag im Orphan-Report zum Absturz gebracht.
2. Der KI-Crawler-Blocker-Check hätte fälschlich "3 blockierte Seiten" gemeldet – das waren aber nur die robots.txt-Datei selbst (in 3 URL-Varianten: www/non-www/http), keine echten Inhaltsseiten. Rausgefiltert, jetzt korrekt "0 echte Blocker".

## Eine offene Einschränkung – braucht deine Aktion in Ahrefs selbst
Der Core-Web-Vitals-Teil von `performance_report` liefert aktuell keine Lighthouse-Daten. Grund: Ahrefs hat für dieses Projekt PageSpeed-Insights-Checks noch nie angefragt (`psi_request_status: "Gapi_psi_user_not_asked"`) – das ist eine Ahrefs-Projekteinstellung, keine Fehlfunktion des Codes. Müsste einmalig in den Ahrefs-Site-Audit-Projekteinstellungen (Crawl-Einstellungen) aktiviert werden, danach füllt sich der Bericht beim nächsten Lauf automatisch. Der Bilder-Teil (15 Seiten) funktioniert schon jetzt unabhängig davon.

Kleinere Einschränkung bei `schema_check`: Ahrefs liefert über die API nur, welche Seiten betroffen sind und welche Schema-Typen sie nutzen – nicht die genaue Fehlermeldung selbst (`jsonld_validation_kinds` kam bei allen getesteten Seiten leer zurück, auch bei bestätigt betroffenen Seiten). Für die exakte Fehlermeldung je Seite bräuchte man das Ahrefs-Dashboard oder Googles Rich-Results-Test direkt.

## Cron-Einrichtung
Eingerichtet und verifiziert (`crontab -l`):

```
# Woechentlich Montags 06:00 - Site-Audit-Report, Orphan-Watch, Schema-Check, Performance-Report
0 6 * * 1  cd /root/praxis-seo && python3 ahrefs_tool.py audit_report
5 6 * * 1  cd /root/praxis-seo && python3 ahrefs_tool.py orphan_watch
10 6 * * 1 cd /root/praxis-seo && python3 ahrefs_tool.py schema_check
15 6 * * 1 cd /root/praxis-seo && python3 ahrefs_tool.py performance_report

# Monatlich am 1. um 06:30 - KI-Sichtbarkeits-Monitor
30 6 1 * * cd /root/praxis-seo && python3 ahrefs_tool.py ai_visibility
```

Logs laufen in `/root/praxis-seo/output/cron_ahrefs.log`. Jeder Lauf pusht automatisch neue Reports ins Reports-Repo – du bekommst also laufend aktuelle Berichte, ohne dass jemand manuell etwas anstoßen muss.

## Verlaufs-/Historien-Speicher
Für `audit_report` und `ai_visibility` wird jeweils der letzte Stand lokal unter `/root/praxis-seo/output/_history/` gespeichert (nicht öffentlich im Reports-Repo), damit künftige Läufe zeigen können, was sich seit dem letzten Mal verändert hat. Erster Lauf zeigt dazu logischerweise "kein Vorlauf zum Vergleich" – ab dem zweiten Lauf (nächsten Montag) gibt es echte Vergleichswerte.

---

**Nächster sinnvoller Schritt (nicht Teil dieser Session):** PageSpeed-Insights-Checks im Ahrefs-Projekt aktivieren, damit `performance_report` vollständig wird.
