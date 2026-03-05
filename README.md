<div align="center">

```
████████╗██╗   ██╗██╗  ██╗
   ██╔══╝██║   ██║╚██╗██╔╝
   ██║   ██║   ██║ ╚███╔╝ 
   ██║   ██║   ██║ ██╔██╗ 
   ██║   ╚██████╔╝██╔╝ ██╗
   ╚═╝    ╚═════╝ ╚═╝  ╚═╝
```

**Package Manager & APK/AAB Builder · v3.0.0**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/crystalshankbro/TUX/blob/main/LICENSE)
[![Shell: Bash](https://img.shields.io/badge/Shell-Bash-4EAA25?logo=gnubash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20Windows%20%7C%20macOS-blue)](#)
[![No SDK](https://img.shields.io/badge/Android%20SDK-Not%20Required-success)](#)

*Installs Java · Kotlin · Gradle · Python · Node.js · Builds APK & AAB without Android SDK*

</div>

---

<!-- ENGLISH -->

# 🇬🇧 English

## Table of Contents

- [What is Tux?](#what-is-tux)
- [Quick Install](#quick-install)
- [Interactive Menu](#interactive-menu)
- [Commands](#commands)
  - [tux install](#tux-install)
  - [tux build](#tux-build)
  - [tux list](#tux-list)
  - [tux logs](#tux-logs)
  - [tux update-tools](#tux-update-tools)
- [APK Build Pipeline](#apk-build-pipeline)
- [Tool Sizes](#tool-sizes)
- [Platform Support](#platform-support)

---

## What is Tux?

Tux is a single-file Bash package manager and APK/AAB builder. It installs popular development runtimes and builds Android APK/AAB files **without requiring Android Studio or Android SDK** — it downloads only what it needs, automatically.

```
No Android Studio. No Android SDK. No Gradle project setup.
Just: tux install kotlin → tux install apk Main.kt
```

---

## Quick Install

**Linux / macOS / WSL:**
```bash
curl -fsSL https://raw.githubusercontent.com/crystalshankbro/TUX/main/tux \
  -o /usr/local/bin/tux && chmod +x /usr/local/bin/tux
```

**Or manually:**
```bash
# Download
wget https://raw.githubusercontent.com/crystalshankbro/TUX/main/tux

# Make executable
chmod +x tux

# Move to PATH (Linux/macOS)
sudo mv tux /usr/local/bin/

# Or for current user only
mkdir -p ~/.local/bin && mv tux ~/.local/bin/
```

**Windows (Git Bash / MSYS2):**
```bash
curl -fsSL https://raw.githubusercontent.com/crystalshankbro/TUX/main/tux \
  -o ~/bin/tux && chmod +x ~/bin/tux
```

> **Requirements:** `bash 4+`, `curl` or `wget`, `unzip`, `zip`

---

## Interactive Menu

Run `tux` with no arguments to open the interactive terminal menu:

```
tux
```

```
  ████████╗██╗   ██╗██╗  ██╗
     ██╔══╝██║   ██║╚██╗██╔╝
     ██║   ██║   ██║ ╚███╔╝
     ██║   ██║   ██║ ██╔██╗
     ██║   ╚██████╔╝██╔╝ ██╗
     ╚═╝    ╚═════╝ ╚═╝  ╚═╝
  Package Manager v3.0  |  linux

  Main Menu  (↑↓ to navigate, Enter to select)

  ▶  📦  Install languages
     🔨  Build APK / AAB
     📋  tux list — installed packages
     📄  Build logs
     🔧  Update APK tools
     ❓  Help
     🚪  Exit
```

Navigate with **↑ ↓ arrow keys**, confirm with **Enter**.

---

## Commands

### `tux install`

Install programming languages and runtimes.

---

#### `tux install java`

Installs the latest **Java LTS** (Adoptium Temurin 21) from [adoptium.net](https://adoptium.net).

```bash
tux install java
```

| Detail | Value |
|--------|-------|
| Source | api.adoptium.net |
| Version | OpenJDK 21 LTS (latest) |
| Install path | `~/.tux/java/` |
| Sets | `JAVA_HOME`, adds to `PATH` |
| Download size | ~190 MB (Linux x64) |
| Disk after install | ~310 MB |

---

#### `tux install kotlin`

Installs the latest **Kotlin Compiler** from [JetBrains GitHub Releases](https://github.com/JetBrains/kotlin/releases/latest).

```bash
tux install kotlin
```

> Automatically installs Java first if not found.

| Detail | Value |
|--------|-------|
| Source | github.com/JetBrains/kotlin |
| Version | Latest stable |
| Install path | `~/.tux/kotlin/` |
| Adds | `kotlinc`, `kotlin` to PATH |
| Download size | ~65 MB |
| Disk after install | ~130 MB |

---

#### `tux install gradle`

Installs the latest stable **Gradle** from [services.gradle.org](https://gradle.org/releases/).

```bash
tux install gradle
```

| Detail | Value |
|--------|-------|
| Source | services.gradle.org |
| Version | Latest stable |
| Install path | `~/.tux/gradle/` |
| Adds | `gradle` to PATH |
| Download size | ~120 MB |
| Disk after install | ~155 MB |

---

#### `tux install python`

Installs **Python 3** (latest stable).

```bash
tux install python
```

Strategy by OS:
- **Linux** — uses system `apt` / `dnf` / `pacman`, or `pyenv` as fallback
- **Windows** — downloads embeddable Python from [python.org](https://www.python.org/downloads/)
- **macOS** — uses `brew install python3`

| Detail | Value |
|--------|-------|
| Source | python.org / system package manager |
| Version | Latest stable (3.12+) |
| Install path | `~/.tux/python/` |
| Disk after install | ~30–120 MB (varies by method) |

---

#### `tux install node`

Installs **Node.js LTS** from [nodejs.org](https://nodejs.org/en/download).

```bash
tux install node
```

| Detail | Value |
|--------|-------|
| Source | nodejs.org |
| Version | Latest LTS (v20.x) |
| Install path | `~/.tux/node/` |
| Adds | `node`, `npm`, `npx` to PATH |
| Download size | ~25 MB (Linux x64) |
| Disk after install | ~75 MB |

---

#### `tux install apk`

Builds an **Android APK** from `.kt` source files. No Android Studio or SDK needed.

```bash
# Single file
tux install apk Main.kt

# Multiple files (separated by +)
tux install apk Main.kt+Utils.kt+Network.kt

# Release build with signing
tux install apk Main.kt release
```

**Debug build** (default) — signed with auto-generated debug keystore.
**Release build** — prompts for your own keystore or creates a new one.

Output: `ProjectName-debug.apk` or `ProjectName-release.apk` in current directory.

---

### `tux build`

#### `tux build aab`

Builds an **Android App Bundle (.aab)** — the format required for Google Play uploads.

```bash
# Single file
tux build aab Main.kt

# Multiple files
tux build aab Main.kt+Utils.kt+Network.kt
```

Output: `ProjectName.aab` in current directory.

After building, test locally with [bundletool](https://developer.android.com/tools/bundletool):
```bash
bundletool build-apks --bundle=App.aab --output=app.apks
bundletool install-apks --apks=app.apks
```

---

### `tux list`

Shows a table of all installed packages and APK tools.

```bash
tux list
```

```
  Installed packages

  ──────────────────────────────────────
  Package      Version              Size       Path
  ──────────────────────────────────────
  ✓ Java       21.0.3+9             310 MB    ~/.tux/java
  ✓ Kotlin     1.9.23              130 MB    ~/.tux/kotlin
  ✓ Gradle     8.7                 155 MB    ~/.tux/gradle
  ✗ Python     not installed
  ✗ Node.js    not installed
  ──────────────────────────────────────

  APK Tools:
  ✓ R8/D8 DEX Compiler    (18 MB)
  ✓ Android API stubs     (12 MB)
  ✓ APK Signer            (1.2 MB)
  ✓ Debug Keystore        (2 KB)
```

---

### `tux logs`

Opens the build log viewer. Every APK/AAB build saves a full log to `~/.tux/logs/`.

```bash
tux logs
```

Shows a numbered list of recent logs. Enter the number to view a log file.

Log location: `~/.tux/logs/YYYYMMDD_HHMMSS_build_apk_debug.log`

---

### `tux update-tools`

Re-downloads all APK build tools (R8/D8, android.jar, apksig).

```bash
tux update-tools
```

Use this if a build fails or you want the latest tool versions.

---

### `tux version`

Alias for `tux list`. Shows installed versions and APK tool status.

```bash
tux version
```

---

### `tux help`

Prints the full command reference.

```bash
tux help
```

---

## APK Build Pipeline

Tux builds Android APKs in 5 steps, downloading everything needed automatically:

```
┌─────────────────────────────────────────────────────────────┐
│                   TUX APK BUILD PIPELINE                    │
├──────┬──────────────────────────────────────────────────────┤
│  1   │  .kt files  →  kotlinc  →  app.jar (JVM bytecode)   │
│  2   │  app.jar    →  R8/D8    →  classes.dex (Android)     │
│  3   │  Auto-generate AndroidManifest.xml                   │
│  4   │  ZIP pack: classes.dex + AndroidManifest.xml → .apk  │
│  5   │  Sign APK with apksig (debug or release key)         │
└──────┴──────────────────────────────────────────────────────┘
```

**Tools downloaded automatically (no Android SDK needed):**

| Tool | Source | Size | Purpose |
|------|--------|------|---------|
| `r8.jar` | Maven Google | ~18 MB | JAR → DEX compiler |
| `android.jar` | Sable/android-platforms (GitHub) | ~12 MB | Android API stubs |
| `apksig.jar` | Maven Google | ~1.2 MB | APK signing |
| `tux-debug.keystore` | Generated locally | ~2 KB | Debug signing key |

---

## Tool Sizes

Full reference of download and disk sizes for everything Tux installs:

| Component | Download | Disk Usage | Location |
|-----------|----------|------------|----------|
| Java 21 (Linux x64) | ~190 MB | ~310 MB | `~/.tux/java/` |
| Java 21 (Windows x64) | ~180 MB | ~295 MB | `~/.tux/java/` |
| Java 21 (macOS arm64) | ~185 MB | ~300 MB | `~/.tux/java/` |
| Kotlin (latest) | ~65 MB | ~130 MB | `~/.tux/kotlin/` |
| Gradle (latest) | ~120 MB | ~155 MB | `~/.tux/gradle/` |
| Python 3 (via apt) | ~5 MB | ~30 MB | system |
| Python 3 (Windows embed) | ~8 MB | ~18 MB | `~/.tux/python/` |
| Node.js LTS (Linux x64) | ~25 MB | ~75 MB | `~/.tux/node/` |
| Node.js LTS (Windows x64) | ~28 MB | ~80 MB | `~/.tux/node/` |
| r8.jar (R8/D8) | ~18 MB | ~18 MB | `~/.tux/tools/` |
| android.jar | ~12 MB | ~12 MB | `~/.tux/tools/` |
| apksig.jar | ~1.2 MB | ~1.2 MB | `~/.tux/tools/` |
| **Full install (all)** | **~625 MB** | **~1.0 GB** | `~/.tux/` |

> Sizes are approximate and may vary by version. APK tools are downloaded once and cached.

---

## Platform Support

| Feature | Linux | Windows (Git Bash / MSYS2 / WSL) | macOS |
|---------|-------|----------------------------------|-------|
| Install Java | ✅ | ✅ | ✅ |
| Install Kotlin | ✅ | ✅ | ✅ |
| Install Gradle | ✅ | ✅ | ✅ |
| Install Python | ✅ | ✅ | ✅ |
| Install Node.js | ✅ | ✅ | ✅ |
| Build APK | ✅ | ✅ | ✅ |
| Build AAB | ✅ | ✅ | ✅ |
| Interactive menu | ✅ | ✅ | ✅ |
| Build logs | ✅ | ✅ | ✅ |

---

<!-- RUSSIAN -->

---

<br>

# 🇷🇺 Русский

## Содержание

- [Что такое Tux?](#что-такое-tux)
- [Быстрая установка](#быстрая-установка)
- [Интерактивное меню](#интерактивное-меню)
- [Команды](#команды)
  - [tux install](#tux-install-1)
  - [tux build](#tux-build-1)
  - [tux list](#tux-list-1)
  - [tux logs](#tux-logs-1)
  - [tux update-tools](#tux-update-tools-1)
- [Пайплайн сборки APK](#пайплайн-сборки-apk)
- [Размеры компонентов](#размеры-компонентов)
- [Поддержка платформ](#поддержка-платформ)

---

## Что такое Tux?

Tux — это пакетный менеджер и сборщик APK/AAB в одном bash-файле. Устанавливает популярные языки программирования и собирает Android APK/AAB **без Android Studio и Android SDK** — скачивает только то, что нужно, автоматически.

```
Не нужен Android Studio. Не нужен Android SDK. Не нужен Gradle-проект.
Просто: tux install kotlin → tux install apk Main.kt
```

---

## Быстрая установка

**Linux / macOS / WSL:**
```bash
curl -fsSL https://raw.githubusercontent.com/crystalshankbro/TUX/main/tux \
  -o /usr/local/bin/tux && chmod +x /usr/local/bin/tux
```

**Или вручную:**
```bash
# Скачать
wget https://raw.githubusercontent.com/crystalshankbro/TUX/main/tux

# Сделать исполняемым
chmod +x tux

# Переместить в PATH (Linux/macOS)
sudo mv tux /usr/local/bin/

# Или только для текущего пользователя
mkdir -p ~/.local/bin && mv tux ~/.local/bin/
```

**Windows (Git Bash / MSYS2):**
```bash
curl -fsSL https://raw.githubusercontent.com/crystalshankbro/TUX/main/tux \
  -o ~/bin/tux && chmod +x ~/bin/tux
```

> **Требования:** `bash 4+`, `curl` или `wget`, `unzip`, `zip`

---

## Интерактивное меню

Запусти `tux` без аргументов — откроется интерактивное меню:

```bash
tux
```

Навигация **стрелками ↑ ↓**, выбор **Enter**.

---

## Команды

### `tux install`

Установка языков программирования и сред выполнения.

---

#### `tux install java`

Устанавливает последнюю **Java LTS** (Adoptium Temurin 21) с [adoptium.net](https://adoptium.net).

```bash
tux install java
```

| Параметр | Значение |
|----------|----------|
| Источник | api.adoptium.net |
| Версия | OpenJDK 21 LTS (последняя) |
| Путь установки | `~/.tux/java/` |
| Устанавливает | `JAVA_HOME`, добавляет в `PATH` |
| Размер скачивания | ~190 МБ (Linux x64) |
| Размер на диске | ~310 МБ |

---

#### `tux install kotlin`

Устанавливает последний **Kotlin Compiler** с [GitHub JetBrains](https://github.com/JetBrains/kotlin/releases/latest).

```bash
tux install kotlin
```

> Автоматически установит Java, если она не найдена.

| Параметр | Значение |
|----------|----------|
| Источник | github.com/JetBrains/kotlin |
| Версия | Последняя стабильная |
| Путь установки | `~/.tux/kotlin/` |
| Добавляет | `kotlinc`, `kotlin` в PATH |
| Размер скачивания | ~65 МБ |
| Размер на диске | ~130 МБ |

---

#### `tux install gradle`

Устанавливает последний стабильный **Gradle** с [services.gradle.org](https://gradle.org/releases/).

```bash
tux install gradle
```

| Параметр | Значение |
|----------|----------|
| Источник | services.gradle.org |
| Версия | Последняя стабильная |
| Путь установки | `~/.tux/gradle/` |
| Добавляет | `gradle` в PATH |
| Размер скачивания | ~120 МБ |
| Размер на диске | ~155 МБ |

---

#### `tux install python`

Устанавливает **Python 3** (последняя стабильная версия).

```bash
tux install python
```

Стратегия по ОС:
- **Linux** — использует `apt` / `dnf` / `pacman`, или `pyenv` как запасной вариант
- **Windows** — скачивает embeddable Python с [python.org](https://www.python.org/downloads/)
- **macOS** — использует `brew install python3`

| Параметр | Значение |
|----------|----------|
| Источник | python.org / системный менеджер пакетов |
| Версия | Последняя стабильная (3.12+) |
| Путь установки | `~/.tux/python/` |
| Размер на диске | ~30–120 МБ (зависит от метода) |

---

#### `tux install node`

Устанавливает **Node.js LTS** с [nodejs.org](https://nodejs.org/en/download).

```bash
tux install node
```

| Параметр | Значение |
|----------|----------|
| Источник | nodejs.org |
| Версия | Последняя LTS (v20.x) |
| Путь установки | `~/.tux/node/` |
| Добавляет | `node`, `npm`, `npx` в PATH |
| Размер скачивания | ~25 МБ (Linux x64) |
| Размер на диске | ~75 МБ |

---

#### `tux install apk`

Собирает **Android APK** из `.kt` файлов. Android Studio и SDK не нужны.

```bash
# Один файл
tux install apk Main.kt

# Несколько файлов (через +)
tux install apk Main.kt+Utils.kt+Network.kt

# Release сборка с подписью
tux install apk Main.kt release
```

**Debug сборка** (по умолчанию) — подписывается автоматически сгенерированным debug-ключом.  
**Release сборка** — запросит твой keystore или создаст новый.

Результат: `ProjectName-debug.apk` или `ProjectName-release.apk` в текущей директории.

---

### `tux build`

#### `tux build aab`

Собирает **Android App Bundle (.aab)** — формат для загрузки в Google Play.

```bash
# Один файл
tux build aab Main.kt

# Несколько файлов
tux build aab Main.kt+Utils.kt+Network.kt
```

Результат: `ProjectName.aab` в текущей директории.

Локальное тестирование через [bundletool](https://developer.android.com/tools/bundletool):
```bash
bundletool build-apks --bundle=App.aab --output=app.apks
bundletool install-apks --apks=app.apks
```

---

### `tux list`

Показывает таблицу всех установленных пакетов и инструментов APK.

```bash
tux list
```

---

### `tux logs`

Открывает просмотрщик логов сборки. Каждая сборка APK/AAB сохраняет полный лог в `~/.tux/logs/`.

```bash
tux logs
```

Показывает нумерованный список последних логов. Введи номер чтобы открыть лог.

Расположение логов: `~/.tux/logs/YYYYMMDD_HHMMSS_build_apk_debug.log`

---

### `tux update-tools`

Перескачивает все инструменты сборки APK (R8/D8, android.jar, apksig).

```bash
tux update-tools
```

Используй если сборка падает или хочешь обновить инструменты до последних версий.

---

### `tux version`

Псевдоним для `tux list`. Показывает установленные версии и статус инструментов APK.

```bash
tux version
```

---

### `tux help`

Выводит полный справочник команд.

```bash
tux help
```

---

## Пайплайн сборки APK

Tux собирает Android APK в 5 шагов, скачивая всё необходимое автоматически:

```
┌─────────────────────────────────────────────────────────────────┐
│                 ПАЙПЛАЙН СБОРКИ APK В TUX                       │
├──────┬──────────────────────────────────────────────────────────┤
│  1   │  .kt файлы  →  kotlinc  →  app.jar (JVM байткод)        │
│  2   │  app.jar    →  R8/D8    →  classes.dex (Android)         │
│  3   │  Автогенерация AndroidManifest.xml                       │
│  4   │  ZIP упаковка: classes.dex + манифест → .apk             │
│  5   │  Подпись через apksig (debug или release ключ)           │
└──────┴──────────────────────────────────────────────────────────┘
```

**Инструменты скачиваются автоматически (Android SDK не нужен):**

| Инструмент | Источник | Размер | Назначение |
|------------|----------|--------|------------|
| `r8.jar` | Maven Google | ~18 МБ | Компилятор JAR → DEX |
| `android.jar` | Sable/android-platforms (GitHub) | ~12 МБ | Заглушки Android API |
| `apksig.jar` | Maven Google | ~1.2 МБ | Подпись APK |
| `tux-debug.keystore` | Генерируется локально | ~2 КБ | Debug ключ подписи |

---

## Размеры компонентов

Полная справка по размерам скачивания и дискового пространства:

| Компонент | Скачивание | На диске | Расположение |
|-----------|------------|----------|--------------|
| Java 21 (Linux x64) | ~190 МБ | ~310 МБ | `~/.tux/java/` |
| Java 21 (Windows x64) | ~180 МБ | ~295 МБ | `~/.tux/java/` |
| Java 21 (macOS arm64) | ~185 МБ | ~300 МБ | `~/.tux/java/` |
| Kotlin (последняя) | ~65 МБ | ~130 МБ | `~/.tux/kotlin/` |
| Gradle (последняя) | ~120 МБ | ~155 МБ | `~/.tux/gradle/` |
| Python 3 (через apt) | ~5 МБ | ~30 МБ | системный |
| Python 3 (Windows embeddable) | ~8 МБ | ~18 МБ | `~/.tux/python/` |
| Node.js LTS (Linux x64) | ~25 МБ | ~75 МБ | `~/.tux/node/` |
| Node.js LTS (Windows x64) | ~28 МБ | ~80 МБ | `~/.tux/node/` |
| r8.jar (R8/D8) | ~18 МБ | ~18 МБ | `~/.tux/tools/` |
| android.jar | ~12 МБ | ~12 МБ | `~/.tux/tools/` |
| apksig.jar | ~1.2 МБ | ~1.2 МБ | `~/.tux/tools/` |
| **Полная установка (всё)** | **~625 МБ** | **~1.0 ГБ** | `~/.tux/` |

> Размеры приблизительны и могут меняться в зависимости от версии. Инструменты APK скачиваются один раз и кешируются.

---

## Поддержка платформ

| Функция | Linux | Windows (Git Bash / MSYS2 / WSL) | macOS |
|---------|-------|----------------------------------|-------|
| Установка Java | ✅ | ✅ | ✅ |
| Установка Kotlin | ✅ | ✅ | ✅ |
| Установка Gradle | ✅ | ✅ | ✅ |
| Установка Python | ✅ | ✅ | ✅ |
| Установка Node.js | ✅ | ✅ | ✅ |
| Сборка APK | ✅ | ✅ | ✅ |
| Сборка AAB | ✅ | ✅ | ✅ |
| Интерактивное меню | ✅ | ✅ | ✅ |
| Логи сборки | ✅ | ✅ | ✅ |

---

<div align="center">

Made with ❤️ by crystalshankbro · MIT License · © 2026 Crystal

</div>
