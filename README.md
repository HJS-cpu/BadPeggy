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

### New Features
- **Open Folder**: Right-click context menu option to open the file location
- **File Selection**: When opening folder, the file is now highlighted/selected in Explorer (Windows) or Finder (macOS)

### Improvements
- Updated to **Java 17**
- **Maven build system** for easier building
- **GitHub Actions CI/CD**: Automatic builds for Windows, Linux, and macOS (ARM64)
- Performance optimizations
- Fixed signature file exclusion in shaded JAR

## Download

Pre-built binaries are available under [Releases](https://github.com/HJS-cpu/BadPeggy/releases) or as build artifacts from [GitHub Actions](https://github.com/HJS-cpu/BadPeggy/actions).

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

For shipping clone the [jre-reduce](https://github.com/coderslagoon/jre-reduce)
repo from GitHub, in parallel to the other projects. Download the appropriate JRE
runtime files, as mentioned in the jre-reduce documentation. Then run *build.sh*
and *build_macos.sh* to create the installer, passing them a version string.

## I18N

New user-facing strings need to be internationalized, meaning being available
in both English and German. New strings have to be added in the NLS files in
*coderslagoon.badpeggy.NLS...*. Please test for both languages, and watch out
for proper format string rendering.
