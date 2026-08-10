# Block 6 – Schnellere Indexierung nach Veröffentlichung
**Stand: 4. August 2026**

## Ergebnis: bereits vorhanden und aktiv – kein neuer Code nötig

RankMath PRO 3.0.118 hat ein eigenes "Instant Indexing"-Modul (IndexNow-Protokoll) fest eingebaut,
über die REST-Routen `rankmath/v1/in/submitUrls`, `getLog`, `resetKey`. Das Modul ist bei uns
**bereits aktiv** und meldet seit Wochen automatisch jede Veröffentlichung/Aktualisierung.

## Beweis: bestehendes Log (vor dem Test)

Das Log (`getLog`) zeigt echte, akzeptierte Meldungen (Status 200) genau zu den Zeitpunkten,
als der Rücken-Cluster veröffentlicht wurde, z.B.:

| URL | Zeitpunkt |
|---|---|
| ruecken-uebungen | 2026-07-29 18:24 |
| bandscheibenvorfall-lws-syndrom | 2026-07-29 18:24 |
| ischias-ischiasnerv | 2026-07-29 18:24 |
| rueckenschmerzen | 2026-07-29 18:24 |

Das heißt: schon bei der Rücken-Cluster-Veröffentlichung ist die IndexNow-Meldung automatisch raus.

## Frischer Live-Test (gerade eben, zur Bestätigung)

Manuell `submitUrls` für `ischias-ischiasnerv/` aufgerufen:
- Antwort: `success: true, "1 URL erfolgreich übermittelt."`
- Im Log sofort danach sichtbar: Status 200, "OK", Zeitstempel "vor 10 Sekunden"

Damit ist bestätigt: die Meldung kommt tatsächlich an und wird akzeptiert.

## Zum klassischen Google-Sitemap-Ping (dein Punkt 2, erster Teil)

Ehrlich gesagt: Google hat den klassischen Sitemap-Ping-Endpunkt (`google.com/ping?sitemap=...`)
im Juni 2023 abgeschaltet – der würde heute nichts mehr bewirken, ich baue daher bewusst nichts
dafür. Der moderne Ersatz für Google ist die Sitemap-Einreichung über Search Console, die bei uns
bereits läuft (GSC-Anbindung aktiv). IndexNow selbst wird zuverlässig von Bing/Yandex/Seznam
konsumiert; ob Google es inzwischen auch nutzt, ist offiziell nicht bestätigt – aber das deckt
RankMath mit demselben Aufruf ohnehin ab, es kostet nichts extra.

## Fazit

Nichts zu bauen, nichts an wp_publish.py zu ändern. Instant Indexing läuft bereits automatisch
bei jeder Veröffentlichung/Aktualisierung über RankMath. Block 6 ist damit erledigt – ohne
zusätzliches Risiko, weil kein neuer Code in die Publish-Pipeline eingebaut wurde.
