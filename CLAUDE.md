# Bad Peggy - Projektnotizen

## Übersicht

Bad Peggy ist ein Fork des Original-Projekts von coderslagoon. Das Original-Repository existiert nicht mehr auf GitHub.

- **Repository:** https://github.com/HJS-cpu/BadPeggy
- **Website:** http://hjs.bplaced.net/BadPeggy
- **Aktuelle Version:** 2.4.2
- **Java Version:** 17 (OpenJDK Temurin)
- **Build System:** Maven
- **GUI Framework:** SWT (Eclipse)
- **Copyright:** coderslagoon und HJS, GPLv3
- **Sprachen:** Deutsch, Englisch (Tschechisch entfernt, Backup in `BackUps/`)

## Lokale Pfade

- **Quellcode:** `C:\Users\HJS\Claude.ai\BadPeggy`
- **Installierte Version:** `C:\Tools\Multimedia Tools\Bad Peggy`

## Implementierte Features (in diesem Fork)

### Progressbar in Statusleiste (v2.4.2)
- **Datei:** `src/coderslagoon/badpeggy/GUI.java`
- **Widget:** `Canvas` mit `PaintListener` ersetzt das alte `Label`
- **Farbe:** Steel Blue (`RGB(70, 130, 180)`) füllt sich proportional zum Scan-Fortschritt
- **Text:** Weißer Text über dem Fortschrittsbalken (Dateipfad, Status-Meldungen)
- **Phase 1 (Dateisuche):** Pulsierender Balken (Sinus-Interpolation, ~4 Sek. Zyklus) mit Dateianzahl
- **Phase 2 (Scannen):** Determinierter Fortschrittsbalken füllt sich proportional
- **Hilfsmethoden:** `setInfoText()`, `setInfoProgress()`, `startIndeterminateAnimation()`, `stopIndeterminateAnimation()`
- **Felder:** `indeterminate`, `indeterminatePos`, `indeterminateTimer`
- **Stil:** `SWT.DOUBLE_BUFFERED` für flackerfreies Rendering

### Toolbar mit Icons (v2.4.1)
- **Datei:** `src/coderslagoon/badpeggy/GUI.java`
- **Icons:** Feather Icons (MIT Lizenz) - play, stop-circle, trash-2, move, folder, x-circle
- **Buttons:** Scannen, Löschen, Verschieben, Ordner öffnen, Leeren
- **Verhalten:** Während Scan wechselt das Icon von Play zu Stop
- **Tooltips:** Beschreibung bei Mouse-Over

### Verbesserter About-Dialog (v2.4.1, überarbeitet v2.4.2)
- Größeres Logo (128x128px, skaliert von 256x256)
- Fette Überschrift mit Version
- Quadratischer Dialog, Inhalt vertikal zentriert
- Copyright zweizeilig: "Copyright 2005-2026" / "coderslagoon und HJS, GPLv3"
- Website-Link entfernt (separater Menü-Eintrag vorhanden)
- Menü: "Produktinformation" → "Über"

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

### Native MessageBox-Dialoge
- Ersetzt `MessageBox2` durch native SWT `MessageBox`
- Buttons korrekt rechts ausgerichtet (Windows-Standard)
- Hilfsmethode `showMessage()` in GUI.java

### Weitere Verbesserungen
- Maven Build System
- GitHub Actions CI/CD mit Custom JRE
- Java 17 Update
- Performance-Optimierungen
- Signature-Datei-Ausschluss im Shaded JAR

## Build & Deployment

**WICHTIG:** Nicht versuchen lokal zu bauen! Builds werden ausschließlich über GitHub Actions ausgeführt (Push oder manueller Trigger).

### GitHub Actions
- **Standard (Push/PR):** Nur JAR-Build (schnell, zum Testen)
- **Release-Paket:** Manueller Trigger mit "full_release" Checkbox (Default: true)
- **Alle Plattformen:** Manueller Trigger mit "all_platforms" Checkbox
- **Workflow:** `.github/workflows/build.yml`
- **Artifacts:** https://github.com/HJS-cpu/BadPeggy/actions

Der Build erstellt:
1. **Immer:** JAR mit allen Abhängigkeiten (`badpeggy-*-standalone.jar`)
2. **Nur bei full_release:** Custom JRE mit jlink (~35-40 MB)
3. **Nur bei full_release:** Fertiges Release-Paket (`BadPeggy-Windows-x64`)

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

### Release-Paket Inhalt
- `badpeggy.jar` - Standalone JAR
- `jre/` - Custom Java Runtime
- `badpeggy.ico` - Icon
- `install.vbs` - Desktop-Verknüpfung erstellen
- `BadPeggy.cmd` - Startskript
- `LICENSE.txt` - Lizenz
- `README.txt` - Installationsanleitung (EN)
- `LIESMICH.txt` - Installationsanleitung (DE)
- ~~`CTIMNE.txt` - Installationsanleitung (CZ)~~ (entfernt, siehe `BackUps/`)


## Wichtige Dateien

| Datei | Beschreibung |
|-------|--------------|
| `GUI.java` | Haupt-GUI-Klasse mit Toolbar, About-Dialog, Tabellenfarben |
| `resources/icons/` | Toolbar-Icons (Feather Icons, PNG) |
| `NLS.java` | Internationalisierung (DE/EN) |
| `NLS_de.properties` | Deutsche Übersetzungen |
| `NLS_en.properties` | Englische Übersetzungen |
| `ImageScanner.java` | Bild-Scan-Logik |
| `pom.xml` | Maven Build-Konfiguration |
| `build.yml` | GitHub Actions Workflow mit jlink |
| `etc/scripts/install.vbs` | Desktop-Verknüpfung erstellen |

## Internationalisierung (I18N)

Neue Strings müssen in beiden Sprachen hinzugefügt werden:
- `src/coderslagoon/badpeggy/NLS_de.properties`
- `src/coderslagoon/badpeggy/NLS_en.properties`

**Hinweis:** Tschechisch wurde entfernt. Backup-Dateien liegen in `BackUps/` (NLS_cz.properties, badpeggy_CZ.html, CTIMNE.txt).

## Bekannte Warnungen (können ignoriert werden)

Beim Build erscheinen diese Warnungen, die harmlos sind:
```
[WARNING] The POM for com.coderslagoon:baselib-swt:jar:1.0.2 is invalid...
[ERROR] 'dependencies.dependency.artifactId' for org.eclipse.platform:org.eclipse.swt.${swt.os}:jar...
```
Diese kommen von ungültigen Variablen in den baselib-swt und SWT POMs, die wir mit `<exclusions>` umgehen.

## Session-Historie

### 2026-02-04 (Abend)
- **Indeterminate Progressbar:** Pulsierender Balken während Dateisuche (Phase 1)
  - Sinus-Interpolation zwischen Dunkelgrau und Steel Blue (~4 Sek. Zyklus)
  - Statustext zeigt live Dateianzahl: "%d Dateien gefunden"
  - NLS-String `GUI_MSG_SEARCHING_2` (DE/EN)
- **Tschechisch entfernt:** Komplette CZ-Sprachunterstützung ausgebaut
  - Dateien nach `BackUps/` verschoben (NLS_cz.properties, badpeggy_CZ.html, CTIMNE.txt)
  - `LANGS`-Array, Doku (HTML, README), build.yml angepasst
- **About-Dialog überarbeitet:**
  - Menü "Produktinformation" → "Über"
  - Website-Link entfernt (doppelt mit Menü-Eintrag)
  - Copyright zweizeilig: "Copyright 2005-2026" / "coderslagoon und HJS, GPLv3"
  - Dialog quadratisch, Inhalt vertikal zentriert
- **Toolbar-Fix:** Scan-Button nicht mehr fokussiert/hervorgehoben beim Start (`badLst.setFocus()`)

### 2026-02-04
- **Version 2.4.2:** Progressbar in Statusleiste
- **Statusleiste:** `Label` durch `Canvas` mit `PaintListener` ersetzt
- **Fortschrittsbalken:** Steel Blue füllt sich proportional zum Scan-Fortschritt
- **Felder:** `infoBar`, `infoText`, `infoProgress`, `progressColor`
- **Build-Hinweis:** CLAUDE.md aktualisiert - Builds nur über GitHub Actions

### 2026-02-03 (Nacht)
- **CI Test-Schritte entfernt:** Tests benötigen Display und schlugen auf headless GitHub Actions fehl
- Tests waren bereits `continue-on-error: true`, jetzt komplett aus Workflow entfernt (Windows, Linux, macOS)
- Build-Annotation "exit code 1" damit behoben
- **Workflow umbenannt:** "Build and Test" → "Build" (da keine Tests mehr)
- **GitHub Release v2.4.1 erstellt:** https://github.com/HJS-cpu/BadPeggy/releases/tag/v2.4.1

### 2026-02-03 (Abend)
- **Toolbar Icons:** Feather Icons (MIT) hinzugefügt - play, stop-circle, trash-2, move, folder, x-circle
- **Native MessageBox:** MessageBox2 durch native SWT MessageBox ersetzt (korrekte Button-Ausrichtung)
- **Workflow optimiert:** `full_release` Option - Release-Paket nur bei manuellem Trigger
- **Repository bereinigt:** Obsolete Dateien entfernt (.classpath, .project, build.sh, etc.)
- **Duplikate entfernt:** Root-Dateien gelöscht, Workflow kopiert aus etc/

### 2026-02-03
- **jlink Fix:** `--compress=zip-6` → `--compress=2` (JDK 17 Syntax)
- **SWT Manifest Fix:** `SWT-OS` und `SWT-Arch` Attribute zum shaded JAR hinzugefügt
- **Transitive Abhängigkeit Fix:** baselib-swt SWT-Abhängigkeiten ausgeschlossen
- **Release-Paket vervollständigt:** install.vbs, Icon, alle READMEs (EN/DE/CZ), Lizenz
- **README.md aktualisiert:** v2.4.1 Features, neues Build-System dokumentiert

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
