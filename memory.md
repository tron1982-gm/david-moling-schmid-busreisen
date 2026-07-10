# Projekt-Gedächtnis: Schmid Busreisen Website Relaunch

## Kontext
- Auftraggeber: **David Moling** (Grafiker/Designer), arbeitet für **NFBrands.X GmbH**.
- Aufgabe: David hat den bestehenden Website-Datenbestand von schmid.moling.site (Kunde: Schmid Busreisen, Nauders) übernommen, weiß aber nicht, welche Bilder es in besserer Auflösung gibt. Ziel: interaktive Review-Seite, auf der der Kunde (Schmid Busreisen) pro Bild Feedback geben kann.
- Repo: `https://github.com/tron1982-gm/david-moling-schmid-busreisen`
- Live-URL (GitHub Pages, Branch main, Root): `https://tron1982-gm.github.io/david-moling-schmid-busreisen/`
- Lokaler Projektordner: `/Users/matthiaslechner/Documents/Claude/Projects/David Moling - Schmid Busreisen`

## Was existiert
- `index.html` — die eigentliche Review-Seite (44 Bilder aus `Bilder der Website/` + `team/`).
- `README.md` — Anleitung für GitHub Pages Setup.
- `Bilder der Website/` und `team/` — die von der Live-Website heruntergeladenen Originalbilder (aus `/images/...`, nicht die komprimierten `_next/image`-Varianten).
- `Schmid Busreisen von David aus Google Drive - drive-download-20260709T165110Z-2-001/` — zusätzliche HiRes-Fotos, die David separat von Google Drive bekommen hat. Enthält u.a. Fuhrpark-/Team-Fotoshooting-Dateien in bis zu 6000×4001px.

## Funktionsumfang der Review-Seite
- Pro Bild: Vorschaubild (klickbar → Lightbox mit Originalgröße), Kategorie-Tags (Auflösung, Color Grading, Motiv/Bildausschnitt, Bildqualität, Ersetzen, Sonstiges), Freitext-Kommentar, Speichern/Bearbeiten-Button (sperrt Felder, grüner "gespeichert"-Zustand).
- Daten werden im Browser des Kunden per `localStorage` (Key `schmid-bildfeedback-v1`) zwischengespeichert — bleiben NUR lokal beim Kunden, bis er aktiv sendet.
- Button "Feedback absenden" schickt eine Zusammenfassung + Rohdaten-JSON per POST an Davids **Formspree-Endpoint**: `https://formspree.io/f/mwvdddwd`.
- Button "JSON herunterladen" als lokales Backup/Alternative, falls Versand fehlschlägt.
- Design: helle Variante des NFBrands.X-Corporate-Designs. Header mit NFBrands.X-Logo (extern verlinkt von `https://nfbrands.xyz/images/logo.svg`, mit CSS-Filter `brightness(0)` schwarz eingefärbt, da das Original-SVG weiß ist). Dunkler Footer im Stil der echten nfbrands.xyz-Seite (Farbverlauf-Copyright-Leiste unten, ohne Social-Icons), Logo dort weiß via `brightness(0) invert(1)`.
- Oben ein Banner: "Auftraggeber: David Moling | Projekt: Schmid Busreisen Website Relaunch | Nur für den internen Gebrauch".
- Footer enthält NFBrands.X GmbH Kontaktdaten: Innsbruck (**Lutterottistraße 7 / Top 1**, 6020 Innsbruck — bewusst abweichend von der echten öffentlichen Adamgasse-23-Adresse auf nfbrands.xyz, auf Wunsch des Nutzers), Wien (Gonzagagasse 11/25), Bozen (Brennerstraße 16), alle Office-Mails als mailto-Links verlinkt (Schriftfarbe grau/unterstrichen, nicht die Akzentfarbe).

## Bekannte HIRES-Zuordnungen (bestätigt durch visuellen Vergleich)
Diese Website-Bilder haben ein bestätigtes größeres Original im Google-Drive-Ordner — bekommen auf der Review-Seite statt der Checkbox ein grünes "✅ HIRES-Datei bereits vorhanden"-Badge (Feld `hires` im JS-Array `images`):
- `story2.webp` UND `gruppenfahrten.webp` ← `Fuhrpark1.jpg` (gleiche Flottenaufnahme, nur unterschiedlicher komposierter Bergpanorama-Hintergrund)
- `bus-service.webp` ← `25-JAP08415.jpg`
- `hero-bus-taxi.webp` ← `17-JAP08445.jpg`
- `cycling-shuttle.webp` ← `6.jpg` (obwohl diese Datei mit nur 231 KB selbst recht klein ist)

Noch ungeklärt / kein Treffer gefunden: weitere Dateien im Google-Drive-Ordner wurden nicht erschöpfend mit allen 44 Website-Bildern abgeglichen (zeitintensiv). Bei Bedarf weiter zuordnen, falls David neue Hinweise gibt.

## Wichtige technische Stolperfallen
1. **PATH-Problem im Terminal des Nutzers:** Neue Terminal-Fenster/Tabs auf seinem Mac haben oft ein leeres `$PATH` (selbst `cat`, `dirname`, `git` etc. "not found"). Workaround, der zuverlässig funktioniert:
   ```bash
   export PATH="/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
   ```
   Das muss vor jedem `git`-Befehl in einem neuen Terminal-Fenster erneut ausgeführt werden, bis die Ursache in seiner Shell-Konfiguration (`~/.zshrc`/`~/.zprofile`) behoben ist (bisher nicht untersucht/behoben).
2. Web-Fetch/Sandbox kann keine Binärdateien (Bilder etc.) von fremden Domains herunterladen — nur der Nutzer selbst kann das per `wget` im eigenen Terminal.
3. GitHub-Push-Workflow, das für dieses Projekt etabliert wurde:
   ```bash
   cd "/Users/matthiaslechner/Documents/Claude/Projects/David Moling - Schmid Busreisen"
   export PATH="/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
   git add -A
   git commit -m "..."
   git push
   ```
4. Frühere Bugs (bereits behoben, zur Erinnerung): negative CSS-Margins (`margin:0 -40px`) verursachten horizontalen Overflow; ein generisches `footer{max-width:1100px}`-Selektor-Rule hatte den ganzen Footer eingeschränkt (Lehre: bei "volle Breite"-Problemen immer nach Tag-Selektoren suchen, die mit Klassen-Selektoren kollidieren).

## Offene Punkte / mögliche nächste Schritte
- Formspree-Formular muss beim ersten echten Versand vom Nutzer per Aktivierungsmail bestätigt werden (kostenloser Plan: 50 Übermittlungen/Monat).
- Bildrechte-Hinweis aus dem ursprünglichen Impressum von schmid.moling.site: Fotos teilweise von Boris Plangger, doris oberfrank-list (Fotolia), Joachim Kreft (Fotolia) — relevant falls Lizenzfragen bei Weiterverwendung aufkommen.
- Nicht alle 44 Bilder wurden gegen den kompletten Google-Drive-Ordner abgeglichen — bei weiteren HiRes-Funden einfach das Muster aus diesem Dokument fortsetzen (Bild visuell vergleichen, `hires: "dateiname.jpg"` im `images`-Array in `index.html` ergänzen).
