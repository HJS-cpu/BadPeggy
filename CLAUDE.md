# Bad Peggy - Projektnotizen

## Übersicht

Bad Peggy ist ein Fork des Original-Projekts von coderslagoon. Das Original-Repository existiert nicht mehr auf GitHub.

- **Repository:** https://github.com/HJS-cpu/BadPeggy
- **Aktuelle Version:** 2.4
- **Java Version:** 17 (OpenJDK Temurin)
- **Build System:** Maven
- **GUI Framework:** SWT (Eclipse)

## Lokale Pfade

- **Quellcode:** `C:\Users\HJS\Claude.ai\BadPeggy`
- **Installierte Version:** `C:\Tools\Multimedia Tools\Bad Peggy`

## Implementierte Features (in diesem Fork)

### Open Folder mit Datei-Markierung
- **Datei:** `src/coderslagoon/badpeggy/GUI.java` (Zeile 867-904)
- **Funktion:** `onOpenFolder` Listener
- **Verhalten:**
  - Windows: `explorer /select,"Dateipfad"` - Datei wird im Explorer markiert
  - macOS: `open -R "Dateipfad"` - Datei wird im Finder markiert
  - Linux: Fallback auf Ordner öffnen

### Weitere Verbesserungen
- Maven Build System
- GitHub Actions CI/CD (Windows, Linux, macOS ARM64)
- Java 17 Update
- Performance-Optimierungen
- Signature-Datei-Ausschluss im Shaded JAR

## Build & Deployment

### Lokaler Build
```bash
mvn clean package -DskipTests -Dswt.artifactId=org.eclipse.swt.win32.win32.x86_64
```

### GitHub Actions
- Build wird automatisch ausgelöst bei Push auf `master`
- Workflow: `.github/workflows/build.yml`
- Artifacts verfügbar unter: https://github.com/HJS-cpu/BadPeggy/actions

### Release ZIP erstellen
- **Skript:** `C:\Tools\Multimedia Tools\Bad Peggy\create_release_zip.cmd`
- Erstellt `BadPeggy_Windows_x64.zip` (~129 MB)
- Enthält: JAR, JRE, Libs, Dokumentation
- Ausgeschlossen: `badpeggy_old.jar`, `badpeggy.properties`

## Wichtige Dateien

| Datei | Beschreibung |
|-------|--------------|
| `GUI.java` | Haupt-GUI-Klasse mit allen UI-Komponenten |
| `NLS.java` | Internationalisierung (DE/EN/CZ) |
| `NLS_de.properties` | Deutsche Übersetzungen |
| `NLS_en.properties` | Englische Übersetzungen |
| `ImageScanner.java` | Bild-Scan-Logik |
| `pom.xml` | Maven Build-Konfiguration |
| `README.md` | Projekt-Dokumentation mit Screenshot |
| `Bad Peggy.png` | Screenshot für README (400px) |
| `create_release_zip.cmd` | Skript zum Erstellen des Release-ZIPs |

## Internationalisierung (I18N)

Neue Strings müssen in beiden Sprachen hinzugefügt werden:
- `src/coderslagoon/badpeggy/NLS_de.properties`
- `src/coderslagoon/badpeggy/NLS_en.properties`

## Session-Historie

### 2025-02-01
- **Open Folder verbessert:** Datei wird jetzt im Explorer/Finder markiert statt nur den Ordner zu öffnen
- **README.md aktualisiert:** Fork-Hinweis, Feature-Liste, Build-Anleitung hinzugefügt
- **README.md Screenshot:** `Bad Peggy.png` mit 400px Breite eingebunden
- **Release-Skript erstellt:** `create_release_zip.cmd` für saubere ZIP-Verteilung
  - Kopiert alle benötigten Dateien (JAR, JRE, Libs, alle TXT-Dateien)
  - Schließt `badpeggy_old.jar` und `badpeggy.properties` aus
  - Erstellt `BadPeggy_Windows_x64.zip`
