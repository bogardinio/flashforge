# FlashForge ⚡

Anki-ähnliche Karteikarten-PWA — komplett offline, kein Build-Step, kein Server nötig.

## Lokal testen

```bash
cd anki-pwa
python3 -m http.server 8080
# Dann: http://localhost:8080
```

Oder mit Node.js:
```bash
npx serve .
```

> **Wichtig:** Direkt als `file://` öffnen funktioniert nicht (Service Worker braucht HTTP/HTTPS).

## Auf GitHub Pages deployen

1. Repository erstellen (z.B. `flashforge`)
2. Den Inhalt des `anki-pwa/`-Ordners in den Repository-Root pushen
3. Einstellungen → Pages → Branch: `main`, Ordner: `/` (root)
4. Die App ist dann unter `https://DEINNAME.github.io/flashforge/` erreichbar

```bash
git init
git add .
git commit -m "Initial FlashForge"
git branch -M main
git remote add origin https://github.com/DEINNAME/flashforge.git
git push -u origin main
```

## Auf dem iPhone installieren

1. Die App-URL in **Safari** öffnen (kein Chrome, kein Firefox!)
2. Teilen-Button (Rechteck mit Pfeil nach oben) tippen
3. **„Zum Home-Bildschirm"** auswählen
4. Name bestätigen → **Hinzufügen**

Die App startet dann wie eine native App ohne Browser-UI.

## CSV importieren

### Aus Anki Desktop exportieren
1. Anki Desktop → Datei → Exportieren
2. Format: **„Notizen im Klartext (.txt)"**
3. Häkchen setzen: „Tags einschließen" (optional)
4. Exportierte `.txt`-Datei in FlashForge importieren

### Eigene CSV erstellen
Semikolon-getrennt mit optionalen Anführungszeichen:
```
"Guten Tag.";"Dzień dobry."
"Danke.";"Dziękuję."
```
Oder Tab-getrennt (z.B. aus Excel mit „Als TSV speichern").

### Wieder in Anki importieren
1. Anki Desktop → Datei → Importieren → CSV-Datei wählen
2. Trennzeichen: **Semikolon**
3. Erstes Feld = Vorderseite, Zweites Feld = Rückseite

## Datei-Struktur

```
anki-pwa/
├── index.html    # Komplette App (HTML + CSS + JS inline)
├── sw.js         # Service Worker für Offline-Caching
├── manifest.json # PWA-Manifest
├── icon.svg      # App-Icon
└── README.md     # Diese Datei
```

## Funktionen

- **SM-2 Algorithmus** (wie Anki) — Again / Schwer / Gut / Leicht
- **CSV-Import** — Anki-Export (.txt), Semikolon-CSV, Tab-CSV
- **JSON-Backup** — Vollständiger Export/Import mit Lernfortschritt
- **CSV-Export** — Anki-kompatibel (Semikolon-getrennt)
- **Statistiken** — Streak, Aktivitäts-Heatmap, Karten-Verteilung
- **Offline-First** — IndexedDB + Service Worker
- **Dark Mode** — OLED-optimiert
