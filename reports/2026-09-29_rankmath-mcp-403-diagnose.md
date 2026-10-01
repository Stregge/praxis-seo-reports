# RankMath-MCP Teil 2: 403 für claude.ai – Diagnose
_Datum: 29.09.2026 · nur Diagnose, nichts geändert_

## Ergebnis
Blockiert wird **in Apache, per .htaccess, noch bevor WordPress läuft**. Verantwortlich ist die 6G-Firewall von Perishable Press im Abschnitt `# 6G:[USER AGENT]` der Datei `httpdocs/naturheilpraxis-straehuber/.htaccess` (Zeilen 376–394):

```apache
SetEnvIfNoCase User-Agent (...|pycurl|python|seekerspider|...) bad_bot
...
<RequireAll>
    Require all Granted
    Require not env bad_bot
</RequireAll>
```
Der Connector-Check von claude.ai sendet den User-Agent **`python-httpx/0.28.1`**. Der enthält `python`, deshalb wird die Anfrage als `bad_bot` markiert und Apache antwortet mit 403.

## Belege
**1. User-Agent-Test**, jeweils POST auf /wp-json/mcp/mcp-oauth-server vom VPS aus:
| User-Agent | Ergebnis |
|---|---|
| Claude-User | 401 `mcp_unauthorized` |
| ClaudeBot | 401 `mcp_unauthorized` |
| anthropic-ai | 401 `mcp_unauthorized` |
| python-httpx/0.27.0 | **403 Apache „Forbidden“** (HTML) |
| ohne UA | 401 `mcp_unauthorized` |

Mit `python-httpx` sind ebenfalls blockiert: `GET /.well-known/oauth-protected-resource/` (403) und `POST /oauth/token` (403).

**3. Logs** (`logs/naturheilpraxis-straehuber.de/`):
```
access_ssl_log: 160.79.106.175 [29/Sep/2026:10:27:02 +0200] "POST /wp-json/mcp/mcp-oauth-server" 403 "python-httpx/0.28.1"
error_log:      [10:27:02] [authz_core:error] [client 160.79.106.175] AH01630: client denied by server configuration: .../wp-json
```
- Dieselbe Sperre gab es schon am 28.09. um 19:08 (160.79.106.169) und um 19:25 (160.79.106.185).
- Die IPs liegen alle in 160.79.104.0/21, das ist der Adressbereich von Anthropic.
- ModSecurity: 0 Einträge. Die Meldung `AH01630`/authz_core passt genau zu `Require not env bad_bot`.

**2. .htaccess**
- Im Webspace-Root gibt es keine .htaccess. `httpdocs/.htaccess` hat 15 Zeilen und keine Bot-Regeln.
- Die Sperre steht nur in der .htaccess der Praxis-Installation.
- Andere Blöcke dort (6G Query-String, Methode, Referrer, Request-String) treffen den OAuth-Flow nach Test nicht. Ein realistischer `/oauth/authorize`-Aufruf mit Browser-UA kommt durch.

**4. Plugins/Snippets**
- Die Anfrage wird abgewiesen, bevor PHP startet. Plugins spielen deshalb für diesen 403 keine Rolle.
- WPCodeBox: kein Snippet filtert nach User-Agent oder KI-Bots.
- Snippet #13 (robots.txt) enthält `Disallow: /wp-json/`. Das blockt technisch nichts, siehe offene Punkte.
- In den Plugin-Dateien findet sich „python-httpx“ nur in der UA-Parser-Bibliothek von RankMath, einer reinen Erkennungsliste.

## Vorschlag (NICHT umgesetzt): eng begrenzte Ausnahme
Nur im Block `<IfModule mod_authz_core.c>` des Abschnitts 6G:[USER AGENT]. Die Bot-Liste selbst bleibt unverändert.

```apache
	<IfModule mod_authz_core.c>
		<RequireAny>
			# Ausnahme MCP/OAuth (claude.ai-Connector sendet UA python-httpx) - nur diese Pfade, ohne ".."
			Require expr "%{THE_REQUEST} =~ m#^[A-Z]+ /(wp-json/mcp/|\.well-known/oauth-|oauth/)# && ! %{THE_REQUEST} =~ m#(\.\.|%2e)#i"
			<RequireAll>
				Require all granted
				Require not env bad_bot
			</RequireAll>
		</RequireAny>
	</IfModule>
```

**Warum `THE_REQUEST` und nicht `REQUEST_URI`:**
- WordPress leitet `/wp-json/...` intern auf `/index.php` um, und Apache prüft den Zugriff danach erneut.
- Bei dieser zweiten Prüfung enthält `REQUEST_URI` nur noch `/index.php`, `THE_REQUEST` dagegen weiterhin die ursprüngliche Anfragezeile.
- Pfade mit `..` oder `%2e` sind von der Ausnahme ausgenommen.

**Wirkung:**
- Nur Anfragen auf `/wp-json/mcp/…`, `/.well-known/oauth-…` und `/oauth/…` umgehen die UA-Bot-Liste.
- Alle anderen Pfade bleiben für `python*` und die übrigen Bot-UAs gesperrt.
- Die WordPress-REST-Sperre (Snippet #3) und die Authentifizierung von RankMath greifen weiterhin.

**Umsetzung nach Freigabe:**
1. Backup der .htaccess
2. Block ersetzen
3. Tests mit UA `python-httpx/0.28.1`:
   - POST mcp → 401 `mcp_unauthorized` + `WWW-Authenticate`
   - beide well-known → 200 JSON
   - POST /oauth/token → 400 `invalid_grant`
   - `/` → weiterhin 403
   - `/wp-json/wp/v2/users` → 403
   - `/wp-json/mcp/../wp/v2/users` → 403
4. Tests mit Browser-UA: Startseite 200
5. Wenn irgendein Test fehlschlägt: sofort Backup zurückspielen

**Risiko:** Ein Syntaxfehler in der .htaccess erzeugt einen 500-Fehler auf der ganzen Website, bis das Backup zurück ist. Das Zurückspielen dauert unter einer Minute, weil die alte Datei direkt zurückkopiert wird.

## Offene Punkte / Unsicherheiten
- Ob Apache 2.4 bei der erneuten Prüfung nach der internen Umleitung wirklich `THE_REQUEST` auswertet wie beschrieben, weiß ich nicht sicher. Der Test in Schritt 3 klärt das. Scheitert er, wird sofort zurückgespielt.
- robots.txt enthält `Disallow: /wp-json/`. Ob der MCP-Client von claude.ai robots.txt beachtet, weiß ich nicht. Vermutlich nicht, denn Tool-Aufrufe sind keine Crawls. Nicht geprüft.
- Nebenbefund: WPCodeBox schreibt bei jedem Request PHP-Warnings ins error_log (`Undefined variable $hook`, `Array to string conversion`). Ohne Auswirkung auf dieses Problem, nicht angefasst.
