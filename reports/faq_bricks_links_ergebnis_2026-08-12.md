# FAQ-Links in Bricks-Seiten: Ergebnis
**Stand: 12. August 2026**

## Ergebnis: Alle 11 Links erfolgreich eingefügt

| Seite | Links | Live verifiziert |
|---|---|---|
| Kontakt (ID 111) | 4 (Termin-Logistik) | ✅ Status 200, alle 4 URLs im HTML gefunden, Seitengröße +839 Byte |
| Ablauf (ID 235) | 5 (Kosten/Versicherung) | ✅ Status 200, alle 5 URLs im HTML gefunden |
| Über mich (ID 237) | 2 (Vertrauen/Methoden-Skepsis) | ✅ Status 200, beide URLs im HTML gefunden |

Auf allen drei Seiten: bestehender Inhalt unverändert (Stichproben auf bekannte Textteile,
Seiten enden korrekt mit `</html>`, keine PHP-Fehler im Output). Format: neuer Abschnitt
"Weiterführende Fragen und Antworten:" (Überschrift) + Liste der Fragen als Links, exakt wie
in der Copy-Paste-Liste vorgegeben – keine eigenen Texte.

## Aufteilung Ablauf/Über mich

Die ursprüngliche Liste hatte "Ablauf / Über mich" als eine gemeinsame Gruppe (7 Links) ohne
festgelegte Aufteilung. Ich habe das inhaltlich sinnvoll getrennt: die 2 Vertrauens-/
Methoden-Fragen auf **Über mich** (passt zur Person/zum Vertrauen), die 5 Kosten-/
Versicherungs-Fragen auf **Ablauf** (passt zum Praxisablauf inkl. Kosten). Falls du das anders
verteilt haben willst, sag Bescheid – lässt sich leicht verschieben.

## Wie es technisch gelöst wurde

1. **WP-CLI war nicht vorinstalliert**, aber PHP war vorhanden – WP-CLI als portable Datei
   (`wp-cli.phar`) heruntergeladen, nach Gebrauch wieder gelöscht.
2. **PHP-Versions-Stolperstein:** Die Standard-Shell-PHP-Version (7.2) ist zu alt für die
   WordPress-Version. Die passende PHP-8.1-Installation unter `/usr/local/php81/bin/php`
   gefunden und verwendet.
3. **Bricks-Struktur verstanden, bevor etwas verändert wurde:** Das Feld `_bricks_page_content_2`
   ist eine flache Liste von Elementen (id/parent/children/settings) – ausgelesen, als JSON
   exportiert, Struktur von Section/Container/Heading/Text-Elementen anhand bestehender Beispiele
   auf der Seite selbst nachgebaut (nicht geraten).
4. **Rundweg-Sicherheitstest zuerst:** Bevor irgendein neuer Inhalt geschrieben wurde, habe ich
   den bestehenden Inhalt unverändert zurückgeschrieben und die Live-Seite Byte-für-Byte mit
   vorher verglichen (identisch) – das hat bestätigt, dass der Lese-Schreib-Weg selbst
   verlustfrei funktioniert, bevor ich damit etwas Neues hinzufüge.
5. **Ein Stolperstein unterwegs:** Der erste echte Schreibversuch (mit neuem Inhalt) wurde von
   Bricks selbst mit "Failed to update" abgelehnt – keine Fehlermeldung im Log. Ursache
   gefunden: Bricks blockiert Schreibzugriffe auf dieses Feld grundsätzlich, wenn kein
   WordPress-Benutzer mit Editor-Berechtigung "angemeldet" ist (das ist in der Kommandozeile
   normalerweise niemand). Gelöst durch Ausführen als der bestehende `ClaudeCode`-Adminaccount
   (`wp --user=ClaudeCode ...`) – exakt dafür ist dieser Account ja eingerichtet.
6. **Cache-Stolperstein:** WP Rocket zeigte nach dem Schreiben zunächst weiter die alte
   Seitenversion. Den betroffenen Seiten-Cache gezielt gelöscht (nur die drei betroffenen
   Seiten, nicht der komplette Cache), danach war der neue Inhalt sofort sichtbar.
7. **Backup:** Original-Zustand aller drei Seiten (vor der Änderung) und die neu geschriebene
   Version liegen als JSON in `/root/praxis-seo/backup/content/bricks_pages_*` – bei Bedarf
   könnte ich den alten Zustand über denselben Mechanismus zurückschreiben.
8. Alle temporären Dateien (WP-CLI, JSON-Exporte) wurden nach Gebrauch vom Hosting-Server
   wieder gelöscht.

## Für künftige ähnliche Aufgaben

Jetzt, wo der Weg bekannt und einmal sicher getestet ist (SSH + WP-CLI + `--user=ClaudeCode`
für Bricks-Schreibzugriffe + gezielte Cache-Leerung), kann ich das bei Bedarf wiederholen, ohne
erneut bei null anzufangen. Die SSH-Zugangsdaten liegen jetzt gesichert unter
`/root/.env.netcup-hosting` (chmod 600).
