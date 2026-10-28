# 7aMergeCast

Tool der **7aktuell**-Medienagentur: mehrere Videoclips per Drag & Drop zu **einer**
normalisierten Datei zusammenfügen (macOS & Windows) – mit Sichten und Aussortieren,
automatischem Verpixeln von Gesichtern und Kennzeichen und lokaler O-Ton-Transkription.

## Download

Neueste Version: **[Releases → latest](https://github.com/7aktuell/7aMergeCast-Tool/releases/latest)**
(dieses Handbuch beschreibt Version 0.4.0)

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
- O-Töne transkribieren: gesprochenen Text von Interviews erkennen, korrigieren und kopieren oder als Textdatei speichern (Kapitel 7).
- Optional und experimentell: Ton entrauschen und Video stabilisieren (Kapitel 5).

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
- Tastatur: ↑/↓ Clip wechseln · Leertaste Abspielen/Pause · X ins Export ein/aus · G Gesichter verpixeln · K Kennzeichen verpixeln · O als O-Ton markieren.
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

## 5 · Weitere Bearbeitung (optionale Schalter)

„Audio verbessern“ und „Video stabilisieren“ sind experimentell und liegen im eingeklappten Bereich „Weitere Bearbeitung“ – ein Klick auf die Überschrift öffnet ihn. Ist ein Schalter an, steht das auch zugeklappt in der Überschrift. Beide gelten für den ganzen Export und werden gemerkt; das Verpixeln von Gesichtern/Kennzeichen wählst du pro Clip. Alle Optionen verlängern die Verarbeitung, weil zusätzliche Schritte durchlaufen werden.

### Audio verbessern

Reduziert Störgeräusche – Wind, Hintergrund, Rauschen – mit dem neuronalen Verfahren DeepFilterNet und gleicht anschließend die Lautstärke an (EBU R128). Ideal für leise oder verrauschte Interviews aus dem Feld.

- Das Audio wird dafür auf Mono / 48 kHz verarbeitet (sprachoptimiert).
- Läuft vollständig offline auf dem Gerät – nichts wird hochgeladen.
- Stärke: Leicht, Mittel, Stark oder Voll (Standard). Bei „Voll“ wird das Rauschen so weit wie möglich entfernt; die Stimme kann dann etwas künstlich klingen. Die schwächeren Stufen lassen bewusst etwas Umgebung stehen und klingen natürlicher. Die Stärke gilt für alle Clips des Exports und wird gemerkt.

### Entrauschen vorher anhören

In der Vorschau steht unter dem Clip die Zeile „Entrauschen“. So findest du die passende Stärke:

- Stelle im Clip wählen (Filmstreifen oder Wiedergabe) und „Probe hören“ klicken: Die App entrauscht 10 Sekunden ab dieser Stelle genau so wie später im Export und spielt sie ab – bei MP4/MOV mit dem Bild dazu.
- Während der Probe mit „Original / Entrauscht“ hin- und herschalten. Beide Fassungen sind gleich laut gemacht, damit man nur den Unterschied im Rauschen hört.
- Eine andere Stärke anklicken, während die Probe läuft: Es geht an derselben Stelle mit der neuen Stärke weiter. Schon gehörte Proben werden gemerkt und starten sofort.
- Ist „Audio verbessern“ ausgeschaltet, sagt die Zeile das und bietet „einschalten“ an – sonst wird beim Export gar nicht entrauscht.

### Video stabilisieren

Glättet verwackelte Handaufnahmen.

- Windows: vidstab (Zwei-Pass: erst Bewegungsanalyse, dann Korrektur – genauer).
- macOS: deshake (Ein-Pass, eingebaut).
- Das Bild wird dabei leicht hineingezoomt (minimaler Randbeschnitt).
- Achtung: Die Stabilisierung macht den Export etwa 2–3× langsamer als ohne – daher behutsam und nur gezielt einsetzen (bei wirklich wackligem Material).

### Grafikkarte oder Prozessor

Zum Kodieren nutzt 7aMergeCast automatisch die Grafikkarte, wenn sie das kann – das ist um ein Vielfaches schneller als der Prozessor. Beim Start prüft die App kurz, was auf dem Rechner funktioniert: unter Windows NVIDIA, Intel-Grafik oder AMD, auf dem Mac der eingebaute Grafikchip. Neben dem Schalter „Nur Prozessor kodieren“ steht, was erkannt wurde.

- Klappt es mit der Grafikkarte mitten im Export nicht (z. B. Treiberproblem), kodiert die App automatisch noch einmal mit dem Prozessor und sagt das am Ende an.
- „Nur Prozessor kodieren“ ist nur nötig, wenn die Grafikkarte sichtbar schlechte oder fehlerhafte Bilder liefert. Der Export dauert dann deutlich länger.

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

## 7 · O-Töne transkribieren

7aMergeCast erkennt den gesprochenen Text von Interviews und Statements und gibt ihn als Fließtext aus – zum Kopieren in Meldung, CMS oder Mail. Das läuft komplett auf dem Rechner und unabhängig vom Zusammenfügen: Man muss vorher und nachher nichts zusammenfügen.

### Clips markieren

- In der Clip-Liste auf das Mikrofon-Symbol klicken (oder in der Vorschau „O-Ton“, Taste O). Markierte Clips haben links einen grünen Rand. Die Markierung bleibt beim Umsortieren erhalten.
- Jeder Clip zeigt, welchen Ton er hat („Ton 2 Kan.“, „Ton mono“, „4 Tonspuren“, „kein Ton“). Clips ohne Tonspur lassen sich nicht markieren.

### Tonkanal – warum Kanal 1?

- Das externe Mikro (Funk- oder Ansteckmikro) liegt bei Profi-Aufnahmen fast immer auf Kanal 1, auf Kanal 2 oft das deutlich schlechtere Kameramikro. Eine Mischung holt Hall und Umgebung des Kameramikros dazu und verschlechtert die Erkennung spürbar. Deshalb liest die App standardmäßig nur Kanal 1.
- Umstellen unter „O-Ton-Erkennung“: Kanal 1, Kanal 2 oder Mischung – wird gemerkt.
- Ist der gewählte Kanal stumm (z. B. Funkmikro war auf Kanal 2 gesteckt), nimmt die App automatisch den anderen und vermerkt das über dem Text („Kanal 1 war stumm – Kanal 2 verwendet“). Sind beide stumm, kommt eine klare Meldung statt eines leeren Textes.
- Mono-Ton wird einfach so verwendet. Bei mehreren getrennten Tonspuren (z. B. MXF mit vier Mono-Spuren) gilt Spur 1 als Kanal 1 und Spur 2 als Kanal 2; in der Vorschau lässt sich die Spur auch fest wählen.
- Der Ton wird immer aus der Originaldatei gelesen, nie aus dem zusammengefügten Ergebnis.

### Transkribieren

- „O-Töne transkribieren (n)“ startet. Fortschritt, ETA und Geschwindigkeit wie beim Zusammenfügen; die Statuszeile zeigt Clip und Phase (Ton extrahieren → ggf. entrauschen → Sprache erkennen). „Abbrechen“ stoppt sauber, fertige Clips bleiben erhalten.
- Optional „Ton vor der Erkennung entrauschen“ (DeepFilterNet): hilft bei Wind und Lärm, dauert etwas länger.
- Schon erkannte Clips werden nicht erneut verarbeitet, solange Datei und Einstellungen gleich sind. „Neu transkribieren“ im Ergebnisfenster erzwingt es (z. B. nach geändertem Glossar).
- Fehlerhafte Clips werden übersprungen und im Ergebnis mit Grund genannt; technische Details lassen sich aufklappen. Der Rest läuft weiter.
- Tempo (Richtwert): Auf einem Mac mit M1 etwa 7-mal so schnell wie Echtzeit – ein 3-Minuten-O-Ton ist in rund 25 Sekunden erkannt. Ohne Grafikbeschleunigung deutlich langsamer.

### Einmaliger Modell-Download

- Beim ersten Transkribieren fragt die App, ob das Sprachmodell geladen werden soll („Genau“: 574 MB, „Schnell“: 190 MB). Es kommt von huggingface.co, wird per Prüfsumme kontrolliert und im App-Datenordner abgelegt. Ein abgebrochener Download wird beim nächsten Mal an derselben Stelle fortgesetzt.
- Danach läuft die Erkennung komplett ohne Internet – auch nachts im Auto mit schlechtem Netz. Tipp: Modell schon im Büro laden („O-Ton-Erkennung“ → „Modell laden“).
- „Genau“ (empfohlen) liefert die beste Qualität, „Schnell“ ist für schwache Rechner. Findet die App keinen nutzbaren Grafikprozessor, nimmt sie automatisch „Schnell“ und sagt das an.

### Glossar für Eigennamen

- Im Feld „Eigennamen / Glossar“ stehen Orte, Behörden, wiederkehrende Namen und Straßen, durch Komma getrennt. Die Erkennung bekommt die Liste als Hinweis und schreibt Eigennamen dadurch richtig (z. B. „Bad Cannstatt“ statt „Bad Kahnstadt“).
- Vorbelegt mit Behörden und Orten aus dem Berichtsgebiet, frei änderbar, wird gemerkt; „Standardliste“ stellt sie wieder her. Wirksam sind etwa die letzten 150 Wörter – Wichtiges also ans Ende.

### Ergebnis

- Das Fenster „O-Ton-Transkript“ zeigt den Text als Fließtext mit Absätzen an den Sprechpausen, je Clip ein Abschnitt mit dem Clipnamen als Überschrift. Keine Timecodes.
- Geschlossen? „Transkript anzeigen“ öffnet das letzte Ergebnis wieder – mit allen Korrekturen.
- Fehler direkt im Fenster korrigieren – Korrekturen werden mitkopiert und mitgespeichert.
- „Alles kopieren“ legt den gesamten Text in die Zwischenablage, das Kopier-Symbol neben einem Abschnitt nur diesen. Kurz erscheint „Kopiert“.
- „Als Text speichern“ legt eine Textdatei neben die (erste) Quelldatei: JJJJMMTT\_&lt;Freitext&gt;\_O-Ton.txt. Geht das nicht (z. B. schreibgeschützte Karte), landet sie im Ausgabeordner.
- Wichtig: Die Erkennung ist sehr gut, aber nicht fehlerfrei. Zitate vor der Veröffentlichung gegenhören – besonders Namen und Zahlen.

## 8 · Hinweise und Fehlerbehebung

- Defekte Clips: werden automatisch übersprungen und am Ende als „übersprungen“ gemeldet.
- 10-Bit-Material (z. B. HEVC Main 10): wird automatisch auf 8-Bit gewandelt, damit das Ergebnis überall abspielbar ist.
- macOS „… ist beschädigt“: nicht wirklich beschädigt, nur das Download-Quarantäne-Flag der unsignierten App. Fix im Terminal: xattr -dr com.apple.quarantine "/Applications/7aMergeCast.app" (Pfad anpassen), dann öffnen. Bei „unbekannter Entwickler“ genügt Rechtsklick → „Öffnen“. Windows: SmartScreen → „Trotzdem ausführen“.
- Speicherplatz: Auch wenn die App auf ein anderes Laufwerk installiert wird, braucht Windows Platz auf C: – für das Entpacken bei der Installation, Zwischendateien beim Zusammenfügen und das Sprachmodell (bis 574 MB). Meldet der Installer „Error writing to file“, ist meist C: voll. Ein paar GB frei halten.
- Verarbeitung wirkt eingefroren? Auf Windows nicht ins Konsolenfenster klicken (QuickEdit-Modus pausiert Prozesse) – einmal Esc drücken.
- Handbuch und Version: Knopf „Handbuch“ oben rechts öffnet dieses PDF; „Über“ zeigt Version und Build-Zeit (wichtig bei Rückfragen, weil sich die Versionsnummer nicht bei jedem Build ändert). Auf dem Mac zusätzlich: Menü „Hilfe“ → „Benutzerhandbuch“.
- Debug-Bericht: Nach einem Lauf (auch nach Fehler oder Abbruch) speichert „Debug-Bericht speichern“ alle technischen Details als Textdatei in den Ausgabeordner – Quelldateien, Spuren und Längen, alle ffmpeg-Aufrufe und Meldungen. Diese Datei bei Problemen einfach mitschicken. Sie enthält keine Videodaten.

## 9 · Kurz zur Technik

7aMergeCast ist eine schlanke Tauri-App (Rust-Kern, Web-Oberfläche). ffmpeg/ffprobe und DeepFilterNet sind als mitgelieferte Programme eingebunden und laufen lokal. Kodiert wird mit der Grafikkarte, wo möglich: macOS nutzt VideoToolbox, Windows je nach Rechner NVIDIA NVENC, Intel Quick Sync oder AMD AMF – sonst den Software-Encoder libx264. Das Zusammenfügen erfolgt über den ffmpeg-concat-Demuxer mit Neukodierung auf die gewählte Zielbitrate. Die O-Ton-Erkennung nutzt whisper.cpp (OpenAI Whisper, large-v3-turbo) mit Grafikbeschleunigung (Mac: Metal, Windows: Vulkan) und Silero VAD für die Sprechpausen.

### Internet-Zugriffe

7aMergeCast geht nur in zwei Fällen ins Internet, beide nur auf Knopfdruck: (1) „Netz testen“ lädt einige MB Testdaten zu Cloudflare hoch (speed.cloudflare.com), um die Upload-Zeit zu schätzen. (2) Der einmalige Download des Sprachmodells für die O-Ton-Erkennung von huggingface.co – nur nach Rückfrage. Sonst nichts: keine Telemetrie, keine Update-Prüfung. Videos, Ton und erkannte Texte verlassen den Rechner nicht.
