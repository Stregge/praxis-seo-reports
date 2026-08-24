# Neue Seite "Presse & Fachpublikationen" + Verlinkung
**Stand: 22. August 2026**

## 1. Neue Seite erstellt (als Entwurf)

- **Post-Typ:** `posts` statt `pages` (umgeht das Bricks-Problem, wie beim
  Mikronährstoffanalyse-Vorgehen)
- **Slug:** `/presse/`
- **Status:** Entwurf – nicht live, wartet auf deine Freigabe
- Text 1:1 wie geliefert übernommen, keine eigenen Änderungen
- Vorschau: `https://www.naturheilpraxis-straehuber.de/wp-admin/post.php?post=33881&action=edit`
  (Live-Crawl-Verifikation der neuen Seite selbst ist erst nach Veröffentlichung möglich –
  aktuell erwartungsgemäß 404 auf der öffentlichen URL, da Entwurf)

## RankMath-Meta gesetzt und verifiziert

| Feld | Wert |
|---|---|
| Titel | Presse & Fachpublikationen \| Naturheilpraxis Strähuber |
| Fokus-Keyword | Roland Strähuber Fachpublikationen |
| Meta-Description | Übersicht meiner Fachartikel in medizinischen Fachzeitschriften wie der AKOM – Einblick in meine fachliche Arbeit über die tägliche Praxis hinaus. (146 Zeichen) |

**Kleiner technischer Hinweis:** Meine automatische Verifikation meldete beim Titel kurz einen
Fehlalarm, weil WordPress das "&" im Titel beim Speichern intern als `&amp;` kodiert (normales,
unschädliches Verhalten – wird beim Anzeigen automatisch wieder korrekt als "&" dargestellt).
Ich habe das geprüft und bestätigt: der Titel ist korrekt und vollständig gespeichert.

Die Meta-Description habe ich – wie zuletzt besprochen – nicht frei neu formuliert, sondern
wörtlich aus deinem freigegebenen Seitentext extrahiert/gekürzt, um nicht in die Textautorenschaft
einzugreifen. Falls du/Chat eine eigene Formulierung bevorzugt, sag Bescheid.

## 2. Link auf "Über mich" ergänzt – live verifiziert

Auf der Bricks-Seite `/ueber-mich/` gab es bereits einen passenden Abschnitt
"Veröffentlichungen" mit genau dem AKOM-Fachartikel. Dort den Satz **"Meine Fachartikel finden
Sie [hier](/presse/)."** direkt angehängt – keine neue Struktur, kein neues Element, nur der
bestehende Textblock erweitert. Damit bleibt der Rest der Seite unangetastet.

- Backup des Vorher-Zustands: `/root/praxis-seo/backup/content/bricks_pages_237_..._vor_presse_link.json`
- Technik: SSH + WP-CLI + `--user=ClaudeCode` (etablierter Weg vom 12.08.), gezielte
  Cache-Leerung für `/ueber-mich/`
- Live-Crawl-Verifikation: Status 200, neuer Link vorhanden und korrekt verlinkt, bestehender
  AKOM-Text intakt, restliche Seitenabschnitte (Werdegang, Philosophie, Werte, FAQ-Links)
  unverändert vorhanden

**Live-Link:** https://www.naturheilpraxis-straehuber.de/ueber-mich/ (Link zeigt aktuell auf
`/presse/`, das noch als Entwurf existiert – wird automatisch funktionsfähig, sobald die
Presse-Seite veröffentlicht ist)

## Zusammenfassung

| Was | Status |
|---|---|
| Presse-Seite angelegt | ✅ Entwurf, wartet auf Freigabe |
| RankMath-Meta gesetzt | ✅ verifiziert |
| Link auf Über-mich-Seite | ✅ live, verifiziert |

Sobald du die Presse-Seite freigibst, setze ich sie auf "veröffentlicht" – dann sind beide
Seiten korrekt miteinander verlinkt.
