# LA-Punkte

PWA für den LK Sport: Leichtathletik-Leistungen eintragen, automatisch EPA-Punkte (0–100+), Notenpunkte Unterricht (15 ab 65) und Abitur (15 ab 75) sowie Vierkampf berechnen.

## Dateien
- `index.html` – komplette App (Tabellen EPA EB Sport 2019, S. 45–47, eingebettet)
- `manifest.json`, `sw.js`, `icons/` – Installation auf dem Home-Bildschirm, offline nutzbar

## Veröffentlichen (einmalig, wie beim Kochbuch)
1. Auf github.com ein neues Repository `la-punkte` anlegen (öffentlich).
2. Im Terminal:
   ```bash
   cd ~/Claude/Projects/"LK Sport_2627"/Output/LA-Punkte
   git init && git add . && git commit -m "LA-Punkte App"
   git branch -M main
   git remote add origin https://github.com/sebschroeer18-stack/la-punkte.git
   git push -u origin main
   ```
3. Im Repository: Settings → Pages → Branch `main`, Ordner `/ (root)` → Save.
4. Nach ca. 1 Minute läuft die App unter `https://sebschroeer18-stack.github.io/la-punkte/`.
5. Auf iPhone/iPad in **Safari** öffnen → Teilen → „Zum Home-Bildschirm“.

Die Seite selbst ist öffentlich, die Schülerdaten nicht: Sie liegen nur im Speicher des jeweiligen Geräts.

## Daten
- Speicherung automatisch im Gerät (localStorage), bleibt nach dem Schließen erhalten.
- Sicherung: Daten → „Sicherung speichern (JSON)“ → in Dateien/iCloud ablegen. Wiederherstellen über „Sicherung laden“. Die App erinnert, wenn die letzte Sicherung älter als 7 Tage ist.
- Gerätewechsel = Sicherung exportieren und auf dem anderen Gerät laden. Es gibt keinen automatischen Abgleich.
- Wichtig: Die Home-Bildschirm-App und Safari haben getrennte Speicher. Immer über das Home-Icon arbeiten.

## Bewertungslogik
- Punkte: lineare Interpolation zwischen den 5er-Stufen, abgerundet, Überpunkte über 100 per Steigung der obersten Stufe.
- Notenpunkte Unterricht: 15 ab 65, je 5 Punkte eine Stufe bis 3 ab 5; 2 ab 3 und 1 ab 1 geschätzt.
- Notenpunkte Abitur: 15 ab 75, je 5 Punkte eine Stufe.
- Vierkampf: Abitur nach EPA S. 44 (15 ab 300, je 20 Punkte). Unterricht analog über den Durchschnitt pro Disziplin (15 ab 260).
- U18 (jahrgangsmäßig 16/17 im Jahr des Ergebnisses): leichtere Wurfgeräte, gleiche Tabelle.
- Leitern ändern: in `index.html` die Konstante `LADDER`.

## Update ausrollen
Nach Änderungen die Cache-Version in `sw.js` erhöhen (`la-punkte-v2` …), committen und pushen.
