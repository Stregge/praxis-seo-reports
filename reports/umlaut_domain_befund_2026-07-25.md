# Umlaut-Domain naturheilpraxis-strähuber.de – Befund
**Stand: 25. Juli 2026**

## Technischer Zustand

Die Domain läuft nicht als eigene Installation und ist keine Parking-Seite – es ist bereits eine serverseitige Weiterleitung eingerichtet (Plesk-Ebene, erkennbar am Header `X-Powered-By: PleskLin`). Das Problem liegt woanders:

| Protokoll | Test | Ergebnis |
|---|---|---|
| HTTP | `http://naturheilpraxis-strähuber.de/` | 301 → `http://www.naturheilpraxis-straehuber.de/` → (2. Hop) → `https://www.naturheilpraxis-straehuber.de/` → 200 OK |
| HTTP, spezifischer Artikel | `http://naturheilpraxis-strähuber.de/faszientherapie/` | 301 → `http://www.naturheilpraxis-straehuber.de/faszientherapie/` (Pfad bleibt korrekt erhalten – gut) |
| **HTTPS** | `https://naturheilpraxis-strähuber.de/` | **Fehler: SSL certificate problem: self-signed certificate** – keine Weiterleitung, Verbindung schlägt fehl |

## Root Cause

**Für die Umlaut-Domain ist kein gültiges SSL-Zertifikat eingerichtet** – nur ein Plesk-Standard-Zertifikat (self-signed). Die eigentliche Weiterleitungsregel funktioniert technisch korrekt und behält sogar den Pfad bei (nicht nur pauschal auf die Startseite) – aber nur über **unverschlüsseltes HTTP**. Sobald jemand (ein Browser, ein Backlink, oder ein Crawler wie der von Ahrefs) die Seite über **HTTPS** aufruft – was heute der Standard ist – bricht die Verbindung mit einem Zertifikatsfehler ab, bevor die Weiterleitung überhaupt greift.

**Das erklärt vermutlich die 238 Dofollow-Links in Ahrefs:** Wenn externe Seiten mit `https://naturheilpraxis-strähuber.de/...` verlinken (heute Standard), landet der Ahrefs-Crawler nicht bei der sauberen 301-Weiterleitung, sondern bei einem SSL-Fehler – die Backlinks werden dadurch der (kaputten) Umlaut-Domain zugeordnet, statt sauber als Weiterleitung auf die Hauptdomain erkannt und konsolidiert zu werden.

Nebenbefund: Selbst über HTTP läuft die Weiterleitung in **zwei Hops** (erst zur HTTP-www-Version, dann zur HTTPS-www-Version) statt direkt in einem sauberen 301 zum finalen Ziel – nicht kritisch, aber unnötig.

## Was zu tun wäre

1. **Gültiges SSL-Zertifikat für die Umlaut-Domain ausstellen** (z.B. Let's Encrypt über Plesk – Plesk unterstützt IDN-Domains dafür in der Regel direkt).
2. **Weiterleitungsregel auf einen einzigen 301-Hop direkt zu `https://www.naturheilpraxis-straehuber.de/$PFAD` umstellen**, statt der aktuellen Zwei-Hop-Kette.

## ⚠️ Ich kann das nicht selbst umsetzen

Das ist eine **Plesk-Hosting-Panel-Einstellung** (SSL-Zertifikat + Weiterleitungsregel auf Serverebene), keine WordPress-Einstellung. Ich habe dafür keinen Zugriff – es gibt kein `.env.plesk` oder vergleichbare Zugangsdaten auf diesem Server (nur `.env.wordpress`, `.env.ahrefs`, `.env.gsc`, `.env.marky`, `.env.gemini`). Das müsstest du entweder:

- selbst kurz im Plesk-Panel erledigen (Let's Encrypt-Zertifikat für die Domain aktivieren + Weiterleitung auf einen Hop reduzieren), oder
- mir Plesk-Zugangsdaten geben, falls das Panel eine API hat, die ich nutzen könnte (müsste ich dann prüfen, ob Netcup/Plesk das für diesen Tarif anbietet).

Ich kann dir bei Bedarf eine Schritt-für-Schritt-Anleitung für Plesk schreiben, wenn du das selbst machen willst.

---

**Status: Nur Befund, keine Änderung vorgenommen** (technisch auch nicht möglich ohne Plesk-Zugriff).
