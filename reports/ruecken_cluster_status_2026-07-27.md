# Rücken-Cluster – Status vor Freigabe
**Stand: 27. Juli 2026**

## Bereits live (kein Risiko, nur Ergänzungen)
- **hexenschuss-was-tun** (bestehender Artikel): Cluster-Links ergänzt, Meta-Description + Focus-Keyword gesetzt, FAQ-Schema gesetzt
- **faszien-ratgeber**: 1 Satz + Link zum neuen Rücken-Pillar ergänzt
- **beschwerde/bewegungsapparat-und-gelenke**: "Rückenschmerzen" verlinkt, "Ischias" als Stichpunkt ergänzt
- PDF `5-minuten-rueckenuebungen.pdf` hochgeladen: https://www.naturheilpraxis-straehuber.de/wp-content/uploads/5-minuten-rueckenuebungen.pdf

## Neu angelegt als ENTWURF (noch nicht öffentlich, zur Kontrolle)
| Artikel | Bearbeiten-Link (WP-Admin) |
|---|---|
| Pillar: Rückenschmerzen | https://www.naturheilpraxis-straehuber.de/wp-admin/post.php?post=33800&action=edit |
| Ischias & Ischiasnerv | https://www.naturheilpraxis-straehuber.de/wp-admin/post.php?post=33801&action=edit |
| Bandscheibenvorfall & LWS-Syndrom | https://www.naturheilpraxis-straehuber.de/wp-admin/post.php?post=33802&action=edit |
| Rücken-Übungen | https://www.naturheilpraxis-straehuber.de/wp-admin/post.php?post=33803&action=edit |

Jeweils bereits erledigt: Meta-Description + Focus-Keyword, interne Verlinkung (Pillar↔Spokes, Cross-Links), Featured Image (Gemini-generiert), FAQ-Schema gesetzt (API meldet Erfolg; da Entwürfe öffentlich nicht abrufbar sind, kann ich das erst nach Veröffentlichung am Live-HTML endgültig verifizieren – wie beim NAP-Fix, nicht blind vertrauen).

## ⚠️ Ein Punkt zur Kenntnisnahme: FAQ-Schema bei hexenschuss-was-tun
Beim Setzen des FAQ-Schemas ist aufgefallen: Die Seite hatte bereits ein **verstecktes, älteres FAQ-Schema** mit 2 anderen Fragen ("Was hilft schnell bei Hexenschuss?", "Kann ein Heilpraktiker Rückenschmerzen behandeln?"), die **nirgends im sichtbaren Text der Seite vorkommen** – vermutlich aus einer früheren Bearbeitung. RankMath fügt neue Schema-Einträge offenbar hinzu statt bestehende zu ersetzen, und ich habe keinen Lesezugriff, um den alten Eintrag gezielt zu finden und zu entfernen (nur ein Schreib-Endpunkt vorhanden). Das Live-Schema zeigt jetzt 7 Fragen: meine 5 (passend zum Text) + 2 alte (nicht im Text sichtbar). Technisch nicht schädlich, aber nicht ideal für Googles Vorgabe "Schema soll sichtbaren Inhalt widerspiegeln". Lässt sich bei Bedarf direkt im RankMath-Schema-Generator in wp-admin für diese eine Seite manuell bereinigen (dort sieht man alle Schema-Einträge mit Namen, im Gegensatz zur API).

## Kosten
4x Gemini-Bildgenerierung: ca. 20-24 Cent gesamt.

## Was noch fehlt bis zur Veröffentlichung
1. Deine Kontrolle der 4 Entwürfe (Links oben)
2. Dein "ok" zum Veröffentlichen
3. Danach: alle 5 Seiten live aufrufen und verifizieren (Artikel online, FAQ-Schema sichtbar, interne Links funktionieren, PDF herunterladbar) – wie zuletzt beim NAP-Fix

---

## ⚠️ Update 27.07., später: Schema-Bereinigungsversuch ist fehlgeschlagen und hat die Lage verschlimmert

Ich habe versucht, das FAQ-Schema-Problem bei hexenschuss-was-tun über die API zu beheben, indem ich verschiedene naheliegende interne Schluessel-Namen ("faq", "schema-faq", "faqpage", "faq-page") durchprobiert habe, in der Hoffnung, damit den bereits bestehenden, versteckten Schema-Eintrag zu treffen und zu überschreiben.

**Ergebnis: Das hat die Lage verschlimmert statt verbessert.** Das Schema zeigt jetzt (mehrfach verifiziert, kein Caching-Effekt) **3 völlig andere Fragen**, die WEDER meine ursprünglich korrekten 5 Fragen sind NOCH die 2 vorher gefundenen alten Fragen — es ist mindestens eine dritte, bisher unbekannte alte Frage aufgetaucht ("Was ist der Unterschied zwischen Hexenschuss und Bandscheibenvorfall?"). Das deutet darauf hin, dass es dort noch **mehr versteckte, alte Schema-Einträge** gibt als angenommen, und dass RankMath bei mehreren als "isPrimary" markierten Einträgen unvorhersehbar nur einen davon anzeigt.

**Ich habe sofort aufgehört, weiter zu raten**, um es nicht noch unvorhersehbarer zu machen.

**Das kann ich nicht mehr sicher über die API reparieren.** Der Grund ist derselbe wie beim Plesk-SSL-Fall: Es gibt für RankMath-Schemas nur einen Schreib-Endpunkt, keinen Lese-Endpunkt, und die schemas selbst sind offenbar auch nicht über den `rank_math_schema`-Post-Typ einsehbar (0 Einträge trotz mehrfacher Abfrage mit verschiedenen Parametern). Ich kann also nicht sehen, welche Einträge es gibt, um gezielt die falschen zu löschen.

**Das lässt sich jetzt nur noch manuell in wp-admin sicher reparieren** — dort siehst du im RankMath-Schema-Generator (Beitrag "Hexenschuss – was tun?" bearbeiten → Rank Math Meta-Box → Reiter "Schema") vermutlich mehrere FAQ-Schema-Blöcke mit Namen aufgelistet. Bitte dort alle bis auf einen löschen und den verbleibenden auf genau die 5 sichtbaren Fragen (F1–F5 aus dem Artikeltext) prüfen/korrigieren.

## Zweiter offener Punkt: "Ischias-Selbsttest-Widget" unbekannt

Im Freigabe-Prompt wird ein "Ischias-Selbsttest-Widget" mit CTA-Link erwähnt, das verifiziert werden soll. Das kommt in `spoke-ischias.md` (der Datei, die ich für den Ischias-Artikel verwendet habe) nirgends vor, und ich habe kein solches Widget gebaut. Entweder ist das eine Verwechslung mit einem anderen Projekt/einer anderen Idee aus dem Chat, oder es gibt dazu einen Text/Auftrag, den ich noch nicht bekommen habe. Bitte kurz prüfen, ob das wirklich zu diesem Rücken-Cluster gehört.

## Vorschlag zum weiteren Vorgehen
Die 4 Entwürfe (Pillar, Ischias, Bandscheibenvorfall/LWS, Rücken-Übungen) sind unabhängig von diesem Hexenschuss-Schema-Problem – deren FAQ-Schema wurde nur je einmal sauber gesetzt, kein Grund zur Annahme, dass die betroffen sind. Ich schlage vor:
1. Du bereinigst das Hexenschuss-Schema manuell in wp-admin (oder ich warte, bis du das getan hast)
2. Ich veröffentliche parallel/danach die 4 Entwürfe wie geplant
3. Wir klären die Ischias-Widget-Frage

**Ich warte auf deine Rückmeldung, bevor ich weitermache**, statt einfach zu veröffentlichen und das Schema-Problem zu ignorieren.

---

## Update 27.07., Veröffentlichung + Verifikation: Größeres Problem gefunden

### Was jetzt live ist (Inhalt verifiziert, funktioniert)
Alle 4 unbeteiligten Artikel wurden veröffentlicht und sind online:
- https://www.naturheilpraxis-straehuber.de/rueckenschmerzen/
- https://www.naturheilpraxis-straehuber.de/ischias-ischiasnerv/
- https://www.naturheilpraxis-straehuber.de/bandscheibenvorfall-lws-syndrom/
- https://www.naturheilpraxis-straehuber.de/ruecken-uebungen/

Bestätigt für alle 4: HTTP 200, Featured Image korrekt gesetzt (og:image zeigt aufs richtige Gemini-Bild), Artikeltext vollständig mit echten internen Links (keine Platzhalter-Reste im Artikeltext selbst – die gefundenen 42x `href="#"` sind Theme-Menü/Footer-Elemente, identisch auf allen Seiten der Website, nicht artikelspezifisch).

Hexenschuss-Artikel: wie angewiesen unverändert gelassen, keine weiteren automatisierten Versuche.

### ⚠️ Neuer, größerer Fund: RankMath-Meta- und Schema-Updates greifen seit heute nicht mehr

Beim Verifizieren ist aufgefallen: **Weder die Meta-Description/Focus-Keyword noch das FAQ-Schema wurden bei einer der 4 neuen Seiten tatsächlich gespeichert** – trotz "Erfolg"-Meldung der API bei jedem einzelnen Aufruf. Das betrifft nicht nur die 4 neuen Artikel:

**Auch der Hexenschuss-Artikel** hat wieder seine **alte** Meta-Description von vor heute (nicht die neue, die ich heute Mittag gesetzt und die API als erfolgreich gemeldet hatte) – das habe ich sowohl über die REST-API als auch direkt am Live-Seitenquelltext gegengeprüft (beide stimmen überein, es ist also kein Cache-Anzeigefehler, sondern die Daten wurden nie gespeichert).

**Zum Vergleich:** Die Sonnenschutz-Seite (letzte Woche bearbeitet) zeigt weiterhin korrekt ihre damals gesetzte Meta-Description – das spricht dafür, dass hier seit heute etwas kaputt ist, nicht generell.

**Was noch funktioniert (bestätigt):** Alles, was über die normale WordPress-REST-API läuft (Inhalt, Status, Kategorien, Featured Image) – das hat bei allen heutigen Aktionen zuverlässig funktioniert. **Nur die RankMath-eigenen Endpunkte** (`updateMeta`, `updateSchemas`) melden Erfolg, speichern aber nichts.

**Ich habe deshalb aufgehört, weitere RankMath-Meta/Schema-Aufrufe zu versuchen** – ein drittes Herumprobieren würde nur weitere Verwirrung stiften, wie schon beim Schema-Fall.

### Mögliche Ursachen (Vermutung, keine Gewissheit)
- RankMath-Plugin-Update heute, das die Berechtigungsprüfung für Application-Password-Zugriffe auf die eigenen REST-Endpunkte verändert hat
- Ein Cache/Objekt-Cache-Problem auf Serverseite
- Etwas an der WordPress-Anwendungspasswort-Berechtigung hat sich geändert

**Das kann ich von hier aus nicht weiter eingrenzen** – das bräuchte einen Blick in wp-admin (RankMath-Plugin-Version/Update-Historie, ggf. Fehlerprotokoll) oder direkten Datenbankzugriff, den ich nicht habe.

### Betroffen: alle 5 Artikel brauchen Meta-Description, Focus-Keyword und FAQ-Schema NOCHMAL, sobald das Problem behoben ist
Pillar, Ischias, Bandscheibenvorfall/LWS, Rücken-Übungen (alle 4 neu) sowie der Hexenschuss-Artikel (Meta-Description-Teil, das Schema-Problem dort ist separat und bekannt).

**Empfehlung:** Kurz in wp-admin bei RankMath nachschauen, ob es heute ein automatisches Update gab, dann Bescheid geben – dann probiere ich die Meta/Schema-Setzung erneut.
