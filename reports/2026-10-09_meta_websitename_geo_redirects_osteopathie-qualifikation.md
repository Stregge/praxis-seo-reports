# 09.10.2026 – Meta Kontakt, Website-Name, Geo-Vergleich, 8 Weiterleitungen + Osteopathie-Qualifikationssätze (Lesen)
Nicht angefasst: robots.txt, Plugin- und WordPress-Updates, Bricks-Felder. Es gibt keine pauschalen Freigaben, und Zugangsdaten wurden nicht ausgegeben. Die DB-Zugangsdatei auf dem Hosting ist nach Abschluss entfernt.

## 1) Kontakt-Seite – Rank-Math-Meta-Description ✅
- **Vorher:** „Jetzt Termin vereinbaren bei Heilpraktiker Roland Strähuber in Dorfen. Telefon: 08081 / 954 89 89. Ganzheitliche Naturheilkunde – persönlich & individuell.“
- **Nachher (exakt wie vorgegeben, 138 Zeichen):** „Naturheilpraxis Strähuber, Heilpraktiker in Dorfen: Termin unter 08082 4249608 vereinbaren. Anfahrt, Öffnungszeiten und Videosprechstunde.“
- **Schreibweg:** Die REST-API gibt `rank_math_description` für **Seiten** nicht aus; das Feld ist nur für Beiträge registriert. Ein REST-Schreibversuch wäre also wahrscheinlich still verworfen worden. Deshalb habe ich per SQL-UPDATE genau eine Zeile geändert (`sh_postmeta`, post_id 111, `rank_math_description`). Der Wert ist einfacher Text, nicht serialisiert.
  - Ein erster Versuch scheiterte vorher sauber am fehlenden `xxd` (SQL-Fehler, nichts geschrieben).
- **Rücklesen DB:** identisch.
- **Live** (/kontakt/, nach Cache-Leerung): `meta name="description"`, `og:description` und `twitter:description` sind identisch.
- **Bricks-Feld unverändert:** MD5 von `_bricks_page_content_2` vorher und nachher `1dff0874b5be5133e802120634868fb6`.
- Backup: `/root/praxis-seo/backups/kontakt111_rankmath-meta_20261009-104356.sql`

## 2) Rank Math – Website-Name ✅
- Option `rank-math-options-titles` → `website_name`: „Naturheilpraxis Strähuber von Heilpraktiker Roland“ → **„Naturheilpraxis Strähuber“**
- Rundweg-Test bestanden; geändert ist nur dieser Schlüssel (320 → 320 Schlüssel). Rücklesen: identisch mit dem vorbereiteten Wert.
- Live Startseite: `WebSite.name` im JSON-LD = „Naturheilpraxis Strähuber“; `og:site_name` = „Naturheilpraxis Strähuber“. Das `MedicalBusiness`/`Organization`-Schema hieß bereits so.
- Backup: `/root/praxis-seo/backups/rankmath-options-titles_20261009-104356.sql`
- **Nebenbefund (nicht geändert):** Im JSON-LD der Startseite steht als Autor (`Person`, `Article.author`) **„SEO-Revolution“**.

## 3) Geo-Koordinaten (nur gelesen, nicht geändert)
Referenz: OpenStreetMap-Geocoder Nominatim, Treffer auf Gebäudeebene „45, Wasentegernbach, Dorfen, Landkreis Erding, Bayern, 84405“.

| Quelle | Breite | Länge | Abweichung zur Referenz |
|---|---|---|---|
| **Geocoder Nominatim (Referenz)** | 48.275210 | 12.217319 | 0,00 km |
| Rank Math Lokales SEO (`geo`) | 48.275678 | 12.219060 | **0,14 km** |
| WPCodeBox-Snippet #12 (JSON-LD Startseite) | 48.266900 | 12.162800 | **4,14 km** |
| Kontakt-Seite: Bricks-Kartenelement | 48.275950 | 12.218137 | 0,10 km |
| Kontakt-Seite: Google-Maps-Routenlink | 48.275250 | 12.217257 | 0,01 km |

Snippet #12 liegt 4,28 km neben dem Rank-Math-Wert.

## 4) Acht 301-Weiterleitungen ✅
**Weg:** direkt in Rank Maths eigene Tabelle `sh_rank_math_redirections`, im selben Format, das das Admin-Formular (`DB::add`) erzeugt. Vorher im Rank-Math-Code geprüft:
- `DB::add()` ist ein reines INSERT mit serialisierten `sources`, ohne weitere Nebenwirkungen.
- Beim Aufruf sucht Rank Math aktive Zeilen in dieser Tabelle und füllt seinen Cache erst bei einem Treffer.
- Im Cache standen 3 alte Einträge auf den Papierkorb-Redirect #27. Das blockiert nicht: Rank Math akzeptiert nur aktive Weiterleitungen und sucht sonst regulär weiter. Den Cache habe ich deshalb nicht angefasst.

Backup beider Tabellen (Weiterleitungen und Cache): `/root/praxis-seo/backups/rankmath-redirections_20261009-104356.sql`

| ID | Quelle (exact) | Ziel | HTTP-Test |
|---|---|---|---|
| 31 | redirect-saeure-basen-haushalt-arthrose | /saeure-basen-haushalt-arthrose/ | 301 ✔ |
| 32 | redirect-ernaehrung-bei-arthrose-was-wirklich-hilft-und-was-du-meiden-solltest | /ernaehrung-bei-arthrose-was-wirklich-hilft-und-was-du-meiden-solltest/ | 301 ✔ |
| 33 | redirect-arthrose-protokoll-heilpraktiker | /arthrose-protokoll-heilpraktiker/ | 301 ✔ |
| 34 | redirect-arthrose-schlafen-tipps | /arthrose-schlafen-tipps/ | 301 ✔ |
| 35 | redirect-hueftarthrose-schulterarthrose-naturheilkunde | /hueftarthrose-schulterarthrose-naturheilkunde/ | 301 ✔ |
| 36 | redirect-faszientherapie-arthrose | /faszientherapie-arthrose/ | 301 ✔ |
| 37 | Heilpraktiker.html | / | 301 ✔ |
| 38 | de | / | 301 ✔ |

- Getestet jeweils mit und ohne Schrägstrich am Ende (16 Abrufe): alle 301 auf das richtige Ziel. Alle Ziele liefern 200.
- Aktive Weiterleitungen: 28 → 36 (gesamt 30 → 38).
- In der Rank-Math-Weiterleitungsliste erscheinen die 8 Einträge ganz normal und lassen sich dort bearbeiten oder löschen.
- Rückbau: die Zeilen mit ID 31–38 löschen oder das Backup einspielen.

---

## Lese-Auftrag: Osteopathie-Sätze mit Bezug zu Ausbildung, Abschluss, Titel oder Qualifikation
Quellen: gerendertes HTML aller 207 Sitemap-URLs (Crawl vom 07.10.) und Startseite, /therapie/osteopathie/, /zinkmangel-symptome/ und FAQ 467 frisch abgerufen am 09.10. Wortlaut unverändert, ohne Bewertung.

### 1) Autorenbox (ca. 70 Beitragsseiten, wörtlich, Schreibweise ohne Umlaute wie im Original)
> Ueber den Autor
> Roland Straehuber
> Heilpraktiker · Naturheilpraxis Straehuber, Dorfen
> Roland Straehuber ist staatlich gepruefter Heilpraktiker und behandelt in seiner Naturheilpraxis in Dorfen (Bayern) Menschen mit einem ganzheitlichen Ansatz. Seine Schwerpunkte liegen in der Osteopathie, Faszientherapie, Spagyrik und Dorn-Therapie.

### 2a) Startseite – https://www.naturheilpraxis-straehuber.de/
- **Meta-Description:** „Naturheilpraxis Strähuber in Dorfen bei Erding: Osteopathie, Faszientherapie, Dorn-Methode und Mikronährstoffanalyse. Heilpraktiker Roland Strähuber – persönlich, ganzheitlich, erfahren.“
- **Überschrift (H3):** „Osteopathie“
- **Fließtext:** „Bei der Osteopathie handelt es sich um eine sanfte Form der Medizin, die auf das Erkennen und Behandeln von Funktionsstörungen und Strukturstörungen ausgerichtet ist.“
- Ein Satz zu Ausbildung, Abschluss, Titel oder Qualifikation in Osteopathie: **keiner gefunden.**

### 2b) https://www.naturheilpraxis-straehuber.de/therapie/osteopathie/ (ID 291)
- **Title:** „Osteopathie Dorfen – den Patienten als Ganzes betrachten“
- **Meta-Description:** „Sie sind auf der Suche nach einen Osteopathen? In meiner Naturheilpraxis wende ich Osteopathie seit Jahren erfolgreich an. Erfahren Sie mehr über diese Methode“
- **H1:** „Osteopathie – den Patienten als Ganzes betrachten, um Ursachen von Schmerzen zu erkennen“
- **H2:** „Die 5 Grundprinzipien der Osteopathie“ · „Bei welchen Beschwerden kann die Osteopathie hilfreich sein?“
- **Fließtext mit „Osteopath…“:**
  - „Die Osteopathie ist eine medizinische Behandlungsform, in der durch manuelle Techniken körperliche Funktionsstörungen und Blockaden behandelt werden.“
  - „Osteopathische Techniken helfen dabei, die ursprüngliche Bewegungsfähigkeit wieder herzustellen, damit alles wieder optimal funktioniert.“
  - „In der Osteopathie wird versucht, eine ideale Ver- und Entsorgung aller Strukturen mit Körperflüssigkeiten sicherzustellen, um so eine ideale Funktion des Körpers zu erreichen.“
  - „Deshalb werden in der Osteopathie nie einzelne Beschwerden behandelt, sondern immer der Mensch in seiner Gesamtheit.“
  - „Mit der Osteopathie wird die Beweglichkeit des Gewebes und die Zirkulation der Körperflüssigkeiten wiederhergestellt, sodass die natürlichen Heilungsprozesse im Körper unterstützt …“
  - „Osteopathische Behandlungen im Bereich des Nackens und der Wirbelsäule können zu einer Verbesserung von Kopfschmerzen und Migräne führen.“
  - „Osteopathie kann als entspannende Therapie betrachtet werden, die dazu beitragen kann, Stress abzubauen und das allgemeine Wohlbefinden zu fördern.“
- Satz mit Bezug zu Titel oder Qualifikation: nur die Meta-Description („… einen Osteopathen? … wende ich Osteopathie seit Jahren erfolgreich an.“).

### 3) Weitere Treffer (Ausbildung, Abschluss, Titel, Qualifikation, Verband, Berufsbezeichnung „Osteopath“)
| URL (ID) | Stelle | Wortlaut |
|---|---|---|
| /ueber-mich/ (237) | Meta-Description | „Roland Strähuber ist Heilpraktiker in Dorfen – ausgebildet in Osteopathie, Faszientherapie & Psychotherapie. Erfahren Sie mehr über seinen ganzheitlichen…“ |
| /ueber-mich/ (237) | Abschnitt „Meine Ausbildung und Fortbildungen“ › Schmerz- und Bewegungstherapie | „Faszientherapie Konzept Modul 1-8 (2019) – Manuelle Therapien und AORT Osteopathie (2014-2018) – Dorn-Breuss-Therapie (2011/2012)“ |
| /ueber-mich/ (237) | Abschnitt „Meine Werte“ | „Fortwährende & intensive Weiterbildung im Gesundheitsbereich · Mitgliedschaft in einem namhaften Heilpraktikerverband“ (ohne Osteopathie-Bezug, steht im selben Block) |
| /faq/sind-sie-auch-mitglied-in-einem-osteopathie-verband/ (467) | Titel / Frage | „Sind sie auch Mitglied in einem Osteopathie-Verband?“ |
| /faq/sind-sie-auch-mitglied-in-einem-osteopathie-verband/ (467) | Antwort | „Nein. Um Mitglied in einem solchen Osteopathie-Verband zu werden, wird die große 5-jährige Osteopathie-Ausbildung vorausgesetzt. Diese habe ich nicht, da sie für mich nicht relevant war und ich trotzdem viele osteopathische Techniken erlernt habe.“ |
| /faq/sind-sie-auch-mitglied-in-einem-osteopathie-verband/ (467) | Meta-Description | „Nein. Um Mitglied in einem solchen Osteopathie-Verband zu werden, wird die große 5-jährige Osteopathie-Ausbildung vorausgesetzt. Diese habe ich nicht, da sie“ (abgeschnitten) |
| /faq/ (Übersicht) | FAQ-Liste | Frage + Antwort wie bei 467 |
| /faq/haben-sie-die-grosse-heilpraktikerausbildung/ (464), /faq/sind-sie-mitglied-in-einem-verband/ (466), /faq/wie-lange-liegt-ihre-pruefung-schon-zurueck/ (465), /lexikon/heilpraktiker/ (33661), /lexikon/osteopathie/ (33666) | Linkliste „Weiterführende Fragen und Antworten“ | „Sind sie auch Mitglied in einem Osteopathie-Verband?“ |
| /lexikon/osteopathie/ (33666) | Fließtext | „Der Osteopath arbeitet ausschließlich mit seinen Händen: Er erspürt Spannungen, Blockaden und Bewegungseinschränkungen im Gewebe – in Muskeln, Faszien, Organen und am Schädel – und löst diese durch gezielte, sanfte Techniken.“ |
| /faszium-konzept/ (33736) | Fließtext | „Das faszium-Konzept ist aus der jahrelangen Erfahrung von Physiotherapeuten und Osteopathen entstanden.“ |
| /rueckenschmerzen/ (33800) | Fließtext | „Je nach Ursache kommen Hausarzt, Orthopäde, Osteopath oder Heilpraktiker in Frage.“ |

Keine Treffer für „Diplom“, „Studium/studiert“, „zertifiziert“ oder „D.O.“ in Verbindung mit Osteopathie. „Zertifizierter Hypnotiseur“ auf /ueber-mich/ betrifft nicht die Osteopathie.
