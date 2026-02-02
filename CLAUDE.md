# Bad Peggy - Projektnotizen

## Übersicht

Bad Peggy ist ein Fork des Original-Projekts von coderslagoon. Das Original-Repository existiert nicht mehr auf GitHub.

- **Repository:** https://github.com/HJS-cpu/BadPeggy
- **Website:** http://hjs.bplaced.net/BadPeggy
- **Aktuelle Version:** 2.4.1
- **Java Version:** 17 (OpenJDK Temurin)
- **Build System:** Maven
- **GUI Framework:** SWT (Eclipse)
- **Copyright:** coderslagoon & HJS, GPLv3+

## Lokale Pfade

- **Quellcode:** `C:\Users\HJS\Claude.ai\BadPeggy`
- **Installierte Version:** `C:\Tools\Multimedia Tools\Bad Peggy`

## Implementierte Features (in diesem Fork)

### Toolbar (v2.4.1)
- **Datei:** `src/coderslagoon/badpeggy/GUI.java`
- **Buttons:** Scannen, Löschen, Verschieben, Ordner öffnen, Leeren
- **Verhalten:** Während Scan zeigt der Scan-Button "Stopp"

### Verbesserter About-Dialog (v2.4.1)
- Größeres Logo (128x128px, skaliert von 256x256)
- Fette Überschrift mit Version
- Klickbarer Website-Link
- Zentrierter Dialog

### Optimierte Tabellenfarben (v2.4.1)
- **Differentiate-Modus:** Helleres Grau (200-245) mit schwarzem Text
- **Selektion:** Helles Grün (`#90EE90`)
- **Hover-Effekt:** Noch helleres Grün (`#98FB98`)

### Open Folder mit Datei-Markierung
- **Datei:** `src/coderslagoon/badpeggy/GUI.java`
- **Funktion:** `onOpenFolder` Listener
- **Verhalten:**
  - Windows: `explorer /select,"Dateipfad"` - Datei wird im Explorer markiert
  - macOS: `open -R "Dateipfad"` - Datei wird im Finder markiert
  - Linux: Fallback auf Ordner öffnen

### Weitere Verbesserungen
- Maven Build System
- GitHub Actions CI/CD mit Custom JRE
- Java 17 Update
- Performance-Optimierungen
- Signature-Datei-Ausschluss im Shaded JAR

## Build & Deployment

### GitHub Actions (empfohlen)
- **Standard (Push/PR):** Nur Windows-Build (~2 Min)
- **Alle Plattformen:** Manueller Trigger mit "all_platforms" Checkbox
- **Workflow:** `.github/workflows/build.yml`
- **Artifacts:** https://github.com/HJS-cpu/BadPeggy/actions

Der Build erstellt automatisch:
1. JAR mit allen Abhängigkeiten (`badpeggy-*-standalone.jar`)
2. Custom JRE mit jlink (~35-40 MB statt ~126 MB)
3. Fertiges Release-Paket (`BadPeggy-Windows-x64`)

### Custom JRE (jlink)
Die Runtime wird mit jlink auf die benötigten Module reduziert:
- `java.base` - Grundfunktionen
- `java.desktop` - Bildverarbeitung (ImageIO, AWT)
- `java.logging` - Logging
- `java.prefs` - Einstellungen speichern

**Größenvergleich:**
| | Vollständige JRE | Custom JRE |
|--|------------------|------------|
| Unkomprimiert | ~126 MB | ~35-40 MB |
| ZIP | ~45 MB | ~15-20 MB |

### Lokaler Build (optional)
```bash
mvn clean package -DskipTests -Dswt.artifactId=org.eclipse.swt.win32.win32.x86_64
```

### Lokale Custom JRE erstellen (optional)
Erfordert JDK 17 Installation:
- `C:\Tools\Multimedia Tools\Bad Peggy\create_custom_jre.cmd`
- `C:\Tools\Multimedia Tools\Bad Peggy\apply_custom_jre.cmd`

## Wichtige Dateien

| Datei | Beschreibung |
|-------|--------------|
| `GUI.java` | Haupt-GUI-Klasse mit Toolbar, About-Dialog, Tabellenfarben |
| `NLS.java` | Internationalisierung (DE/EN/CZ) |
| `NLS_de.properties` | Deutsche Übersetzungen |
| `NLS_en.properties` | Englische Übersetzungen |
| `NLS_cz.properties` | Tschechische Übersetzungen |
| `ImageScanner.java` | Bild-Scan-Logik |
| `pom.xml` | Maven Build-Konfiguration |
| `build.yml` | GitHub Actions Workflow mit jlink |
| `README.md` | Projekt-Dokumentation mit Screenshot |

## Internationalisierung (I18N)

Neue Strings müssen in allen drei Sprachen hinzugefügt werden:
- `src/coderslagoon/badpeggy/NLS_de.properties`
- `src/coderslagoon/badpeggy/NLS_en.properties`
- `src/coderslagoon/badpeggy/NLS_cz.properties`

## Session-Historie

### 2026-02-02
- **Version 2.4.1:** Neue Version mit UI-Verbesserungen
- **Toolbar hinzugefügt:** Scan, Löschen, Verschieben, Ordner, Leeren
- **About-Dialog neu gestaltet:** Größeres Logo, klickbarer Website-Link
- **Tabellenfarben optimiert:** Helleres Grau, grüne Selektion/Hover
- **Copyright aktualisiert:** "coderslagoon & HJS"
- **CI/CD optimiert:** Standard nur Windows-Build (schneller)
- **Custom JRE mit jlink:** Release-Größe von ~45 MB auf ~15-20 MB reduziert
- **Release-Paket im Workflow:** Fertiges Paket als Artifact verfügbar

### 2026-02-01
- **Website-URL geändert:** `PRODUCT_SITE` auf `http://hjs.bplaced.net/BadPeggy` aktualisiert
- **onWebsite Listener vereinfacht:** Query-Parameter entfernt, Code von 19 auf 9 Zeilen reduziert
- **workflow_dispatch hinzugefügt:** Manuelle Builds über GitHub Actions möglich
- **README.md Badges:** Build-Status und Website-Badge hinzugefügt
- **Website-Projekt ausgelagert:** Separates Projekt unter `C:\Users\HJS\Claude.ai\BadPeggy Website`

### 2025-02-01
- **Open Folder verbessert:** Datei wird jetzt im Explorer/Finder markiert statt nur den Ordner zu öffnen
- **README.md aktualisiert:** Fork-Hinweis, Feature-Liste, Build-Anleitung hinzugefügt
- **README.md Screenshot:** `Bad Peggy.png` mit 400px Breite eingebunden
- **Release-Skript erstellt:** `create_release_zip.cmd` für saubere ZIP-Verteilung
