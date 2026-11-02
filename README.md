# NBT Struktur-Generator

Beschreibe ein Minecraft-Bauwerk in eigenen Worten. Claude entwirft es für genau diese Anfrage und schreibt den Bau-Code dafür. Du siehst das Ergebnis als 3D-Vorschau und lädst es als `.nbt` herunter. Die Datei funktioniert mit dem **Create-Schematic-Tisch / der Schematicannon** und mit dem **Strukturblock**.

**Direkt im Browser nutzen:** https://drakune.github.io/nbt-struktur-generator/

Oder `index.html` herunterladen und per Doppelklick öffnen. Installation oder Server sind nicht nötig.

## Funktionen

- **Eigene Entwürfe statt Vorlagen**: Claude schreibt für jede Anfrage eigenen Bau-Code. Der läuft abgeschottet im Browser (Web Worker, ohne Zugriff auf Seite oder API-Key).
- **Modellauswahl mit Kosten**: Claude Opus 5.5, Sonnet 5.5, Haiku 5.5 und Fable 5.1, dazu ein einstellbarer Denk-Aufwand. Vor dem Senden siehst du eine Kostenschätzung, danach die echten Kosten laut Token-Verbrauch und die Summe aller Anfragen.
- **Nachbessern im Dialog**: Änderungswünsche wie „Dach steiler, mehr Fenster“ überarbeiten den Entwurf. Fehler im Bau-Code kann Claude auf Knopfdruck selbst beheben.
- **Vorhandene `.nbt` laden** (Drag & Drop oder „.nbt öffnen“): ansehen, filtern, wieder exportieren oder von Claude umbauen und erweitern lassen. Block-Entity-Daten (Kisteninhalte, Create-Daten) und Entities bleiben erhalten, auch bei Mod-Blöcken.
- **Ebenen**: Achse (Y/X/Z), Richtung (von unten/oben, Westen/Osten, Norden/Süden) und Modus „nur eine Ebene“.
- **Blockliste**: Anzahl je Blocktyp. Jeder Typ lässt sich in der Vorschau ausblenden oder vom Export ausschließen.
- **Code-Ansicht**: Den Bau-Code selbst bearbeiten und lokal neu ausführen, das kostet nichts.
- Minecraft Java 1.20.1, 1.20.4, 1.21.1, 1.21.4 (die DataVersion wird passend gesetzt).

## API-Key und Kosten

Du brauchst einen eigenen Claude-API-Key von [console.anthropic.com](https://console.anthropic.com/settings/keys). Abgerechnet wird über dein Anthropic-Konto.

- Der Key wird **nur direkt an `api.anthropic.com`** geschickt. Auf Wunsch speichert die Seite ihn im `localStorage` deines Browsers, sonst bleibt er nur bis zum Schließen der Seite erhalten.
- Leg am besten einen eigenen Key mit Ausgabenlimit an.
- Eine typische Anfrage kostet je nach Modell und Aufwand zwischen unter 1 Cent (Haiku) und einigen Zehntel-Dollar (Opus mit hohem Aufwand). Die Preise stehen in `index.html` im Objekt `MODELS` (Listenpreise, ohne Gewähr).

## Im Spiel laden

- **Create**: `.nbt` in den Ordner `schematics` der Instanz legen und am Schematic-Tisch auswählen. Die Schematicannon setzt in der Regel keine Flüssigkeiten, Wasser und Lava füllst du dann selbst mit Eimern auf.
- **Strukturblock**: `.nbt` nach `saves/<Welt>/generated/minecraft/structures/` kopieren und im Strukturblock (Modus „Laden“) den Dateinamen eintragen.

## Technik

Eine einzige HTML-Datei ohne Build-Schritt. Bibliotheken kommen per CDN: [Anthropic TypeScript SDK](https://github.com/anthropics/anthropic-sdk-typescript) über esm.sh und [three.js](https://threejs.org) über jsDelivr. NBT lesen und schreiben, gzip und Vorschau laufen komplett im Browser.

## Lizenz

MIT
