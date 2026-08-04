# Block 5 – Link-Selbstheilung: Dry-Run-Ergebnis
**Stand: 4. August 2026**

## Live-Crawl (aktueller Zustand der Seite)

- **72** eindeutige interne Links im Content aller Posts/Seiten/CPTs gefunden und live geprüft (echter HTTP-Check, nicht nur Ahrefs-Cache)
- **0 kaputte Links** (404) aktuell auf der Seite
- **0 Redirect-Ketten** (2+ Hops) aktuell auf der Seite
- Alle 72 Links direkt erreichbar bzw. maximal 1 Hop (z.B. http→https+www, ganz normal, kein Handlungsbedarf)

**Kurz gesagt: die Seite ist aktuell sauber, es gibt gerade nichts zu reparieren.**

## Warum ich trotzdem sicher bin, dass die Logik funktioniert

Da es aktuell keine echten kaputten Links gibt, um die Automatik am lebenden Objekt zu zeigen, habe ich die drei Kernfälle mit gezielten Test-Links geprüft (nur Lesezugriffe, nichts am Content verändert):

| Test | Eingabe | Ergebnis |
|---|---|---|
| Eindeutig korrigierbar | `ischias-ischiasnerv-kaputt-test/` (erfundener Slug-Tippfehler) | Als 404 erkannt, korrekt und eindeutig zurückgeführt auf `ischias-ischiasnerv/` (Score 0.76) |
| Normaler Redirect (kein Handlungsbedarf) | http-Version eines echten Links | Korrekt als 1 Hop erkannt, NICHT als "Kette" gemeldet |
| Mehrdeutig (Sicherheitsnetz) | `ruecken-info/` (bewusst vage, zwischen mehreren Rücken-Artikeln) | Korrekt als "nicht eindeutig" (Score 0.64) eingestuft → würde als "manuell prüfen" gemeldet, NICHT geraten |

Das bestätigt: die Automatik korrigiert nur, wenn ein Kandidat klar und mit Abstand vor allen anderen liegt – bei Unsicherheit wird nichts geraten, sondern zur manuellen Prüfung gelistet (genau wie gefordert).

## Was als Nächstes ansteht (auf deine Freigabe)

Da aktuell nichts zu reparieren ist, gibt es auch nichts "live zu schalten" – aber ich würde das Skript trotzdem in den Montags-Cron aufnehmen, damit es **zukünftig** neu entstehende kaputte Links (z.B. wenn du mal einen Slug änderst) automatisch erkennt und eindeutige Fälle sofort korrigiert, ohne dass wir es manuell antriggern müssen.

**Sicherheitsnetz wie bei Block 3:** Vor jeder Content-Änderung wird der Original-Content automatisch nach `/root/praxis-seo/backup/content/` gesichert (analog zu den Bild-Backups).

**Offener Punkt zu Redirect-Ketten:** Falls künftig eine echte Kette über eine RankMath-Redirection-Regel entsteht (nicht nur ein veralteter Link in unserem eigenen Content), fasse ich RankMath's Redirect-Manager selbst nicht automatisch an – aus denselben Gründen wie beim Schema-Problem in Block 1 (unzuverlässige/undokumentierte RankMath-API). Ich korrigiere nur unseren eigenen Link direkt aufs Endziel und melde die Kette zusätzlich im Report, falls du die Redirect-Regel selbst noch bereinigen willst.

## Frage an dich

Soll ich:
1. Das Skript so wie getestet in den Montags-Cron aufnehmen (nach Alt-Texten, vor dem Audit-Report) und den Wochenreport um den Abschnitt "Link-Selbstheilung" erweitern? oder
2. Noch warten, bis es mal einen echten Fall gibt, um es dir live zu zeigen?
