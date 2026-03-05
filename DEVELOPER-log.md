# FlashForge — Developer Log

## 2026-03-05

### Problem: App funktioniert nicht offline (iOS Safari)

**Symptom:** App startet nicht wenn der Webserver nicht erreichbar ist. `sw.js` erscheint nie in den Server-Logs.

**Ursache:** Service Workers erfordern einen sicheren Kontext (HTTPS oder `localhost`).
Bei Zugriff über `http://192.168.x.x:8000` ist `'serviceWorker' in navigator === false` auf iOS Safari.
Die SW-Registrierung wird nie ausgeführt, nichts wird gecacht.

```javascript
// Diese Bedingung ist false über http:// auf iOS Safari:
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('./sw.js?v=2') // wird nie aufgerufen
}
```

**Referenz:** MDN — Service Worker API: *"Service workers only run over HTTPS"*

**Lösung:** App muss über HTTPS bereitgestellt werden.
Empfehlung: GitHub Pages, Netlify oder Cloudflare Pages (alle kostenlos, HTTPS inklusive).

---

### Weitere Änderungen (diese Session)

- `sw.js` v1 → v2: Google Fonts aus `addAll()` entfernt (externes Fetch schlug fehl und verhinderte die gesamte SW-Installation)
- SW-Registrierung auf `./sw.js?v=2` geändert um Browser-Cache des alten SW zu umgehen
