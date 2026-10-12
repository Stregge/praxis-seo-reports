# MyMarky – Bestandsaufnahme (nur gelesen)
_Stand: 07.10.2026, ca. 13:00 Uhr · ausschließlich GET-Abfragen, nichts geändert, nichts angelegt, nichts veröffentlicht_

## 0. Zugang
- **Ja, auf der VPS gibt es einen Zugang:** einen API-Schlüssel (`mk_live_…`) in `/root/.env.marky` (chmod 600), die Business-ID in `wp_publish.py` und das installierte Claude-Code-Plugin „marky“ (v0.16.1). Den Schlüssel habe ich nicht ausgegeben und nirgends gespeichert.
- Das Marky-MCP ist in dieser Sitzung **nicht verbunden**; die Abfragen liefen über die REST-API (nur GET).
- Workspaces in der Organisation: **Naturheilpraxis Strähuber** (`cea7a7fc-…`), dazu „Darmkur – echt jetzt“, „Lebendig Gesund“ und „feeling“ (nicht geprüft).

## ⚠ Dringend: Es wird automatisch veröffentlicht
- Der **Posting-Plan ist aktiv (`paused: false`)**: täglich 14:00 UTC = **16:00 Uhr deutscher Zeit**.
- **3 Beiträge stehen in der Warteschlange (Status SCHEDULED):**

| Position | Geplant | Kanäle | Beitrag (Anfang) |
|---|---|---|---|
| 1 | **heute, 07.10., 16:00** | alle gültigen Kanäle (keine Einschränkung) | „Wenn Sie im Schichtdienst arbeiten …“ – Bild: **Stockfoto**, Mann in Sportkleidung an einer Hafenpromenade mit Großstadt-Skyline (kein Praxisbezug) |
| 2 | 08.10., 16:00 | LinkedIn-Profil, Facebook | „3 Einträge können Verstopfung in einem anderen Licht zeigen.“ (Video) |
| 3 | 09.10., 16:00 | LinkedIn-Profil, Facebook | „‚Hier ist es ganz anders, als ich es mir vorgestellt habe.‘“ (Video) |

- In den 50 neuesten Beiträgen gibt es **keinen einzigen Entwurf (NEW)**: 27 veröffentlicht, 3 eingeplant, 20 abgelehnt.
- Die 27 veröffentlichten Beiträge liefen vom **10.09. bis 06.10.2026**, fast täglich. Kanäle: Facebook 27, LinkedIn-Profil 26, Google Business 15.
- **Instagram ist als Verbindung „invalid“.** Auf Instagram ging nichts raus.

**Zur Projekteinstellung „Veröffentlichung“ (Entwurf oder automatisch):** Die API gibt diese Einstellung nicht als Feld aus. Ich kann sie also nicht direkt auslesen und weiß nicht, ob jeder Beitrag einzeln freigegeben wurde. **Das tatsächliche Verhalten spricht aber gegen „Entwurf“:** Der Zeitplan läuft, die Warteschlange ist gefüllt, und es wird täglich veröffentlicht. Ob jemand die 27 Beiträge vorher einzeln angenommen hat, geht aus den Daten nicht hervor. Bitte in der App prüfen: Business-Einstellungen und Posting-Plan.

## a) Markenprofil (Brand Kit) – aktueller Wortlaut der relevanten Felder
Zuletzt geändert: 06.10.2026, 14:01 UTC. Sprache: German.

**tone:**
> Ruhig, erfahren und ehrlich — ein Heilpraktiker, der Symptombilder kennt und einordnet, statt zu dramatisieren. Warm und auf Augenhöhe, verbindet Körperliches mit Seelischem, ohne ins Schwärmerische zu kippen. Erste Person Singular, konkret aus dem Praxisalltag in Dorfen/Erding, verständlich ohne Fachjargon. Einladend ohne Verkaufsdruck — und sagt auch, was ärztlich abgeklärt gehört.

**caption_writing_rules (Schreibregeln):**
> • Write captions of approximately 60–140 words; occasional short teaser posts with link/CTA are acceptable, but most posts are mid-length and reflective.
> • Open with a direct question, surprising statement, or body-focused hook that names a symptom, sensation, or insight.
> • Use short paragraphs with clear line breaks for a calm, easy-to-read flow.
> • Frequently frame symptoms as messages or signals from the body and connect physical complaints with emotional or inner states.
> • Use light emoji sparingly, typically 0–3 per post, often in the hook or before a gentle emphasis point.
> • When listing tips, causes, or examples, use bullet points or short enumerations.
> • End many captions with a reflective question, a gentle self-awareness prompt, or a soft invitation to pause and notice what the body is saying.
> • Use gentle, non-pushy calls to action for appointments, website visits, or blog links when relevant.
> • Hashtag use is typically heavy and placed at the end; combine topic-specific hashtags with the established brand hashtag block.
> • Ende jeden zweiten Post mit einer direkten Frage an die Leser, die sie einlädt, ihre Erfahrung in den Kommentaren zu teilen. Zum Beispiel: "Kennst du das?" oder "Was hilft dir in solchen Momenten?"
> • Immer "Videosprechstunde", niemals "Fernberatung".
> • Keine Heilversprechen und keine krankheitsbezogenen Erfolgsaussagen ("heilt", "beseitigt", "garantiert schmerzfrei", "Detox", "entschlackend") — stattdessen "kann unterstützen", "begleite ich", "besprechen wir gemeinsam".
> • Osteopathie, Faszientherapie und Dorn-Methode niemals als online/per Video verfügbar darstellen — nur vor Ort.
> • Keine erfundenen Patientenfälle als echte Einzelfälle ausgeben; nur typisierte Formulierungen ("ein Muster, das mir in der Praxis immer wieder begegnet").
> • Patienten werden gesiezt; keine Ausrufezeichen-Ketten, keine Superlative ohne Beleg, Emojis höchstens vereinzelt.
> • Preise nur nennen, wenn bestätigt (aktuell einziger fester Preis: Mikronährstoffanalyse 249 €).
> • Floskelverbot: "in der heutigen schnelllebigen Zeit", "revolutionär", "maßgeschneiderte Lösungen"; "ganzheitlich" nur wo inhaltlich konkret belegt.
> • Direkter Call-to-Action in etwa 1 von 5 Posts, restliche Posts liefern Mehrwert/Einblick ohne CTA.

**platform_writing_instructions (Instagram):**
> Adapt the caption for Instagram in German using a calm, reflective, body-aware style that speaks directly to the reader. […] usually 60–140 words, often opening with a symptom, question, or surprising body fact. Emphasize the connection between Körper, Seele, Stress, and Selbstwahrnehmung; use 0–3 soft emojis […] End with either a reflective question, a gentle prompt to pause and feel inward, or a soft appointment/blog CTA. […]

**caption_suffix (an jeden Beitrag angehängt):**
> #naturheilpraxis #heilpraktiker #ganzheitlich #körpergeistseele #achtsamkeit #gesundheitsreise #emotionaleheilung #spagyrik #osteopathie #faszientherapie #vertraueninsleben #bewusstleben #lebensfreude #Dorfen #Erding #OsteopathieDorfen #HeilpraktikerBayern #NaturheilpraxisDorfen

**ctas:** „Termin in der Praxis vereinbaren“, „Videosprechstunde buchen“
**custom_caption_prompt / custom_design_text_prompt / custom_carousel_prompt / custom_meme_prompt:** leer (null)
**imagery_preferences:** leer (null)
**design_style:** enthält u. a. „Prefer authentic practice imagery from the library … do not use stock photography.“ **Zur Anrede (Sie oder du) im Bildtext sagt es nichts.**

### Auffälligkeiten im Markenprofil
1. **Widerspruch zur Anrede:** Die Regel „Patienten werden gesiezt“ steht neben der Regel mit den Beispielen **„Kennst du das?“ / „Was hilft dir in solchen Momenten?“**. Das ist die wahrscheinlichste Quelle der du-Form in den Bildtexten.
2. **Keine Anrede-Regel für Bild-/Design-Text:** Die Schreibregeln gelten für die Caption. Für die Texte, die Marky in Grafiken und Videos setzt, gibt es weder eine Regel noch einen eigenen Prompt (`custom_design_text_prompt` = leer).
3. **Heil-Nähe in Feldern, die in die Texterstellung einfließen:**
   - `audience_combined` → Ziele: „Schmerzen und körperliche Symptome nachhaltig verstehen und **lösen**“, „Emotionale Blockaden erkennen und **wandeln**“
   - Hashtag **#emotionaleheilung** steht im Suffix und hängt damit an *jedem* Beitrag.
   - `description`: „… aber **heilen** darf der Mensch sich selbst …“
   Das sind keine direkten Heilversprechen im Beitragstext, aber Formulierungen, die du nach HWG prüfen lassen solltest.
4. **Stockfotos trotz „no stock photography“:** Der heute geplante Beitrag (Mann vor Großstadt-Skyline) und der abgelehnte Verstopfungs-Beitrag (Arzt im weißen Kittel mit Stethoskop) nutzen Stockmaterial.

## b) Die letzten 10 Beiträge
Alle 10 stammen aus einer Charge vom 03.10.2026, 14:34 UTC (gleiche Erstellzeit). Sortiert nach Erstellzeit.
„Bildtext“: bei Bildern selbst angesehen; bei Videos **nicht prüfbar** (auf der VPS gibt es kein Werkzeug zum Auslesen von Video-Einzelbildern, installiert wurde nichts).

| # | Status | Datum | Kanäle | Caption (Anfang) | Text im Bild? | du/dein/dir? |
|---|---|---|---|---|---|---|
| 1 | **veröffentlicht** | 06.10. | Google Business, LinkedIn, Facebook | „Müssen Sie vor dem Termin erst alle Befunde sortieren?“ | **ja**: „Musst du erst alle Befunde sortieren?“ / „Bring mit, was du hast. Eine fertige Erklärung brauchst du nicht. Was wirklich wichtig ist, klären wir gemeinsam.“ | **Bild: ja (du ×3)**, Caption: Sie |
| 2 | **eingeplant – heute 16:00** | 07.10. | alle gültigen | „Wenn Sie im Schichtdienst arbeiten …“ | nein (Stockfoto, Mann an Hafenpromenade) | nein |
| 3 | abgelehnt | – | – | „Spüren Sie nach der spagyrischen Begleitung kaum eine Veränderung …“ | Video – nicht prüfbar | Caption: nein |
| 4 | abgelehnt | – | – | „So ordne ich Beschwerden ein: erst die Warnzeichen.“ | ja: „SO ORDNE ICH BESCHWERDE N EIN:“ (falsche Silbentrennung), „… lesen Sie in der Caption.“ | nein (Sie) |
| 5 | abgelehnt | – | – | „Rollen Sie nicht jede gespannte Stelle einfach weg.“ | Video – nicht prüfbar | Caption: nein |
| 6 | abgelehnt | – | – | „Nicht jedes Symptom ist seelisch …“ | nein (Foto Behandlungsraum) | nein |
| 7 | abgelehnt | – | – | „Verstopfung kann sich verändern, bevor die Ursache sichtbar wird.“ | ja: „TERMIN VEREINBAREN – NEUE VERSTOPFUNG? NICHT ABWARTEN.“ (Stockfoto Arzt im Kittel) | nein |
| 8 | **eingeplant – 08.10. 16:00** | 08.10. | LinkedIn, Facebook | „3 Einträge können Verstopfung in einem anderen Licht zeigen.“ | Video – nicht prüfbar | Caption: nein |
| 9 | **eingeplant – 09.10. 16:00** | 09.10. | LinkedIn, Facebook | „‚Hier ist es ganz anders, als ich es mir vorgestellt habe.‘“ | Video – nicht prüfbar | Caption: nein |
| 10 | abgelehnt | – | – | „‚Natürlich‘ heißt nicht automatisch harmlos …“ | Video – nicht prüfbar | Caption: nein |

### Markierungen
**du/dein/dir:**
- In den Captions **nie**: Alle 50 geprüften Captions siezen.
- **In den Bild- und Videotexten der veröffentlichten Beiträge aber regelmäßig.** Laut Marky-Bildbeschreibung sind **10 der 27 veröffentlichten Beiträge** betroffen; Nr. 1 habe ich selbst angesehen und bestätigt:

| Veröffentlicht | Text im Bild/Video (laut Marky-Beschreibung) |
|---|---|
| 06.10. | „Musst du erst alle Befunde sortieren? … Bring mit, was du hast … brauchst du nicht“ (selbst geprüft) |
| 05.10. | „Dehnst du dann stärker?“ (Video) |
| 04.10. | „Vermeidest du Bewegung? Das hat Folgen.“ |
| 03.10. | „MUSST DU ERST WISSEN, WAS LOS IST, BEVOR DU DIR HILFE HOLEN DARFST?“ / „DU MUSST ES NICHT WISSEN“ (Video) |
| 22.09. | „DEIN ALLTAG WIRD LEISER … was du längst vermisst“ |
| 20.09. | „Morgens steif? Deine Faszien sind nicht einfach ‚verkürzt‘.“ |
| 18.09. | „Kehrt dein Schmerz immer an dieselbe Stelle zurück?“ (Video) |
| 14.09. | „Behandle nicht nur den Schmerzort: Wenn du wegen deines Knies ausweichst … Was dein Bewegungsmuster verrät …“ |
| 13.09. | „Wenn du am Schreibtisch arbeitest und dein Körper erst abends lauter wird:“ |
| 12.09. | „Was überhörst du gerade – bis dein Körper deutlicher werden muss?“ |

**Heilversprechen** („hilft bei“, „heilt“, „löst“, „lindert“, „schmerzfrei“, „Heilung“ usw.):
- In den 50 Captions **kein Heilversprechen**. Die Suchtreffer sind alle unkritisch im Kontext:
  - „… dass die Begleitung sie ausge**löst** hat“
  - „Solche Beobachtungen sind **kein Beweis für Heilung**“
  - „kleine, **schmerzfreie** Bewegungen machen“
  - „Kiefer **lösen**“ (Atemübung)
- Heil-nahe Formulierungen stecken dagegen im **Markenprofil** (siehe oben: „lösen“, „wandeln“, #emotionaleheilung).

**Veröffentlicht, obwohl der Modus Entwurf sein soll:**
- 27 Beiträge zwischen 10.09. und 06.10.2026, zuletzt Nr. 1 am 06.10.
- 3 weitere sind für 07., 08. und 09.10. jeweils 16:00 Uhr eingeplant.
- Ob einzelne davon vorher in der App angenommen wurden, ist über die API nicht feststellbar.

## Patientendaten
Keine gefunden. Die Captions verwenden nur typisierte Formulierungen; die Bilder zeigen Praxisräume und Stock-/Modellfotos.

## Nicht geprüft / Grenzen
- Die Textinhalte der 5 Videos unter den letzten 10 (kein ffmpeg/OpenCV auf der VPS; bewusst nichts installiert).
- Die du-Funde in den 9 übrigen veröffentlichten Beiträgen stammen aus Markys eigener Bildbeschreibung, nicht aus meiner Sichtprüfung.
- Die Einstellung „Veröffentlichung“ selbst (kein API-Feld).
- Die anderen drei Workspaces.

## Nächster Schritt (STOPP)
Ich habe nichts geändert. Das Markenprofil wird erst angepasst, wenn Roland den neuen Wortlaut in der Vorschau freigegeben hat (Texte kommen vom Chat). Ob der Beitrag heute um 16:00 Uhr rausgehen soll, entscheidet Roland: Er kann in der App den Posting-Plan pausieren oder den Beitrag aus der Warteschlange nehmen.
