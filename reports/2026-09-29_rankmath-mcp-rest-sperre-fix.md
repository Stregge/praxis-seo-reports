# RankMath-MCP: REST-Sperre blockierte OAuth-Flow – Fix
_Datum: 29.09.2026_

## Ursache
- Die REST-Sperre sitzt im **WPCodeBox-Snippet #3** „Deactivate REST API when not logged in“: aktiv, PHP, Hook `plugins_loaded`.
- Gespeichert in der DB `k75670_nhp`, Tabelle `sh_wpcb_snippets`, Felder `code` und `original_code`.
- WordPress-Install: Netcup-Webhosting, `httpdocs/naturheilpraxis-straehuber/`.
- Das Snippet hängt am Filter `rest_authentication_errors` und gibt allen anonymen REST-Anfragen `rest_not_logged_in` (401) zurück. Dadurch kam auf `/wp-json/mcp/mcp-oauth-server` nicht die RankMath-Antwort `mcp_unauthorized` mit `WWW-Authenticate`-Header, und der OAuth-Flow von claude.ai startete nicht.
- Nicht betroffen: mu-plugins, Theme und Plugins (dort 0 Treffer). Snippet #16 war ein Fehltreffer (inaktives Manus-Debug-Snippet).

## Änderung
Eine Ausnahme für anonyme Anfragen, deren REST-Route mit `/mcp/` beginnt:
```php
/* Ausnahme: MCP-Routen (RankMath MCP / OAuth-Flow claude.ai) – Auth macht RankMath selbst */
$route = isset( $GLOBALS['wp']->query_vars['rest_route'] ) ? (string) $GLOBALS['wp']->query_vars['rest_route'] : '';
if ( 0 === strpos( $route, '/mcp/' ) ) {
    return $result;
}
```
Der Rest des Snippets ist unverändert. Danach wurde der WP-Rocket-Cache geleert.

Backup: `/root/praxis-seo/backups/wpcb_snippet3_20260929-102127.sql` (SQL-INSERT der Zeile) und `.php` (Code im Klartext).

## Verifikation (anonym, live)
| Test | Ergebnis |
|---|---|
| a) POST /wp-json/mcp/mcp-oauth-server | 401 `mcp_unauthorized` + `WWW-Authenticate: Bearer realm=…, resource_metadata="…/.well-known/oauth-protected-resource"` ✅ |
| b) GET /wp-json/wp/v2/users | 401 `rest_not_logged_in` ✅ |
| c) /.well-known/oauth-protected-resource und oauth-authorization-server | 200 JSON (nach 301 auf die Adresse mit Slash am Ende) ✅ |
| d) Startseite | 200, ca. 501 KB, korrekter Title ✅ |
| e) /?rest_route=/wp/v2/users | 401 `rest_not_logged_in` ✅ |
| f) /wp-json/mcp/../wp/v2/users (roh) | 404 `rest_no_route`, keine Benutzerdaten ✅ |
| f-Varianten (%2e%2e, ?rest_route=/mcp/../…, /mcp//../…) | 404 `rest_no_route` bzw. Apache 403/404, keine Benutzerdaten ✅ |
| /wp-json/mcp (Namespace-Index) | 401 `rest_not_logged_in` (weiter gesperrt) |
| /wp-json/mcp/mcp-adapter-default-server | 401 `rest_forbidden` (eigene Prüfung des MCP-Adapters) |

## Offene Punkte
- `/.well-known/oauth-*` ohne Slash am Ende leitet per 301 weiter. Die meisten Clients folgen dieser Weiterleitung. Falls die Verbindung von claude.ai weiter scheitert, ist das der nächste Verdacht.
- Rückbau: SQL-Backup einspielen oder den alten Code aus der `.php`-Datei in WPCodeBox einsetzen.
