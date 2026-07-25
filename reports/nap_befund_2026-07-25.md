# NAP-Konsistenz-Prüfung – Befund (noch NICHTS geändert)
**Stand: 25. Juli 2026**

## Verbindliche Quelle (Impressum)
- **Name:** Roland Strähuber / Naturheilpraxis Strähuber
- **Adresse:** Wasentegernbach 45, 84405 Dorfen
- **Telefon:** 08082 4249-608 (`tel:+4980824249608`)
- **E-Mail:** info@nhp-straehuber.de

Site-weit geprüft (alle veröffentlichten Beiträge/Seiten/Lexikon/FAQ/Beschwerde/Therapie-Einträge) über zwei Methoden: Regex-Suche nach Telefonmustern/Adressbegriffen im Text UND gezielte Suche nach allen `tel:`-Links und Schema.org-Blöcken (verlässlicher als reine Textsuche, da Formatierungen stark variieren).

## Korrekt (keine Änderung nötig)
| Seite | Gefunden |
|---|---|
| Impressum | Quelle selbst |
| Datenschutz | Wasentegernbach 45 / 08082 4249-608 ✓ |
| /rotlichttherapie-rueckenschmerzen-gelenke/ | Wasentegernbach 45 / 08082 4249-608 ✓ (Autoren-Signatur) |

## Gefundene Abweichungen – 5 Seiten

| # | Seite | Aktuell hinterlegt | Soll werden |
|---|---|---|---|
| 1 | **/arthrose-heilpraktiker-erding/** (sichtbarer Text) | "Rathausplatz 12, 84405 Dorfen" / "Telefon: 08081 952520" | "Wasentegernbach 45, 84405 Dorfen" / "Telefon: 08082 4249-608" |
| 1b | **/arthrose-heilpraktiker-erding/** (Schema.org JSON-LD) | `telephone: "+49-8081-952520"`, `streetAddress: "Rathausplatz 12"` | `telephone: "+49-8082-4249608"`, `streetAddress: "Wasentegernbach 45"` |
| 2 | **/heilpraktiker-muenchen-ost/** (sichtbarer Text) | "Rathausplatz 12, 84405 Dorfen" / "Telefon: 08081 952520" (identisch zu Erding-Seite) | "Wasentegernbach 45, 84405 Dorfen" / "Telefon: 08082 4249-608" |
| 2b | **/heilpraktiker-muenchen-ost/** (Schema.org JSON-LD) | `telephone: "+49-8081-952520"`, `streetAddress: "Rathausplatz 12"`, **zusätzlich:** `url: ".../naturheilpraxis-muenchen-ost/"` (falsche Slug – Seite liegt tatsächlich unter `/heilpraktiker-muenchen-ost/`) | `telephone: "+49-8082-4249608"`, `streetAddress: "Wasentegernbach 45"`, `url: ".../heilpraktiker-muenchen-ost/"` |
| 3 | **/natuerlicher-sonnenschutz-ohne-chemie/** (Empfehlungsbox am Ende) | `tel:+4987199699` → "08071 / 9 96 99" | `tel:+4980824249608` → "08082 4249-608" |
| 4 | **/das-lifewave-x39-pflaster-mehr-vitalitaet-durch-innovative-lichttherapie/** | `tel:+4987109576730` → "08710 9576730" | `tel:+4980824249608` → "08082 4249-608" |
| 5 | **/warum-ich-das-lavita-vitalstoffkonzentrat-empfehle/** | `tel:+4980819074630` → "08081 / 90 74 630" | `tel:+4980824249608` → "08082 4249-608" |

**Auffällig:** Alle 5 falschen Nummern sind unterschiedlich (nicht derselbe Zahlendreher) und keine ähnelt der echten – sieht nach frei erfundenen, plausibel wirkenden Platzhalter-Telefonnummern aus der Content-Erstellung aus (z.B. durch eine KI beim Text-Erstellen "erfunden"), nicht nach Tippfehlern an der echten Nummer.

## ⚠️ Zusätzliches Problem, das über reines Datenaustauschen hinausgeht

Sowohl die Erding- als auch die München-Ost-Seite enthalten **Anfahrtsbeschreibungen, die sich explizit auf "Rathausplatz" beziehen** (z.B. München-Ost: *"kostenlose Parkplätze direkt am Rathausplatz in unmittelbarer Nähe der Praxis"*; Erding: *"Kostenlose Parkplätze stehen Ihnen direkt in der Nähe der Praxis am Rathausplatz zur Verfügung"*). Wenn die Praxis tatsächlich in der Wasentegernbach 45 liegt, könnte diese Parkplatz-Aussage **inhaltlich falsch** werden, nicht nur die reine Adresszeile. Fahrzeit-Angaben (Erding: "ca. 20 Min. über die B388", München Ost: "ca. 35 Min. über die A94") könnten je nach genauer Lage der Wasentegernbach-Adresse ebenfalls leicht abweichen.

**Ich kann die Adresse/Telefonnummer 1:1 austauschen, aber die Anfahrts-/Parkplatz-Sätze inhaltlich korrekt umformulieren ist eher eine Aufgabe für den Text-Chat (Claude), da ich die tatsächliche Lage/Parksituation an der Wasentegernbach 45 nicht kenne.** Vorschlag: Ich tausche die reinen Kontaktdaten (Adresse/Telefon/Schema) jetzt aus, lasse aber die Parkplatz-Sätze unverändert und markiere sie dir separat zur inhaltlichen Prüfung – oder du sagst mir, dass ich sie ebenfalls schon entschärfen soll (z.B. "kostenlose Parkplätze in der Nähe der Praxis" ohne "Rathausplatz"-Ortsangabe).

---

**Noch nichts geändert.** Warte auf dein "ok" (und deine Entscheidung zur Parkplatz-Formulierung) für Teil 1, bevor ich live setze. Danach Teil 2 (Umlaut-Domain).

---

## Status: Live gesetzt und verifiziert (25.07.2026, 12:36 Uhr)

Alle 5 Korrekturen wurden live gesetzt und direkt danach per API-Abfrage verifiziert (Rohinhalt erneut gelesen, nicht nur auf die Erfolgsmeldung vertraut):

| Seite | Wasentegernbach 45 | 08082 4249-608 | Alte falsche Werte weg |
|---|---|---|---|
| Erding | ✅ | ✅ | ✅ |
| München-Ost (+ korrigierte Schema-URL) | ✅ | ✅ | ✅ |
| Sonnenschutz | – (keine Adresse dort) | ✅ | ✅ |
| LifeWave X39 | – (keine Adresse dort) | ✅ | ✅ |
| LaVita | – (keine Adresse dort) | ✅ | ✅ |

Anfahrts-/Parkplatz-Sätze mit "Rathausplatz"-Bezug wie besprochen unverändert gelassen (je 1x auf Erding- und München-Ost-Seite) – zur separaten inhaltlichen Prüfung.

**Teil 1 (NAP-Konsistenz) abgeschlossen.**
