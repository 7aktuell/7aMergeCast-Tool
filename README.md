# 7aMergeCast

Tool der **7aktuell**-Medienagentur: mehrere Videoclips per Drag & Drop zu **einer**
normalisierten Datei zusammenfügen (macOS & Windows) – mit Sichten und Aussortieren
und automatischem Verpixeln von Gesichtern und Kennzeichen.

## Download

Neueste Version: **[Releases → latest](https://github.com/7aktuell/7aMergeCast-Tool/releases/latest)**
(dieses Handbuch beschreibt Version 0.3.0)

- **macOS** (Apple Silicon): `7aMergeCast_*_aarch64.dmg`
- **Windows** (64-bit): `7aMergeCast_*_x64-setup.exe`

> Als PDF zum Ausdrucken: [7aMergeCast-Benutzerhandbuch.pdf](7aMergeCast-Benutzerhandbuch.pdf)

---

# Benutzerhandbuch

## 1 · Was ist 7aMergeCast?

7aMergeCast fügt mehrere Videoclips per Drag & Drop zu EINER fertigen, normalisierten Datei zusammen – gedacht für den schnellen Reporter-Alltag (z. B. Material direkt aus der Kamera, auch Sony XAVC / HEVC). Die Clips werden auf ein einheitliches Format gebracht (1920×1080, H.264) und mit gewählter Bitrate neu kodiert. ffmpeg ist bereits eingebaut – es muss nichts installiert werden.

Dazu kommt, was man im Alltag rund um das Material braucht – alles lokal auf dem Rechner:

- Sichten und aussortieren: Clips im Schnelldurchlauf ansehen, abspielen und per Häkchen aus dem Export nehmen (Kapitel 3).
- Gesichter und Kfz-Kennzeichen automatisch verpixeln – pro Clip wählbar (Kapitel 5).
- Optional: Ton entrauschen und Video stabilisieren (Kapitel 5).

## 2 · Starten

- macOS: .dmg öffnen und 7aMergeCast.app nach „Programme“ ziehen.
- Meldung „… ist beschädigt und kann nicht geöffnet werden“? Das ist nicht wirklich beschädigt, sondern nur das Download-Quarantäne-Flag der unsignierten App. Einmal im Terminal ausführen (Pfad anpassen): xattr -dr com.apple.quarantine "/Applications/7aMergeCast.app" – danach öffnen.
- Erscheint nur „unbekannter Entwickler“: Rechtsklick auf die App → „Öffnen“ → nochmal „Öffnen“.
- Windows: bei der SmartScreen-Meldung „Weitere Informationen“ → „Trotzdem ausführen“.
- Unterstützte Eingabeformate: .mp4, .mov, .mxf, .mts, .m2ts, .mpg, .mpeg, .hevc.

## 3 · Clips hinzufügen und ordnen

- Hinzufügen: Dateien oder ganze Ordner ins Fenster ziehen (Ordner werden rekursiv nach Videos durchsucht) – oder über den Button „Clips hinzufügen…“.
- Reihenfolge: Clips werden beim Hinzufügen natürlich sortiert (datei\_2 kommt vor datei\_10). Per Drag lassen sie sich frei umsortieren; „Natürlich sortieren“ stellt die Namenssortierung wieder her.
- „+ Hinzufügen“ über der Liste nimmt weitere Clips dazu; „Alle entfernen“ leert die Liste (die Dateien selbst bleiben unberührt).
- Jeder Clip zeigt ein Vorschaubild, Dauer, Aufnahmedatum/-zeit und – wenn vorhanden – die Kamera aus den Metadaten. Defekte/unlesbare Clips werden erkannt und beim Zusammenfügen übersprungen (mit Hinweis).

### Sichten und aussortieren

Ein Klick auf einen Clip zeigt ihn rechts in der Vorschau. So triffst du schnell die Auswahl fürs Endmaterial:

- Durchsehen: einfach die Maus über das Vorschaubild bewegen – der Clip wird über einen Filmstreifen (12 Bilder) im Schnelldurchlauf gezeigt. Ein Klick auf ein Bild im Streifen springt dorthin.
- Abspielen: „Abspielen“ (oder Doppelklick auf den Clip) spielt ab dem gerade gezeigten Bild ab – mit Ton. Für Formate, die die Vorschau nicht direkt kann (z. B. MXF, MTS), wird einmalig eine kleine Vorschaudatei erzeugt.
- Häkchen vorne in der Clip-Liste („Im Export“, Taste X): abgewählte Clips bleiben in der Liste (abgedunkelt), kommen aber nicht ins Endmaterial. Größe, Länge und Uploadzeit rechnen nur mit den ausgewählten Clips.
- Tastatur: ↑/↓ Clip wechseln · Leertaste Abspielen/Pause · X ins Export ein/aus · G Gesichter verpixeln · K Kennzeichen verpixeln.
- Einzel-Fix (Knopf in der Vorschau): verarbeitet nur den gewählten Clip separat und normalisiert dessen erste Video- und Tonspur – hilfreich bei problematischen Dateien (z. B. Sony-XAVC mit zusätzlichem Metadaten-Stream). Ergebnis: &lt;name&gt;\_fix.mp4.

## 4 · Export-Einstellungen

### Bitrate

4 / 8 / 12 Mbit/s (Standard 12) oder ein eigener Wert. Höhere Bitrate = bessere Qualität und größere Datei.

### Dateiname

Format JJJJMMTT\_&lt;Freitext&gt;\_&lt;Laufzeit&gt;.mp4, z. B. 20261026\_HagelunwetterRT\_3min50.mp4. Datum ist heute, die Laufzeit (Minuten/Sekunden der fertigen Datei) wird automatisch ermittelt. Der Freitext wird automatisch gesäubert: Leerzeichen werden zu „\_“, Umlaute umgeschrieben (ä→ae …), Sonderzeichen entfernt. Die Live-Vorschau zeigt den fertigen Namen.

### Ausgabeordner

Frei wählbar; vorbelegt mit dem Ordner des ersten Clips bzw. dem zuletzt genutzten.

### Uploadzeit (Netz testen)

Optional: „Netz testen“ misst kurz die Upload-Geschwindigkeit deiner Verbindung. Daraus und aus der geschätzten Dateigröße wird die voraussichtliche Upload-Dauer berechnet und – praktisch für die Bitratenwahl – bei jedem Bitraten-Wechsel aktualisiert.

## 5 · Verbesserungen (optionale Schalter)

„Audio verbessern“ und „Video stabilisieren“ gelten für den ganzen Export und werden gemerkt; das Verpixeln von Gesichtern/Kennzeichen wählst du pro Clip. Alle Optionen verlängern die Verarbeitung, weil zusätzliche Schritte durchlaufen werden.

### Audio verbessern

Reduziert Störgeräusche – Wind, Hintergrund, Rauschen – mit dem neuronalen Verfahren DeepFilterNet und gleicht anschließend die Lautstärke an (EBU R128). Ideal für leise oder verrauschte Interviews aus dem Feld.

- Das Audio wird dafür auf Mono / 48 kHz verarbeitet (sprachoptimiert).
- Läuft vollständig offline auf dem Gerät – nichts wird hochgeladen.

### Video stabilisieren

Glättet verwackelte Handaufnahmen.

- Windows: vidstab (Zwei-Pass: erst Bewegungsanalyse, dann Korrektur – genauer).
- macOS: deshake (Ein-Pass, eingebaut).
- Das Bild wird dabei leicht hineingezoomt (minimaler Randbeschnitt).
- Achtung: Die Stabilisierung macht den Export etwa 2–3× langsamer als ohne – daher behutsam und nur gezielt einsetzen (bei wirklich wackligem Material).

### Gesichter / Kennzeichen verpixeln (pro Clip)

Für einzelne Clips lassen sich Gesichter und/oder Kfz-Kennzeichen automatisch unkenntlich machen – etwa bei Blaulicht-Material. Du entscheidest pro Clip: in der Liste über die Symbole Person (Gesichter) und Auto (Kennzeichen) oder in der Vorschau über die Haken.

- Für alle auf einmal: „Alle Gesichter“ bzw. „Alle Kennzeichen“ in der Leiste über der Clip-Liste schaltet die Option bei allen Clips ein – ein zweiter Klick bei allen wieder aus. Danach lassen sich einzelne Clips wie gewohnt abweichend einstellen.
- Die Erkennung läuft mehrmals pro Sekunde über den ganzen Clip und folgt dadurch auch bewegten Personen und Fahrzeugen. Jede Fundstelle wird grob verpixelt (Gesichter als Ellipse, Kennzeichen als Rechteck).
- Nur angehakte Clips werden analysiert; alle anderen bleiben unverändert.
- Läuft vollständig offline auf dem Gerät – nichts wird hochgeladen.
- Rechenzeit: Das Verpixeln braucht natürlich Rechenzeit – jedes Bild wird analysiert. Angehakte Clips brauchen etwa doppelt so lange wie ohne Anonymisierung; der Export dauert dadurch spürbar länger. Daher nur die Clips anhaken, die es wirklich brauchen.
- Wichtig: Die automatische Erkennung ist eine Hilfe, keine Garantie. Sehr kleine, stark verdeckte oder extrem schräge Gesichter/Kennzeichen können übersehen werden. Das Ergebnis vor der Weitergabe bitte immer selbst sichten.

## 6 · Zusammenfügen und Fortschritt

- Mit „Zusammenfügen“ starten. Die Anzeige zeigt die aktuelle Phase (Analyse → Kodieren → Entrauschen → Mischen), den Fortschritt in Prozent sowie ETA und Geschwindigkeit.
- „Abbrechen“ stoppt die laufende Verarbeitung.
- Nach Erfolg zeigt „Im Finder zeigen“ (Windows: „Im Explorer zeigen“) die fertige Datei direkt im Dateimanager.
- Existiert die Zieldatei schon, wird vorher gefragt, ob überschrieben werden soll.
- Unter „ffmpeg-Protokoll“ lassen sich bei Bedarf die technischen Details aus-/einklappen (bei Fehlern automatisch geöffnet).

## 7 · Hinweise und Fehlerbehebung

- Defekte Clips: werden automatisch übersprungen und am Ende als „übersprungen“ gemeldet.
- 10-Bit-Material (z. B. HEVC Main 10): wird automatisch auf 8-Bit gewandelt, damit das Ergebnis überall abspielbar ist.
- macOS „… ist beschädigt“: nicht wirklich beschädigt, nur das Download-Quarantäne-Flag der unsignierten App. Fix im Terminal: xattr -dr com.apple.quarantine "/Applications/7aMergeCast.app" (Pfad anpassen), dann öffnen. Bei „unbekannter Entwickler“ genügt Rechtsklick → „Öffnen“. Windows: SmartScreen → „Trotzdem ausführen“.
- Speicherplatz: Auch wenn die App auf ein anderes Laufwerk installiert wird, braucht Windows Platz auf C: – für das Entpacken bei der Installation und für Zwischendateien beim Zusammenfügen. Meldet der Installer „Error writing to file“, ist meist C: voll. Ein paar GB frei halten.
- Verarbeitung wirkt eingefroren? Auf Windows nicht ins Konsolenfenster klicken (QuickEdit-Modus pausiert Prozesse) – einmal Esc drücken.
- Handbuch und Version: Knopf „Handbuch“ oben rechts öffnet dieses PDF; „Über“ zeigt Version und Build-Zeit (wichtig bei Rückfragen, weil sich die Versionsnummer nicht bei jedem Build ändert). Auf dem Mac zusätzlich: Menü „Hilfe“ → „Benutzerhandbuch“.
- Debug-Bericht: Nach einem Lauf (auch nach Fehler oder Abbruch) speichert „Debug-Bericht speichern“ alle technischen Details als Textdatei in den Ausgabeordner – Quelldateien, Spuren und Längen, alle ffmpeg-Aufrufe und Meldungen. Diese Datei bei Problemen einfach mitschicken. Sie enthält keine Videodaten.

## 8 · Kurz zur Technik

7aMergeCast ist eine schlanke Tauri-App (Rust-Kern, Web-Oberfläche). ffmpeg/ffprobe und DeepFilterNet sind als mitgelieferte Programme eingebunden und laufen lokal. Kodiert wird plattformabhängig: macOS nutzt die Hardwarebeschleunigung VideoToolbox, Windows den Software-Encoder libx264. Das Zusammenfügen erfolgt über den ffmpeg-concat-Demuxer mit Neukodierung auf die gewählte Zielbitrate.
