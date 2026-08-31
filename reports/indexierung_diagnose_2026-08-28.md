# Vollständige Indexierungs-Diagnose naturheilpraxis-straehuber.de
Stand: 28.08.2026 — alle Befunde live gegen HTML/Crawl-Ergebnisse verifiziert (kein Punkt basiert nur auf API-Erfolgsmeldung)

## Ausgangslage
GSC meldet ~138 nicht indexierte Seiten (44 robots.txt, 12 noindex, 11 Weiterleitung, 4× 404, 33 „gefunden – zurzeit nicht indexiert", 31 „gecrawlt – zurzeit nicht indexiert"). Ahrefs zeigt nur 12 getrackte Keywords, 17 organischen Traffic. Wichtige Einschränkung vorab: **Googles Coverage-Report-Aufschlüsselung nach genauem Grund ist nicht über die API abrufbar, nur im UI.** Alle Zahlen unten sind über Live-Checks und die GSC-Einzel-URL-API (urlInspection) rekonstruiert, nicht 1:1 aus dem UI-Report exportiert.

---

## 1. Robots.txt (44 blockierte Seiten)
**Ergebnis: sauber, kein Fix nötig.** 0 von 205 echten Content-URLs (70 Posts, 11 Pages, 78 Lexikon, 33 FAQ, 8 Beschwerde, 5 Therapie) werden blockiert. Nur Standard-Systempfade sind gesperrt, `/wp-content/uploads/` ist explizit erlaubt, Sitemap-Direktive korrekt gesetzt. Die 44 blockierten URLs sind plausibel Systempfade + ggf. historische Suchergebnis-URLs — technisch unauffällig.

## 2. Noindex-Seiten (12 gemeldet)
5 konkrete noindex-URLs gefunden und einzeln geprüft:

| URL | ID/Typ | Status |
|---|---|---|
| /datenschutz/ | Page 18 | korrekt, beabsichtigt |
| /author/roland/ | User 2 | korrekt (RankMath-Standard) |
| /author/claudecode/ | User 5 | korrekt noindexed, aber Ghost-Account |
| /author/manus-temp/ | User 3 | korrekt noindexed, aber Ghost-Account |
| /author/seo-revolution/ | User 1 | korrekt noindexed, aber Ghost-Account |

Die restlichen ~7 der gemeldeten 12 sind plausibel verschiedene historische Suchergebnis-URLs (`?s=...`), die Google zu unterschiedlichen Zeitpunkten gecrawlt hat — nicht abschließend zählbar ohne GSC-UI.

**Kein Fix nötig** — alle gefundenen Noindex-Einstellungen sind korrekt. Einzige Auffälligkeit: 3 der 4 WordPress-Benutzer (claudecode, manus-temp, seo-revolution) sind erkennbare Test-/Automations-Accounts aus früheren Workflows. Kein SEO-Schaden (ihre Archivseiten sind ohnehin noindex), aber Aufräum-Kandidat — **das kannst nur du entscheiden/machen** (Benutzer löschen und Beiträge umhängen, siehe unten).

## 3. Stichprobe „33 gefunden" + „31 gecrawlt – nicht indexiert" (22 URLs geprüft)
18 von 22 sind indexiert. 4 sind „Crawled – currently not indexed": `/es-ist-jetzt-zeit-sich-zeit-zu-nehmen/`, `/was-tun-bei-zeckenbiss/`, `/hintern-juckt-bei-kindern/`, `/heilpraktiker-versicherung/`.

Für alle 4 geprüft und **ausgeschlossen**: technischer Robots-Block (robots-meta = `index,follow` bei allen 4, live verifiziert), dünner Content (1330–1530 Wörter), Orphan-Status (alle von /ratgeber/ verlinkt, allerdings nur auf Seite 2 der Paginierung). Kein technisches Muster erkennbar. Auffällig ist nur: alle 4 behandeln stark umkämpfte generische Gesundheitsthemen (Zeckenbiss, Wurmbefall bei Kindern, Versicherung), bei denen große Gesundheitsportale dominieren — das ist eine inhaltliche/Autoritäts-Frage, kein technischer Bug.

**Ergebnis:** ~18% der Stichprobe betroffen, aber ohne fixbare technische Ursache.

## 4. Sitemap-Frische (Cache-Bug-Rückfall-Check)
**Bestätigt: kein Rückfall.** post-sitemap.xml zuletzt aktualisiert 22.08. 13:48 UTC, alle 7 zuletzt veröffentlichten Seiten enthalten (Leaky-Gut-Test, Welche Vitamine bei Müdigkeit, Zinkmangel, Magnesiummangel, Vitamin-B12-Mangel, Presse, Mikronährstoffanalyse). Der am 22.08. behobene RankMath-eigene Sitemap-Datei-Cache-Bug ist nicht wieder aufgetreten.

## 5. Weiterleitungen (11) und 404-Fehler (4)
Bestätigt und live geprüft:

| URL | Ziel | Code | Einschätzung |
|---|---|---|---|
| /allgemein/ | /ratgeber/ | 301 | bewusste Kategorie-Konsolidierung |
| /alltag/ | /ratgeber/ | 301 | bewusste Kategorie-Konsolidierung |
| /praxis/ | /ratgeber/ | 301 | bewusste Kategorie-Konsolidierung |
| /2026/, /2026/08/, /2023/, /2023/07/ (Datums-Archive) | Startseite | 301 | RankMath-Standardeinstellung, korrekt |

Zusätzlich geprüft und ausgeschlossen: der im Juli dokumentierte RankMath-Redirect-Bug auf 3 Arthrose/Hexenschuss-Artikel — **alle 3 live erneut auf HTTP 200 verifiziert** (`/hexenschuss-was-tun/`, `/arthrose-schlafen-tipps/`, `/arthrose-protokoll-heilpraktiker/`), Google hat den Fix bereits nachvollzogen (GSC: „Submitted and indexed", zuletzt gecrawlt 24.–26.07.). Der geplante LifeWave-X39-Merge-Redirect wurde nie umgesetzt (kein Redirect, aber beide LifeWave-Artikel konkurrieren weiter um ähnliche Keywords — Kannibalisierungs-Nebenbefund, kein Teil dieser Aufgabe).

**Die restlichen ~8 Redirects und alle 4 gemeldeten 404-Fehler konnten nicht identifiziert werden.** Alle verfügbaren Kanäle kamen sauber zurück: interner Link-Crawl (115 Links, 0 kaputt), frischer Ahrefs-Audit (405 URLs, 0 Fehler), 0 kaputte Backlinks, Sitemap 100% deckungsgleich. Das ist technisch plausibel: URLs, die nirgends mehr verlinkt sind, sind per Definition nicht mehr live crawlbar — sie liegen nur noch in Googles historischem Index-Gedächtnis (alte URL-Struktur, alte Sitemap-Version, o.ä.) und lösen sich normalerweise von selbst auf, sobald Google neu crawlt. Eine abschließende Identifikation ist nur über den GSC-UI-Coverage-Report möglich.

## 6. Warum Health Score 98 aber nur 12 Keywords?
Die Punkte 1–4 liefern **keine** Erklärung — dort ist praktisch alles sauber oder bereits behoben. Auch Punkt 5 liefert keinen aktiven Bug mehr. Der Health Score misst technische On-Page-Hygiene (Meta, Schema, interne Links, Ladezeit) — das ist tatsächlich gut. Er misst **nicht** Domain-Autorität oder Ranking-Wahrscheinlichkeit.

Die wahrscheinlichste Erklärung, gestützt durch Punkt 3: **geringe Domain-Autorität kombiniert mit hoher thematischer Konkurrenz durch etablierte große Gesundheitsportale (NetDoktor, Apotheken Umschau u.ä.).** Google crawlt die Seiten (das funktioniert), entscheidet sich aber bei generischen, stark umkämpften Themen gegen eine Indexierung. Verstärkender Faktor: die Publikations-Bursts (z. B. 9+ Artikel an einem Tag) verteilen das ohnehin begrenzte Crawl-/Indexierungsbudget einer Domain mit noch junger/schwacher Autorität auf viele URLs gleichzeitig, statt es auf einzelne Artikel zu konzentrieren.

Das ist eine strukturelle, keine technische Ursache — sie lässt sich nicht per Fix beheben, sondern nur langfristig durch mehr Backlinks/Domain-Autorität und ggf. gestrecktere statt gebündelte Publikation verbessern.

---

## Vorher/Nachher
| Kennzahl | Vorher (Ausgangslage) | Nachher (dieser Check) |
|---|---|---|
| Sitemap-Cache-Bug | Rückfall befürchtet | bestätigt: kein Rückfall, Sitemap aktuell |
| Bekannte Redirect-Bugs (Arthrose/Hexenschuss) | dokumentiert im Juli | bestätigt behoben, von Google übernommen |
| Robots.txt-Blockaden auf echtem Content | unklar | bestätigt: 0 von 205 |
| Noindex auf echtem Content | unklar | bestätigt: 0 von 205 (nur Datenschutz korrekt) |
| Aktive technische Redirect-/404-Bugs | unklar | keine gefunden |
| Erklärung für Keyword-Lücke | unklar | Domain-Autorität + Themenkonkurrenz + Crawl-Budget-Verteilung, kein technischer Bug |

**Es wurde in diesem Durchgang keine Änderung an der Website vorgenommen** — die Diagnose ergab keinen fixbaren technischen Bug, der einen Eingriff gerechtfertigt hätte. Alle bereits in früheren Sessions behobenen Probleme (Sitemap-Cache, Arthrose-Redirects, Homepage-Meta, Schema) sind weiterhin stabil.

## Was nur du machen kannst
1. **GSC-Coverage-Report im UI öffnen** (nicht per API möglich) und dort die exakte Liste der 33+31 „nicht indexiert"-URLs sowie der 11 Redirects/4×404 exportieren — das schließt die verbleibende Lücke aus Punkt 3 und 5, die technisch nicht mehr rekonstruierbar war.
2. **Ghost-Autoren-Accounts aufräumen** (claudecode, manus-temp, seo-revolution) — Beiträge ggf. umhängen und Accounts löschen. Kein SEO-Risiko, aber Hygiene.
3. **Strategische Entscheidung zu den 4 unindexierten Themen** (Zeckenbiss, Wurmbefall Kinder, Heilpraktiker-Versicherung, Zeit-Artikel): entweder mit stärkerer Differenzierung/mehr Tiefe gegen die großen Portale nacharbeiten, oder akzeptieren, dass diese generischen Themen in absehbarer Zeit nicht ranken werden.
4. **Publikationstempo überdenken**: statt Bursts (9+ Artikel/Tag) eine gestrecktere Taktung erwägen, um das Crawl-Budget nicht zu verwässern — das betrifft aber zukünftige Content-Planung, keine technische Änderung.
