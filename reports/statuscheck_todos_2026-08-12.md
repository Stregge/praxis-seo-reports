# Statuscheck – Antwort auf Briefing vom 12.08.2026
**Stand: 12. August 2026 – reine Bestandsaufnahme, nichts ausgeführt/verändert**

## Hohe Priorität

**1. Mikronährstoffanalyse (Post-ID 33861) – teilweise erledigt**
Seite steht weiterhin als **Entwurf** (nicht veröffentlicht). Von den 4 offenen Punkten:
- Preise: weiterhin Platzhalter, nicht befüllt
- Vorschau-Freigabe: noch nicht erfolgt
- CTA-Verlinkung: zeigt vorläufig auf `/kontakt/`, keine direkte Lapsula-URL ermittelbar
- Lapsula-Terminart/WhatsApp-Setup: offen, kein Lapsula-Zugang vorhanden
Alle 4 Punkte identisch zum Stand vom 10.08. – nichts hat sich seither bewegt.

**2. FAQ-Links in die drei Bricks-Seiten – erledigt**
Alle 11 Links (Kontakt 4, Ablauf 5, Über mich 2) live verifiziert, siehe
`faq_bricks_links_ergebnis_2026-08-12.md`.

**3. FAQ-Schema Hexenschuss + 4 Rücken-Artikel – offen**
Laut aktuellstem Schema-Check (10.08.): `hexenschuss-was-tun` zeigt weiterhin einen Google-Rich-Results-Fehler
mit FAQPage-Schema (unverändert seit Block 1). Die 4 neuen Rücken-Artikel
(ruecken-uebungen, bandscheibenvorfall-lws-syndrom, ischias-ischiasnerv, rueckenschmerzen)
tauchen im aktuellen Schema-Report **ohne** FAQPage-Typ auf – d.h. dort wurde nie FAQ-Schema
gesetzt (bekannte RankMath-API-Einschränkung, seit Block 1 bewusst nicht weiterverfolgt).
Nichts hat sich seit dem letzten Stand geändert – wartet weiterhin auf manuelle Bearbeitung
in wp-admin.

## Mittlere Priorität

**4. Meta Descriptions (5 neue + 13 alte Seiten) – kein Beleg für Umsetzung gefunden**
Ich habe einen Übergabe-Text vom 24.07. (`meta_description_uebergabe_chat_2026-07-24.md`,
7 Seiten mit zu kurzer Meta-Description, HWG-geprüft) und einen Vorher/Nachher-Vergleich
gefunden. Das war die Text-Vorbereitung (Chat-Seite). Ob die fertigen Texte seither tatsächlich
per wp_publish.py gesetzt wurden, kann ich anhand meiner Unterlagen nicht bestätigen – kein
Ausführungs-Log dazu gefunden. Bitte bei dir/Chat nachfragen, ob die Freigabe schon zurückkam.

**5. PageSpeed Insights in Ahrefs aktiviert? – kann ich nicht per API prüfen**
Das ist eine Projekteinstellung im Ahrefs-Dashboard selbst, nicht über die Site-Audit-API
abfragbar. Der Performance-Report läuft zwar wöchentlich automatisiert weiter
(`ahrefs_performance_report_2026-08-10.md` existiert), aber ob PSI-Daten darin *aktiv* sind,
sehe ich anhand der API-Response nicht zweifelsfrei. Müsste im Ahrefs-Dashboard geprüft werden.

**6. E-Mail-Versand für ai_visibility-Report – offen**
Im Cron läuft `ahrefs_tool.py ai_visibility` monatlich, aber es gibt keinen E-Mail-Versand-Schritt
im Code oder Cron – nur Speichern + GitHub-Push. Kein E-Mail-Versand eingerichtet.

**7. Cannibalization konsolidiert (Heilpraktiker-bei-Arthrose, Silent Inflammation) – kein Beleg für Umsetzung**
Analyse vom 06.07. vorhanden (`gsc_cannibalization_auswertung_2026-07-06.md`), die
"heilpraktiker bei arthrose"-Konflikte (3 Seiten) identifiziert. Keine Folge-Datei zu
Redirects/Konsolidierung danach gefunden. Vermutlich noch offen – bitte prüfen, ob das separat
mit Chat besprochen/entschieden wurde.

**8. Faszien-Cluster-Performance in GSC erneut gecheckt? – kein aktueller Report gefunden**
Kein dedizierter Faszien-Cluster-GSC-Report seit dem letzten mir bekannten Stand gefunden.
Offen bzw. nicht in meinen Unterlagen sichtbar.

**9. Monatlicher Content-Strategie-Report – läuft nicht automatisiert**
Kein entsprechender Cron-Eintrag, kein Skript dafür in `/root/praxis-seo/` vorhanden. Falls es
das gibt, läuft es außerhalb meines Systems (z.B. manuell von Chat erstellt).

**10. Ischias-Selbsttest-Widget im Browser getestet – nein, noch nicht**
Ich habe aktuell keinen Zugriff auf ein Browser-Tool in dieser Session. Nicht durchgeführt.

**11. Domain networkring.de – teilweise geklärt**
DNS zeigt auf eine andere IP (91.230.22.26) mit Mailrouting über "webhoster.de/.org/.at" –
technisch nicht mit deiner eigenen Infrastruktur (Netcup-Server) verbunden, wirkt wie ein
generisches Drittanbieter-Hosting. Ohne zu wissen, wo genau dir die Domain aufgefallen ist
(Referrer-Traffic? Backlink-Report? E-Mail-Header?), kann ich den Kontext aber nicht
abschließend klären – dafür bräuchte ich die Fundstelle.

## Niedrige Priorität

**12–19. Silent-Inflammation-Cluster, Persönlichkeitsarbeit-Cluster, wp_publish.py Stufe 2,
Erding/Poing-Landingpages, Arthrose-Pillar-Modell, RankMath-Onpage-Scores (Bluthochdruck/Jacobsen),
Phase-5-Technik-Batch, NeuronWriter-Workflow – keine Belege in meinen Unterlagen**
Für keinen dieser Punkte finde ich Dateien, Cron-Einträge oder Code-Änderungen, die auf eine
Bearbeitung hindeuten (Ausnahme: Erding/Poing hat eine Ist-Zustand-Analyse vom 24.07.,
`erding_poing_istzustand_2026-07-24.md`, aber keine sichtbare Fortsetzung danach). Alle
vermutlich offen, oder auf Chat-Seite in Bearbeitung ohne dass es bei mir ankam – bitte dort
nachfragen, damit ich hier nicht rate.

## Später evaluieren

**20. ClickRank/Respona/Visby – kein Beleg für eine Prüfung**
Keine Unterlagen dazu gefunden.

---

## Was sich seit dem 10.08.-Briefing am meisten bewegt hat

Zwei kompakte, in sich abgeschlossene Sachen kamen seit dem 10.08. dazu, beide nicht auf deiner
Liste, weil sie danach entstanden sind:
1. **FAQ-Links in die drei Bricks-Seiten** (Punkt 2 oben) – inklusive erstmaligem SSH/WP-CLI-Zugang
   zum Hosting-Server, der jetzt für ähnliche Aufgaben wiederverwendbar bereitsteht
   (`/root/.env.netcup-hosting`, chmod 600).
2. Der Bricks-Zugriffsweg selbst ist jetzt als funktionierendes, getestetes Verfahren dokumentiert
   (WP-CLI + `--user=ClaudeCode` + gezielte Cache-Leerung) – relevant für alle künftigen Aufgaben,
   die Bricks-Seiten betreffen (z.B. falls Über mich/Ablauf/Kontakt nochmal angepasst werden sollen).

Ansonsten: Zwischen dem 05.08. (FAQ-Verlinkungsprojekt) und dem 10.08. sehe ich in meinen
Unterlagen keine Aktivität zu den mittleren/niedrigen Prioritätspunkten – die scheinen seit
Mitte Juli/Anfang August nicht angefasst worden zu sein, jedenfalls nicht über mich.
