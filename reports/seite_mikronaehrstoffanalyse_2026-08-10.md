# Neue Seite: Mikronährstoffanalyse – Status
**Stand: 10. August 2026**

## Erledigt

- Seite als **Entwurf** angelegt (Post-ID 33861), Text 1:1 wie freigegeben übernommen, keine
  eigenen Änderungen.
- Slug: `/mikronaehrstoffanalyse/` (deine Wahl, passend zum Fokus-Keyword)
- RankMath-Meta gesetzt und verifiziert: Title, Description, Fokus-Keyword "Mikronährstoffanalyse"
- Preis-Platzhalter **bewusst nicht befüllt** – steht als `[Platzhalter – Roland ergänzt ...]`
  im Text, genau wie angegeben.
- Bearbeiten/Vorschau: `https://www.naturheilpraxis-straehuber.de/wp-admin/post.php?post=33861&action=edit`
  (dort auf "Vorschau" klicken, da als Entwurf noch nicht öffentlich sichtbar)

## Technische Entscheidung: Post-Typ "posts" statt "pages"

Ich habe die Seite als Blog-Artikel (`posts`) statt als klassische "Seite" (`pages`) angelegt.
Grund: 6 von 11 bestehenden "Seiten" auf der Website (u.a. Kontakt, Über mich, Ablauf) sind
Bricks-Builder-Seiten ohne Inhalt im Standard-Feld – eine neu angelegte "Seite" hätte das Risiko,
ebenfalls automatisch in den Bricks-Modus zu fallen und den Text unsichtbar zu machen. Bei
"posts" ist das nicht der Fall (alle 63 bestehenden Artikel sind normal editierbar). Inhaltlich
ändert das nichts – URL, Aufbau und SEO funktionieren identisch.

## CTA-Button: vorläufiges Link-Ziel

Der Button "Jetzt Fernberatung online buchen" verlinkt aktuell auf `/kontakt/` (die bestehende
Seite mit dem "Termin online buchen"-Button). Ich konnte die konkrete Lapsula-Buchungs-URL nicht
selbst ermitteln – das Buchungs-Widget lädt laut früherer Prüfung erst nach Cookie-Zustimmung per
JavaScript nach und taucht deshalb nirgends im Quelltext der Seite auf.

## Nicht umsetzbar mit aktuellem Zugriff (bitte prüfen/übernehmen)

1. **Separate Lapsula-Terminart "Fernberatung"/"Online-Beratung" anlegen:** Dafür bräuchte ich
   einen Lapsula-Login oder API-Zugang – liegt aktuell nicht vor (kein `.env.lapsula`, keine
   API-Doku). Bitte im Lapsula-Dashboard selbst prüfen, ob das geht, oder mir Zugang geben.
2. **WhatsApp-Plugin-Setup ("Missing setup") in Lapsula:** Gleicher Grund – ohne Lapsula-Zugang
   kann ich das weder prüfen noch einrichten.

Sobald du mir Lapsula-Zugangsdaten gibst (idealerweise als `/root/.env.lapsula`, chmod 600),
kann ich beides direkt übernehmen und den CTA-Button anschließend auf die richtige Terminart
verlinken.

## Bevor die Seite live geht, brauche ich von dir

1. Die konkreten Preise für Kit + Beratung (Platzhalter im Text)
2. Kurze Freigabe der Entwurfs-Vorschau
3. Ggf. Lapsula-Zugang für die zwei offenen technischen Punkte oben

Dann setze ich Status auf "veröffentlicht" – nicht vorher.
