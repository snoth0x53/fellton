# Fellton – Mikrofon-Test-Tool: Benutzeranleitung

Das Mikrofon-Test-Tool ist ein eigenständiges Diagnose-Werkzeug, mit dem man ein
Mikrofon-Setup prüfen kann, bevor es im Fellton-Rechner zum Einsatz kommt.

🔗 https://snoh0x53.github.io/fellton/mic-test.html

**Wichtig:** Das Tool benötigt HTTPS. Die Live-Version funktioniert direkt im Browser.
Für lokale Tests: `python3 -m http.server 8000` im Projektordner, dann
http://localhost:8000/mic-test.html öffnen.

---

## Wozu das Tool?

Bevor man mit dem Rechner arbeitet, lohnt es sich zu prüfen ob das Mikrofon
zuverlässige Werte liefert. Das Test-Tool zeigt:

- Wie stabil die Frequenzerkennung über mehrere Anschläge ist
- Wie laut das Signal tatsächlich ist (Pegel)
- Ob das Mikrofon die relevanten Frequenzen korrekt erfasst
- Einen **Sound Score** der die Signalqualität bewertet
- Einen Log der letzten Anschläge zum direkten Vergleich

---

## Starten

1. Seite öffnen.
2. Unter **„Eingabegerät"** das gewünschte Mikrofon auswählen.
3. **„Starten"** drücken — der Browser fragt einmalig nach Mikrofon-Erlaubnis.
4. Die grüne Statusanzeige **„Live — hört zu"** bestätigt dass alles läuft.

---

## Hauptanzeige

**Stärkste Gruppe (wie im Rechner)** — die große Zahl in der Mitte. Das ist der Wert
den der Fellton-Rechner bei diesem Anschlag anzeigen würde, inklusive Notenname
(z. B. `200.3 Hz (G#)`).

**Stabil über letzte Anschläge** — der stabilste Wert über die letzten 6 Anschläge.
Dieser Wert ist robuster als der Einzelwert und ein guter Indikator ob das Mikrofon
konsistent misst.

**YIN-Grundton (Vergleich)** — ein alternativer Algorithmus zur Frequenzerkennung,
nur zum Vergleich. Bei Perkussion oft unzuverlässig, daher nur als Referenz.

**Gruppen im Spektrum** — alle erkannten Frequenzgruppen des letzten Anschlags,
z. B. `200 · 315 · 419 Hz`. Die fett markierte Gruppe ist die ausgewählte.

**Pegel (RMS)** — der Balken und der Prozentwert darunter zeigen wie laut das Signal
ist. Ein zu niedriger Pegel kann die Erkennung beeinträchtigen.

---

## Sound Score

Der Sound Score (0–100) bewertet die Qualität des Signals anhand von fünf Faktoren:

- **Attack-Schärfe:** Wie klar und definiert ist der Anschlagsimpuls?
- **Tiefton-Energie (20–150 Hz):** Wie viel Tiefton-Anteil hat das Signal?
- **Harmonizität:** Wie klar sind die Partialtöne gegenüber dem Rauschen?
- **Ring-Chaos:** Wie gleichmäßig klingen die erkannten Partialtöne?
- **Dynamikumfang:** Wie groß ist der Abstand zwischen lautestem Peak und Grundrauschen?

Der Score ist pegelunabhängig normalisiert — zwei Mikrofone mit unterschiedlichem
Pegel können verglichen werden. Ein hoher Wert bedeutet ein sauberes, klar
definiertes Signal.

---

## Wellenform und Frequenzspektrum

**Wellenform (Zeitbereich)** — zeigt das Rohsignal des Mikrofons in Echtzeit.
Gut sichtbare Transienten beim Anschlag sind ein gutes Zeichen.

**Frequenzspektrum** — zeigt alle erkannten Frequenzen. Die farbigen Markierungen
zeigen die erkannten Gruppen: grün = stärkste/ausgewählte Gruppe, rot = weitere Gruppen.

---

## Log der letzten Anschläge

Die Tabelle unten zeigt die letzten 10 Anschläge mit:
- Uhrzeit
- Erkannte Gruppen (Hz)
- YIN-Wert (Vergleich)
- Pegel (%)
- Sound Score

So lässt sich auf einen Blick prüfen ob die Erkennung über mehrere Anschläge stabil ist.

---

## Trommel-Metadaten und CSV-Export

Vor der Messung können oben **Metadaten** eingetragen werden:
- **Trommel / Modell** — z. B. „Rogers Dynasonic 14×5"
- **Fell-Typ** — z. B. „Remo Ambassador Coated"
- **Bewertung (1–5 Sterne)** — subjektive Einschätzung des Klangs
- **Notizen** — z. B. „Stimmung nach Konzert, Snare-Seite locker"

Mit **„CSV exportieren"** werden alle Anschläge des Logs zusammen mit den Metadaten
als CSV-Datei gespeichert. Der Dateiname enthält automatisch das Datum.

Das ist nützlich um verschiedene Mikrofone oder Fell-Typen miteinander zu vergleichen.

---

## Einfrieren und Log leeren

**„Einfrieren"** hält die Live-Anzeige an — nützlich um einen Wert in Ruhe ablesen
zu können, ohne dass neue Anschläge ihn überschreiben. **„Weiter"** setzt die
Messung fort.

**„Log leeren"** löscht alle bisherigen Einträge und setzt den stabilen Wert zurück.

---

## Mikrofone vergleichen

Das Tool eignet sich gut um verschiedene Mikrofone zu vergleichen:

1. Erstes Mikrofon auswählen, mehrere Anschläge am selben Lug machen, CSV exportieren.
2. Stoppen, zweites Mikrofon auswählen, Log leeren, wieder messen, CSV exportieren.
3. Die beiden CSV-Dateien vergleichen: Sind die erkannten Frequenzen gleich? Ist der
   Pegel ähnlich? Ist der Sound Score vergleichbar?

---

## Tipps

**Pegel zu niedrig:**
Mikrofon näher ans Fell halten. Beim Smartphone hilft es, das Gerät direkt an die
Anschlagsstelle zu halten — je näher, desto stabiler die Erkennung.

**Viele verschiedene Gruppen im Spektrum:**
Das ist normal — ein Fell schwingt in mehreren Moden gleichzeitig. Der Algorithmus
wählt automatisch die tiefste bestätigte Grundmode aus. Wenn der angezeigte Wert
trotzdem schwankt, ein externes Mikrofon direkt am Fell verwenden.

**Snare:**
Teppich aushängen. Das Rasseln erzeugt viele Störfrequenzen und macht die Erkennung
deutlich unzuverlässiger.

**Erster Anschlag nach dem Start:**
Der allererste Anschlag nach dem Starten kann manchmal unzuverlässig sein, weil das
Mikrofon noch einpegelt. Einfach ignorieren und ab dem zweiten Anschlag messen.
