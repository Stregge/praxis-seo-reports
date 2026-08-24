# Diagnose: Markensuche "Naturheilpraxis Strähuber" fehlt in organischen Google-Ergebnissen
**Stand: 22. August 2026 – reine Diagnose, nichts verändert**

## Kurzfassung der Einschätzung (Details unten)

**Kein technischer Indexierungsfehler.** Alle klassischen "Katastrophen-Ursachen" (noindex,
robots-Block, WordPress-Sperre, Redirect-Ketten, falsches Canonical) sind sauber ausgeschlossen –
Google hat die Startseite heute Morgen (06:12 Uhr) aktiv gecrawlt und als indexiert bestätigt.
Das eigentliche Bild ist differenzierter: die Seite taucht in echten Suchergebnissen durchaus auf,
konkurriert aber um den bloßen Nachnamen "Strähuber" mit einer **unabhängigen, gleichnamigen
Firma in Dorfen** (Straehuber AG, Bodenleger) sowie mehreren Arztverzeichnis-Seiten. Zusätzlich
ist die Meta-Description der Startseite technisch fehlerhaft (leer in der Datenbank, wird von
RankMath automatisch und mitten im Wort abgeschnitten generiert).

---

## 1. Indexierungs-Grundcheck

| Check | Ergebnis |
|---|---|
| robots.txt | Sauber – nur Standard-WordPress-Ausschlüsse (wp-admin, feed, search etc.), keine Kernseite blockiert, Sitemap korrekt referenziert |
| noindex-Meta/X-Robots-Tag auf Startseite, Über mich, Kontakt, /presse/, Faszientherapie-Artikel | Alle 5 zeigen `index, follow` – kein noindex irgendwo |
| WordPress `blog_public` (per WP-CLI, read-only) | **1** – korrekt, Indexierung erlaubt (die potenzielle "Katastrophe" ist ausgeschlossen) |

## 2. Google Search Console

| Check | Ergebnis |
|---|---|
| Echter Google-Index-Status (URL Inspection API) – Startseite | **PASS – "Submitted and indexed"**, zuletzt gecrawlt 2026-08-22, 06:12 Uhr (heute!), Indexierung erlaubt, Google-kanonische URL stimmt mit User-Canonical überein |
| Gleicher Check – Über mich, Faszientherapie-Artikel | Beide ebenfalls PASS/indexiert |
| Manuelle Maßnahmen / Sicherheitsprobleme | **Nicht per API prüfbar** – Google stellt diesen Report nicht über die Search Console API bereit, nur über die GSC-Weboberfläche. Bitte dort manuell unter "Sicherheit & manuelle Maßnahmen" nachsehen – das ist der einzige Punkt aus deiner Liste, den ich nicht technisch verifizieren konnte. |
| Impressionen/Klicks letzte 90 Tage für Marken-Queries | Siehe Tabelle unten |

**Marken-Suchanfragen (90 Tage, aus echten GSC-Daten):**

| Suchanfrage | Impressionen | Klicks | Ø Position |
|---|---|---|---|
| strähuber dorfen | 46 | 4 | **1,6** (rankt sehr gut) |
| straehuber (ohne Umlaut) | 90 | 0 | 6,0 |
| strähuber (mit Umlaut) | 64 | 1 | 5,2 |
| straehuber ag dorfen | 1 | 0 | 21,0 (das ist die *andere* Firma – siehe unten) |
| "naturheilpraxis strähuber" / "heilpraktiker strähuber" (als eigene Phrase) | **0** | 0 | – |

Auffällig: Für die von Visby/Ahrefs genannten Phrasen "Naturheilpraxis Strähuber" und
"Heilpraktiker Strähuber" gibt es in 90 Tagen **keine einzige registrierte Impression** – diese
exakten Wortkombinationen werden von echten Nutzern offenbar praktisch nie so eingegeben.

## 3. Sitemap-Check

| Check | Ergebnis |
|---|---|
| sitemap.xml erreichbar | Ja, aber mit 301-Redirect auf `sitemap_index.xml` (unschädlich, aber ein Extra-Hop) |
| Enthält Kernseiten | Ja – Startseite, Kontakt, Über mich etc. sind im `page-sitemap.xml` |
| In GSC eingereicht | Nicht per API prüfbar (auch das ein reiner UI-Report), aber die URL Inspection zeigt aktives Crawling, das spricht für eine funktionierende Sitemap-Anbindung |
| **Nebenbefund (nicht Teil deiner Fragen, aber relevant):** `post-sitemap.xml` zeigt `lastmod: 2026-07-24` und enthält **keinen** der seither veröffentlichten Artikel (Presse, Mikronährstoffanalyse, die 4 Vitalstoff-Artikel). Die Sitemap aktualisiert sich offenbar nicht automatisch bei neuen Veröffentlichungen. | ⚠️ Sollte separat behoben werden |

## 4. Title/Meta der Startseite

| Feld | Live-Wert |
|---|---|
| `<title>` | "Heilpraktiker Dorfen \| Naturheilpraxis Strähuber" – enthält die Marke konsistent geschrieben |
| Meta-Description (live im HTML) | "Heilpraktiker Roland Strähuber in Dorfen behandelt ganzheitlich: Osteopathie, Faszientherapie, Spagyrik & Psychotherapie. Jetzt Termin vereinbaren –…" – **bricht mitten im Satz ab** |
| **Root Cause gefunden:** rohe `rank_math_description` in der Datenbank für die Startseite (Page-ID 12) | **Komplett leer.** Es wurde nie eine Meta-Description für die Startseite gesetzt – RankMath generiert sie automatisch aus dem Seiteninhalt und schneidet dabei stur nach einer festen Zeichenzahl ab, ohne auf Wort-/Satzgrenzen zu achten. Das erklärt den abrupten Abbruch exakt. |
| og:site_name | "Naturheilpraxis Strähuber von Heilpraktiker Roland" – leicht andere Formulierung als Title/Description, siehe Visbys Hinweis auf "inkonsistente Markenschreibweise" |

## 5. Kanonische URLs & Redirects

| Check | Ergebnis |
|---|---|
| Canonical-Tag Startseite | `https://www.naturheilpraxis-straehuber.de/` – korrekt |
| http → https | 301, ein Hop, landet direkt korrekt |
| https ohne www → mit www | 301, ein Hop, landet direkt korrekt |
| http ohne www → https mit www | 301, ein Hop, landet direkt korrekt |
| Redirect-Ketten | **Keine gefunden** – alle Varianten in genau einem Sprung zur richtigen URL |

## Zusätzliche Diagnose (nicht in deiner Liste, aber aufschlussreich)

Ich habe die drei von den Tools genannten Suchbegriffe testweise selbst gesucht (echte
Web-Suche), um zu sehen, was tatsächlich in den Ergebnissen erscheint:

- **"Naturheilpraxis Strähuber Dorfen"** → Die eigene Website erscheint mehrfach (Startseite,
  /therapie/, /kontakt/, /ratgeber/ etc.), konkurriert aber mit Verzeichnis-Einträgen
  (Yelp, therapeutenfinder.com, connektar.de)
- **"Heilpraktiker Strähuber"** → Website erscheint ebenfalls mehrfach, konkurriert zusätzlich
  mit aerzte.de, st-leonhards-akademie.de und einem Wikipedia-Eintrag zu einem völlig anderen
  "Alexander Strähuber" (Maler, 19. Jhd. – reiner Namenszufall)
- **"Strähuber Dorfen"** (bloßer Nachname) → **Wichtigster Fund:** Es gibt eine völlig
  unabhängige Firma **"Straehuber AG"** – ein Bodenleger/Fußbodenbau-Unternehmen, ebenfalls in
  Dorfen ansässig – die bei dieser Suche mehrfach auftaucht (northdata.com, heinze.de,
  bodenleger.net, dasoertliche.de, orte.muenchen.de) und um dieselbe Suchanfrage konkurriert.
  Das erklärt auch den GSC-Fund "straehuber ag dorfen" als eigene, an uns vorbeigehende
  Suchanfrage.

Das erklärt sehr plausibel, warum die reine Nachnamen-Suche ("Strähuber"/"Straehuber" ohne
weiteren Zusatz) in GSC nur Position 5-6 erreicht, obwohl "Strähuber Dorfen" mit Ortszusatz
Position 1,6 erreicht: Ohne Ortsbezug teilt sich die Suche mit einer unrelated Firma
gleichen Namens.

---

## Einschätzung: Wahrscheinlichste Ursache

**Kein einzelner technischer Blocker – eher eine Kombination aus drei eigenständigen,
kleineren Faktoren:**

1. **Kein Ranking-/Indexierungsproblem im technischen Sinn.** Alle Kernmechanismen (Indexierung,
   robots, Sitemap, Canonical, Redirects) sind sauber. Google crawlt und indexiert die Seite
   aktiv und aktuell.

2. **Echte Namenskonkurrenz:** Die unabhängige "Straehuber AG" (Bodenleger) in Dorfen konkurriert
   um den bloßen Nachnamen – das dürfte der Hauptgrund sein, warum "Strähuber" ohne weiteren
   Kontext nicht #1 rankt, obwohl "Strähuber Dorfen" mit Praxis-Bezug sehr gut rankt (Pos. 1,6).

3. **Vermutlich ein Methodik-Aspekt bei Visby/Ahrefs:** Die exakten Phrasen "Naturheilpraxis
   Strähuber" und "Heilpraktiker Strähuber" werden laut GSC von echten Nutzern in 90 Tagen
   **nicht ein einziges Mal** so gesucht – die Tools könnten mit synthetischen/exakten
   Test-Queries arbeiten, die keine reale Suchnachfrage widerspiegeln. Das würde erklären,
   warum die Tools "nicht sichtbar" melden, obwohl reale, ähnliche Suchanfragen ("strähuber
   dorfen") gut performen.

4. **Ein klar identifizierter, eigenständiger Bug:** Die leere/automatisch abgeschnittene
   Meta-Description auf der Startseite ist ein echter, unabhängig davon behebbarer Fehler –
   beeinflusst eher Klickrate als Ranking-Sichtbarkeit selbst, ist aber trotzdem ein sinnvoller
   erster Fix.

**Nicht abschließend geklärt** (keine API-Möglichkeit): ob in GSC manuelle Maßnahmen oder
Sicherheitsprobleme gemeldet sind – das bitte einmal manuell im GSC-Dashboard prüfen, das ist
der einzige Blinde Fleck in dieser Diagnose.

## Vorschlag für die gemeinsame Besprechung der Fixes

- Meta-Description der Startseite manuell/durch Chat formulieren lassen und setzen (klarer,
  eigenständiger Fix)
- Sitemap-Aktualisierungsproblem (Nebenbefund) separat beheben
- Bei der Namenskonkurrenz mit der Bodenleger-Firma: eher strategische Frage (z. B. stärkerer
  Fokus auf "Strähuber Dorfen"/"Naturheilpraxis Strähuber" statt bloßem Nachnamen in Title/H1,
  Local-SEO/Google-Business-Profile-Signale stärken) als ein technischer Fix
- GSC-Sicherheitsbereich einmal manuell prüfen, um den letzten offenen Punkt zu schließen
