# Monatliche Report-Automatisierung: Klärung
**Stand: 13. August 2026**

## Teil 1: Monatlicher Content-Strategie-Report

**Ergebnis: Existiert nicht – weder als Skript noch als Konzept in meinen Unterlagen.**

Geprüft: `/root/praxis-seo/` komplett nach Skripten/Dateien mit "content"+"strategie" im
Namen oder Inhalt durchsucht, Crontab durchsucht, Memory durchsucht. Kein Treffer außer meiner
eigenen Erwähnung im Statuscheck vom 12.08. (dass er fehlt).

Ich baue hier bewusst nichts, wie im Auftrag verlangt – "Content-Strategie-Report" ist zu
unspezifisch, um es zu raten. Bevor ich etwas aufsetze, brauche ich von dir/Chat:

1. **Was soll drin stehen?** (z.B. Content-Cluster-Fortschritt, Keyword-Rankings-Entwicklung,
   welche Artikel als Nächstes geplant sind, GSC-Trend-Zusammenfassung ...?)
2. **Woher kommen die Daten?** (Ahrefs? GSC? Manuelle Planungsnotizen, die eigentlich bei
   Chat-Claude liegen?)
3. **Für wen/welches Format?** (Reiner Datenreport wie die anderen Ahrefs-Reports, oder eher ein
   strategisches Dokument mit Empfehlungen – Letzteres wäre eher Chat-Aufgabe als Code-Aufgabe,
   siehe Rollenaufteilung.)

Sobald das geklärt ist, baue ich das Skript + Cron in einem Rutsch.

## Teil 2: E-Mail-Versand für ai_visibility-Report

**Aktueller Stand:** Report wird monatlich per Cron erzeugt (`ahrefs_tool.py ai_visibility`,
1. des Monats 06:30 Uhr), landet als .md/.json in `/root/praxis-seo/output/` und wird automatisch
ins öffentliche GitHub-Reports-Repo gepusht (`_push_reports()`). Kein E-Mail-Versand bisher.

**Geprüft, warum E-Mail-Versand fehlt – zwei Wege durchgetestet, beide aktuell nicht nutzbar:**

1. **Dieser Claude-Code-Server (VPS):** Kein lokaler Mailserver installiert (kein
   sendmail/postfix/msmtp), kein Mail-Port offen, keine SMTP-Zugangsdaten in den `.env`-Dateien
   hinterlegt.
2. **WordPress-Hosting-Server** (über den neu eingerichteten SSH-Zugang geprüft, da die
   Domain-Mailbox dort vermutlich sowieso liegt): PHP ist zwar auf `sendmail_path` konfiguriert,
   aber das `/usr/sbin/sendmail`-Programm existiert in der chroot-Umgebung dieses
   Webhosting-Accounts gar nicht – ein echter Testversand ist entsprechend fehlgeschlagen
   (`mail()` lieferte `false`). Das ist eine bewusste Einschränkung des Hosting-Providers
   (Shared-Hosting erlaubt aus Spam-Schutzgründen meist keinen rohen Sendmail-Zugriff, sondern nur
   authentifizierten SMTP-Versand über die eigene Mailbox).

**Was ich konkret brauche, um das sauber einzurichten:**

Die **SMTP-Zugangsdaten der Mailbox info@nhp-straehuber.de** (oder eines dedizierten
Versand-Postfachs) – also: SMTP-Server-Adresse, Port, Benutzername, Passwort. Damit kann ich
den Versand direkt von diesem Server aus per Python (authentifiziertes SMTP, verschlüsselt)
einrichten, ohne Umweg über das Hosting-Chroot. Diese Zugangsdaten findest du normalerweise im
selben Netcup-Panel-Bereich wie den E-Mail-Account selbst (E-Mail-Postfach-Einstellungen,
meist "SMTP-Server" oder "Postausgangsserver" genannt).

Bitte in derselben Form wie den SSH-Zugang übermitteln (Panel-Angaben 1:1, nicht aus dem
Gedächtnis) – ich speichere es direkt sicher unter `/root/.env.smtp` (chmod 600) und melde mich
mit einem Testversand zurück, bevor der Cron-Job scharf geschaltet wird.

## Zusammenfassung

| Teil | Status |
|---|---|
| Content-Strategie-Report | Existiert nicht – Rückfrage nötig, bevor irgendwas gebaut wird |
| ai_visibility E-Mail-Versand | Technisch geprüft, zwei Wege ausgeschlossen, SMTP-Zugangsdaten für info@nhp-straehuber.de nötig |

Nichts wurde an bestehenden Skripten verändert – reine Prüfung plus ein Testversand-Versuch
(fehlgeschlagen, kein Effekt auf produktive Systeme).
