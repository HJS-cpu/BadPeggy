# BadPeggy Projekt-Dokumentation

## Projektübersicht

**BadPeggy** ist ein Java/SWT-Tool zum Scannen und Erkennen beschädigter Bilddateien (JPEG, PNG, etc.).

- **Version**: 2.4
- **Lizenz**: GPLv3+
- **Copyright**: CODERSLAGOON, HJS
- **GitHub Repository**: https://github.com/HJS-cpu/BadPeggy

## Durchgeführte Arbeiten

### 1. Maven Build-System eingerichtet

- `pom.xml` erstellt mit allen Abhängigkeiten
- Abhängigkeiten von Maven Central:
  - `com.coderslagoon:baselib:1.0.2`
  - `com.coderslagoon:baselib-swt:1.0.2`
  - `org.eclipse.swt` (plattformspezifisch)

### 2. GitHub Actions CI/CD

- Workflow in `.github/workflows/build.yml`
- Baut für drei Plattformen:
  - Windows (x86_64)
  - Linux (x86_64)
  - macOS (ARM64/aarch64)
- Java 17 erforderlich (baselib-swt Abhängigkeit)

### 3. Performance-Optimierungen

- `LinkedList` → `ArrayList` für bessere Iteration
- `HashSet<Object> resultTags` für O(1) Duplikaterkennung
- Color-Caching mit `Map<Integer, Color> colorCache` (verhindert Memory Leaks)
- `finalizeRemoval()` optimiert mit `removeAll()`

### 4. Neue Features (Version 2.4)

- **"Verzeichnis öffnen"** im Kontextmenü - öffnet den übergeordneten Ordner im Explorer
- Übersetzungen in DE, EN, CZ

### 5. Portable Windows-Version

Erstellt in `C:\Users\HJS\Downloads\badpeggy-new\` (kann beliebig umbenannt werden)

## Dateistruktur - Portable Version

```
BadPeggy/
├── BadPeggy.cmd          # Startskript (CMD)
├── badpeggy.jar          # Hauptanwendung
├── badpeggy.ico          # Anwendungs-Icon
├── badpeggy.properties   # Konfigurationsdatei (wird zur Laufzeit erstellt)
├── install.vbs           # Erstellt Desktop-Verknüpfung
├── jre/                  # Java 17 Runtime (Adoptium JRE 17.0.17+10)
└── lib/                  # Abhängigkeiten
    ├── baselib-1.0.2.jar
    ├── baselib-swt-1.0.2.jar
    └── org.eclipse.swt.win32.win32.x86_64-3.130.0.jar
```

## Build-Anleitung

### Lokaler Build (erfordert Maven + Java 17)

```bash
cd C:\Users\HJS\Claude.ai\BadPeggy
mvn clean package -P windows
```

### GitHub Actions Build

1. Änderungen committen und pushen
2. Build läuft automatisch
3. Artefakte herunterladen:
   ```bash
   gh run download <run-id> -n badpeggy-windows-latest
   ```

## Wichtige Dateien im Repository

| Datei | Beschreibung |
|-------|--------------|
| `pom.xml` | Maven Build-Konfiguration |
| `.github/workflows/build.yml` | CI/CD Pipeline |
| `src/coderslagoon/badpeggy/GUI.java` | Haupt-GUI-Klasse |
| `src/coderslagoon/badpeggy/NLS.java` | Sprachschlüssel-Definitionen |
| `src/coderslagoon/badpeggy/NLS_de.properties` | Deutsche Übersetzungen |
| `src/coderslagoon/badpeggy/NLS_en.properties` | Englische Übersetzungen |
| `src/coderslagoon/badpeggy/NLS_cz.properties` | Tschechische Übersetzungen |
| `src/coderslagoon/badpeggy/GUIProps.java` | Konfigurationsschlüssel |
| `src/coderslagoon/badpeggy/scanner/ImageScanner.java` | Bild-Scanner-Logik |

## Portable Version aktualisieren

Nach einem neuen Build:

1. Artefakt herunterladen:
   ```bash
   gh run download <run-id> -n badpeggy-windows-latest --repo HJS-cpu/BadPeggy
   ```

2. Alte JAR löschen und neue umbenennen:
   ```bash
   rm badpeggy.jar
   mv badpeggy-X.Y-SNAPSHOT.jar badpeggy.jar
   ```

3. Standalone-JAR kann gelöscht werden (wird nicht benötigt):
   ```bash
   rm badpeggy-X.Y-SNAPSHOT-standalone.jar
   ```

## Bekannte Einschränkungen

- Java 17 erforderlich (wegen baselib-swt Abhängigkeit)
- SWT ist plattformspezifisch - separate Builds für Windows/Linux/macOS nötig
- Tests schlagen fehl (keine echten Tests vorhanden, nur Platzhalter)

## Nächste Schritte / Ideen

- [ ] Weitere Sprachen hinzufügen
- [ ] Installer für Windows erstellen (z.B. mit Inno Setup)
- [ ] Linux/macOS portable Versionen erstellen
- [ ] Unit Tests implementieren
- [ ] Version ohne SNAPSHOT-Suffix für Release

## Commits-Historie (relevant)

```
319634c Add Open Folder feature and update to version 2.4
cd1af1a Fix: Exclude signature files from shaded JAR
b40fddb Performance optimizations
87dd293 Remove retired macOS-13 runner
5503f73 Fix: Update to Java 17
596b2d2 Fix: Use bash shell for Maven commands
```

---

*Letzte Aktualisierung: 2026-02-01*
