# Sitemap-Problem: Befund weicht von der Annahme ab
**Stand: 24. Juli 2026**

## Kurzfassung
Die Annahme im Auftrag war: "alte, umbenannte URL leitet auf die neue Ziel-URL weiter – Sitemap muss auf das neue Ziel zeigen." **Das stimmt nicht.** Alle 3 URLs leiten auf die **Startseite** weiter (Status 301), nicht auf einen neuen, spezifischen Artikel. Gleichzeitig existieren zu allen 3 URLs **aktuell veröffentlichte, fertig ausgearbeitete Artikel** in WordPress – mit sauberem SEO-Titel, Meta-Description und Fokus-Keyword.

| URL | WordPress-Status | Redirect-Ziel (live getestet) | Post-ID |
|---|---|---|---|
| /hexenschuss-was-tun/ | **publish** – "Hexenschuss – was tun?" | → https://www.naturheilpraxis-straehuber.de/ (301) | 30992 |
| /arthrose-schlafen-tipps/ | **publish** – "Mit Arthrose schlafen: Warum der Körper nachts so laut wird" | → https://www.naturheilpraxis-straehuber.de/ (301) | 32358 |
| /arthrose-protokoll-heilpraktiker/ | **publish** – "Mein Arthrose-Protokoll: Fünf Schritte und eine Haltung" | → https://www.naturheilpraxis-straehuber.de/ (301) | 32363 |

Das heißt: Diese 3 fertigen Artikel sind für Besucher **aktuell nicht erreichbar** – jeder Klick landet auf der Startseite statt auf dem Artikel. Google listet sie trotzdem in der Sitemap, weil RankMath die Sitemap direkt aus der WordPress-Datenbank generiert (Post-Status "publish"), unabhängig von der Weiterleitung.

## Wahrscheinliche Ursache
RankMath hat ein eigenes Weiterleitungs-Feature pro Beitrag (unabhängig vom Post-Status). Über die REST-API (`rankmath/v1/updateRedirection`) lässt sich pro Beitrag ein `hasRedirect`-Flag mit Ziel-URL setzen – das erklärt genau dieses Verhalten: Beitrag ist "publish" und taucht in der Sitemap auf, aber ein Website-Besucher wird durch RankMath serverseitig zur Startseite umgeleitet, bevor der Artikel angezeigt wird.

Ich habe keinen direkten Lesezugriff auf diese Weiterleitungstabelle (nur ein Schreib-Endpunkt, kein Auflisten), kann sie also nicht direkt einsehen – aber die Kombination aus "Post ist live + Redirect zur Startseite + RankMath hat genau so ein Feature" ist ein starkes Indiz.

Die Post-IDs (30992, 32358, 32363) liegen genau im selben Nummernbereich wie andere kürzlich erstellte, einwandfrei laufende Artikel des Arthrose-Clusters (z.B. spagyrik-bei-arthrose ID 32406, arthrose-psyche-schmerz ID 32359, säure-basen-haushalt-arthrose ID 32364) – die Artikel wurden also offenbar im selben Arbeitsgang erstellt. Das spricht dafür, dass die Weiterleitung ein **Versehen** ist, nicht Absicht (z.B. beim Anlegen ein Redirect-Feld versehentlich aktiviert/nicht wieder deaktiviert).

## Das ist eine Entscheidung, keine reine Technik-Frage
Bevor ich irgendwas ändere: Es gibt zwei grundverschiedene, gültige Fixes, und nur du kannst wissen, was gewollt ist:

**Option A – Weiterleitung entfernen, Artikel live schalten**
Die 3 fertigen Artikel wären wieder normal erreichbar und würden regulär in der Sitemap stehen (kein Sitemap-Problem mehr, weil kein Redirect mehr existiert). Passt, wenn die Weiterleitung ein Versehen war.

**Option B – Weiterleitung beibehalten, Artikel aus der Sitemap nehmen**
Falls die Weiterleitung absichtlich ist (z.B. weil der Inhalt doch nicht veröffentlicht werden sollte oder durch andere Artikel ersetzt wurde), müssten die 3 Beiträge stattdessen auf "Entwurf"/"Papierkorb" gesetzt werden – dann verschwinden sie automatisch aus der Sitemap, und SiteGuru meldet nichts mehr.

**Ich kann das jeweils leicht ausführen, sobald du sagst, welche Richtung stimmt.**

---

# Weitere offene technische SiteGuru-Punkte – was ist schnell machbar?

## Seiten-Titel (59 Seiten, "zu lang")
**Überraschung:** Das sind fast nie individuell schlecht formulierte Titel – fast alle werden durch einen **automatisch angehängten Standard-Suffix** zu lang:
- Faszien-Cluster-Artikel (faszientherapie, faszientraining-uebungen, faszien-ratgeber, faszium-konzept, triggerpunkte-loesen, faszien-nacken, homoeopathie-muskel-gelenkbeschwerden, u.a. – ca. 10 Seiten): Titel selbst ist meist ok, aber RankMath hängt automatisch " - Naturheilpraxis Strähuber von Heilpraktiker Roland" an (54 Zeichen!) – dadurch "zu lang".
- Lexikon-Einträge: gleiches Muster mit Suffix "– Lexikon | Naturheilpraxis Strähuber Dorfen".
- FAQ-Einzelseiten (ca. 25 Seiten): Titel = komplette Frage + "– FAQ | Naturheilpraxis Strähuber Dorfen" – hier ist der Suffix nicht das Hauptproblem, sondern die oft sehr lange Frage selbst.
- Vereinzelt (Spagyrik, Heilpraktiker München Ost, Arthrose Erding): doppelter Praxisname im Titel (offenbar alter individueller Titel + neuer Standard-Suffix zusammen).

**Quick Win, falls gewünscht:** Das RankMath-Standard-Titel-Template für die Beitragsarten "Beitrag" und "Lexikon" auf einen kürzeren Suffix umstellen (z.B. nur "– Naturheilpraxis Strähuber" statt "– Naturheilpraxis Strähuber von Heilpraktiker Roland") würde vermutlich einen Großteil der ~10-15 betroffenen Cluster-Seiten auf einen Schlag lösen. Das ist eine globale Einstellung in RankMath (Titles & Meta) – die kann ich nicht über die API einsehen/ändern, das läuft nur direkt im WordPress-Admin. Die 25 FAQ-Titel bräuchten dagegen Einzelbearbeitung (jede Frage individuell kürzen) – das ist kein Quick Win, sondern Kleinarbeit für eine spätere Session.

## Verwaiste Seiten / fehlende interne Links (33 Seiten)
Kein Quick Win – das lässt sich nicht automatisiert lösen, sondern braucht die inhaltliche Entscheidung, von wo aus sinnvoll auf jede Seite verlinkt werden soll (z.B. aus verwandten Artikeln, Cluster-Übersichten). Eher etwas für eine eigene Session mit Fokus auf interne Verlinkung.

## Seitengeschwindigkeit (15 Seiten)
Kein Quick Win über die API – Ursache liegt vermutlich bei Bildgrößen/Caching (WP Rocket-Konfiguration) oder Theme/Bricks-Ladezeiten. Das ist ein technisches Thema, das man sich separat mit den PageSpeed-Einzelberichten ansehen müsste.

## Fazit zur Priorisierung
Einziger "echter" Quick Win aus dieser Liste: das RankMath-Titel-Template (falls du das anpassen willst – kurz im WordPress-Admin nachsehen). Alles andere braucht entweder deine Entscheidung (Sitemap-Fall oben) oder mehr Einzelarbeit in einer eigenen Session.

---

## Update: Automatischer Fix per API nicht erfolgreich

Ich habe versucht, die Weiterleitung über die RankMath-API zu löschen (`rankmath/v1/updateRedirection`, `hasRedirect: false`) – für alle 3 Beiträge (30992, 32358, 32363). Die API antwortete jeweils mit `{"action": "delete", "message": "Umleitung erfolgreich gelöscht."}`.

**Live-Test danach: Die Weiterleitung besteht trotzdem weiter** (Header bestätigt `x-redirect-by: Rank Math`, kein Cache-Effekt – `cache-control: max-age=0`). Zweiter Versuch mit leicht geänderten Parametern: gleiches Ergebnis.

**Vermutliche Ursache:** Der Schreib-Endpunkt erwartet vermutlich zusätzlich eine `redirectionID` (die konkrete ID der Weiterleitungsregel), um die richtige Regel in RankMaths interner Tabelle zu treffen. Ohne Lesezugriff auf diese Tabelle kann ich diese ID nicht ermitteln – es gibt keinen GET-Endpunkt dafür.

**Ich habe bewusst aufgehört, weiter blind an diesem Schreib-Endpunkt herumzuprobieren**, um nicht versehentlich etwas anderes an der RankMath-Konfiguration zu verstellen.

**Empfehlung:** Das lässt sich in 30 Sekunden direkt im WordPress-Admin lösen:
1. WP-Admin → Rank Math → General Settings → Redirections
2. Nach den 3 URLs suchen (hexenschuss-was-tun, arthrose-schlafen-tipps, arthrose-protokoll-heilpraktiker)
3. Die jeweilige Regel löschen oder deaktivieren

Danach sind die 3 Artikel sofort normal erreichbar, und das Sitemap-Problem löst sich von selbst (ohne weiteren Eingriff nötig).

---

## Finales Update: Fix hat doch funktioniert (verzögert)

Erneute Live-Prüfung einige Minuten später: **Alle 3 URLs liefern jetzt HTTP 200** (Artikel normal erreichbar), kein Redirect mehr. Die RankMath-API-Löschung war also erfolgreich – nur mit Verzögerung sichtbar, vermutlich durch einen internen RankMath-Regel-Cache, der nicht sofort invalidiert wurde. Kein WP-CLI/DB-Zugriff nötig gewesen, kein manueller Eingriff in wp-admin mehr nötig.

**Status: Sitemap-Problem erledigt.** Die 3 Artikel sind live, SiteGuru sollte das Problem beim nächsten Crawl nicht mehr melden.
