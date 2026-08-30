# Fellton – Benutzeranleitung

Fellton ist ein kostenloser Web-Rechner zum Stimmen von Schlagzeugfellen. Er läuft
direkt im Browser, benötigt keine Installation und funktioniert auch offline.

🔗 https://snoh0x53.github.io/fellton/

---

## Erste Schritte

Fellton öffnen und oben links auf **„Geräte laden"** klicken, um das Mikrofon
freizugeben. Der Browser fragt einmalig nach der Erlaubnis — einmal bestätigen, danach
wird sie gespeichert. Dann das gewünschte Mikrofon aus der Dropdown-Liste auswählen.

---

## Set benennen

Ganz oben gibt es ein Textfeld neben **„Set:"**. Dort kann das Kit einen Namen
bekommen, z. B. „Rogers XP8" oder „Proberaum-Set". Der Name erscheint beim Drucken
auf der PDF und hilft, mehrere Stimmungen auseinanderzuhalten.

---

## Trommel einrichten

Jede Trommel hat folgende Einstellungen:

**Typ** — Bass Drum, Tom, Floor Tom oder Snare. Der Typ bestimmt den zulässigen
Frequenzbereich für die Mikrofon-Messung: Snare 150–600 Hz, Tom/Floor Tom 50–350 Hz,
Bassdrum 30–160 Hz. Frequenzen außerhalb werden ignoriert.

**Durchmesser** — in Zoll, z. B. 14 für eine 14"-Snare. Wird zur Dokumentation
verwendet.

**Lugs** — Anzahl der Spannschrauben. Bestimmt die Kreuz-Stimmreihenfolge im Ring.

**Grundton** — die gewünschte Tonhöhe der Trommel, z. B. D# in Oktave 3. Daraus
werden alle Ziel-Frequenzen berechnet.

---

## Resonance-Modus (Toms und Bassdrum)

Der Resonance-Modus legt das Intervall zwischen Schlagfell und Resonanzfell fest:

- **Maximum (Unisono):** Beide Felle auf gleicher Frequenz — maximales Sustain,
  offener Klang.
- **High:** Leichtes Intervall — guter Kompromiss zwischen Sustain und Kontrolle,
  für Live gut geeignet.
- **Medium:** Deutlicheres Intervall — klarerer Attack.
- **Low:** Größtes Intervall — kürzestes Sustain, viel Attack.
- **Profi-Durchschnitt:** Berechnet aus über 90 realen Tunings professioneller
  Drummer (tune-bot.com/artists).

Zusätzlich lässt sich einstellen welches Fell höher gestimmt ist — Schlagfell oder
Resonanzfell. Das vertauscht die berechneten Frequenzen zwischen oben und unten.

---

## Snare-Intervall

Bei Snares gibt es statt des Resonance-Modus eine Intervall-Auswahl für das
Verhältnis von Resofell zu Schlagfell:

- **Perfekte Quinte (×1,5):** Standard, Resofell höher als Schlagfell.
- **Perfekte Quarte (×1,33):** Etwas enger.
- **Große Terz (×1,26):** Noch enger, kompakter Klang.
- **Unisono:** Beide Felle gleich.
- **Profi-Durchschnitt (n=22):** Empirischer Mittelwert — die meisten Profis stimmen
  enger als die Quinte, näher an Quarte/Terz.

**Hinweis:** Snare immer mit ausgehängtem Teppich messen, damit das Rasseln nicht
ins Signal kommt.

---

## Lug-für-Lug stimmen mit der Mikrofon-Messung

Unter jeder Trommel gibt es einen **🎤 Messen**-Button. Ein Klick startet die
Messung, ein weiterer stoppt sie.

**Wo anschlagen:**
- **Nah am Lug (2–3 cm vom Rand):** Misst die Lug-Frequenz dieser Schraube. So
  bringt man alle Lugs nacheinander auf denselben Zielwert.
- **Mittig:** Misst den Grundton der ganzen Trommel.

**Der Lug-Ring** zeigt die empfohlene Kreuz-Stimmreihenfolge: immer zum
gegenüberliegenden Lug, dann eine Schraube weiter und wieder gegenüber. So verteilt
sich die Spannung gleichmäßig.

**Ablauf:**
1. Trommel umdrehen — das zu stimmende Fell zeigt nach oben, das andere liegt auf
   einer weichen Unterlage (dämpft es ab, damit es nicht mitklingt).
2. Messen starten, jeden Lug in Kreuz-Reihenfolge anschlagen.
3. Schrauben anpassen bis der angezeigte Wert dem Zielwert entspricht (grün = nah dran).
4. Trommel umdrehen und das zweite Fell genauso stimmen.

---

## Filter für den Hochtonbereich

Ab etwa 300 Hz wird die Messung ungenauer, weil die Fell-Partialtöne enger
zusammenrücken. Dafür gibt es den **Filter**:

1. Erst eine korrekte Messung machen.
2. **Filter**-Button drücken — der zuletzt gemessene Wert wird zur Referenz.
3. Ab dann werden nur noch Frequenzen im Bereich von ±2 Halbtönen um diesen Wert
   berücksichtigt. Oktavfehler und Störpeaks fallen heraus.

Filter wieder ausschalten: nochmal auf **Filter** drücken. Bei größeren
Stimmungsänderungen neu setzen. Beim Fellwechsel, wenn man von unten hocharbeitet,
lässt man ihn am besten aus.

---

## Kalibrieren

Die Kalibrierfunktion ersetzt die generischen Formeln durch einen individuellen
Koeffizienten für genau diese Trommel und dieses Fell.

**Schritt 1:** Beide Felle auf exakt dieselbe Lug-Frequenz stimmen (Unisono).

**Schritt 2:** Trommel auf einen Ständer stellen (beide Felle frei, nichts gedämpft),
mittig anschlagen und den Grundton messen. Der abgelesene Wert ist die reale
Fundamentalfrequenz.

**Schritt 3:** Auf **„+ Kalibrieren"** klicken und beide Werte eintragen:
- Lug-Frequenz (der Wert den man am Lug gemessen hat)
- Fundamentalfrequenz (der Wert beim mittigen Anschlag auf dem Ständer)

**Übernehmen** drücken — ab jetzt rechnet Fellton mit dem individuellen Koeffizienten.
Er bleibt aktiv bis man auf **Zurücksetzen** drückt.

---

## Eigenes Set erstellen

Unten auf **„+ Trommel hinzufügen"** klicken. Die neue Trommel erscheint mit
Standard-Einstellungen (Tom). Typ, Durchmesser, Lugs, Grundton und Oktave anpassen.
Jede Trommel hat ein Namensfeld oben — dort z. B. „14" Snare" oder „22" Kick"
eintragen.

Nicht mehr benötigte Trommeln über **„Entfernen"** löschen.

---

## Ton-Vorschau

Die kleinen **▶**-Buttons spielen einen synthetischen Ton:
- Neben **Schlagfell (Lug)** und **Resofell (Lug):** reiner Sinuston auf
  Zielfrequenz — zum Hörvergleich beim Stimmen.
- Neben **Grundton (Trommelklang):** simulierter Trommelklang mit Partialtönen und
  Attack-Transient. Gibt eine grobe Vorstellung des Gesamtklangs.

---

## Drucken und als PDF speichern

Oben rechts auf **🖨 Drucken / Als PDF speichern** klicken. Das öffnet den
Browser-Druckdialog. Als Drucker „Als PDF speichern" wählen.

Das PDF enthält alle Trommeln mit ihren Einstellungen und berechneten Frequenzen,
das Datum und den Set-Namen. Die Mikrofon-Steuerung und alle Buttons werden
ausgeblendet.

Der **Erläuterungstext** erscheint auf einer eigenen letzten Seite — er kann im
Druckdialog einfach abgewählt werden wenn man ihn nicht braucht.

---

## Tipps aus der Praxis

**Smartphone als Mikrofon:**
Das eingebaute Mikrofon funktioniert, aber das Signal ist schwächer als bei einem
externen Mikrofon. Am besten das Smartphone möglichst nah an die Anschlagsstelle am
Lug halten — je näher, desto stabiler die Erkennung.

**Externes Ansteckmikrofon:**
Ein günstiges Lavaliermikrofon (z. B. Boya By-V10) direkt ans Fell geklammert liefert
deutlich zuverlässigere Ergebnisse als das eingebaute Laptop- oder Handy-Mikrofon.

**Ruhige Umgebung:**
Störgeräusche (andere Trommeln, Gespräche, Musik im Hintergrund) können die Erkennung
beeinflussen. Im Zweifel den Filter nutzen.

**Snare-Teppich aushängen:**
Das Rasseln des Teppichs überlagert das Fell-Signal stark. Snare immer mit
ausgehängtem Teppich messen.

**Nach dem Fellwechsel:**
Filter ausschalten und von unten hocharbeiten. Erst wenn die Grundstimmung steht,
Filter auf den Zielwert setzen und feinjustieren.

**Kalibrierung lohnt sich:**
Jede Trommel klingt anders. Ein kalibrierter Koeffizient ist deutlich genauer als
die Standardwerte, weil Kesselmaterial, Felltyp und Bauart bereits darin stecken.
Einmal kalibrieren, dann stimmt die Berechnung für genau diese Trommel.

---

## Häufige Fragen

**Die Messung springt zwischen verschiedenen Werten hin und her.**
Den Filter setzen — er begrenzt die Erkennung auf einen engen Frequenzbereich und
filtert Ausreißer heraus.

**Der gemessene Wert stimmt nicht mit dem erwarteten überein.**
Sicherstellen dass nah am Lug angeschlagen wird (2–3 cm vom Rand). Mittig anschlagen
misst den Grundton, nicht die Lug-Frequenz.

**Die App fragt nicht nach Mikrofon-Erlaubnis.**
Fellton benötigt HTTPS. Die Live-Version unter snoh0x53.github.io/fellton funktioniert
direkt. Für lokale Tests: `python3 -m http.server 8000` im Projektordner, dann
http://localhost:8000 öffnen.

**Der Messen-Button reagiert nicht.**
Browser-Tab neu laden und erneut auf „Geräte laden" klicken.
