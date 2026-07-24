# SiteGuru – Detailaufschlüsselung Sitemap & Meta-Descriptions
**Stand: 22. Juli 2026 – naturheilpraxis-straehuber.de**

---

## Sitemap-Problem: 3 betroffene URLs

Es fehlt **keine** Seite in der Sitemap (0 fehlende Seiten). Das Problem sind **3 URLs, die IN der Sitemap stehen, aber auf eine andere Adresse weiterleiten** (Redirect statt direktem Ziel):

1. `/hexenschuss-was-tun/`
2. `/arthrose-schlafen-tipps/`
3. `/arthrose-protokoll-heilpraktiker/`

**Was das bedeutet:** Google bekommt über die Sitemap eine URL genannt, landet dort aber nur nach einer Weiterleitung – das verschwendet Crawl-Budget und verzögert Indexierung leicht. SiteGuru hat das Redirect-Ziel nicht mitgeliefert (http_status/redirects_to leer) – das müsste direkt im WordPress/RankMath geprüft werden (vermutlich alte URLs, die umbenannt wurden).

**Fix:** In der Sitemap sollten die aktuellen Ziel-URLs stehen, nicht die alten Redirect-Quellen. Das behebt sich meist automatisch, sobald RankMath die Sitemap neu generiert – zu prüfen, ob diese 3 alten Slugs noch aktiv irgendwo verlinkt sind (intern) und ggf. dort direkt auf die neue URL verweisen.

Report: https://app.siteguru.co/sites/sitemap_report/89094

---

## Meta-Description-Problem: 20 betroffene Seiten

Kriterium: 120–170 Zeichen ist der Zielbereich. Alle 20 Seiten sind **"zu kurz"**, eine davon **komplett leer**.

### Echte Content-/Themenseiten (Priorität – bringen Suchtraffic)
| Seite | Aktuelle Länge | Text |
|---|---|---|
| /therapie/spagyrik/ | 115 | "Die Spagyrik gehört zu den natürlichen Heilmitteln. Ich wende diese Form der Therapie in meiner Naturheilpraxis an." |
| /lexikon/faszientherapie/ | 116 | "Faszientherapie löst Faszienverklebungen und lindert Schmerzen. Jetzt mehr über sanfte Behandlungsmethoden erfahren!" |
| /lexikon/entzuendungsmarker/ | 116 | "Entzündungsmarker zeigen Entzündungen im Körper an. Erfahren Sie mehr über Diagnose und Therapie. Jetzt informieren!" |
| /lifewave-pflaster-die-akupunktur-fuer-zu-hause/ | 112 | "LifeWave Pflaster als moderne Akupunktur: Wie sie funktionieren und was meine Patienten in Dorfen damit erleben." |
| /hintern-juckt-bei-kindern/ | 110 | "Juckreiz am Po bei Kindern: Häufige Ursachen wie Würmer oder Pilze und was du ganzheitlich dagegen tun kannst." |
| /beschwerde/beschwerden-im-kindesalter/ | 108 | "Alle Beschwerden von Erwachsenen können ebenso im Kindesalter auftreten und gleichsam gut therapiert werden." |
| /lexikon/fettleber/ | 74 | "Eine Fettleber kann durch eine Kombination von Faktoren verursacht werden:" |

→ **Achtung: "Faszientherapie löst ... lindert Schmerzen"** – das ist ein Heilversprechen (HWG-Verstoß, Regel #2). Muss bei Überarbeitung sachlicher formuliert werden ("kann unterstützen" statt "löst/lindert").

### Archiv-/Übersichtsseiten (niedrigere Priorität, aber leicht zu fixen)
| Seite | Länge | Text |
|---|---|---|
| /faq/ | 65 | "FAQs Archive - Naturheilpraxis Strähuber von Heilpraktiker Roland" |
| /lexikon/ | 68 | "Lexikon Archive - Naturheilpraxis Strähuber von Heilpraktiker Roland" |
| /beschwerde/ | 72 | "Beschwerden Archive - Naturheilpraxis Strähuber von Heilpraktiker Roland" |
| /therapie/ | 70 | "Therapien Archive - Naturheilpraxis Strähuber von Heilpraktiker Roland" |
| /beschwerden/ | 0 | **fehlt komplett** (Duplikat-Archiv-URL zu /beschwerde/ – prüfen, ob das überhaupt eine echte, separate Seite sein soll) |

### FAQ-Einzelseiten (Antwort ist der Meta-Text – SEO-Nutzen gering, da Snippet meist aus der Frage/Antwort selbst kommt)
| Seite | Länge | Text |
|---|---|---|
| /faq/kann-ich-mit-post-covid-oder-post-vac-symptomen-kommen/ | 107 | "Ja, ich habe hierzu schon einige Patienten behandelt und mich auch in diese Richtung mehrfach fortgebildet." |
| /faq/meine-symptome-sind-nur-ab-und-zu-da/ | 89 | "Auch in diesem Fall handelt es sich ja um eine Thematik, die ihre Lebensqualität mindert." |
| /faq/gibt-es-zu-ihren-behandlungsmethoden-auch-weiterfuehrende-literatur-die-sie-mir-empfehlen-koennen/ | 41 | "Ich kann Ihnen folgende Bücher empfehlen:" |
| /faq/machen-sie-auch-hausbesuche/ | 33 | "Nein, Hausbesuche gebe ich keine." |
| /faq/bieten-sie-auch-online-termine-an/ | 35 | "Ja auch Onlinetermine sind möglich." |
| /faq/wie-alt-sollte-ein-kind-sein-damit-sie-es-behandeln-koennen/ | 58 | "Auch kleine Kinder und auch Babys können behandelt werden." |
| /faq/wonach-berechnen-sie-die-kosten-ihrer-behandlungen/ | 97 | "Die Kosten meiner Behandlungen rechne ich nach der Gebührenordnung für Heilpraktiker (GebüH) ab." |

### Rechtsseite (laut SiteGuru-Empfehlung meist keine Priorität)
| Seite | Länge | Text |
|---|---|---|
| /impressum/ | 42 | "Hier finden Sie alle Kontaktdaten von mir." |

---

Report: https://app.siteguru.co/sites/report/meta_description/89094
