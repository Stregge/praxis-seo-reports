# Block 4 – Fehlende Alt-Texte per Gemini: Ergebnis
**Stand: 3. August 2026**

## Aufräumen (vorab erledigt)
Die 15 bestätigt verwaisten WebP-Duplikate aus dem versehentlichen Doppel-Lauf sind gelöscht und verifiziert (404 bei Nachprüfung).

## Block 4: Alt-Texte

Ahrefs meldet aktuell 2 Seiten mit fehlendem Alt-Text (beide Featured Images). Für beide per Gemini-Vision (Bild + Kontext-Prompt) einen kurzen deutschen Alt-Text generiert, gesetzt und live verifiziert:

| Seite | Bild | Neuer Alt-Text |
|---|---|---|
| warum-leinoel-als-omega-3-quelle-nicht-ausreicht | Media 14729 | "Leinölflasche mit Fischsymbol, umgeben von Leinsamen. Text: "Warum Leinöl als Omega3 Quelle nicht ausreicht." |
| intervallfasten-arthrose | Media 33742 | "Wecker auf leerem Teller, dazu Wasserglas und grüne Blätter auf Holztisch." |

Beide Beschreibungen wurden von mir vorab visuell mit dem tatsächlichen Bild abgeglichen (korrekt) und nach dem Setzen zusätzlich unabhängig über die Live-Seite geprüft (erscheinen korrekt im echten `<img alt="...">`-Tag).

## Technisch
- Neue Funktion `gemini_describe_image()` in `ahrefs_tool.py` (Gemini-Vision, multimodal: Bild + Text-Prompt)
- Neue Funktion `fix_missing_alt_text()` in `image_optimize.py` – deckt beide Fälle ab: Featured Image (Attachment-Meta) UND Inline-`<img>` im Content (Attribut wird direkt im Content ergänzt/ersetzt)
- Aufruf: `python3 image_optimize.py --alt-texte` (Vorschau) bzw. `--alt-texte --live`
- Ein Datenpunkt zur Kenntnis: die Gemini-Antwort schwankt leicht in der Länge trotz "max. 100 Zeichen"-Vorgabe (einmal 58, einmal 108 Zeichen) – kein hartes technisches Limit für Alt-Texte, daher unkritisch, aber nicht perfekt konsistent.

## Noch nicht erledigt
- **Cron-Integration:** Noch nicht in den Montags-Lauf aufgenommen – soll ich das jetzt mit einbauen (z.B. direkt nach der Bild-Kompression um 05:50)?
- **Wochenreport:** Noch nicht mit Alt-Text-Zahlen erweitert (analog zur Bild-Kompression).
