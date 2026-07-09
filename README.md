# Schmid Busreisen — Bildreview-Seite

Interaktive Review-Seite für den Kunden: `index.html` zeigt alle 43 Bilder von der
Schmid-Busreisen-Website. Der Kunde kann pro Bild eine "größere Version"-Anfrage
markieren, Kategorien anklicken (Auflösung, Color Grading, Motiv/Bildausschnitt,
Bildqualität, Ersetzen, Sonstiges) und einen Freitext-Kommentar hinterlassen.
Über den Button unten rechts wird das gesamte Feedback als JSON-Datei
heruntergeladen.

## Lokal testen

Einfach `index.html` per Doppelklick im Browser öffnen — die Bilder liegen
relativ dazu in `Bilder der Website/` und `team/`.

## Per GitHub Pages veröffentlichen

1. Neues (privates oder öffentliches) GitHub-Repository erstellen, z. B.
   `schmid-busreisen-review`.
2. Diesen kompletten Ordner (`index.html`, `Bilder der Website/`, `team/`,
   `README.md`) in das Repository hochladen — entweder per GitHub Desktop,
   per Drag & Drop im Browser (github.com → "Add file" → "Upload files"),
   oder per Terminal:

   ```bash
   cd "David Moling - Schmid Busreisen"
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/<dein-github-name>/schmid-busreisen-review.git
   git push -u origin main
   ```

3. Im Repository auf GitHub: **Settings → Pages** öffnen.
4. Unter "Build and deployment" → Source: **Deploy from a branch** wählen,
   Branch **main**, Ordner **/ (root)** — dann **Save**.
5. Nach ein bis zwei Minuten ist die Seite unter
   `https://<dein-github-name>.github.io/schmid-busreisen-review/` erreichbar.
   Diesen Link kannst du direkt an den Kunden schicken.

## Hinweise

- Das NFBrands.X-Logo oben rechts wird aktuell live von `nfbrands.xyz`
  eingebunden (kein lokaler Download möglich gewesen). Funktioniert auf
  GitHub Pages einwandfrei, solange die NFBrands-Website online bleibt.
- Das JSON-Export-Feature läuft rein im Browser (kein Server nötig) — die
  Datei landet im Download-Ordner des Kunden. Für eine automatische
  Zustellung des Feedbacks per E-Mail müsste ein Formular-Service wie
  Formspree ergänzt werden.
