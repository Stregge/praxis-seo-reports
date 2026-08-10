# 33 verwaiste FAQ-Seiten: Ergebnis der Verlinkung
**Stand: 5. August 2026**

## Zusammenfassung

- **32 von 33 FAQ-Seiten** wurden intern verlinkt (Backlink von 1-4 passenden Hauptseiten/Artikeln
  + Cross-Links zu thematisch verwandten FAQs, wo sinnvoll)
- **1 FAQ ohne guten Treffer**, bewusst unverlinkt gelassen statt erzwungen:
  `faq/ich-habe-eine-allergie-wann-soll-ich-kommen/`
- **15 Hauptseiten/Artikel** erhielten mindestens einen Rücklink zur passenden FAQ (Anchor-Text
  = FAQ-Frage)
- **0 Fehler**, alle 47 Schreibvorgänge (32 FAQ + 15 Zielseiten) live verifiziert
- Alle 47 Original-Contents vorher gesichert unter `/root/praxis-seo/backup/content/`

## Vorher/Nachher

| | Vorher | Nachher |
|---|---|---|
| FAQ-Seiten mit ≥1 eingehendem internen Link | 0 von 33 | 32 von 33 |
| Eindeutige interne Link-Ziele auf der Seite gesamt | 72 | 113 |

Live per frischem Crawl bestätigt (nicht nur API-Rückmeldung): 32 der 33 FAQ-URLs sind jetzt
tatsächlich als Link-Ziel im Content zu finden, nur die Allergie-FAQ bleibt wie geplant offen.

## Wichtiger technischer Fund während der Arbeit

Die eigentlich naheliegendsten Zielseiten für einen Großteil der FAQs (Über mich, Ablauf,
Kontakt, Home, Lexikon-Hub, Ratgeber-Hub sowie `/therapie/osteopathie/`) sind Bricks-Builder-Seiten
ohne Inhalt im Standard-WordPress-Feld – dieselbe Silent-Failure-Falle wie beim RankMath-Schema in
Block 1. Ich habe diese bewusst nicht automatisch angefasst. Stattdessen wurden inhaltlich passende
Alternativen genutzt (v.a. `/lexikon/heilpraktiker/`, `/beschwerde/unerklaerliche-beschwerden/`,
`/beschwerde/aengste-sorgen-und-depressionen/`, `/beschwerde/beschwerden-im-kindesalter/`,
`/datenschutz/`).

Für die 12 FAQs, deren ideale Zielseite (v.a. Kontakt für Termin-Logistik, Über mich/Ablauf für
Kosten-Fragen) blockiert war, gab es nur FAQ-Querverlinkung untereinander, keinen Hauptseiten-Link
– passend dazu liegt dir eine separate Copy-Paste-Liste vor (siehe unten), falls du diese Links
selbst in Bricks ergänzen willst.

## Cluster-Übersicht (was wohin verlinkt wurde)

| Cluster | FAQs | Hauptanker |
|---|---|---|
| A. Qualifikation/Verband | 4 | `/lexikon/heilpraktiker/` (+ `/lexikon/osteopathie/` für 1) |
| B. Kosten/Versicherung | 5 | 3× schwacher Link zu `/lexikon/heilpraktiker/`, 2× nur Cross-Link |
| C. Vertrauen/Methoden-Skepsis | 6 | `/beschwerde/aengste-sorgen-und-depressionen/`, `/beschwerde/unerklaerliche-beschwerden/` (nicht bei allen) |
| D. Erstgespräch-Vorbereitung | 6 | `/beschwerde/unerklaerliche-beschwerden/` (+ `/lexikon/biopsychosoziales-schmerzmodell/` für 1) |
| E. Termin-Logistik | 4 | nur Cross-Link (kein Hauptanker verfügbar) |
| Einzelfälle | 7 | individuell (Literatur→3 Lexikon-Methoden, Analysen→AMSAT/Bioelektrisch, Kind→Kindesalter+Post, Post-Covid→Fatigue+Entzündung, Datenschutz→Datenschutzseite, OP→Bewegungsapparat, Medikamente→Heilpraktiker) |
| Ohne Treffer | 1 | Allergie-FAQ, bewusst unverlinkt |

## Für Über mich / Ablauf / Kontakt (manuell zu ergänzen, falls gewünscht)

Fertige Liste zum Copy-Paste, falls du diese selbst in Bricks einbauen willst:

**Kontakt** (Termin-Logistik):
- [Bekomme ich auch kurzfristig einen Termin bei Ihnen, wenn ich akute Schmerzen habe?](https://www.naturheilpraxis-straehuber.de/faq/bekomme-ich-auch-kurzfristig-einen-termin-bei-ihnen-wenn-ich-akute-schmerzen-habe/)
- [Vergeben Sie auch Termine am Wochenende oder spät abends?](https://www.naturheilpraxis-straehuber.de/faq/vergeben-sie-auch-termine-am-wochenende-oder-spaet-abends/)
- [Bieten Sie auch Online-Termine an?](https://www.naturheilpraxis-straehuber.de/faq/bieten-sie-auch-online-termine-an/)
- [Machen Sie auch Hausbesuche?](https://www.naturheilpraxis-straehuber.de/faq/machen-sie-auch-hausbesuche/)

**Ablauf / Über mich** (Vertrauen/Kosten):
- [Was ist, wenn ich mit Ihrer Art oder Ihnen nicht klarkomme?](https://www.naturheilpraxis-straehuber.de/faq/was-ist-wenn-ich-mit-ihrer-art-oder-ihnen-nicht-klarkomme/)
- [Was ist, wenn Ihre Behandlungsmethode nicht anschlägt?](https://www.naturheilpraxis-straehuber.de/faq/was-ist-wenn-ihre-behandlungsmethode-nicht-anschlaegt/)
- [Werden die Behandlungskosten von privaten Krankenkassen erstattet?](https://www.naturheilpraxis-straehuber.de/faq/werden-die-behandlungskosten-von-privaten-krankenkassen-erstattet/)
- [Werden meine Behandlungskosten von der gesetzlichen Krankenkasse übernommen?](https://www.naturheilpraxis-straehuber.de/faq/werden-meine-behandlungskosten-von-der-gesetzlichen-krankenkasse-uebernommen/)
- [Muss ich die Rechnung gleich in der Praxis bezahlen?](https://www.naturheilpraxis-straehuber.de/faq/muss-ich-die-rechnung-gleich-in-der-praxis-bezahlen/)
- [Können sie mir eine Heilpraktiker-Zusatzversicherung empfehlen?](https://www.naturheilpraxis-straehuber.de/faq/koennen-sie-mir-eine-heilpraktiker-zusatzversicherung-empfehlen/)
- [Wonach berechnen Sie die Kosten Ihrer Behandlungen?](https://www.naturheilpraxis-straehuber.de/faq/wonach-berechnen-sie-die-kosten-ihrer-behandlungen/)

## Kein Treffer

`ich-habe-eine-allergie-wann-soll-ich-kommen` – kein thematisch passendes Hauptartikel-Ziel
gefunden. Möglich wäre langfristig ein eigener kurzer Artikel/Absatz zu Allergien, oder die
Frage bleibt als reine FAQ ohne Backlink stehen (schadet nicht, ist nur weiterhin nicht optimal
für internes Linkjuice).
