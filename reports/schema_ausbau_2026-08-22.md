# Schema-Ausbau Priorität 1+2 – Ergebnis
**Stand: 22. August 2026**

## Zusammenfassung

Beide Prioritäten sind live umgesetzt und per echtem JSON-LD-Nachweis verifiziert (nicht nur
API-Rückmeldung). Unterwegs zwei echte RankMath-Bugs gefunden und behoben – beide erklären,
warum bereits vorhandene, korrekt eingegebene Daten monatelang nie im Live-Schema ankamen.

## Priorität 1: LocalBusiness/MedicalBusiness-Schema

**Überraschender Fund:** Alle geforderten Daten (Name, Adresse, Telefon, E-Mail, Geo-Koordinaten,
Öffnungszeiten) waren bereits **korrekt in der Datenbank hinterlegt** – vermutlich aus einer
früheren Einrichtung. Trotzdem erschienen sie nie im Live-Schema.

**Root Cause (echter RankMath-Bug):** Das Feld `knowledgegraph_type` stand auf `"organization"`,
der Code prüft aber intern nur auf die Werte `"company"` oder `"person"` – `"organization"` trifft
keinen der beiden Fälle, wodurch die komplette Organization/LocalBusiness-Ausgabe stillschweigend
übersprungen wurde. Zusätzlich stand `local_business_type` (das eigentliche Feld für den
Schema-Untertyp) auf `"LocalBusiness"` statt `"MedicalBusiness"` – ein separates, unbenutztes
Feld (`business_type`) hatte fälschlich den richtigen Wert, wurde aber vom aktuellen Code gar
nicht gelesen.

**Fix:**
- `knowledgegraph_type`: `organization` → `company` (= UI-Bezeichnung "Organization", wie von dir
  vorab autorisiert)
- `local_business_type`: `LocalBusiness` → `MedicalBusiness`
- `organization_description`: ersetzt durch deinen neuen Text (der alte Text stand noch auf
  "Dorfen bei München")
- Backup der kompletten Voreinstellung vor der Änderung:
  `/root/praxis-seo/backup/content/rankmath_options_titles_..._vor_schema_ausbau.json`
- Rundweg-Sicherheitstest (unverändert zurückschreiben) vor der echten Änderung durchgeführt

**Live-Nachweis (Startseite, JSON-LD):**
```json
{
  "@type": ["MedicalBusiness", "Organization"],
  "name": "Naturheilpraxis Strähuber",
  "address": { "streetAddress": "Wasentegernbach 45", "addressLocality": "Dorfen", ... },
  "telephone": "08082 4249-608",
  "email": "info@nhp-straehuber.de",
  "openingHours": ["Monday 08:30-19:00", "Tuesday 08:30-16:00", "Wednesday 12:30-18:00",
                    "Thursday 08:30-13:00", "Friday 08:30-17:30"],
  "description": "Naturheilpraxis von Heilpraktiker Roland Strähuber in Dorfen bei Erding. ...",
  "location": { "@id": ".../#place" }
}
```
Geo-Koordinaten im referenzierten Place-Knoten ebenfalls bestätigt (48.27567.../12.21905...).

**Öffnungszeiten:** Keine Rückfrage nötig – standen bereits korrekt hinterlegt (aus der
Kontakt-Seite bekannt: Mo–Fr, keine Wochenendzeiten), nichts erfunden.

## Priorität 2: Person-Schema Roland Strähuber

**Mechanismus:** RankMath baut die Autor-Person automatisch aus dem WordPress-Nutzerprofil des
tatsächlichen Post-Autors auf – kein separates, manuell zu pflegendes Schema-Objekt. `worksFor`
wird dabei **automatisch** mit dem Organization-Schema aus Priorität 1 verknüpft, sobald das
korrekt ausgegeben wird (kein Zusatzaufwand nötig – direkter Nutzen aus dem Fix oben).

**Gesetzt (Rolands WP-Profil, User-ID 2):**
- `description` (WordPress-Standard-Bio-Feld): dein Text
- `additional_profile_urls` (RankMath-Feld für `sameAs`): `/presse/`

**Zweiter RankMath-Bug gefunden:** Der Autor-Beschreibungstext im Schema kam trotz korrekt
gesetztem Bio-Feld zunächst nicht an. Ursache: RankMaths interner Code hängt beim Auslesen
automatisch das Präfix `rank_math_` an den Feldnamen – gesucht wurde also
`rank_math_description`, nicht das WordPress-Standardfeld `description`. Zusätzlich das Feld
`rank_math_description` mit demselben Text gesetzt, danach direkt im PHP-Code nachvollzogen
(nicht nur HTML-Output), dass RankMath ihn jetzt korrekt liest.

**Live-Nachweis (Artikel "arthrose-ohne-op-...", von Roland bereits korrekt autorisiert):**
```json
{
  "@type": "Person",
  "name": "Roland Strähuber",
  "description": "Roland Strähuber ist Heilpraktiker mit eigener Naturheilpraxis in Dorfen bei Erding und Autor von Fachartikeln in der AKOM (Angewandte Komplementärmedizin).",
  "sameAs": ["https://www.naturheilpraxis-straehuber.de/presse/"],
  "worksFor": { "@id": "https://www.naturheilpraxis-straehuber.de/#organization" }
}
```

**Ein Punkt, den RankMath nicht unterstützt:** `jobTitle` ("Heilpraktiker" als formale
schema.org-Eigenschaft) wird von RankMaths Autor-Schema-Mechanismus nicht ausgegeben – es gibt
im Code keine Property dafür. Der Beruf steht zwar im ersten Satz der Beschreibung, aber nicht
als eigenes, maschinenlesbares Feld. Keine Umgehung versucht (kein offizieller Weg gefunden,
der nicht riskant wäre) – das ist eine Grenze des Plugins, keine offene Aufgabe meinerseits.

## Priorität 3 / offene Entscheidung: Autor-Zuordnung der Artikel

Das Person-Schema greift nur, wenn `post_author` tatsächlich auf Rolands Account zeigt. Stand
der 70 veröffentlichten Blogartikel:

| Autor | Anzahl |
|---|---|
| Roland Strähuber (korrekt) | 36 |
| „manuski" (alter/anderer Account) | 23 |
| „ClaudeCode" (u.a. die zuletzt veröffentlichten Vitalstoff-Artikel, Presse, Mikronährstoffanalyse) | 11 |

Für die 34 Artikel mit „manuski"/„ClaudeCode" als Autor zeigt das Schema aktuell **nicht**
Roland als Person, sondern diese technischen Accounts – dort greift der neue Ausbau also noch
nicht. Das war nicht Teil des ursprünglichen Auftrags (der sich auf die Schema-Mechanik selbst
bezog), deshalb habe ich hier nichts bulk-verändert. Frage an dich: Sollen alle 34 Artikel auf
Roland als Autor umgestellt werden (reine Metadaten-Änderung, keine Inhalts- oder URL-Änderung,
leicht rückgängig zu machen)? Falls ja, mache ich das gerne als nächsten Schritt.

## Zusammenfassung

| Was | Status |
|---|---|
| LocalBusiness/MedicalBusiness-Schema | ✅ live verifiziert |
| Person-Schema Roland (bei korrekt zugeordneten Artikeln) | ✅ live verifiziert |
| worksFor-Verknüpfung | ✅ automatisch, live verifiziert |
| jobTitle | ❌ von RankMath nicht unterstützt (Plugin-Grenze) |
| Autor-Zuordnung bei 34 Artikeln | ⏳ offene Entscheidung, siehe oben |
