# Rüstzeithaus Salza

Statische Webseite des Rüstzeithauses der evangelischen Gemeinde Salza.

## Projektstruktur

```
public/          → Statische Dateien (wird deployed)
.github/         → GitHub Actions Workflows
```

## Deployment

Das Deployment erfolgt automatisch via GitHub Action auf einen SFTP-Server:

- Push auf `main` → Produktion
- Push auf `test` → Testumgebung (z. B. `test.ruestzeithaus-salza.de`)

### Benötigte Secrets

Folgende Secrets müssen im Repository konfiguriert werden:

| Secret | Beschreibung |
|--------|-------------|
| `SFTP_HOST` | Hostname des SFTP-Servers |
| `SFTP_USER` | Benutzername |
| `SFTP_PASSWORD` | Passwort |
| `SFTP_PORT` | Port (Standard: 22) |
| `SFTP_REMOTE_PATH` | Zielverzeichnis auf dem Server |
| `SFTP_TEST_USER` | Benutzername für Testdeployment |
| `SFTP_TEST_PASSWORD` | Passwort für Testdeployment |
| `SFTP_TEST_REMOTE_PATH` | Zielverzeichnis für Testdeployment |
| `TEST_BASIC_AUTH_USER` | Benutzername für HTTP Basic Auth auf `test` |
| `TEST_BASIC_AUTH_PASSWORD_HASH` | bcrypt-Hash für HTTP Basic Auth auf `test` |
| `TEST_BASIC_AUTH_USERFILE` | Absoluter Serverpfad zur `.htpasswd`-Datei (z. B. `/home/.../test/.htpasswd`) |

### Basic Auth auf `test`

Die Testumgebung wird beim Deployment auf Branch `test` vollständig per HTTP Basic Auth geschützt.

- `.htaccess` und `.htpasswd` werden in der GitHub Action zur Laufzeit erzeugt und nicht im Repository gespeichert
- `TEST_BASIC_AUTH_USERFILE` muss ein **absoluter Pfad** auf dem Webserver sein (relativer Pfad führt bei Apache zu `500 Internal Server Error`)

Hash für `TEST_BASIC_AUTH_PASSWORD_HASH` erstellen:

```bash
htpasswd -nbBC 10 BENUTZER PASSWORT | cut -d ":" -f2-
```

## Lokale Entwicklung

Die Dateien in `public/` können direkt im Browser geöffnet oder mit einem lokalen Webserver getestet werden:

```bash
cd public && python3 -m http.server 8000
```
