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

## Lokale Entwicklung

Die Dateien in `public/` können direkt im Browser geöffnet oder mit einem lokalen Webserver getestet werden:

```bash
cd public && python3 -m http.server 8000
```
