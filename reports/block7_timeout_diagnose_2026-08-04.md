# Block 7 – Diagnose der 3 Timeout-Funde vom 29.07.
**Stand: 4. August 2026**

## 1. Welche URLs

| URL | curl_code | http_code | Ladezeit (Ahrefs-Crawl) |
|---|---|---|---|
| `/therapie/faszientherapie/` | 28 (Timeout) | 0 | 5002 ms |
| `/lexikon/ischias/` | 28 (Timeout) | 0 | 5000 ms |
| `/lexikon/stille-entzundungen/` | 28 (Timeout) | 0 | 5001 ms |

Alle drei: `time_to_first_byte: 0` – der Server hat also gar nicht erst geantwortet (kein
"langsam geladen", sondern "keine Antwort innerhalb von Ahrefs' 5-Sekunden-Fenster").
Alle drei sind CPT-Einzelseiten (`therapie/`, `lexikon/`), über die Sitemap gefunden (depth 0).

## 2. Wichtiger Nebenfund: die Daten sind veraltet

Die Projekt-Metadaten von Ahrefs zeigen: `"date": "2026-07-29T12:30:15Z"` – das ist der
Zeitpunkt des **letzten abgeschlossenen Crawls**. Ahrefs hat das Projekt seitdem **nicht neu
gecrawlt**. Das bedeutet: unsere automatischen Wochenreports vom 03.08. und 04.08. haben beide
Male exakt dieselbe alte 29.07.-Momentaufnahme angezeigt, nicht neue Daten – die Zahlen waren
"unveraendert", weil schlicht nichts Neues gecrawlt wurde, nicht weil sich nichts geändert hätte.

Über die Ahrefs-API (Lite-Plan) lässt sich kein neuer Crawl anstoßen – das geht nur manuell im
Ahrefs-Dashboard oder über den dort eingestellten Crawl-Zeitplan.

## 3. Live-Test von hier aus (gerade eben)

Alle drei URLs direkt angefragt (20 Sekunden Timeout, echter Request von unserem Server):

| URL | Status | Ladezeit |
|---|---|---|
| `/therapie/faszientherapie/` | 200 | 0,16 s |
| `/lexikon/ischias/` | 200 | 0,03 s |
| `/lexikon/stille-entzundungen/` | 200 | 0,03 s |

Alle drei laden **aktuell blitzschnell und fehlerfrei**. Kein Hinweis auf ein bestehendes
Server-Performance-Problem.

## Einschätzung

Passt zu deiner Vermutung: höchstwahrscheinlich ein **einmaliger Crawl-Glitch am 29.07.**,
zeitlich passend zur intensiven Publishing-Aktivität an dem Tag (Rücken-Cluster-Rollout mit
vielen REST-API-Schreibvorgängen, Bildverarbeitung etc. – der Server könnte kurz überlastet
gewesen sein, genau als Ahrefs diese drei Seiten crawlen wollte).

**Aber:** Ich kann das nicht mit hundertprozentiger Sicherheit "entwarnen", weil Ahrefs seit dem
29.07. schlicht nicht neu gecrawlt hat – die "immer noch als Timeout markiert"-Meldung in unserem
Report ist also kein neuer Beweis für ein bestehendes Problem, sondern nur eine alte Meldung, die
nie aktualisiert wurde. Mein eigener Live-Test jetzt ist der einzige echte, aktuelle Beweis – und
der ist sauber.

## Empfehlung

1. Kein Handlungsbedarf am Server/an der Seite – die Seiten laufen einwandfrei.
2. Zur Sicherheit: im Ahrefs-Dashboard prüfen, wie der Crawl-Zeitplan für das Projekt eingestellt
   ist (Site Audit → Projekteinstellungen), und bei Gelegenheit einen manuellen Re-Crawl anstoßen,
   damit unser Wochenreport wieder echte aktuelle Daten zeigt statt der 29.07.-Momentaufnahme.
   Das ist unabhängig vom Timeout-Thema – aber jetzt aufgefallen, deshalb hier vermerkt.
