# Rücken-Cluster – Umsetzungsplan (noch NICHTS veröffentlicht)
**Stand: 27. Juli 2026**

## ⚠️ Wichtigster Fund zuerst: Duplicate-Content-Risiko bei "Hexenschuss"

Es gibt bereits einen fertigen, gut geschriebenen Artikel dazu: **"Hexenschuss – was tun?"** (Post-ID 30992, Slug `hexenschuss-was-tun`, 1.571 Wörter, live, mit Quellenangaben) – das ist genau die Seite, deren kaputten Redirect wir am 25.07. repariert haben. Der neue Spoke `spoke-hexenschuss.md` behandelt inhaltlich fast dasselbe Thema unter dem geplanten Slug `hexenschuss`.

Zwei fertige Artikel zum selben Thema/Keyword würden sich gegenseitig die Rankings streitig machen (Kannibalisierung) – genau das Problem, das wir letzte Woche bei anderen Keywords schon gefunden haben.

**Meine Empfehlung:** Keinen neuen Artikel unter `hexenschuss` anlegen. Stattdessen den bestehenden Artikel `hexenschuss-was-tun` als Hexenschuss-Spoke ins Cluster einbinden (Links zum Pillar und den anderen Spokes ergänzen, ggf. die neue FAQ-Sektion aus `spoke-hexenschuss.md` ergänzen, falls sie mehr/andere Fragen abdeckt als der bestehende Artikel). Das spart Dopplung und nutzt die bereits vorhandene Indexierung/Historie der Seite weiter.

**Alternative, falls du den neuen Text lieber komplett übernehmen willst:** Ich ersetze den Inhalt von `hexenschuss-was-tun` durch den neuen, kürzeren Text aus `spoke-hexenschuss.md` (URL/Slug bleibt gleich, kein neuer Artikel, keine Dopplung) – dann geht aber der bestehende, längere Text mit Quellenangaben verloren.

**Das entscheidest du bitte, bevor ich irgendetwas veröffentliche.**

---

## Sonst: keine weiteren Kollisionen gefunden

Geprüft (Slug + Volltextsuche über alle Post-Typen): `rueckenschmerzen`, `ischias-ischiasnerv`, `bandscheibenvorfall-lws-syndrom`, `ruecken-uebungen` – keine Konflikte. Es gibt kurze Lexikon-Einträge zu "Ischias", "Bandscheibenvorfall", "Wirbelsäule" – die sind aber Glossar-Kurztexte, kein inhaltliches Duplikat zu den ausführlichen neuen Ratgeber-Artikeln, sondern gute Verlinkungsziele (siehe unten).

---

## Ablauf (zur Freigabe)

1. **4 (oder 5, je nach deiner Hexenschuss-Entscheidung) Artikel als ENTWURF anlegen** – noch nicht live/indexiert. Kategorie wie beim Faszien-Cluster, Autor "ClaudeCode".
2. Im Entwurf: Meta-Description + Focus-Keyword setzen, interne Links einbauen (Platzhalter ersetzen + Rückverlinkung zum Pillar ergänzen), FAQ-Schema setzen, Featured Image generieren.
3. **Dir die fertigen Entwürfe zur Kontrolle zeigen** (Links zu den WP-Editor-Vorschauen).
4. Erst nach deinem "ok" auf "veröffentlicht" umstellen und live verifizieren (wie beim NAP-Fix: Seiten wirklich aufrufen, nicht nur der Erfolgsmeldung vertrauen).

## Meta-Descriptions (Entwurf, alle unter 155 Zeichen)

| Artikel | Meta-Description | Zeichen |
|---|---|---|
| Pillar (rueckenschmerzen) | "Rückenschmerzen im unteren, mittleren oder oberen Rücken? Ursachen erkennen und ganzheitlich behandeln lassen – Heilpraktiker Roland Strähuber in Dorfen." | 153 |
| Ischias | "Ischias-Schmerzen bis ins Bein? Ursachen des gereizten Ischiasnervs verstehen und ganzheitlich behandeln lassen – Heilpraktiker Roland Strähuber, Dorfen." | 153 |
| Hexenschuss (falls neu) | "Akuter Hexenschuss? Was jetzt wirklich hilft, plus ganzheitliche Behandlung durch Heilpraktiker Roland Strähuber in Dorfen – auch für Erding und Poing." | 151 |
| Bandscheibenvorfall/LWS | "Bandscheibenvorfall oder LWS-Syndrom? Ursachen, Übungen und ganzheitliche Unterstützung durch Heilpraktiker Roland Strähuber in Dorfen." | 135 |
| Rücken-Übungen | "Gezielte Rücken-Übungen gegen Rückenschmerzen – inkl. kostenlosem PDF zum Ausdrucken. Von Heilpraktiker Roland Strähuber, Naturheilpraxis Dorfen." | 145 |

Focus-Keywords wie in deinem Prompt vorgegeben (rückenschmerzen / ischias / hexenschuss / bandscheibenvorfall / rückenübungen).

## Interne Verlinkung (Platzhalter-Ersetzung)

| Datei | Platzhalter | Wird ersetzt durch |
|---|---|---|
| Pillar | `[Faszien-Ratgeber](#)` | Link zu `/faszien-ratgeber/` |
| Pillar | 4x "in Arbeit"-Hinweis | echte Links zu den 4 Spokes |
| Ischias | `[Rücken-Übungen-Ratgeber](#)` | Link zu `/ruecken-uebungen/` |
| Bandscheibenvorfall/LWS | `[Rücken-Übungen-Ratgeber](#)` | Link zu `/ruecken-uebungen/` |
| Rücken-Übungen | `[Ischias-Ratgeber](#)` | Link zu `/ischias-ischiasnerv/` |
| Rücken-Übungen | `[5-Minuten-Rückenübungen-PDF](#)` | echter Medien-Link nach PDF-Upload |
| Alle 4 Spokes | – (kein Platzhalter vorhanden) | ergänze je einen Rückverlinkungs-Satz zum Pillar, z.B. *"Mehr zum Thema: [Rückenschmerzen – Ursachen, Behandlung und was wirklich hilft](/rueckenschmerzen/)"* |

**Zusätzlich vorgeschlagen (optional, deine Entscheidung):** Je einen Satz/Link in zwei bestehende, bereits veröffentlichte Seiten ergänzen, damit die neuen Seiten von Anfang an auch von außerhalb des Clusters erreichbar sind:
- `/faszien-ratgeber/` → ein Verweis auf den neuen Rücken-Pillar (thematische Überschneidung: Faszien spielen bei Rückenschmerzen eine Rolle, wird im Pillar auch erwähnt)
- `/beschwerde/bewegungsapparat-und-gelenke/` → Rückenschmerzen/Ischias/Hexenschuss als verlinkte Stichpunkte in der bestehenden "Kurzüberblick"-Liste ergänzen (passt strukturell genau in das vorhandene Format)

**Nicht möglich:** Verlinkung von der Startseite aus – die Startseite ist mit Bricks Builder gebaut, ihr Inhalt ist nicht über die normale WordPress-REST-API bearbeitbar (der Content-Block ist leer/nicht zugreifbar, siehe frühere Recherche). Das müsstest du selbst im Bricks-Editor ergänzen, falls gewünscht.

## FAQ-Schema (technischer Hinweis)

RankMath hat einen Schreib-Endpunkt dafür (`rankmath/v1/updateSchemas`), aber keinen Lese-Endpunkt – ich kann das exakte JSON-Format vorab nicht gegen eine echte, funktionierende Seite verifizieren (anders, als du es zuletzt für die Ahrefs-Arbeit von mir verlangt hast – hier lässt es die API technisch nicht zu). Ich nutze das allgemein bekannte RankMath-Schema-Format (FAQPage mit Frage/Antwort-Paaren) und verifiziere danach direkt am Live-HTML der Seite (RankMath rendert Schema als sichtbaren `<script type="application/ld+json">`-Block im Seitenquelltext), ob es tatsächlich ankommt – bevor die Seiten final freigegeben werden. Sollte es nicht auf Anhieb klappen, ist das ungefährlich (Seite bleibt normal lesbar, nur ohne Schema) und ich korrigiere es nach.

## Featured Images

Wie beim Faszien-Cluster: 4-5 Bilder per Gemini generieren, ca. 5-6 Cent/Bild, macht insgesamt ca. 20-30 Cent.

## PDF-Lead-Magnet

`5-minuten-rueckenuebungen.pdf` wird in die Mediathek hochgeladen, Direkt-Link wird zurückgemeldet. Download-Gate (Name+E-Mail-Pflicht) wird wie besprochen NICHT für den ersten Wurf umgesetzt (direkter Link reicht erstmal) – CleverReach-Anbindung ist separates, noch offenes Thema.

---

**Nichts davon ist umgesetzt.** Warte auf deine Hexenschuss-Entscheidung + generelles "ok" für den Rest.
