# 7aMergeCast

Tool der **7aktuell**-Medienagentur zum Zusammenfügen mehrerer Videoclips zu
**einer** normalisierten Datei (macOS & Windows) – per Drag & Drop, mit optionaler
Audio-Verbesserung (DeepFilterNet) und Video-Stabilisierung.

## Download

Neueste Version: **[Releases → latest](https://github.com/7aktuell/7aMergeCast-Tool/releases/latest)**

- **macOS** (Apple Silicon): `7aMergeCast_*_aarch64.dmg`
- **Windows** (64-bit): `7aMergeCast_*_x64-setup.exe`

> Als PDF zum Ausdrucken: [7aMergeCast-Benutzerhandbuch.pdf](7aMergeCast-Benutzerhandbuch.pdf)

---

# Benutzerhandbuch

## 1 · Was ist 7aMergeCast?

7aMergeCast fügt mehrere Videoclips per Drag & Drop zu **einer** fertigen,
normalisierten Datei zusammen – gedacht für den schnellen Reporter-Alltag
(z. B. Material direkt aus der Kamera, auch Sony XAVC / HEVC). Die Clips werden
auf ein einheitliches Format gebracht (1920×1080, H.264) und mit gewählter
Bitrate neu kodiert. ffmpeg ist bereits eingebaut – es muss nichts installiert werden.

## 2 · Starten

- **macOS:** `.dmg` öffnen und `7aMergeCast.app` nach **Programme** ziehen.
  - Meldung **„… ist beschädigt und kann nicht geöffnet werden"**? Das ist nur das
    Download-Quarantäne-Flag der unsignierten App (nicht wirklich beschädigt). Einmal
    im **Terminal** ausführen (Pfad anpassen):
    ```bash
    xattr -dr com.apple.quarantine "/Applications/7aMergeCast.app"
    ```
    Danach normal per Doppelklick öffnen.
  - Erscheint stattdessen nur „unbekannter Entwickler": **Rechtsklick** auf die App →
    **„Öffnen"** → nochmal **„Öffnen"**.
- **Windows:** bei der SmartScreen-Meldung **„Weitere Informationen"** → **„Trotzdem ausführen"**.
- Unterstützte Eingabeformate: **.mp4, .mov, .mxf**.

## 3 · Clips hinzufügen und ordnen

- **Hinzufügen:** Dateien oder ganze Ordner ins Fenster ziehen (Ordner werden
  rekursiv nach Videos durchsucht) – oder über den Button **„Clips hinzufügen…"**.
- **Reihenfolge:** Clips werden beim Hinzufügen natürlich sortiert
  (`datei_2` vor `datei_10`). Per Drag frei umsortierbar; **„Natürlich sortieren"**
  stellt die Namenssortierung wieder her.
- Jeder Clip zeigt ein **Vorschaubild**, **Aufnahmedatum/-zeit** und – wenn vorhanden –
  die **Kamera** aus den Metadaten. Defekte/unlesbare Clips werden erkannt und beim
  Zusammenfügen übersprungen (mit Hinweis).
- **Einzel-Fix** (Knopf am Clip): verarbeitet eine einzelne Datei separat und
  normalisiert nur deren erste Video- und Tonspur – hilfreich bei problematischen
  Dateien (z. B. Sony-XAVC mit zusätzlichem Metadaten-Stream). Ergebnis: `<name>_fix.mp4`.

## 4 · Export-Einstellungen

- **Bitrate:** 4 / 8 / 12 Mbit/s (Standard 12) oder ein eigener Wert. Höhere
  Bitrate = bessere Qualität und größere Datei.
- **Dateiname:** Format `JJJJMMTT_<Freitext>.mp4`, mit dem heutigen Datum
  vorausgefüllt. Der Freitext wird automatisch gesäubert (Leerzeichen → `_`,
  Umlaute umgeschrieben `ä→ae …`, Sonderzeichen entfernt). Die Live-Vorschau zeigt
  den fertigen Namen.
- **Ausgabeordner:** frei wählbar; vorbelegt mit dem Ordner des ersten Clips bzw.
  dem zuletzt genutzten.
- **Uploadzeit (Netz testen):** optional – misst kurz die Upload-Geschwindigkeit
  und schätzt daraus + der Dateigröße die voraussichtliche Upload-Dauer; aktualisiert
  sich bei jedem Bitraten-Wechsel (praktisch für die Bitratenwahl).

## 5 · Verbesserungen (optionale Schalter)

Beide Optionen sind abschaltbar und werden gemerkt. Sie verlängern die Verarbeitung.

- **Audio verbessern:** reduziert Störgeräusche (Wind, Hintergrund, Rauschen) mit dem
  neuronalen Verfahren **DeepFilterNet** und gleicht die Lautstärke an (EBU R128) –
  ideal für leise oder verrauschte Interviews. Das Audio wird dafür auf Mono/48 kHz
  verarbeitet; läuft vollständig offline.
- **Video stabilisieren:** glättet verwackelte Aufnahmen. Windows: **vidstab**
  (Zwei-Pass, genauer); macOS: **deshake** (Ein-Pass). Das Bild wird dabei leicht
  hineingezoomt (minimaler Randbeschnitt).

## 6 · Zusammenfügen und Fortschritt

- Mit **„Zusammenfügen"** starten. Die Anzeige zeigt die aktuelle Phase
  (Analyse → Kodieren → Entrauschen → Mischen), den Fortschritt in Prozent sowie
  **ETA** und **Geschwindigkeit**.
- **„Abbrechen"** stoppt die laufende Verarbeitung.
- Nach Erfolg zeigt **„Im Finder zeigen"** die fertige Datei direkt im Dateimanager.
- Existiert die Zieldatei schon, wird vorher gefragt, ob überschrieben werden soll.
- Unter **„ffmpeg-Protokoll"** lassen sich bei Bedarf die technischen Details
  aus-/einklappen (bei Fehlern automatisch geöffnet).

## 7 · Hinweise und Fehlerbehebung

- **Defekte Clips** werden automatisch übersprungen und am Ende als „übersprungen" gemeldet.
- **10-Bit-Material** (z. B. HEVC Main 10) wird automatisch auf 8-Bit gewandelt,
  damit das Ergebnis überall abspielbar ist.
- **macOS „… ist beschädigt":** nicht wirklich beschädigt, nur das Download-Quarantäne-Flag
  der unsignierten App. Fix: `xattr -dr com.apple.quarantine "/Applications/7aMergeCast.app"`
  (Pfad anpassen), dann öffnen. Bei „unbekannter Entwickler" genügt Rechtsklick → „Öffnen".
- **Windows „unbekannter Herausgeber":** SmartScreen → „Weitere Informationen" → „Trotzdem ausführen".
- **Verarbeitung wirkt eingefroren?** Auf Windows nicht ins Konsolenfenster klicken
  (QuickEdit-Modus pausiert Prozesse) – einmal **Esc** drücken.

## 8 · Kurz zur Technik

7aMergeCast ist eine schlanke Tauri-App (Rust-Kern, Web-Oberfläche). ffmpeg/ffprobe
und DeepFilterNet sind als mitgelieferte Programme eingebunden und laufen lokal.
Kodiert wird plattformabhängig: macOS nutzt die Hardwarebeschleunigung VideoToolbox,
Windows den Software-Encoder libx264. Das Zusammenfügen erfolgt über den
ffmpeg-concat-Demuxer mit Neukodierung auf die gewählte Zielbitrate.
