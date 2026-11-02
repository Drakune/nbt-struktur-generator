# NBT Struktur-Generator

Beschreibe ein Minecraft-Bauwerk in eigenen Worten. Claude entwirft es für genau diese Anfrage und schreibt den Bau-Code dafür. Du siehst das Ergebnis als 3D-Vorschau und lädst es als `.nbt` herunter. Die Datei funktioniert mit dem **Create-Schematic-Tisch / der Schematicannon** und mit dem **Strukturblock**.

**Direkt im Browser nutzen:** https://drakune.github.io/nbt-struktur-generator/

Oder `index.html` herunterladen und per Doppelklick öffnen. Installation oder Server sind nicht nötig.

## Funktionen

- **Eigene Entwürfe statt Vorlagen**: Claude schreibt für jede Anfrage eigenen Bau-Code. Der läuft abgeschottet im Browser (Web Worker, ohne Zugriff auf Seite oder API-Key).
- **Echte Minecraft-Texturen und -Modelle** in der 3D-Vorschau: Treppen, Zäune, Scheiben, Pflanzen usw. sehen aus wie im Spiel (siehe unten).
- **Modellauswahl mit Kosten**: Claude Opus 5.5, Sonnet 5.5, Haiku 5.5 und Fable 5.1, dazu eine einstellbare Gründlichkeit. Vor dem Senden siehst du eine Kostenschätzung, danach die echten Kosten laut Token-Verbrauch und die Summe aller Anfragen.
- **Nachbessern im Dialog**: Änderungswünsche wie „Dach steiler, mehr Fenster“ überarbeiten den Entwurf. Fehler im Bau-Code kann Claude auf Knopfdruck selbst beheben.
- **Vorhandene `.nbt` laden** (Drag & Drop oder „Öffnen“): ansehen, filtern, wieder exportieren oder von Claude umbauen und erweitern lassen. Block-Entity-Daten (Kisteninhalte, Create-Daten) und Entities bleiben erhalten, auch bei Mod-Blöcken.
- **Ebenen**: Achse (Y/X/Z), Richtung (von unten/oben, Westen/Osten, Norden/Süden) und Modus „einzeln“.
- **Blockliste**: Anzahl je Blocktyp mit Textur-Vorschau. Jeder Typ lässt sich in der Vorschau ausblenden oder vom Export ausschließen.
- **Aufgeräumte Oberfläche**: Beide Seitenleisten lassen sich ein- und ausklappen. API-Key und Kosten stehen in den Einstellungen. Dunkles Design (Standard) und helles Design zum Umschalten.
- **Funktioniert auch mit Fingerprinting-Schutz** (Firefox resistFingerprinting, LibreWolf, Brave): Texturen werden selbst dekodiert statt über Canvas ausgelesen.
- **Auswählen, verschieben, gruppieren**: Klick wählt einen Block, Doppelklick einen zusammenhängenden Teil (z. B. ein ganzes Gebäude), mit dem Auswahl-Werkzeug ziehst du einen Rahmen. Die Auswahl lässt sich mit dem Pfeil-Gizmo, den Pfeiltasten (Bild ↑/↓ für die Höhe) oder Buttons verschieben, duplizieren und löschen. Rückgängig und Wiederholen mit Strg+Z / Strg+Y.
- **Gruppen**: Claude teilt jeden Entwurf in benannte Gruppen auf (Fundament, Wände, Dach …). In der Gruppenübersicht kannst du sie umbenennen, auswählen, verschieben und ausblenden oder aus einer Auswahl neue Gruppen bilden. Die Gruppen werden in der `.nbt` mitgespeichert (zusätzlicher Eintrag `nbtgen_groups`, den Minecraft und Create ignorieren) und beim Öffnen wieder eingelesen.
- **Luft-Blöcke** werden standardmäßig entfernt. Unter „Optionen“ lassen sie sich behalten, wenn sie beim Platzieren das Gelände freiräumen sollen.
- **Alle Java-Versionen von 1.16 bis 26.3** (die DataVersion wird passend gesetzt).

## Texturen

Die Texturen werden **automatisch** geladen, sobald eine Struktur angezeigt wird. Die Seite holt sie direkt von den offiziellen Servern:

- **Minecraft** von Mojang (`piston-data.mojang.com`, dieselbe Quelle wie jeder Launcher, ca. 25–30 MB), passend zur eingestellten Version
- **Create** von Modrinth (`cdn.modrinth.com`), sobald die Struktur `create:`-Blöcke enthält

Danach liegen sie nur lokal im Browser (IndexedDB), der Download passiert also nur einmal. Im Repo liegt nichts davon, denn die Minecraft-Texturen gehören Mojang. Unter „Texturen“ kannst du eine andere Version laden, das automatische Laden abschalten oder eigene JARs und Ressourcenpakete (.zip) verwenden, zum Beispiel weitere Mod-JARs.

Blöcke ohne eigenes Modell (Truhen, Betten, Schilder) werden als vereinfachte Form mit ihrer Textur dargestellt, Blöcke ohne geladene Texturen als farbige Würfel.

## API-Key und Kosten

Du brauchst einen eigenen Claude-API-Key von [console.anthropic.com](https://console.anthropic.com/settings/keys). Abgerechnet wird über dein Anthropic-Konto.

- Der Key wird **nur direkt an `api.anthropic.com`** geschickt. Auf Wunsch speichert die Seite ihn im `localStorage` deines Browsers, sonst bleibt er nur bis zum Schließen der Seite erhalten.
- Leg am besten einen eigenen Key mit Ausgabenlimit an.
- Eine typische Anfrage kostet je nach Modell und Aufwand zwischen unter 1 Cent (Haiku) und einigen Zehntel-Dollar (Opus mit hohem Aufwand). Die Preise stehen in `index.html` im Objekt `MODELS` (Listenpreise, ohne Gewähr).

## Im Spiel laden

- **Create**: `.nbt` in den Ordner `schematics` der Instanz legen und am Schematic-Tisch auswählen. Die Schematicannon setzt in der Regel keine Flüssigkeiten, Wasser und Lava füllst du dann selbst mit Eimern auf.
- **Strukturblock**: `.nbt` nach `saves/<Welt>/generated/minecraft/structures/` kopieren und im Strukturblock (Modus „Laden“) den Dateinamen eintragen.

## Technik

Eine einzige HTML-Datei ohne Build-Schritt. Bibliotheken kommen per CDN: [Anthropic TypeScript SDK](https://github.com/anthropics/anthropic-sdk-typescript) über esm.sh und [three.js](https://threejs.org) über jsDelivr. NBT lesen und schreiben, gzip, JAR-Entpacken, Minecraft-Modelle und Vorschau laufen komplett im Browser.

## Lizenz

MIT
