# Fellton

Ein kleiner, eigenständiger Web-Rechner zum Stimmen von Schlagzeugfellen. Kein
Build-Step, kein Backend – läuft komplett im Browser, auch offline.

🔗 **Live:** https://snoth0x53.github.io/fellton/

## Was das Tool macht

- Grundton (Note + Oktave) und Resonance-Modus pro Trommel einstellen
- Automatische Berechnung der Ziel-Lug-Frequenzen für Schlag- und Resonanzfell
- **Kalibrierfunktion:** eigene gemessene Werte eintragen (Lug-Frequenz + reale
  Fundamentalfrequenz) und damit die Standardwerte durch echte Messwerte ersetzen
- **Kreuz-Stimmreihenfolge:** Der Lug-Kreis zeigt die empfohlene Stimm-Reihenfolge –
  immer zum gegenüberliegenden Lug, dann eine Schraube weiter und wieder gegenüber,
  sodass sich die Spannung gleichmäßig verteilt
- **Snare-spezifische Formel:** eigener Rechenweg für Snares (Intervall-basiert:
  Quinte/Quarte/Terz/Unisono), getrennt von der Resonance-Modus-Logik für Toms/Bassdrum
- **Profi-Durchschnitt:** zusätzlicher Modus je Trommelart, basierend auf einer eigenen
  Auswertung von über 90 realen Artist-Tunings (siehe Abschnitt weiter unten)
- **Mikrofon-Messung:** ein "🎤 Messen"-Button pro Trommel misst den tatsächlichen
  Ist-Wert per FFT-Spektralanalyse, mit zuschaltbarem Filter für den kritischen
  Hochtonbereich
- Ton-Vorschau: kurze synthetische Klangbeispiele für Schlagfell, Resonanzfell
  und den resultierenden Trommel-Grundton
- **Set-Name:** ganzes Kit benennen (z. B. "Rogers XP8"), um mehrere Drumsets
  auseinanderzuhalten
- **Drucken / Als PDF speichern:** aktuelle Einstellungen aller Trommeln sichern

## Lug-für-Lug stimmen mit der Mikrofon-Messung

Die Mikrofon-Messung erkennt die Frequenz jedes Anschlags einzeln. Wo du anschlägst,
bestimmt, was gemessen wird:

- **Nah am Lug anschlagen** (2–3 cm vom Rand) → die Lug-Frequenz dieser Schraube.
  So bringst du alle Lugs nacheinander auf denselben Wert.
- **Mittig anschlagen** → der Grundton der ganzen Trommel.

Jeder Anschlag wird für sich ausgewertet und die kräftigste Frequenzgruppe angezeigt –
ohne Verrechnung über mehrere Schläge, damit ein einzelner Fehlgriff sich nicht auf
die folgenden Messungen überträgt. Die Messung läuft, bis du sie manuell stoppst.
Die Snare am besten mit ausgehängtem Teppich messen, damit das Rasseln nicht ins
Signal kommt.

### Filter für den Hochtonbereich

Nach oben hin wird jede Messung ungenauer – der Übergang beginnt etwa ab 250–300 Hz
und wird ab 350 Hz deutlich. Zwei Gründe: Hoch gestimmte Felle klingen kürzer aus und
füllen das Analysefenster nicht mehr aus, und die Fell-Partialtöne rücken enger
zusammen (die dritte und vierte Mode liegen nur rund 7 % auseinander). Dasselbe
Problem betrifft auch Hardware-Stimmgeräte.

Dafür gibt es den Filter: Erst eine korrekte Messung machen, dann **Filter** drücken.
Dieser Wert wird zur Referenz, und ab dann kommen nur noch Frequenzen im Umkreis von
**anderthalb Halbtönen** infrage. Bei 297 Hz ergibt das ein Band von etwa 272 bis
324 Hz – benachbarte Partialtöne, Oktavfehler und tiefe Störpeaks fallen heraus.

Das Band ist bewusst musikalisch definiert statt prozentual: Ein fester Prozentwert
wirkt im Bass eng und im Hochtonbereich viel zu weit (±20 % sind bei 300 Hz bereits
±60 Hz, dort passen mühelos mehrere Partiale hinein). Eine Halbton-Angabe bleibt über
den ganzen Bereich gleich streng.

Bei größeren Stimmänderungen einfach neu setzen; für jede Trommel gilt der Filter
getrennt. Beim Fellwechsel, wenn du von ganz unten hocharbeitest, lässt du ihn am
besten aus. Die Gruppen-Liste unter dem Messwert zeigt weiterhin alle erkannten
Rohwerte, auch die vom Filter verworfenen – so siehst du, wenn der Filter etwas
Echtes ausblendet.

Die Bandbreite lässt sich im Code über die Konstante `FILTER_SEMITONES` anpassen.

## Grundton messen und kalibrieren

Der Grundton (Fundamentalfrequenz) ist die Tonhöhe der ganzen Trommel beim mittigen
Anschlag – nicht die Frequenz an einem einzelnen Lug. Ihn brauchst du für die
Kalibrierfunktion.

**Schritt 1 – Beide Felle unisono stimmen.**
Schlag- und Resonanzfell auf die gleiche Lug-Frequenz bringen. Die beiden Felle
stimmt man dabei getrennt: die jeweils andere Seite auf eine weiche Unterlage legen
(dämpft sie ab, damit nur das freie Fell schwingt), das freie Fell rundum gleichmäßig
stimmen, dann die Trommel umdrehen und das zweite Fell genauso.

**Schritt 2 – Grundton messen.**
Trommel auf einen Ständer stellen (nicht auf eine weiche Unterlage). Mittig aufs Fell
schlagen und den Gesamtklang messen. Der abgelesene Wert ist deine reale
Fundamentalfrequenz.

**Schritt 3 – Kalibrieren.**
Diese gemessene Fundamentalfrequenz zusammen mit der eingestellten Lug-Frequenz in die
**Kalibrierfunktion** eintragen (siehe "+ Kalibrieren" bei jeder Trommel). Daraus wird
dein individueller Koeffizient berechnet, der die generische Formel für genau diese
Trommel und dieses Fell ersetzt – genauer als die Standardwerte.

Warum Unisono? Der Koeffizient ist das Verhältnis `a = Lug ÷ Fundamental`. Sind beide
Felle unterschiedlich gestimmt, gibt es zwei verschiedene Lug-Frequenzen und das
Verhältnis wäre nicht eindeutig. Im Unisono-Zustand gibt es genau eine.

## Formel-Grundlage

Die Multiplikatoren stammen aus dem
[Overtone Labs Tune-Bot Tuning Guide](https://tune-bot.com/tunebottuningguide.pdf)
(2012):

- **Maximum Resonance** (Unisono): Lug-Frequenz beider Felle = Grundton × 1,75
- **High Resonance:** höheres Fell × 1,85, tieferes Fell × 1,5
- **Medium Resonance:** × 2,0 / × 1,4
- **Low Resonance:** × 2,3 / × 1,2

Für **Snares** gilt ein eigener, dort separat beschriebener Ansatz (nicht die
Resonance-Modi oben): Schlagfell ≈ Grundton × 1,4, Resofell = Schlagfell ×
musikalisches Intervall (Standard: Quinte ×1,5).

Eine frühere Version enthielt zusätzlich eine Heuristik, die den Einfluss der
Kesseltiefe abschätzen sollte. Sie wurde entfernt, weil sie in der Praxis keine
verlässlichen Ergebnisse lieferte – auch Hardware-Stimmgeräte berücksichtigen die
Tiefe nicht. Für trommelspezifische Genauigkeit ist die Kalibrierfunktion der
richtige Weg.

## Profi-Durchschnitt: eigene Analyse realer Artist-Tunings

Zusätzlich enthält das Tool einen Modus **"Profi-Durchschnitt"**, der auf einer eigenen
Auswertung von über 90 auf [tune-bot.com/artists](https://tune-bot.com/artists/)
veröffentlichten Tunings professioneller Drummer basiert. Kernergebnisse:

- **Snare (n=22):** Der Standard (Perfekte Quinte, Verhältnis 1,5) liegt über
  dem realen Durchschnitt (≈1,29) – die meisten Profis stimmen enger, näher an
  Terz/Quarte.
- **Tom (n=60):** Der "High"-Modus passt schon gut zur Praxis (berechnetes
  Verhältnis 1,233 vs. beobachtet 1,20).
- **Bassdrum (n=14):** Das Guide-Beispiel setzt das Schlagfell exakt auf den
  Grundton (Verhältnis 1,0) – real liegt der Durchschnitt bei ≈1,62, spürbar
  straffer gestimmt.

Die vollständigen Rohdaten und Berechnungen liegen als CSV bei:
[`data/tune-bot-artist-tunings-analyse.csv`](data/tune-bot-artist-tunings-analyse.csv)
(alle Einzelwerte) und
[`data/tune-bot-analyse-zusammenfassung.csv`](data/tune-bot-analyse-zusammenfassung.csv)
(verdichtete Statistik).

## Mikrofon-Test-Tool

`mic-test.html` ist ein eigenständiges Diagnose-Werkzeug, um ein Mikrofon-Setup zu
prüfen, bevor es im Rechner zum Einsatz kommt: Live-Wellenform, Frequenzspektrum mit
markierten Gruppen, Pegel-Meter (RMS mit einer Dezimalstelle), Log der letzten
Anschläge und ein **Sound Score** (0–100) aus fünf FFT-Faktoren (Attack-Schärfe,
Tiefton-Energie, Harmonizität, Ring-Chaos, Dynamikumfang). Es nutzt dieselbe
Spektralanalyse wie der Rechner; der YIN-Grundton wird als Referenz mit angezeigt.

Für crowd-sourced Vergleiche lassen sich **Trommel-Metadaten** (Modell, Fell-Typ,
Bewertung 1–5, Notizen) eintragen und alle Anschläge als **CSV exportieren**.

🔗 **Live:** https://snoth0x53.github.io/fellton/mic-test.html

**Wichtig:** Mikrofonzugriff funktioniert nur in einem echten Browser-Tab über
HTTPS (oder `localhost`) – nicht in eingebetteten Vorschau-Fenstern. Für lokale
Tests: `python3 -m http.server 8000` im Projektordner, dann
`http://localhost:8000` öffnen.

## Genauigkeit der Mikrofon-Messung

Nach jedem Anschlag wird das Frequenzspektrum per FFT analysiert (Fenstergröße 32768):
Alle Peaks über einer Schwelle (18 dB unter dem stärksten) werden ermittelt und nach
spektraler Nähe gruppiert. Der Gruppierungsabstand skaliert mit der Frequenz (6 %,
mindestens 8 Hz), weil die Partialtöne nach oben hin enger zusammenrücken. Angezeigt
wird die kräftigste Gruppe des jeweiligen Anschlags. Parabel-Interpolation verfeinert
die Auflösung auf unter 1 Hz.

Zusätzliche Maßnahmen:

- **Plausible Frequenzbereiche je Trommelart:** Bassdrum 30–160 Hz, Toms 50–350 Hz,
  Snare 50–450 Hz
- **Filter** (siehe oben) für den kritischen Hochtonbereich

Ein Vergleich gegen ein Hardware-Stimmgerät ergab im Normalbereich sehr ähnliche
Werte; oberhalb von etwa 300 Hz werden beide ungenauer.

Die Mikrofon-Hardware bleibt der limitierende Faktor: Frequenzgang, Abstand zum Fell
und Raumgeräusche wirken sich stärker aus als jede Software-Optimierung. Ein externes
Mikrofon näher am Fell liefert zuverlässigere Werte als das eingebaute Laptop-/Handy-
Mikrofon aus größerer Distanz.

## Technik

Einzelne `index.html`-Datei: React + ReactDOM und Tailwind CSS liegen als lokale
Kopien im Ordner `lib/`, der App-Code ist vorab zu reinem JavaScript kompiliert
(kein Live-Babel im Browser). Kein npm, kein eigener Build-Schritt beim Deployen,
direkt als statische Seite über GitHub Pages hostbar.

Die Bibliotheken wurden bewusst lokal abgelegt statt per CDN eingebunden, damit die
App vollständig ohne Internetverbindung läuft – praktisch im Proberaum. Für die
Überschriften wird dadurch die Systemschrift (Georgia) statt Playfair Display
verwendet.

## Nutzung lokal

`index.html` lässt sich direkt im Browser öffnen – für alle Funktionen außer der
Mikrofon-Messung reicht das. Für den "🎤 Messen"-Button braucht es einen sicheren
Kontext (HTTPS oder `localhost`):

    cd ~/Documents/fellton
    python3 -m http.server 8000

Dann im Browser `http://localhost:8000` öffnen.

## Haftungsausschluss

Alle berechneten Frequenzen sind Richtwerte. Kesselmaterial, Felltyp, -dicke und
Bauart beeinflussen das tatsächliche Klangergebnis. Kein Ersatz für eigenes
Stimmen nach Gehör.