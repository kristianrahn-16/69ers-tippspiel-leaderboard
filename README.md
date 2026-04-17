# Sterkrade 69ers · Tippspiel-Leaderboard

Live-Leaderboard für das NBA Playoff Tippspiel 2026, das die Daten direkt aus dem Google Sheet zieht und als statische Seite über GitHub Pages veröffentlicht wird.

## Funktionsweise

- Die Seite lädt den Tab **„Leaderboard"** aus dem Google Sheet als CSV-Export (via `gviz/tq`-Endpoint).
- Jeder Besuch holt den aktuellen Stand.
- Zusätzlich wird automatisch alle 5 Minuten neu geladen.
- Mit dem **Aktualisieren**-Button kann manuell nachgeladen werden.

## Voraussetzung: Sheet muss öffentlich sein

Im Google Sheet oben rechts auf **Teilen** klicken und einstellen:

> „Jeder mit dem Link" · **Betrachter**

Ohne diese Freigabe kann die Seite die Daten nicht abrufen.

## Deployment über GitHub Pages

1. Neues öffentliches GitHub-Repository anlegen, z. B. `69ers-leaderboard`.
2. Alle Dateien aus diesem Ordner ins Repo legen:
   ```
   /index.html
   /assets/logo.png
   /README.md
   ```
3. Im Repo: **Settings → Pages**
   - **Source**: *Deploy from a branch*
   - **Branch**: `main` · **/** (root) · **Save**
4. Nach ein paar Minuten ist die Seite erreichbar unter:
   `https://<DEIN-USERNAME>.github.io/69ers-leaderboard/`

### Eigene Domain (optional)

Unter **Settings → Pages → Custom domain** eine Subdomain wie `tippspiel.sterkrade69ers.de` eintragen und beim DNS-Provider einen `CNAME` auf `<username>.github.io` setzen.

## Anpassen

In `index.html` oben im `<script>`-Block:

```js
const SHEET_ID   = '1Reqkz1tkFevziPjEhTcE5SrwWHaCLz0oeAXdjHUrYHQ';
const SHEET_NAME = 'Leaderboard';
const REFRESH_MS = 5 * 60 * 1000;   // alle 5 Minuten
```

Die Spalten werden **automatisch erkannt**:
- Spalte mit „Position" / „Rang" / „Platz" / „#" → Position
- Spalte mit „Name" / „Spieler" / „Tipper" → Spielername
- Spalte mit „Punkte" / „Gesamt" / „Total" → Hauptpunktzahl
- Alle weiteren Spalten → als Badges unter dem Namen

Falls die Spalten anders benannt sind: einfach die Keywords im Code (Funktion `classifyColumns`) ergänzen oder die Spalten im Sheet umbenennen.

## Farben & Look

Farben aus dem Vereinslogo:
- Navy **#05274A**
- Orange **#E1630C**
- Creme-Weiß **#FDFAF5**

Schriften: Oswald (Headlines), Bebas Neue (Zahlen), Manrope (Body).
