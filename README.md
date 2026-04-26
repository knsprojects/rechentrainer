# Rechentrainer

Einfache Web-App zum Üben von Kopfrechnen für die Grundschule. Läuft als
eigenständige HTML-Datei direkt im Browser — ohne Server, ohne Build-Tools,
ohne Abhängigkeiten.

Optimiert für die Nutzung auf dem **iPhone im Hochformat** (lässt sich über
Safari als App auf den Home-Bildschirm legen), funktioniert aber genauso auf
Desktop-Browsern und Android.

## Funktionen

- Zufällige Aufgaben aus drei Grundrechenarten
- Eingabe per System-Tastatur, Bestätigung per Button **oder** Enter/Return
- Automatische Auswertung mit visuellem Feedback (grün/rot, 2 s)
- Live-Statistik: richtige/falsche Antworten + Erfolgsquote in %
- **Priorisierung einer Rechenart** mit doppelter Auftrittswahrscheinlichkeit
- **Persistenter Spielstand**: Zähler und Priorität bleiben nach App-Schließen
  erhalten (lokal im Browser)
- Reines HTML/CSS/JavaScript, eine einzige Datei, ~290 Zeilen

## Aufgaben-Spezifikation

| Rechenart | Bereich |
|---|---|
| Addition | zwei- bis dreistellige Summanden (10–999), Summe ≤ 1000 |
| Subtraktion | 0–1000, Ergebnis stets > 0 |
| Multiplikation | Faktor 1: 0–20, Faktor 2: 0–10 |

Additionen und Subtraktionen werden grundschultypisch **untereinander**
dargestellt, Multiplikationen **hintereinander**.

## Live-Demo

> [https://&lt;dein-username&gt;.github.io/rechentrainer/](https://knsprojects.github.io/rechentrainer/)

## Nutzung

### Im Browser öffnen
Datei `index.html` im Browser öffnen — fertig.

### Als App auf dem iPhone installieren
1. URL in **Safari** öffnen
2. Teilen-Symbol antippen (Quadrat mit Pfeil nach oben)
3. *Zum Home-Bildschirm* auswählen → *Hinzufügen*

Beim Start vom Home-Bildschirm läuft die App im Vollbild ohne Browser-Leiste.
Funktioniert nach dem ersten Laden auch offline.

## Bedienung

1. Aufgabe in der Bildschirmmitte ablesen
2. Lösung in das Eingabefeld tippen
3. Bestätigen mit
   - Klick auf den **Prüfen-Button**, oder
   - **Enter** auf der PC-Tastatur, oder
   - **Go/Haken-Taste** auf der iPhone-Systemtastatur
4. Button färbt sich für 2 Sekunden grün („Richtig") oder rot („Falsch")
5. Danach erscheint automatisch die nächste Aufgabe

### Priorisierung einer Rechenart

Über den drei Buttons *Vorrangig +*, *Vorrangig −* und *Vorrangig ×* lässt sich
gezielt eine Rechenart trainieren:

- Tippen aktiviert den Button (er bleibt sichtbar gedrückt: schwarzer Hintergrund)
- Erneutes Tippen auf denselben Button → Deaktivierung (Gleichverteilung)
- Tippen auf einen anderen Button → wechselt die Priorität
- Maximal ein Button gleichzeitig aktiv

| Zustand | Wahrscheinlichkeiten (+, −, ×) |
|---|---|
| Kein Button aktiv | 33,3 % • 33,3 % • 33,3 % |
| *Vorrangig +* aktiv | **50 %** • 25 % • 25 % |
| *Vorrangig −* aktiv | 25 % • **50 %** • 25 % |
| *Vorrangig ×* aktiv | 25 % • 25 % • **50 %** |

Die Auswahl überlebt App-Neustarts.

### Persistenter Spielstand

Richtige Antworten, falsche Antworten und die aktive Priorität werden
automatisch im Browser-Speicher (`localStorage`) gehalten. Beim Wiederöffnen
der App stehen alle Werte unverändert zur Verfügung.

Daten werden gelöscht, wenn der Nutzer die Website-Daten in den
Browser-Einstellungen entfernt. Es findet keine Synchronisation zwischen
Geräten statt.

## Technik

- Vanilla HTML5 / CSS3 / ES6 — keine Frameworks, keine Build-Pipeline
- Eine einzige Datei: `index.html`
- Persistenz über die `localStorage`-Web-API (Schlüssel: `rechentrainer-v1`)
- Keine externen Ressourcen, kein Tracking, kein Backend
- Portrait-only (Querformat ist nicht optimiert)

## Anpassen

Die ganze Logik steckt in `index.html`. Die wichtigsten Stellen zum
Verändern:

| Was | Wo |
|---|---|
| Zahlenbereiche der Aufgaben | Funktion `generate()` im `<script>`-Block |
| Gewichtung der Priorität | Funktion `pickType()` (Standard: Faktor 2) |
| Schriftgrößen, Farben | `<style>`-Block oben |
| Anzeigedauer von „Richtig"/„Falsch" | `setTimeout(nextRound, 2000)` |
| Button-Beschriftungen | HTML-Block für `.prio-btn` und Funktion `check()` |
| Speicher zurücksetzen | Browser-DevTools → *Application → Local Storage* → Eintrag `rechentrainer-v1` löschen |

## Deployment auf GitHub Pages

1. Repository auf GitHub anlegen (public)
2. Datei als `index.html` ins Root-Verzeichnis hochladen
3. *Settings → Pages → Source*: Branch `main` / Ordner `/ (root)` auswählen
4. Nach 1–2 Minuten ist die Seite unter
   `https://<username>.github.io/<repo-name>/` erreichbar

## Lizenz

Frei zur privaten und schulischen Nutzung.
