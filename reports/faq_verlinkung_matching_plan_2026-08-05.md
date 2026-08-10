# 33 verwaiste FAQ-Seiten: Matching-Plan (VOR jeder Änderung, zur Kontrolle)
**Stand: 5. August 2026**

## Live-Bestätigung

Über einen frischen eigenen Crawl (nicht die ältere Ahrefs-Momentaufnahme) bestätigt: alle 33
FAQ-Seiten haben aktuell wirklich **0 eingehende interne Links**. Liste stimmt.

## Wichtiger technischer Fund, der den Plan verändert

Bevor ich verlinke, ein ehrlicher Zwischenstand: Ich habe geprüft, welche potenziellen
Ziel-/Ankerseiten sich überhaupt zuverlässig per REST-API bearbeiten lassen. Ergebnis:

**Nicht editierbar (Bricks-Builder-Seiten ohne Inhalt im Standard-WordPress-Feld – ein Schreiben
würde entweder gar nicht sichtbar werden oder beim nächsten Bricks-Speichern stillschweigend
überschrieben werden, genau das Silent-Failure-Muster, das wir in Block 1 schon einmal hatten):**
- `/ueber-mich/`, `/ablauf/`, `/kontakt/`, `/` (Home), `/lexikon/` (Hub-Seite), `/ratgeber/` (Hub-Seite)
- `/therapie/osteopathie/` (einzelner Ausreißer – die anderen 4 Therapie-Seiten sind aber ok)

Das sind ausgerechnet die Seiten, auf die die meisten der 33 FAQs inhaltlich am besten passen
würden (Praxis-Vertrauen, Ablauf, Kontakt/Termine). Ich fasse das nicht automatisch an – analog
zur Entscheidung beim RankMath-Schema-Problem.

**Editierbar und nutzbar:**
- Alle 63 Blog-Artikel (`posts`)
- Alle 78 Lexikon-Einträge (`lexikon`)
- Alle 8 Beschwerde-Übersichtsseiten (`beschwerde`) – v.a. `beschwerden-im-kindesalter`,
  `unerklaerliche-beschwerden`, `aengste-sorgen-und-depressionen`, `bewegungsapparat-und-gelenke`
- 4 von 5 Therapie-Seiten (`spagyrik`, `dorn-therapie`, `faszientherapie`, `gespraechstherapie`)
- 3 der 11 Pages: `spagyrik`, `heilpraktiker-muenchen-ost`, `arthrose-heilpraktiker-erding`,
  `datenschutz`, `impressum` sind eigentlich Gutenberg-Content und daher OK
- Alle anderen FAQ-Seiten (Cross-Linking zwischen thematisch verwandten Fragen)

## Was das inhaltlich bedeutet

Die 33 FAQs sind fast alle **allgemeine Praxis-/Vertrauens-/Organisationsfragen** – keine
Fragen zu Rücken, Faszien oder Arthrose speziell. Der Rücken-/Faszien-/Arthrose-Cluster passt
daher inhaltlich zu praktisch keiner davon; ich habe dort bewusst nichts erzwungen. Stattdessen
gruppieren sich die 33 in fünf natürliche Themen-Cluster:

| Cluster | Anzahl | Bester editierbarer Hauptanker | Anmerkung |
|---|---|---|---|
| A. Qualifikation/Verband | 4 | `/lexikon/heilpraktiker/` | guter Treffer |
| B. Kosten/Versicherung | 5 | – (Kontakt-Seite blockiert) | nur FAQ-Querverlinkung, kein starker Hauptanker |
| C. Vertrauen/Methoden-Skepsis | 6 | `/beschwerde/aengste-sorgen-und-depressionen/`, `/beschwerde/unerklaerliche-beschwerden/` | guter Treffer |
| D. Erstgespräch-Vorbereitung | 6 | `/beschwerde/unerklaerliche-beschwerden/` | guter Treffer |
| E. Termin-Logistik | 4 | – (Kontakt-Seite blockiert) | nur FAQ-Querverlinkung |
| F. Einzelfälle mit gutem Spezial-Treffer | 8 | siehe Tabelle unten | individuell |

## Vollständige Zuordnung (alle 33)

| # | FAQ (Anchor-Text = Frage) | Cluster | Vorgeschlagene Hauptseiten-Ziele | Guter Treffer? |
|---|---|---|---|---|
| 1 | Wie finden Sie heraus, was mir fehlt? | C | unerklaerliche-beschwerden, lexikon/heilpraktiker | ja |
| 2 | Ich traue mich nicht / schäme mich, mein Thema anzusprechen | C | aengste-sorgen-und-depressionen | ja |
| 3 | Ich bin mir unsicher, ob Sie mir helfen können | C | unerklaerliche-beschwerden | ja |
| 4 | Was ist, wenn ich mit Ihrer Art nicht klarkomme? | C | (kein Hauptseiten-Treffer, nur FAQ-Querlink zu 2/3/20) | schwach |
| 5 | Werden Behandlungskosten von privaten Krankenkassen erstattet? | B | lexikon/heilpraktiker (schwach) | schwach |
| 6 | Können Sie bei Mobbing, Depression, Traurigkeit helfen? | C | aengste-sorgen-und-depressionen | ja, stark |
| 7 | Ich weiß nicht, was mein Problem ist – Termin trotzdem möglich? | D | unerklaerliche-beschwerden | ja, stark |
| 8 | Gibt es weiterführende Literatur zu Ihren Methoden? | F | lexikon/faszientherapie, lexikon/osteopathie, lexikon/dorn-therapie | ja |
| 9 | Schon beim Hausarzt/Fachärzten – macht es trotzdem Sinn? | D | unerklaerliche-beschwerden, lexikon/biopsychosoziales-schmerzmodell | ja |
| 10 | Kosten von der gesetzlichen Krankenkasse übernommen? | B | lexikon/heilpraktiker (schwach) | schwach |
| 11 | Ich habe eine Allergie, wann soll ich kommen? | F | beschwerde/atem-und-chronische-bronchitis (schwach) | **kein guter Treffer** |
| 12 | Soll ich Befunde/Arztberichte mitnehmen? | D | unerklaerliche-beschwerden | mittel |
| 13 | Kurzfristig Termin bei akuten Schmerzen? | E | (kein Hauptseiten-Treffer, nur FAQ-Querlink zu 24/32/33) | schwach |
| 14 | Mitglied in einem Osteopathie-Verband? | A | lexikon/heilpraktiker, lexikon/osteopathie | ja |
| 15 | Werde bald operiert, können Sie unterstützen? | F | beschwerde/bewegungsapparat-und-gelenke | mittel |
| 16 | Muss die Rechnung gleich in der Praxis bezahlt werden? | B | (kein Hauptseiten-Treffer) | schwach |
| 17 | Organische Beschwerden vorher beim Arzt abklären lassen? | D | unerklaerliche-beschwerden | ja |
| 18 | Bin bei meinem Arzt zufrieden, möchte trotzdem kommen | D | unerklaerliche-beschwerden | mittel |
| 19 | Heilpraktiker-Zusatzversicherung empfehlen? | B | lexikon/heilpraktiker (schwach) | schwach |
| 20 | Was ist, wenn Ihre Methode nicht anschlägt? | C | (kein Hauptseiten-Treffer, nur FAQ-Querlink) | schwach |
| 21 | Mitglied in einem Verband? | A | lexikon/heilpraktiker | ja |
| 22 | Große Heilpraktikerausbildung? | A | lexikon/heilpraktiker | ja, stark |
| 23 | Analysen von sicheren Laboren durchgeführt? | F | lexikon/amsat-messung, lexikon/bioelektrische-diagnostik | ja |
| 24 | Termine am Wochenende/spät abends? | E | (kein Hauptseiten-Treffer) | schwach |
| 25 | Verschreiben Sie auch Medikamente? | F | lexikon/heilpraktiker | ja, stark |
| 26 | Wie lange liegt Ihre Prüfung zurück? | A | lexikon/heilpraktiker | ja |
| 27 | Post-Covid/Post-Vac-Symptome – kann ich kommen? | F | die-fatigue-ein-missverstandenes-erschoepfungssyndrom, habe-ich-eine-stille-entzuendung-in-meinem-koerper | ja |
| 28 | Meine Symptome sind nur ab und zu da | D | unerklaerliche-beschwerden | mittel |
| 29 | Werden besprochene Themen weitergegeben? | F | **datenschutz** (Page, editierbar!) | ja, stark |
| 30 | Wonach berechnen Sie die Kosten? | B | (kein Hauptseiten-Treffer) | schwach |
| 31 | Wie alt sollte ein Kind sein? | F | beschwerde/beschwerden-im-kindesalter, hintern-juckt-bei-kindern | ja, stark |
| 32 | Bieten Sie auch Online-Termine an? | E | (kein Hauptseiten-Treffer) | schwach |
| 33 | Machen Sie auch Hausbesuche? | E | (kein Hauptseiten-Treffer) | schwach |

**Zusammenfassung:** 20 von 33 mit gutem/mittlerem Hauptseiten-Treffer, 12 nur mit
FAQ-Querverlinkung untereinander (Cluster B + E + FAQ 4/20), 1 (#11 Allergie) wirklich ohne
brauchbaren Anker irgendwo.

## Rückverlinkung (Hauptseite → FAQ)

Auf jeder der oben genutzten editierbaren Zielseiten mindestens 1 Rücklink zur passendsten FAQ,
Anchor-Text = die FAQ-Frage selbst. Betrifft: `lexikon/heilpraktiker` (5 Rücklinks – ggf. als
kleine Liste "Häufige Fragen dazu"), `beschwerde/unerklaerliche-beschwerden`,
`beschwerde/aengste-sorgen-und-depressionen`, `beschwerde/beschwerden-im-kindesalter`,
`lexikon/osteopathie`, `lexikon/amsat-messung`, `lexikon/bioelektrische-diagnostik`,
`lexikon/faszientherapie`, `lexikon/dorn-therapie`, `datenschutz`, sowie die zwei Posts zu
Post-Covid/Fatigue.

## Für Über mich / Ablauf / Kontakt / Home (die eigentlich besten Ziele)

Da ich diese Bricks-Seiten nicht zuverlässig automatisch bearbeiten kann, hier eine kurze
Liste, welche FAQ-Fragen dort inhaltlich am besten hinpassen würden – falls du sie selbst in
Bricks ergänzen willst (fertige Fragen + Ziel-URLs, nur copy-paste nötig):

- **Kontakt:** FAQ 13, 24, 32, 33 (Termin-Logistik-Cluster E)
- **Ablauf / Über mich:** FAQ 4, 20 (Vertrauen), 5, 10, 16, 19, 30 (Kosten-Cluster B)

## Frage an dich, bevor ich anfange

1. Passt diese Zuordnung so? Insbesondere: FAQ 11 (Allergie) würde ich ohne guten Treffer
   lassen – einverstanden, oder hast du eine Idee, wohin die passen könnte?
2. Soll ich mit der Umsetzung wie beschrieben starten (Backup vor jeder Änderung, Verifikation
   nach jedem Schreibvorgang, wie bei den anderen Blöcken)?
