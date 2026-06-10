# Rüstzeithaus Salza

Statische Webseite des Rüstzeithauses der evangelischen Gemeinde Salza.

## Projektstruktur

```
public/          → Statische Dateien (wird deployed)
.github/         → GitHub Actions Workflows
```

## Deployment

Das Deployment erfolgt automatisch bei Push auf `main` via GitHub Action auf einen SFTP-Server.

### Benötigte Secrets

Folgende Secrets müssen im Repository konfiguriert werden:

| Secret | Beschreibung |
|--------|-------------|
| `SFTP_HOST` | Hostname des SFTP-Servers |
| `SFTP_USER` | Benutzername |
| `SFTP_PASSWORD` | Passwort |
| `SFTP_PORT` | Port (Standard: 22) |
| `SFTP_REMOTE_PATH` | Zielverzeichnis auf dem Server |

## Lokale Entwicklung

Die Dateien in `public/` können direkt im Browser geöffnet oder mit einem lokalen Webserver getestet werden:

```bash
cd public && python3 -m http.server 8000
```
