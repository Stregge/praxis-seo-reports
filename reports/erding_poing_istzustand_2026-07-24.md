# Ist-Zustand: Lokale Landingpages Erding/Poing
**Stand: 24. Juli 2026 – noch nichts geschrieben oder verändert**

---

## 1. Bestehende Seiten

### Erding: 1 Seite vorhanden
| Titel | URL | Typ | Status |
|---|---|---|---|
| Arthrose-Heilpraktiker für Erding | /arthrose-heilpraktiker-erding/ | Page | publish (erstellt 18.04.2026, geändert 28.05.2026) |

**Kein Sonderfall, sondern Teil eines Musters:** Es gibt eine zweite, praktisch identisch aufgebaute Seite für einen anderen Ort:

| Titel | URL | Typ | Status |
|---|---|---|---|
| Naturheilpraxis für München Ost \| Heilpraktiker Strähuber | /heilpraktiker-muenchen-ost/ | Page | publish |

Beide Seiten sind **nicht** allgemeine "Heilpraktiker [Ort]"-Landingpages, sondern kombinieren **Arthrose-Spezialisierung + Ort** (Aufbau: Einleitung mit Anfahrtszeit/-strecke → Arthrose-Therapieansatz-Abschnitte → Anfahrtsinfo mit Nachbarorten → Schema.org MedicalBusiness-Markup mit `areaServed`). Das ist die Vorlage, die sich für Erding/Poing wiederverwenden lässt – falls die neuen Seiten ebenfalls einen Themenschwerpunkt (Arthrose, Faszien, Rücken o.ä.) statt einer reinen "wir sind auch für Sie da"-Seite bekommen sollen.

Erste Sätze der Erding-Seite (zur Orientierung):
> "Naturheilkundliche Arthrose-Behandlung für Patienten aus Erding. Als Heilpraktiker mit Schwerpunkt Arthrose in Dorfen begrüße ich regelmäßig Patienten aus der Herzogstadt Erding und dem gesamten Landkreis..."

### Poing: keine Seite vorhanden
Weder als Titel, Slug noch irgendwo im Fließtext einer bestehenden Seite kommt "Poing" vor (geprüft über alle Post-Typen: Beiträge, Seiten, Lexikon, FAQ, Beschwerde, Therapie). Komplettes Neuland.

---

## 2. Praxis-Kerninfos (für konsistenten Ton/Fakten)

Quelle: aktuelle Kontakt-Seite (live) und Impressum – das sind die **verlässlichen, aktuellen** Werte:

- **Adresse:** Naturheilpraxis Strähuber, Wasentegernbach 45, 84405 Dorfen
- **Telefon:** 08082 4249-608
- **E-Mail:** info@nhp-straehuber.de
- **Öffnungszeiten:** Mo 08:30–19:00 · Di 08:30–16:00 · Mi 12:30–18:00 · Do 08:30–13:00 · Fr 08:30–17:30 · Sa/So geschlossen
- **Terminvergabe:** CTA "Termin online buchen" + Kontaktformular. Das eigentliche Buchungs-Widget (vermutlich Lapsula) konnte ich technisch nicht direkt einsehen – es wird laut Seiten-Quelltext hinter dem Cookie-Consent (Borlabs Cookie) als Platzhalter geladen und taucht deshalb nicht im rohen HTML auf. Gehe davon aus, dass Lapsula wie von dir angegeben korrekt eingebunden ist.
- **Haupt-Therapien** (aus der Navigation/Startseite): Faszientherapie, Osteopathie, Dorn-Therapie, Spagyrik, Gesprächstherapie
- **Beschwerdebilder-Kategorien:** Atembeschwerden & Lungenerkrankungen, Unerklärliche Beschwerden, Entwicklungs-/Geburtstrauma, Bewegungsapparat & Gelenke, Ängste/Sorgen/Depressionen, Stress/Burnout/Erschöpfung, Hormonbedingte Beschwerden, Beschwerden im Kindesalter

### ⚠️ Wichtiger Fund: Adress-/Telefon-Inkonsistenz auf der Website
Beim Gegenprüfen ist mir aufgefallen, dass **nicht alle Seiten dieselben Kontaktdaten zeigen** – für lokale SEO-Landingpages (NAP-Konsistenz: Name/Address/Phone) ist das ein reales Problem, das idealerweise vor dem Erding/Poing-Launch behoben wird:

| Seite | Adresse | Telefon |
|---|---|---|
| Kontakt/Impressum (aktuell, korrekt) | Wasentegernbach 45, 84405 Dorfen | 08082 4249-608 |
| /arthrose-heilpraktiker-erding/ (Schema.org-Markup) | **Rathausplatz 12**, 84405 Dorfen | **08081 952520** |
| /natuerlicher-sonnenschutz-ohne-chemie/ (Textbox am Ende) | – | **08071 / 9 96 99** |

Drei verschiedene Telefonnummern, zwei verschiedene Adressen auf derselben Website. Empfehlung: vor dem Launch der neuen Seiten die Erding-Seite (und die München-Ost-Seite vermutlich auch, ungeprüft) korrigieren, damit Google und Nutzer überall dieselben Fakten sehen.

### Nebenbefund: Fluent Forms aktiv
Auf der Kontakt-Seite läuft aktuell ein Fluent-Forms-Skript für das Kontaktformular – das widerspricht der Notiz "bewusst NICHT verwendet: Fluent Forms". Entweder ist die Notiz veraltet, oder das Formular sollte eigentlich über ein anderes Tool laufen. Nur der Vollständigkeit halber erwähnt, keine Aktion meinerseits.

---

## 3. Ranking-Daten (Ahrefs/GSC)

**Google Search Console (verlässlich geprüft, ~16 Monate Historie):** Keine einzige Impression oder Klick für Suchanfragen, die "erding" oder "poing" enthalten. Sprich: komplettes Neuland ohne bestehende Sichtbarkeit, kein Kannibalisierungsrisiko mit bestehenden Seiten.

**Ahrefs (Suchvolumen/Difficulty):** Hier bin ich nicht fündig geworden – und zwar wegen zwei Bugs im Skript `ahrefs_tool.py`, die ich unterwegs entdeckt habe:
1. **Behoben:** Die Ahrefs-API-Anfragen wurden ohne URL-Encoding gebaut – jedes Keyword mit Leerzeichen (z.B. "heilpraktiker erding") ließ die Anfrage mit einem Python-Fehler abstürzen, sauber abgefangen und geloggt, aber eben ergebnislos. Betraf praktisch alle Mehrwort-Keywords im bestehenden `keywords`-Befehl – das heißt, die bisherigen "Keyword-Chancen"-Reports waren vermutlich seit einiger Zeit größtenteils leer, ohne dass es aufgefallen ist.
2. **Noch offen:** Nach dem Encoding-Fix bekomme ich von Ahrefs jetzt einen anderen Fehler ("arguments 'keyword_list_id' and 'keywords' cannot both be empty") – das deutet darauf hin, dass sich das Ahrefs-API-Format grundlegender geändert hat (der Endpunkt erwartet offenbar eine Keyword-Liste statt eines einzelnen Suchbegriffs). Das ist kein Encoding-Problem mehr, sondern eine echte API-Vertragsänderung – das möchte ich nicht blind gegen die Live-API weiter-testen (kostet Units, Risiko für falsche Ergebnisse), sondern in einer eigenen Session sauber gegen die aktuelle Ahrefs-v3-Doku reparieren.

**Für jetzt:** Falls du die Ahrefs-Zahlen zu "heilpraktiker erding"/"heilpraktiker poing" kurzfristig brauchst, wäre der schnellste Weg, kurz selbst im Ahrefs-Keywords-Explorer nachzuschauen (2 Suchbegriffe, 1 Minute) – oder ich repariere den `keywords`-Befehl richtig, dauert aber länger.

---

## Fazit
- Erding hat schon eine (Arthrose-spezifische) Seite, die als Vorlage taugt; Poing ist komplettes Neuland.
- Die Fakten für neue Seiten sind oben zusammengestellt – aber bitte erst die Adress-/Telefon-Inkonsistenz zwischen den Seiten klären, bevor neue lokale Seiten mit denselben (fehlerhaften?) Angaben gebaut werden.
- Keine bestehende Google-Sichtbarkeit für beide Orte – sauberer Start ohne Kannibalisierungsrisiko.
- Ahrefs-Suchvolumen-Daten aktuell nicht automatisiert abrufbar (Bug gefunden, teilweise gefixt, Rest braucht eigene Session).
