# Bad Peggy (Fork)

[![Build and Test](https://github.com/HJS-cpu/BadPeggy/actions/workflows/build.yml/badge.svg)](https://github.com/HJS-cpu/BadPeggy/actions/workflows/build.yml)
[![Website](https://img.shields.io/badge/Website-BadPeggy-blue)](http://hjs.bplaced.net/BadPeggy)

<img src="Bad Peggy.png" width="400" alt="Bad Peggy Screenshot">

> **This is a fork of Bad Peggy by coderslagoon with additional features and improvements.**

Bad Peggy scans JPEG and other image formats for damage and other blemishes and shows
the results and images instantly. It allows you to find such broken files quickly,
inspect and then either delete or move them to a different location.

Runs on Windows, macOS and Linux.

## Changes in this Fork

### Version 2.4.1
- **Toolbar**: Quick access buttons for Scan, Delete, Move, Open Folder, Clear
- **Improved About Dialog**: Larger logo, clickable website link, centered layout
- **Optimized Table Colors**: Lighter gray rows, green selection/hover effects
- **Custom JRE**: Reduced release size from ~45 MB to ~15-20 MB using jlink

### Previous Improvements
- **Open Folder with Selection**: File is highlighted in Explorer (Windows) or Finder (macOS)
- Updated to **Java 17**
- **Maven build system** for easier building
- **GitHub Actions CI/CD**: Automatic builds for Windows, Linux, and macOS (ARM64)
- **Three languages**: English, German, Czech

## Download

Pre-built binaries are available from [GitHub Actions](https://github.com/HJS-cpu/BadPeggy/actions) (click on the latest successful build, then download `BadPeggy-Windows-x64` from Artifacts).

The release package includes:
- `badpeggy.jar` - Standalone JAR with all dependencies
- `jre/` - Custom Java Runtime (~35 MB)
- `install.vbs` - Creates desktop shortcut (Windows)
- `BadPeggy.cmd` - Start script
- Documentation in EN/DE/CZ

---

## Development

### Building with Maven

```bash
# Build for your platform
mvn clean package -DskipTests

# Build for specific platform (e.g., Windows)
mvn clean package -DskipTests -Dswt.artifactId=org.eclipse.swt.win32.win32.x86_64
```

**Supported SWT artifacts:**
- Windows: `org.eclipse.swt.win32.win32.x86_64`
- Linux: `org.eclipse.swt.gtk.linux.x86_64`
- macOS (ARM): `org.eclipse.swt.cocoa.macosx.aarch64`

### Eclipse Development

BadPeggy development can also be done in Eclipse. Choose the right SWT project
for your platform, and import it into your workspace. You also need the library
[CLBaseLib](https://github.com/coderslagoon/CLBaseLib), which you can clone from GitHub.

You can then run Bad Peggy by debugging the class *coderslagoon.badpeggy.GUI*.

### Tests

The test cases can be executed, though they might fail due to slightly different
image rendering of the test material. This does usually not present a problem.
Frozen reference test material is not included, due to the huge size of it (3+GB).

## Shipping

Release packages are built automatically via GitHub Actions:
- **Windows**: Built on every push (default)
- **All platforms**: Manual trigger with `all_platforms` option

The workflow creates a complete release package with:
- Standalone JAR (maven-shade-plugin)
- Custom JRE via jlink (java.base, java.desktop, java.logging, java.prefs)
- All documentation and install scripts

## I18N

Bad Peggy supports three languages: **English**, **German**, and **Czech**.

New user-facing strings need to be added in all NLS files:
- `NLS_en.properties` (English)
- `NLS_de.properties` (German)
- `NLS_cz.properties` (Czech)

Please test all languages and watch out for proper format string rendering.
