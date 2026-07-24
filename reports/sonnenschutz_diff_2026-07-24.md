# Sonnenschutz-Seite – Diff Vorschau (NOCH NICHT LIVE)
**Post-ID 24698 – natuerlicher-sonnenschutz-ohne-chemie**
**Stand: 24. Juli 2026**

## Was sich ändert

1. **Transparenzhinweis neu ergänzt** (ganz oben, kursiv, vor der ersten Überschrift):
   > *Hinweis: Dieser Artikel enthält Affiliate-Links (als "Anzeige" gekennzeichnet). Wenn du über einen dieser Links einkaufst, erhalte ich ggf. eine kleine Provision – für dich entstehen dadurch keine Mehrkosten.*

2. **"(Anzeige / Affiliate-Link)"-Label bei allen 8 Linkstellen ergänzt** (alle 3 Links, an jeder Stelle wo sie im Text vorkommen).

3. **Alle doppelten Absätze entfernt** (~13 Duplikat-Stellen, z.B. "Dünner und empfindlicher" kam vorher als Listenpunkt UND als Extra-Absatz – jetzt nur noch als Listenpunkt).

4. **HWG-Formulierungen entschärft:**
   | Vorher | Nachher |
   |---|---|
   | "Studien zeigen: Astaxanthin kann die Eigenschutzzeit der Haut verlängern / Rötungen und Sonnenbrand mindern / Hautalterung verlangsamen" | "Einige Studien deuten darauf hin, dass Astaxanthin die Eigenschutzzeit **unterstützen** kann / zu einer **Reduktion von Hautrötungen beitragen** kann / die **Hautalterung positiv beeinflussen** kann" |
   | "ein sanfter, ganzheitlicher Sonnenschutz für Erwachsene und Kinder" | "eine mögliche ganzheitliche Ergänzung für Erwachsene und Kinder" |
   | "perfekte Ergänzung" / "Besonders ideal" | "sinnvolle Ergänzung" / "Besonders interessant" |
   | "sicherer, natürlicher Schutz" (FAQ 1) | "guter natürlicher Schutz" |
   | "schützt Zellen & Pigmente" (Astaxanthin, FAQ 4) | "unterstützt Zellen & Pigmente" |
   | "Sonne kann heilsam sein" | "Sonnenlicht spielt für unser Wohlbefinden eine wichtige Rolle" |
   | "lassen sich Haut und Gesundheit optimal schützen" | "lassen sich Haut und Gesundheit gut begleiten" |
   | "Höheres Risiko für ... Langzeitschäden" | "Höheres Risiko für ... langfristige Hautbelastungen" |
   | Empfehlungsbox: "gibt Ihrer Haut den besten natürlichen Schutz" | "kann eine sinnvolle Ergänzung für den natürlichen Hautschutz sein" |

5. **Empfehlungsbox am Ende** zusätzlich mit kleinem Zusatzhinweis versehen: *(Enthält Affiliate-Empfehlungen / Anzeige)*

6. **Unverändert:** Titel/H1, Meta-Description, alle 3 Produktlinks selbst (URLs identisch), Kontaktdaten, FAQ-Struktur, Kategorien.

## Frage zur "Werbung"-Badge am Artikelanfang

Geprüft über die WordPress REST API:
- Keine Kategorie/Tag mit Bezug zu "Werbung/Anzeige/Affiliate" vorhanden (nur: Allgemein, Alltag, Beschwerden, Kinder, Praxis).
- Kein Custom-Field/Meta-Wert am Post gefunden, der auf ein Badge-System hindeutet.
- Die einzige bestehende Konvention auf der Seite ist der **Text-Hinweis direkt im Content** (so wie bei der LaVita-Seite bereits umgesetzt) – das habe ich hier genauso übernommen.

**Eine sichtbare Badge/Label-Anzeige oberhalb der Überschrift (separates UI-Element, z.B. über Bricks Builder oder WPCodeBox) kann ich über die REST-API nicht einsehen oder einrichten** – das läuft (falls es sowas gibt oder eingerichtet werden soll) über Bricks-Builder-Templates bzw. WPCodeBox-Snippets, die man nur direkt im WordPress-Admin sieht/bearbeitet. Falls gewünscht, müsstest du kurz im Bricks-Editor nachschauen, ob es dort einen globalen "Anzeige"-Baustein gibt – ich kann das nicht von hier aus prüfen.

---

**Status:** Noch NICHT gespeichert/live gesetzt. Warte auf "ok".
