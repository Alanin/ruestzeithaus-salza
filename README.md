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
| `TEST_BASIC_AUTH_PASSWORD` | Passwort für HTTP Basic Auth auf `test` |

### Basic Auth auf `test`

Die Testumgebung wird beim Deployment auf Branch `test` vollständig per HTTP Basic Auth geschützt.

- `.htaccess` wird in der GitHub Action zur Laufzeit erzeugt und nicht im Repository gespeichert
- Es wird kein `AuthUserFile` benötigt, dadurch tritt kein Apache-`500` wegen ungültigem Dateipfad auf

## Lokale Entwicklung

Die Dateien in `public/` können direkt im Browser geöffnet oder mit einem lokalen Webserver getestet werden:

```bash
cd public && python3 -m http.server 8000
```

## Kostenlose SEO-Basis

Folgende Punkte sind im Projekt umgesetzt:

- JSON-LD in `public/index.html` (`LodgingBusiness` + `FAQPage`)
- `public/robots.txt`
- `public/sitemap.xml`

Für Google ohne Werbekosten:

1. Domain in der Google Search Console verifizieren
2. `https://ruestzeithaus-salza.de/sitemap.xml` einreichen
3. Indexierung über URL-Prüfung anstoßen und Verbesserungsberichte beobachten
