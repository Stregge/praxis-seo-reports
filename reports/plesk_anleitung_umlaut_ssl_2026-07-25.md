# Anleitung: SSL-Zertifikat für naturheilpraxis-strähuber.de in Plesk einrichten
**Ziel:** Die Umlaut-Domain soll auch über HTTPS sauber auf https://www.naturheilpraxis-straehuber.de weiterleiten (aktuell bricht HTTPS mit einem Zertifikatsfehler ab).

---

## Schritt 1: In Plesk einloggen und die Domain finden

1. Bei Plesk einloggen (Netcup-Kundencenter oder direkt über die Plesk-URL/Port 8443 deines Servers, z.B. `https://152.53.226.138:8443`).
2. Links im Menü auf **"Websites & Domains"** klicken.
3. In der Liste nach der Domain suchen. Sie kann dort **so oder so ähnlich** angezeigt werden:
   - `naturheilpraxis-strähuber.de` (mit Umlaut), oder
   - `xn--naturheilpraxis-strhuber-8bc.de` (die technische "Punycode"-Schreibweise – das ist dieselbe Domain, nur anders dargestellt)
4. Falls du sie nicht direkt siehst: Sie könnte auch als **"Domain-Alias"** unter der Haupt-Domain `naturheilpraxis-straehuber.de` eingehängt sein, statt als eigene Domain zu erscheinen. Dann findest du sie, indem du auf die Haupt-Domain klickst und dort nach einem Reiter/Abschnitt **"Aliase"** oder **"Domain-Aliase"** schaust.

---

## Schritt 2: SSL-Zertifikat ausstellen

1. Bei der gefundenen Domain (egal ob eigene Domain oder Alias) auf **"SSL/TLS-Zertifikate"** klicken (manchmal auch als Icon mit Schloss-Symbol dargestellt).
2. Dort sollte eine Option **"Let's Encrypt"** oder **"Kostenloses Zertifikat holen"** zu sehen sein.
3. Darauf klicken. Falls ein Formular erscheint:
   - E-Mail-Adresse eintragen (z.B. deine info@nhp-straehuber.de) – wird für Ablauf-Erinnerungen genutzt.
   - Häkchen setzen bei der Domain selbst UND (falls als Option vorhanden) bei **"www.[Domain]"** – beide mit anhaken, falls beide angeboten werden.
   - **Wichtig, falls es dort eine Checkbox namens "Nur für diese Domain sichern" oder "Redirect www zu non-www" gibt:** einfach die Standardauswahl lassen, das ist hier nicht relevant.
4. Auf **"Holen"** / **"Sichern"** klicken. Das dauert meist nur wenige Sekunden bis 1-2 Minuten.
5. Wenn eine Fehlermeldung kommt wie *"Domain-Alias wird nicht unterstützt"* oder *"IDN nicht unterstützt"*: das wäre ein Hinweis, dass diese Kombination (Umlaut-Domain als Alias) technisch schwieriger ist – in dem Fall bitte kurz Bescheid geben, dann schauen wir nach einer Alternative (z.B. die Domain als eigenständige Domain statt als Alias einrichten).

---

## Schritt 3: Weiterleitung prüfen/anpassen (auf einen Hop reduzieren)

Aktuell läuft die Weiterleitung in zwei Schritten (Umlaut-Domain → www-Version ohne https → www-Version mit https). Das ist nicht kritisch, aber besser wäre ein einziger direkter Sprung.

1. Bei derselben Domain/Alias auf **"Hosting-Einstellungen"** oder **"Weiterleitung"** (engl. "Forwarding") klicken.
2. Falls dort ein Weiterleitungsziel eingetragen ist (z.B. `http://www.naturheilpraxis-straehuber.de`), das **https://** davor setzen, also auf `https://www.naturheilpraxis-straehuber.de` ändern.
3. Speichern.

Falls du diesen Bereich nicht findest oder unsicher bist, was dort steht: **Schritt 3 einfach weglassen** – Schritt 2 (das SSL-Zertifikat) ist der eigentlich wichtige Teil, der das Problem behebt. Der doppelte Sprung danach ist nur ein kleiner Bonus-Fix, kein Muss.

---

## Schritt 4: Testen, ob es geklappt hat

Nach ein paar Minuten Wartezeit (Zertifikate brauchen manchmal etwas, bis sie aktiv sind):

1. Browser öffnen (am besten ein privates/Inkognito-Fenster, damit nichts aus dem Cache kommt).
2. Adresse eingeben: `https://naturheilpraxis-strähuber.de`
3. **Erfolg** = du landest ohne Warnmeldung auf `https://www.naturheilpraxis-straehuber.de`
4. **Noch nicht erfolgreich** = Browser zeigt eine Zertifikats-Warnung ("Verbindung ist nicht privat" o.ä.) – dann ist das Zertifikat noch nicht (vollständig) aktiv, kurz warten und nochmal probieren, oder mir Bescheid geben, dann prüfe ich es von hier aus per Testabfrage.

---

**Sag mir einfach Bescheid, wenn du fertig bist – ich prüfe dann von hier aus per Testabfrage (curl), ob die HTTPS-Weiterleitung jetzt sauber funktioniert.**
