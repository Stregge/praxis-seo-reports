# 07.10.2026 – 404-Quellen, Bilder-Abruf, Rank-Math-Einstellungen, Wortlaut „Osteopath…“
_Nur gelesen. Nichts geändert, nichts umgesetzt._

## ⚠ Zwischenfall während der Prüfung: Website ca. 17:50–18:59 nicht erreichbar (502)
- nginx meldete `connect() failed (111: Connection refused) while connecting to upstream` (Apache-Backend `188.68.47.48:7081`). Zwischen 17:49 und 18:59 kam beim Apache keine einzige Anfrage an. Ab 18:59 lief die Seite wieder, alle Kontrollabrufe danach liefern 200.
- **Ursache auf Hosting-Seite**, nicht in WordPress: kein Eintrag im WordPress-Fehlerlog, keine Plugin- oder Core-Änderung seit 14:06. Die nginx-Prozess-IDs waren neu, was auf einen Dienst-Neustart hinweist. Auf netcup-status.de ist keine passende Störung gemeldet.
- Empfehlung: bei Netcup nachfragen (Zeitraum 07.10., ca. 17:50–18:59), ggf. einen Uptime-Monitor einrichten.

---

## Teil A: 404-Adressen aus der Search Console

### Statuscodes (live)
Alle 8 Adressen liefern **404**.

### Interne Links auf diese Adressen
**Keine.** Durchsucht habe ich:
- alle Beiträge, Seiten und CPTs (`post_content`)
- alle Postmeta, also auch die Bricks-Felder von Kontakt, Ablauf, Über mich, Home, Header und Footer
- alle Menüpunkte (`_menu_item_url`: nur /lexikon/ und /faq/)
- alle Optionen
- alle Revisionen

Die einzigen Datenbank-Treffer sind **alte SEOPress-404-Protokolleinträge** (Beitragstyp `seopress_404`, 1.030 Stück, SEOPress inaktiv). Als „Referer“ haben sie nur die Adresse selbst gespeichert:

| Adresse | SEOPress-Eintrag (ID, erster Zugriff, Zähler) |
|---|---|
| /Heilpraktiker.html | 32706, 25.04.2026, 38 Aufrufe |
| /de/ | (32838 betrifft `/de/de`, 02.05., 2 Aufrufe; `/de/` selbst nicht erfasst) |
| /redirect-arthrose-protokoll-heilpraktiker | 33469, 18.05.2026, 4 |
| /redirect-ernaehrung-bei-arthrose-… | 33470, 18.05.2026, 4 |
| /redirect-hueftarthrose-schulterarthrose-naturheilkunde | 33471, 18.05.2026, 2 |
| /redirect-arthrose-schlafen-tipps | 33472, 18.05.2026, 3 |
| /redirect-saeure-basen-haushalt-arthrose | 33473, 18.05.2026, 4 |
| /redirect-faszientherapie-arthrose | 33474, 18.05.2026, 2 |

Die `redirect-…`-Adressen wurden alle am 18.05. binnen einer Minute aufgerufen. Das spricht für frühere Platzhalter-Slugs beim Anlegen der Arthrose-Artikel, die Google damals gefunden hat, nicht für aktuelle Links.

### Rank Math: 404-Monitor und Weiterleitungen
- **404-Monitor:** Die Einträge zu den 8 Adressen stammen **nur von meinen eigenen Statusabrufen** am 07.10. um 14:39 (bzw. 2 Aufrufe inkl. eines vorherigen). Das Log reicht nur bis 05.10. zurück (Limit 100 Einträge, Modus „simple“).
- **Weiterleitung #27 liegt im Papierkorb** (seit 24.07.2026, vorher 1.123 Treffer). Sie ist ein Sammel-Redirect mit **67 Mustern → Startseite**, darunter:
  - `redirect-ernaehrung-bei-arthrose-was-wirklich-hilft-und-was-du-meiden-solltest/`
  - `redirect-saeure-basen-haushalt-arthrose/`
  - `redirect-faszientherapie-arthrose/`
  - außerdem viele Alt-Adressen der früheren Website (`de/de`, `Presse.html`, `news/reader`, `therapien/`, `airnergy/` …). Stichprobe: alle jetzt 404.
- Weiterleitung #12 (aktiv) leitet nur `meine-praxis/gesundheitstipps/Heilpraktiker.html` → /ueber-mich/, **nicht** `/Heilpraktiker.html`.
- Weiterleitung #3 (Papierkorb, 46 Treffer) → /ganzheitliche-arthrose-therapie/; Muster nicht geprüft.

### Vorschlag pro Adresse (nicht umgesetzt)
| Adresse | Vorschlag | Ziel (live 200) |
|---|---|---|
| /redirect-saeure-basen-haushalt-arthrose/ | 301 | /saeure-basen-haushalt-arthrose/ (Post 32364) |
| /redirect-ernaehrung-bei-arthrose-was-wirklich-hilft-und-was-du-meiden-solltest/ | 301 | /ernaehrung-bei-arthrose-was-wirklich-hilft-und-was-du-meiden-solltest/ (Post 31403) |
| /redirect-arthrose-protokoll-heilpraktiker/ | 301 | /arthrose-protokoll-heilpraktiker/ (Post 32363) |
| /redirect-arthrose-schlafen-tipps/ | 301 | /arthrose-schlafen-tipps/ (Post 32358) |
| /redirect-hueftarthrose-schulterarthrose-naturheilkunde/ | 301 | /hueftarthrose-schulterarthrose-naturheilkunde/ (Post 32361) |
| /redirect-faszientherapie-arthrose/ | 301 | /faszientherapie-arthrose/ (Post 32360) |
| /Heilpraktiker.html | 301 | / (Startseite). Alternative: /ueber-mich/ wie bei Redirect #12. Mit 38 Aufrufen die meistgenutzte Alt-Adresse. |
| /de/ | 301 | / (Startseite; Sprachpräfix der alten Website) |

Ein Link auf einer Quellseite muss nirgends korrigiert werden, weil keine Quellseite verlinkt.
Gezielte Einzel-301s sind besser, als Sammel-Redirect #27 wiederherzustellen: Der leitete die Arthrose-Adressen nur auf die Startseite.
Ob die übrigen ~60 Alt-Muster aus #27 eine Weiterleitung brauchen, wäre eine eigene Entscheidung. Die Search Console meldet bisher nur die 8 obigen.

---

## Teil B: Bilder
5 zufällige Bilder aus der Mediathek (271 Bilder), abgerufen mit Browser-, Googlebot- und Googlebot-Image-User-Agent:

| Bild | Browser | Googlebot | Googlebot-Image |
|---|---|---|---|
| /wp-content/uploads/instagram-icon.svg | 200 | 200 | 200 |
| /wp-content/uploads/weitere-untersuchungen.png | 200 | 200 | 200 |
| /wp-content/uploads/faszien_nacken-1.webp | 200 | 200 | 200 |
| /wp-content/uploads/dorn-therapie.png | 200 | 200 | 200 |
| /wp-content/uploads/faszien_nacken.png | 200 (1,5 MB) | 200 | 200 |

**robots.txt:** `Allow: /wp-content/uploads/` – Bilder sind erlaubt.

Nebenbefunde:
- Die robots.txt **sperrt `/wp-content/themes/` und `/wp-content/plugins/`**. Google kann damit CSS- und JS-Dateien von Bricks und den Plugins nicht abrufen, was das Rendering der Seiten für Google beeinträchtigen kann. Die robots.txt kommt aus WPCodeBox-Snippet #13.
- Der Sitemap-Eintrag in der robots.txt lautet `/sitemap.xml`; Rank Math nutzt `/sitemap_index.xml`. Nicht geprüft, ob `/sitemap.xml` weiterleitet.
- WebP-Bilder werden ohne `Content-Type`-Header ausgeliefert (bekannt, Server-Konfiguration).

---

## Teil C: Rank-Math-Einstellungen

### Lokales SEO
| Feld | Wert | Abgleich |
|---|---|---|
| Firmenname (`knowledgegraph_name`) | Naturheilpraxis Strähuber | ✔ |
| Adresse | Wasentegernbach 45, 84405 Dorfen, Bayern, „Deutschland“ | ✔ (Land als Wort statt „DE“) |
| Telefon | 08082 4249-608 (customer support) | ✔ wie Website. Die Meta-Description von /kontakt/ nennt dagegen **08081 / 954 89 89** |
| E-Mail | info@nhp-straehuber.de | ✔ |
| Öffnungszeiten | Mo 08:00–12:00 + 13:00–19:30 · Di 07:30–12:15 · Mi 07:30–12:00 + 13:00–17:30 · Do 07:30–12:15 · Fr 07:30–12:00 + 13:00–17:30 | ✔ (Stand von heute) |
| Geschäftsart | MedicalBusiness | – |
| Geo | 48.27568, 12.21906 | weicht von **Snippet #12** ab (dort 48.2669, 12.1628, ca. 4 km westlich) |
| Website-Name | „Naturheilpraxis Strähuber von Heilpraktiker Roland“ | wirkt abgeschnitten (Nachname fehlt) |
| Beschreibung | „Naturheilpraxis von Heilpraktiker Roland Strähuber in Dorfen bei Erding. Osteopathie, Faszientherapie und Dorn-Methode vor Ort, Mikronährstoffanalyse mit Videosprechstunde.“ | – |

### Analysen (Search Console)
- **Verbunden:** Profil `sc-domain:naturheilpraxis-straehuber.de`, OAuth-Token vorhanden (Wert nicht ausgegeben).
- **Daten von 10.04.2026 bis 04.10.2026** (2.610 Zeilen). In der Tabelle tauchen nur 6 verschiedene `page`-Werte auf; das wirkt wenig, Ursache nicht geprüft.
- Google Analytics ist **nicht** verbunden (siehe Bericht vom Vormittag).

### Bilder-SEO
- „Fehlende ALT-Attribute hinzufügen“: **an**, Format **`%filename%`**
- „Fehlende Title-Attribute hinzufügen“: **an**, Format **`%filename%`**
- Caption und Description: aus
- Diese Rank-Math-Funktion ergänzt nur **fehlende** Alt-Texte beim Ausgeben der Seite; vorhandene Alt-Texte überschreibt sie nicht. Eine Überschreiben-Option ist nicht gesetzt (`image_replacements` leer).

### 404-Monitor – Top 10
Modus „simple“, Limit 100, Log seit 05.10.2026 (60 Einträge). Alle Einträge haben maximal 2 Aufrufe; die meisten sind Bot-Scans.

| URI | Aufrufe | zuletzt |
|---|---|---|
| core/install.php | 2 | 06.10. 07:01 |
| wp-content/plugins/bricksforge/readme.txt | 2 | 06.10. 07:01 |
| administrator/manifests/files/joomla.xml | 2 | 06.10. 07:01 |
| config.toml | 2 | 06.10. 07:01 |
| redirect-hueftarthrose-schulterarthrose-naturheilkunde | 2 | 07.10. 14:39 (meine Prüfung) |
| contact | 2 | 06.10. 18:08 |
| magento_version | 2 | 06.10. 07:01 |
| .svn/pristine | 2 | 06.10. 05:44 |
| wp-content/plugins/wpappninja/readme.txt | 2 | 06.10. 03:38 |
| news/reader/Herbstkur.html | 2 | 06.10. 14:57 |

### Eingebettete Videos
**Keine.** Durchsucht wurden alle 207 Sitemap-URLs (gerendertes HTML) und die Datenbank.
- Es gibt keine YouTube-, Vimeo- oder `<video>`-Einbettung und keinen Borlabs-Content-Blocker für YouTube oder Vimeo.
- Die Content-Blocker auf allen Seiten sind seitenweite Vorlagen (Captcha, OpenStreetMap, Google Maps, Facebook) und das Lapsula-Buchungs-Widget.
- YouTube erscheint nur als Kanal-Link im Footer (`youtube.com/c/SträhuberRolandDorfen`).
- Eine Video-Sitemap bringt daher aktuell nichts.

---

## Teil D: Wortlaut „Osteopath / Osteopathin / Osteopathie / osteopathisch“
Quelle: gerenderter Hauptinhalt (`<main>`) aller 207 Sitemap-URLs plus Title und Meta-Description. Header, Footer und Navigation habe ich nicht mitgezählt.
- 181 Fundstellen auf 106 Seiten, davon **98 verschiedene Sätze**.
- Zwei Sätze stammen aus wiederkehrenden Bausteinen:
  - „Seine Schwerpunkte liegen in der Osteopathie, Faszientherapie, Spagyrik und Dorn-Therapie.“ (Autorenbox, 70 Seiten)
  - „Weiterführende Fragen und Antworten: … Sind sie auch Mitglied in einem Osteopathie-Verband?“ (FAQ-Linkliste, 6 Seiten)
- „ID“ ist die Post-/Seiten-ID aus dem Body-Tag. Startseite (ID 12) und /therapie/osteopathie/ (ID 291) stehen oben.
- Nicht bewertet, nur gelistet.

| # | Wort | Satz / Kontext | Seite(n) (ID) |
|---|---|---|---|
| 1 | osteopathie | Mehr erfahren Osteopathie Bei der Osteopathie handelt es sich um eine sanfte Form der Medizin, die auf das Erkennen und Behandeln von Funktionsstörungen und Strukturstörungen ausgerichtet ist. | / (ID 12) |
| 2 | [META] | Naturheilpraxis Strähuber in Dorfen bei Erding: Osteopathie, Faszientherapie, Dorn-Methode und Mikronährstoffanalyse. Heilpraktiker Roland Strähuber – persönlich, ganzheitlich, erfahren. | / (ID 12) |
| 3 | osteopathie | Osteopathie – den Patienten als Ganzes betrachten, um Ursachen von Schmerzen zu erkennen Die Osteopathie ist eine medizinische Behandlungsform, in der durch manuelle Techniken körperliche Funktionsstörungen und Blockaden behandelt werden. | /therapie/osteopathie/ (ID 291) |
| 4 | osteopathie | Erstgespräch vereinbaren Mehr erfahren Die 5 Grundprinzipien der Osteopathie Bewegung ist leben Alles im Körper muss beweglich sein. | /therapie/osteopathie/ (ID 291) |
| 5 | osteopathische | Osteopathische Techniken helfen dabei, die ursprüngliche Bewegungsfähigkeit wieder herzustellen, damit alles wieder optimal funktioniert. | /therapie/osteopathie/ (ID 291) |
| 6 | osteopathie | In der Osteopathie wird versucht, eine ideale Ver- und Entsorgung aller Strukturen mit Körperflüssigkeiten sicherzustellen, um so eine ideale Funktion des Körpers zu erreichen. | /therapie/osteopathie/ (ID 291) |
| 7 | osteopathie | Deshalb werden in der Osteopathie nie einzelne Beschwerden behandelt, sondern immer der Mensch in seiner Gesamtheit. | /therapie/osteopathie/ (ID 291) |
| 8 | osteopathie | Mit der Osteopathie wird die Beweglichkeit des Gewebes und die Zirkulation der Körperflüssigkeiten wiederhergestellt, sodass die natürlichen Heilungsprozesse im Körper unterstützt | /therapie/osteopathie/ (ID 291) |
| 9 | osteopathie | 5 Erstgespräch vereinbaren Bei welchen Beschwerden kann die Osteopathie hilfreich sein? | /therapie/osteopathie/ (ID 291) |
| 10 | osteopathische | hmerzen Muskelverspannungen Verdauungsprobleme Reizdarm Blähungen Verstopfungen Atemwegsprobleme Asthma Chronische Bronchitis Sinusitis Kopfschmerzen / Migräne Osteopathische Behandlungen im Bereich des Nackens und der Wirbelsäule können zu einer Verbesserung von Kopfschmerzen und Migräne führen. | /therapie/osteopathie/ (ID 291) |
| 11 | osteopathie | Stress Osteopathie kann als entspannende Therapie betrachtet werden, die dazu beitragen kann, Stress abzubauen und das allgemeine Wohlbefinden zu fördern. | /therapie/osteopathie/ (ID 291) |
| 12 | [META] | Osteopathie Dorfen – den Patienten als Ganzes betrachten | /therapie/osteopathie/ (ID 291) |
| 13 | [META] | Sie sind auf der Suche nach einen Osteopathen? In meiner Naturheilpraxis wende ich Osteopathie seit Jahren erfolgreich an. Erfahren Sie mehr über diese Methode | /therapie/osteopathie/ (ID 291) |
| 14 | osteopathie | Seine Schwerpunkte liegen in der Osteopathie, Faszientherapie, Spagyrik und Dorn-Therapie. | 70 Seiten, u. a. /aminosaeuren-die-unsichtbaren-kraftwerke-unseres-koerpers/ (ID 5099), /amsat-messung-arthrose/ (ID 32357), /arthrose-knie-heilpraktiker/ (ID 32356) |
| 15 | osteopathie | Weiterführende Fragen und Antworten: Heilpraktiker Sind sie auch Mitglied in einem Osteopathie-Verband? | 6 Seiten, u. a. /faq/ (ID ?), /faq/ (ID ?), /faq/ (ID ?) |
| 16 | osteopathie | rat und Gelenke Ängste, Sorgen und Depressionen Stress, Burnout und Erschöpfung Hormonbedingte Beschwerden Beschwerden im Kindesalter Therapien Faszientherapie Osteopathie Dorn Therapie Spagyrik Gesprächstherapie Ablauf Über mich Kontakt Start Beschwerden Atembeschwerden und Lungenerkrankungen Unerklärliche Beschwerden Entwicklun | /arthrose-heilpraktiker-erding/ (ID 32515), /heilpraktiker-muenchen-ost/ (ID 32518), /spagyrik/ (ID 32520) |
| 17 | osteopathie | Gelenke Ängste, Sorgen und Depressionen Stress, Burnout und Erschöpfung Hormonbedingte Beschwerden Beschwerden im Kindesalter Therapiemethoden Faszientherapie Osteopathie Dorn Therapie Spagyrik Gesprächstherapie Wichtige Infos Ratgeber FAQ Lexikon Ablauf Über mich Kontakt © 2026 - Naturheilpraxis Strähuber Impressum / Datenschut | /arthrose-heilpraktiker-erding/ (ID 32515), /heilpraktiker-muenchen-ost/ (ID 32518), /spagyrik/ (ID 32520) |
| 18 | osteopathie | Um Mitglied in einem solchen Osteopathie-Verband zu werden, wird die große 5-jährige Osteopathie-Ausbildung vorausgesetzt. | /faq/ (ID ?), /faq/sind-sie-auch-mitglied-in-einem-osteopathie-verband/ (ID 467) |
| 19 | osteopathische | Diese habe ich nicht, da sie für mich nicht relevant war und ich trotzdem viele osteopathische Techniken erlernt habe. | /faq/ (ID ?), /faq/sind-sie-auch-mitglied-in-einem-osteopathie-verband/ (ID 467) |
| 20 | osteopathie | Weiterführende Fragen und Antworten: Heilpraktiker Osteopathie Sind sie Mitglied in einem Verband? | /faq/ (ID ?), /faq/sind-sie-auch-mitglied-in-einem-osteopathie-verband/ (ID 467) |
| 21 | osteopathie | Osteopathie und Faszientherapie bei akutem Hexenschuss Bei einem akuten Hexenschuss können manuelle Therapien wie die Osteopathie und Faszientherapie sehr wirksam sein. | /hexenschuss-was-tun/ (ID 30992), /hexenschuss-was-tun/ (ID 30992) |
| 22 | osteopathie | Durch ganzheitliche Ansätze wie Osteopathie, Faszientherapie, Gesprächstherapie und die Betrachtung der psychosomatischen Zusammenhänge kann die Behandlung dazu beitragen, nicht nur die akuten Beschwerde | /hexenschuss-was-tun/ (ID 30992), /hexenschuss-was-tun/ (ID 30992) |
| 23 | osteopathie | rat und Gelenke Ängste, Sorgen und Depressionen Stress, Burnout und Erschöpfung Hormonbedingte Beschwerden Beschwerden im Kindesalter Therapien Faszientherapie Osteopathie Dorn Therapie Spagyrik Gesprächstherapie Ablauf Über mich Kontakt Arthrose-Heilpraktiker für Erding / Naturheilpraxis Strähuber Naturheilkundliche Arthrose -Be | /arthrose-heilpraktiker-erding/ (ID 32515) |
| 24 | osteopathie | Durch gezielte manuelle Therapien (wie Osteopathie oder Faszientherapie ) und spezielle Dehnübungen können wir diese Spannungen lösen. | /arthrose-ohne-op-behandeln-naturheilkundliche-alternativen-zum-gelenkersatz/ (ID 31408) |
| 25 | osteopathie | In der Praxis sorgen wir mit Osteopathie , Faszientherapie bei Arthrose , Spagyrik und gezielter Ernährung bei Arthrose dafür, dass die Schmerzen weniger werden und die Beweglichkeit wiederkommt. | /arthrose-uebungen-zuhause/ (ID 32407) |
| 26 | osteopathie | Ganzheitliche Unterstützung Nach ärztlichem Ausschluss einer akuten Notfallsituation kann eine manuelle Behandlung – etwa mit der Dorn-Methode oder Osteopathie – helfen, blockierte Segmente der Lendenwirbelsäule zu mobilisieren und die umliegende Muskulatur zu entlasten. | /bandscheibenvorfall-lws-syndrom/ (ID 33802) |
| 27 | osteopathie | Osteopathie – Lösen, was festgehalten wird In der Osteopathie geht es darum, Blockaden zu erkennen und zu lösen. | /behandlung-bei-rueckenschmerzen/ (ID 20423) |
| 28 | osteopathische | Passende Ratgeber-Artikel Osteopathische Lungenmassage nach Atemnot Wasserfasten mit St. | /beschwerde/atem-und-chronische-bronchitis/ (ID 741) |
| 29 | [META] | Rückenschmerzen, Arthrose, Rheuma & Gelenkschmerzen natürlich behandeln. Heilpraktiker Roland Strähuber in Dorfen hilft mit Osteopathie & Faszientherapie. | /beschwerde/bewegungsapparat-und-gelenke/ (ID 246) |
| 30 | osteopathische | Nächster Artikel Osteopathische Lungenmassage nach Atemnot Kommentare (Antwort abbrechen) Name * E-Mail * Website Meinen Namen, E-Mail und Website in diesem Browser speichern, bis ich wieder | /die-fatigue-ein-missverstandenes-erschoepfungssyndrom/ (ID 844) |
| 31 | osteopathie | Sind sie auch Mitglied in einem Osteopathie-Verband? | /faq/ (ID ?) |
| 32 | osteopathie | wahre Lebensfreude und menschliche Verbundenheit in Freiheit Omega-3 – Öl des Lebens: für mehr Gesundheit Weiterführende Fragen und Antworten: Faszientherapie Osteopathie Dorn-Therapie Machen Sie den wichtigen ersten Schritt und kontaktieren Sie mich. | /faq/ (ID ?) |
| 33 | osteopathie | wahre Lebensfreude und menschliche Verbundenheit in Freiheit Omega-3 – Öl des Lebens: für mehr Gesundheit Weiterführende Fragen und Antworten: Faszientherapie Osteopathie Dorn-Therapie | /faq/gibt-es-zu-ihren-behandlungsmethoden-auch-weiterfuehrende-literatur-die-sie-mir-empfehlen-koennen/ (ID 482) |
| 34 | [META] | Sind sie auch Mitglied in einem Osteopathie-Verband? – FAQ / Naturheilpraxis Strähuber Dorfen | /faq/sind-sie-auch-mitglied-in-einem-osteopathie-verband/ (ID 467) |
| 35 | [META] | Nein. Um Mitglied in einem solchen Osteopathie-Verband zu werden, wird die große 5-jährige Osteopathie-Ausbildung vorausgesetzt. Diese habe ich nicht, da sie | /faq/sind-sie-auch-mitglied-in-einem-osteopathie-verband/ (ID 467) |
| 36 | osteopathie | Faszientherapie in meiner Praxis in Dorfen In meiner Naturheilpraxis behandle ich Faszienbeschwerden nach dem faszium-Konzept – der Essenz aus Osteopathie , Physiotherapie und manuellen Faszientechniken. | /faszien-ratgeber/ (ID 33737) |
| 37 | osteopathie | Ich arbeite nach dem faszium-Konzept , einer Methode, die Osteopathie , Physiotherapie und manuelle Faszientechniken verbindet. | /faszientherapie/ (ID 33735) |
| 38 | osteopathie | Als Heilpraktiker behandle ich Faszien - und Bewegungsbeschwerden nach dem faszium-Konzept – einer Verbindung aus Osteopathie , Physiotherapie und gezielten manuellen Faszientechniken. | /faszientherapie-muenchen-ost/ (ID 33734) |
| 39 | osteopathen | Die Essenz aus drei Welten Das faszium-Konzept ist aus der jahrelangen Erfahrung von Physiotherapeuten und Osteopathen entstanden. | /faszium-konzept/ (ID 33736) |
| 40 | osteopathie | Es vereint drei bewährte Welten zu einem Ganzen: die Physiotherapie mit ihrem Wissen über Bewegung und Muskulatur, die Osteopathie mit ihrem ganzheitlichen Blick auf den Körper, und gezielte manuelle Faszientechniken , die direkt am Bindegewebe arbeiten. | /faszium-konzept/ (ID 33736) |
| 41 | osteopathie | Manuelle Therapien: Osteopathie und Faszientherapie Um den enormen Druck von den Gelenken zu nehmen, müssen wir die muskulären und faszialen Spannungen lösen. | /ganzheitliche-arthrose-therapie/ (ID 10649) |
| 42 | osteopathischen | Mit sanften osteopathischen Techniken und gezielter Faszientherapie arbeite ich daran, Verklebungen zu lösen und die natürliche Beweglichkeit wiederherzustellen. | /ganzheitliche-arthrose-therapie/ (ID 10649) |
| 43 | osteopathie | In meiner Praxis arbeite ich bei Schulterarthrose intensiv mit Faszientherapie und Osteopathie, um die Schulterblatt-Stabilisatoren zu entlasten und die Beweglichkeit wiederherzustellen. | /ganzheitliche-arthrose-therapie/ (ID 10649) |
| 44 | [META] | Arthrose ganzheitlich behandeln: Ernährung, Naturheilkunde, Osteopathie. Heilpraktiker Roland Strähuber in Dorfen erklärt seinen Ansatz — mehr als nur… | /ganzheitliche-arthrose-therapie/ (ID 10649) |
| 45 | osteopathische | Mehr ueber Roland Straehuber → Beitrag teilen: Vorheriger Artikel Osteopathische Lungenmassage nach Atemnot Nächster Artikel Was kann ich tun bei Rückenschmerzen? | /habe-ich-eine-stille-entzuendung-in-meinem-koerper/ (ID 605) |
| 46 | osteopathie | rat und Gelenke Ängste, Sorgen und Depressionen Stress, Burnout und Erschöpfung Hormonbedingte Beschwerden Beschwerden im Kindesalter Therapien Faszientherapie Osteopathie Dorn Therapie Spagyrik Gesprächstherapie Ablauf Über mich Kontakt Naturheilpraxis für München Ost / Heilpraktiker Strähuber Naturheilpraxis für Patienten aus M | /heilpraktiker-muenchen-ost/ (ID 32518) |
| 47 | osteopathie | rbelsäule und des Beckens Gezielte Dehnung des Piriformis-Muskels Wärme zur Entspannung der umliegenden Muskulatur Manuelle Techniken wie die Dorn-Methode oder Osteopathie zur Lösung blockierter Gelenke (→ Übungen mit Video-Anleitung findest du im Rücken-Übungen-Ratgeber ) Ischias bei Senioren Gerade bei älteren Patientinnen und | /ischias-ischiasnerv/ (ID 33801) |
| 48 | osteopathie | Erding, Poing und dem Münchner Osten gut erreichbar) schauen wir uns gezielt an, welche Struktur die Reizung tatsächlich auslöst, und setzen mit Dorn-Methode, Osteopathie und Faszientherapie direkt dort an. | /ischias-ischiasnerv/ (ID 33801) |
| 49 | osteopathischen | Gerade in Verbindung mit spagyrischen Anwendungen und osteopathischen Therapien kann das Fasten eine wunderbare Ergänzung zu deinem ganzheitlichen Gesundheitskonzept sein. | /intervallfasten-eine-uralte-methode-fuer-moderne-gesundheit/ (ID 10331) |
| 50 | osteopathische | In meiner Praxis verbinde ich osteopathische und fasziale Therapie mit ganzheitlicher Beratung, um Körper und Geist in Balance zu bringen. | /intervallfasten-eine-uralte-methode-fuer-moderne-gesundheit/ (ID 10331) |
| 51 | osteopathie | agen Kortisol L Laktat (Milchsäure) Latente Azidose Low-Grade-Inflammation M Magnesium Mitochondrien N Nachtschmerz Nebennieren O Omarthrose Omega-3-Fettsäuren Osteopathie Osteoporose Oxidativer Stress P Parasympathikus Photobiomodulation Propriozeption R Rheuma S Schlafapnoe Schlafqualität und Schmerz Schlafstörungen Sehnenschei | /lexikon/ (ID ?) |
| 52 | osteopathie | Naturheilkundliche Ansätze wie Osteopathie (zur Entlastung der Gelenke), Rotlichttherapie (zur Durchblutungsförderung und Entzündungshemmung) und Spagyrik (zur Unterstützung des Stoffwechsels) können da | /lexikon/arthrose/ (ID 33655) |
| 53 | osteopathie | In vielen Fällen können naturheilkundliche Methoden helfen: Osteopathie löst Blockaden und Fehlhaltungen, die die Bandscheibe belasten. | /lexikon/bandscheibenvorfall/ (ID 33657) |
| 54 | osteopathie | Manuelle Therapie – Osteopathie , Faszienbehandlung oder Dorn-Therapie können helfen, strukturelle Ungleichgewichte zu lösen. | /lexikon/dysbalancen/ (ID 19905) |
| 55 | osteopathie | In der Naturheilkunde behandeln wir Fibromyalgie ganzheitlich: Sanfte Körpertherapien wie Faszientherapie und Osteopathie können das Nervensystem beruhigen. | /lexikon/fibromyalgie/ (ID 33660) |
| 56 | osteopathie | Mein Ansatz umfasst Ernährungsanpassung zur Reduktion von Entzündungen, manuelle Therapien ( Osteopathie , Faszientherapie ), gezielte Bewegungsübungen und naturheilkundliche Unterstützung ( Spagyrik , Phytotherapie). | /lexikon/gonarthrose/ (ID 31477) |
| 57 | osteopathie | 👉 Mehr über mich und meinen Ansatz Weiterführende Fragen und Antworten: Sind sie auch Mitglied in einem Osteopathie-Verband? | /lexikon/heilpraktiker/ (ID 33661) |
| 58 | osteopathie | Hier setzt Osteopathie und Faszientherapie an – um nicht nur den Schmerz zu lösen, sondern den nächsten Hexenschuss zu verhindern. | /lexikon/hexenschuss/ (ID 33674) |
| 59 | osteopathie | Je nach Befund kommen Osteopathie , Dorn-Therapie oder Faszientherapie zum Einsatz – oft mit schneller spürbarer Wirkung. | /lexikon/ischias/ (ID 33673) |
| 60 | osteopathie | In Kombination mit Faszientherapie und Osteopathie lässt sich die Qualität des Bindegewebes spürbar verbessern. | /lexikon/kollagen/ (ID 33663) |
| 61 | osteopathie | Osteopathie Osteopathie ist eine ganzheitliche manuelle Therapieform, die davon ausgeht, dass Körper, Geist und Seele eine Einheit bilden – und dass der Körper grundsätzlich in der La | /lexikon/osteopathie/ (ID 33666) |
| 62 | osteopath | Der Osteopath arbeitet ausschließlich mit seinen Händen: Er erspürt Spannungen, Blockaden und Bewegungseinschränkungen im Gewebe – in Muskeln, Faszien , Organen und am Schäd | /lexikon/osteopathie/ (ID 33666) |
| 63 | osteopathie | Osteopathie kann bei vielen Beschwerden helfen: Rückenschmerzen, Kopfschmerzen, Verdauungsproblemen, Gelenkbeschwerden, Erschöpfung – und sogar bei Beschwerden, die schein | /lexikon/osteopathie/ (ID 33666) |
| 64 | osteopathie | Die Osteopathie denkt in diesen Zusammenhängen. | /lexikon/osteopathie/ (ID 33666) |
| 65 | osteopathie | 👉 Mehr zur Osteopathie in der Praxis Weiterführende Fragen und Antworten: Sind sie auch Mitglied in einem Osteopathie-Verband? | /lexikon/osteopathie/ (ID 33666) |
| 66 | [META] | Osteopathie – Lexikon / Naturheilpraxis Strähuber | /lexikon/osteopathie/ (ID 33666) |
| 67 | [META] | Osteopathie ist eine ganzheitliche manuelle Therapieform, die davon ausgeht, dass Körper, Geist und Seele eine Einheit bilden – und dass der Körper | /lexikon/osteopathie/ (ID 33666) |
| 68 | osteopathie | Naturheilkundliche Ansätze wie entzündungshemmende Ernährung, spagyrische Mittel , Faszientherapie und Osteopathie können die Lebensqualität deutlich verbessern – oft ohne die Nebenwirkungen schulmedizinischer Dauertherapien. | /lexikon/rheuma/ (ID 33667) |
| 69 | osteopathie | 👉 Beschwerden am Bewegungsapparat – mein Behandlungsansatz Vorheriger Artikel Osteopathie Nächster Artikel Serotonin Machen Sie den wichtigen ersten Schritt und kontaktieren Sie mich. | /lexikon/rheuma/ (ID 33667) |
| 70 | osteopathie | Osteopathie kann das vegetative Nervensystem regulieren. | /lexikon/schlafstoerungen/ (ID 33680) |
| 71 | osteopathie | Faszientherapie und Osteopathie können die Ursache lösen – ergänzend helfen spagyrische Mittel dabei, die Entzündung zu dämpfen. | /lexikon/sehnenscheidenentzuendung/ (ID 33676) |
| 72 | osteopathie | Und Osteopathie stellt sicher, dass keine Blockierungen in Ellenbogen, Schulter oder Halswirbelsäule die Heilung behindern. | /lexikon/tennisarm/ (ID 33677) |
| 73 | osteopathie | In der ganzheitlichen Naturheilkunde verbinden wir körperorientierte Therapien wie Osteopathie mit der Gesprächstherapie – um Heilung auf allen Ebenen zu ermöglichen. | /lexikon/trauma/ (ID 33678) |
| 74 | osteopathie | In der Behandlung setzen wir auf manuelle Techniken aus der Faszientherapie und Osteopathie , die den Triggerpunkt gezielt lösen. | /lexikon/triggerpunkt/ (ID 33669) |
| 75 | osteopathie | In der Osteopathie gibt es spezifische Techniken, um den Vagusnerv über den Schädel und den Hals zu stimulieren. | /lexikon/vagusnerv/ (ID 33670) |
| 76 | osteopathie | In der Naturheilkunde behandeln wir vegetative Dysregulation ganzheitlich: Osteopathie reguliert das Nervensystem über direkte manuelle Arbeit. | /lexikon/vegetative-dysregulation/ (ID 33679) |
| 77 | osteopathie | In meiner Praxis ist die Regulierung des vegetativen Nervensystems ein zentrales Ziel – durch Osteopathie (die das Nervensystem direkt beeinflusst), spagyrische Mittel und gezielte Entspannungsarbeit. | /lexikon/vegetatives-nervensystem/ (ID 33665) |
| 78 | osteopathie | 👉 Stress und Erschöpfung – mein Behandlungsansatz Vorheriger Artikel Magnesium Nächster Artikel Osteopathie Machen Sie den wichtigen ersten Schritt und kontaktieren Sie mich. | /lexikon/vegetatives-nervensystem/ (ID 33665) |
| 79 | osteopathie | In meiner Praxis behandle ich die Wirbelsäule mit Osteopathie , Dorn-Therapie und Faszientherapie – immer mit dem Ziel, nicht nur das Symptom zu lindern, sondern die Ursache der Fehlbelastung zu finden. | /lexikon/wirbelsaeule/ (ID 33671) |
| 80 | osteopathie | Wichtig zu wissen: Manuelle Verfahren wie Osteopathie , Faszientherapie oder die Dorn-Methode benötigen zwingend eine persönliche Behandlung vor Ort in meiner Praxis in Dorfen – diese Verfahren lassen sich aus nac | /mikronaehrstoffanalyse/ (ID 33861) |
| 81 | osteopathie | r Praxis einsetze In meiner Naturheilpraxis in Dorfen setze ich die Pflaster auf verschiedene Weisen ein: als begleitende Unterstützung zur Faszientherapie und Osteopathie , bei Therapieblockaden, im Rahmen von Entgiftungsmaßnahmen. | /lifewave-pflaster-die-akupunktur-fuer-zu-hause/ (ID 933) |
| 82 | osteopathische | Wir werden uns dann die Körperstatik anschauen, ob funktionelle Themen dazu beitragen, über osteopathische und fasziale Techniken die verspannten Bereiche bearbeiten. | /nackenschmerzen-der-steife-nacken/ (ID 846) |
| 83 | osteopathische | April 2022 0 Kommentare 3 Minuten Osteopathische Lungenmassage nach Atemnot Sie leiden noch unter zeitweise oder dauerhafter Atemnot, nach ihrer Erkrankung? | /osteopathische-lungenmassage-nach-atemnot/ (ID 842) |
| 84 | osteopathie | Hier kann die Osteopathie gute Dienste leisten. | /osteopathische-lungenmassage-nach-atemnot/ (ID 842) |
| 85 | osteopathie | Die Osteopathie hat hier zum einen die Sparte der viszeralen-, das heißt auf die inneren Organe bezogene Osteopathie, aber auch die Faszien-Therapie. | /osteopathische-lungenmassage-nach-atemnot/ (ID 842) |
| 86 | [META] | Osteopathische Lungenmassage – Hilfe bei Atemnot | /osteopathische-lungenmassage-nach-atemnot/ (ID 842) |
| 87 | [META] | Osteopathische Lungenmassage bei Atemnot und Atemwegsbeschwerden: Wie sie wirkt und wem sie helfen kann. Aus meiner Praxis in Dorfen. | /osteopathische-lungenmassage-nach-atemnot/ (ID 842) |
| 88 | osteopathie | In meiner Praxis setze ich die Rotlichttherapie vor allem ergänzend ein – als Unterstützung zu Osteopathie , Faszientherapie und naturheilkundlichen Behandlungen. | /rotlichttherapie-rueckenschmerzen-gelenke/ (ID 33647) |
| 89 | osteopathischen | In Kombination mit osteopathischen Behandlungen erlebe ich oft eine deutlich schnellere Linderung als mit einzelnen Maßnahmen allein. | /rotlichttherapie-rueckenschmerzen-gelenke/ (ID 33647) |
| 90 | osteopathie | In meiner Praxis kombiniere ich Rotlicht je nach Beschwerdebild mit: Osteopathie – um Blockaden zu lösen und das Rotlicht tiefer wirken zu lassen Faszientherapie – um das Gewebe vorzubereiten und die Behandlung zu verlängern Spagyrik – pfla | /rotlichttherapie-rueckenschmerzen-gelenke/ (ID 33647) |
| 91 | osteopathie | Osteopathie : Ein ganzheitlicher Ansatz, der Wirbelsäule, Muskulatur, Faszien und innere Organe als zusammenhängendes System betrachtet. | /rueckenschmerzen/ (ID 33800) |
| 92 | osteopath | Je nach Ursache kommen Hausarzt, Orthopäde, Osteopath oder Heilpraktiker in Frage. | /rueckenschmerzen/ (ID 33800) |
| 93 | osteopathie | rat und Gelenke Ängste, Sorgen und Depressionen Stress, Burnout und Erschöpfung Hormonbedingte Beschwerden Beschwerden im Kindesalter Therapien Faszientherapie Osteopathie Dorn Therapie Spagyrik Gesprächstherapie Ablauf Über mich Kontakt Spagyrik: Wirkung, Anwendung & Essenzen / Naturheilpraxis Strähuber Spagyrik : Die ganzheitli | /spagyrik/ (ID 32520) |
| 94 | osteopathie | Äußerlich kann ich mit Faszientherapie , Osteopathie oder der Dorn-Therapie arbeiten. | /spagyrik-bei-arthrose/ (ID 32406) |
| 95 | osteopathie | Äußerlich schaue ich auf die klassischen Entzündungszeichen — und wenn ich über Osteopathie oder Faszientherapie am Gewebe arbeite, spüre ich, wie das Gewebe sich anfühlt. | /stille-entzuendung-arthrose/ (ID 32354) |
| 96 | osteopathie | Mehr erfahren Osteopathie Sanfte Hände, tiefe Heilung: Entdecken Sie die Vorteile der Osteopathie für Ihr Wohlgefühl. | /therapie/ (ID ?) |
| 97 | osteopathie | ) – Labordiagnostik und Diagnose aus dem Urin (2012/2013) Schmerz- und Bewegungstherapie Faszientherapie Konzept Modul 1-8 (2019) – Manuelle Therapien und AORT Osteopathie (2014-2018) – Dorn-Breuss-Therapie (2011/2012) Stoffwechsel, Ernaehrung und Hormone Ernaehrungsmedizin bei Prof. | /ueber-mich/ (ID 237) |
| 98 | [META] | Roland Strähuber ist Heilpraktiker in Dorfen – ausgebildet in Osteopathie, Faszientherapie & Psychotherapie. Erfahren Sie mehr über seinen ganzheitlichen… | /ueber-mich/ (ID 237) |

---
_DB-Zugangsdatei auf dem Hosting entfernt. Crawl mit max. 2 parallelen Abrufen, nur nach Wiederherstellung der Seite._
