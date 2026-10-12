# 07.10.2026 – Automatische Plugin-Updates angepasst (Option `auto_update_plugins`)

## Ergebnis
Auto-Updates sind jetzt nur noch für **UpdraftPlus** und **Fluent Forms** aktiv. Geändert wurde ausschließlich die Option `auto_update_plugins` in `sh_options` (option_id 362).

| Eintrag | Datei vorhanden | Aktion |
|---|---|---|
| advanced-custom-fields/acf.php | nein | entfernt (veraltet) |
| all-in-one-wp-migration/all-in-one-wp-migration.php | nein | entfernt (veraltet) |
| all-in-one-wp-migration-ftp-extension/all-in-one-wp-migration-ftp-extension.php | nein | entfernt (veraltet) |
| code-snippets/code-snippets.php | nein | entfernt (veraltet) |
| custom-post-type-ui/custom-post-type-ui.php | nein | entfernt (veraltet) |
| fluentform/fluentform.php | ja | **behalten** |
| mainwp-child/mainwp-child.php | ja (inaktiv) | entfernt (Entscheidung Roland; bleibt inaktiv) |
| motionpage/motionpage.php | nein | entfernt (veraltet) |
| seo-by-rank-math/rank-math.php | ja | entfernt → Auto-Update aus |
| seo-by-rank-math-pro/rank-math-pro.php | ja | entfernt → Auto-Update aus |
| updraftplus/updraftplus.php | ja | **behalten** |
| wp-grid-builder/wp-grid-builder.php | nein | entfernt (veraltet) |
| borlabs-cookie/borlabs-cookie.php | ja | entfernt → Auto-Update aus |

## Werte
**Vorher (13 Einträge):**
```
a:13:{i:0;s:30:"advanced-custom-fields/acf.php";i:1;s:51:"all-in-one-wp-migration/all-in-one-wp-migration.php";i:2;s:79:"all-in-one-wp-migration-ftp-extension/all-in-one-wp-migration-ftp-extension.php";i:4;s:31:"code-snippets/code-snippets.php";i:5;s:43:"custom-post-type-ui/custom-post-type-ui.php";i:6;s:25:"fluentform/fluentform.php";i:7;s:29:"mainwp-child/mainwp-child.php";i:8;s:25:"motionpage/motionpage.php";i:9;s:30:"seo-by-rank-math/rank-math.php";i:10;s:38:"seo-by-rank-math-pro/rank-math-pro.php";i:11;s:27:"updraftplus/updraftplus.php";i:12;s:35:"wp-grid-builder/wp-grid-builder.php";i:13;s:33:"borlabs-cookie/borlabs-cookie.php";}
```
**Nachher (2 Einträge):**
```
a:2:{i:0;s:25:"fluentform/fluentform.php";i:1;s:27:"updraftplus/updraftplus.php";}
```

## Vorgehen
1. Backup der Zeile: `/root/praxis-seo/backups/auto_update_plugins_20261007-124125.sql`
2. Vor dem Schreiben geprüft: Der Wert ist byte-gleich mit dem Stand beim Backup, und der Rundweg-Test (serialize(unserialize(x)) === x) ist bestanden.
3. Neuer Wert per PHP: `unserialize` → nur die beiden Einträge behalten → `array_values` → `serialize`. Er ist selbst rundweg-stabil und wurde per Hex-UPDATE geschrieben; die Längenangaben stammen also aus PHP.
4. Zurückgelesen: identisch mit dem vorbereiteten Wert; `unserialize` ok; genau 2 Einträge.

## Nachweis „sonst nichts geändert“
- `active_plugins`: MD5 vorher = nachher (`0ca20ab18ba14d9152097722fb9d55ca`). Es wurde kein Plugin aktiviert oder deaktiviert; MainWP Child ist weiter inaktiv.
- Plugin-Ordner: MD5 der Verzeichnisliste mit Zeitstempeln vorher = nachher (`271a9014b2a7b24421a4e5e2b6ac3b47`). Keine Datei wurde aktualisiert, umbenannt oder gelöscht.
- Keine weitere Option angefasst.

## HTTP-Prüfung
| URL | Status |
|---|---|
| / | 200 |
| /kontakt/ | 200 |
| /ratgeber/ | 200 |

Schritt 6 (Rückspielen) war nicht nötig. Die DB-Zugangsdatei und alle Temp-Dateien auf dem Hosting sind entfernt.

## Hinweis
Rank Math, Rank Math Pro und Borlabs Cookie aktualisieren sich jetzt nicht mehr selbst. Updates dafür erscheinen in wp-admin unter „Aktualisierungen“ und müssen manuell eingespielt werden, am besten einzeln und mit kurzer Prüfung danach.
