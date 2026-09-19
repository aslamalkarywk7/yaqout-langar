# Yaqout Build Guide

## Complete Build Guide for the Yaqout Programming Language

---

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Build on Windows](#build-on-windows)
- [Build on Linux](#build-on-linux)
- [Build on macOS](#build-on-macos)
- [Advanced build options](#advanced-build-options)
- [Source file structure](#source-file-structure)
- [Testing the build](#testing-the-build)
- [Troubleshooting](#troubleshooting)
- [Building the static library](#building-the-static-library)
- [Release packaging](#release-packaging)

---

## Introduction

Yaqout is built on the Lua 5.5 engine written in C. The build is simple and needs no complex external libraries. You can build it with a single command.

### Why is the build easy?

- No external dependencies
- Clean standard C99 code
- Works with any modern C compiler
- Small source (~1MB)

---

## Prerequisites

### Supported compilers

| Compiler | Minimum version | Notes |
|----------|-----------------|-------|
| **GCC** | 4.8+ | Recommended for Linux |
| **MinGW-w64** | 8.0+ | Recommended for Windows |
| **Clang** | 3.5+ | Good alternative |
| **MSVC** | 2015+ | Visual Studio |
| **TCC** | 0.9.27+ | Fast builds |

### Extra tools (optional)

| Tool | Purpose |
|------|---------|
| **Make** | Build automation |
| **Git** | Version management |
| **CMake** | Multi-platform builds |

---

## Build on Windows

### Method 1: MinGW-w64 (recommended)

#### Step 1: Install MinGW-w64

```powershell
# Via winget
winget install -e --id mingw-w64.mingw-w64

# Via Chocolatey
choco install mingw

# Or manual download:
# https://www.mingw-w64.org/downloads/
# Choose: x86_64-posix-seh
```

#### Step 2: Add MinGW to PATH

```powershell
# Add this path to System PATH:
# C:\mingw-w64\x86_64-8.1.0-posix-seh-rt_v6-rev0\mingw64\bin

# Verify:
gcc --version
```

#### Step 3: Build Yaqout

```powershell
# Go to the project folder
cd C:\path\to\yaqout

# Full build (single line)
gcc -O2 -std=c99 -DLUA_USE_WINDOWS -o yaqout.exe lua.c lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c liolib.c lmathlib.c loslib.c lstrlib.c ltablib.c lutf8lib.c loadlib.c linit.c -lm
```

Formatted version for readability:

```powershell
gcc -O2 -std=c99 -DLUA_USE_WINDOWS -o yaqout.exe ^
    lua.c ^
    lapi.c ^
    lcode.c ^
    lctype.c ^
    ldebug.c ^
    ldo.c ^
    ldump.c ^
    lfunc.c ^
    lgc.c ^
    llex.c ^
    lmem.c ^
    lobject.c ^
    lopcodes.c ^
    lparser.c ^
    lstate.c ^
    lstring.c ^
    ltable.c ^
    ltm.c ^
    lundump.c ^
    lvm.c ^
    lzio.c ^
    lauxlib.c ^
    lbaselib.c ^
    lcorolib.c ^
    ldblib.c ^
    liolib.c ^
    lmathlib.c ^
    loslib.c ^
    lstrlib.c ^
    ltablib.c ^
    lutf8lib.c ^
    loadlib.c ^
    linit.c ^
    -lm
```

### Method 2: Visual Studio (MSVC)

#### Step 1: Open Developer Command Prompt

```batch
:: Search for "Developer Command Prompt for VS"
:: Or run:
"C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\Tools\VsDevCmd.bat"
```

#### Step 2: Build

```batch
cd C:\path\to\yaqout

cl /O2 /DLUA_USE_WINDOWS /Fe:yaqout.exe ^
    lua.c lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c ^
    lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c ^
    lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c ^
    lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c ^
    liolib.c lmathlib.c loslib.c lstrlib.c ltablib.c ^
    lutf8lib.c loadlib.c linit.c
```

### Method 3: Automatic build script

Create `build.bat`:

```batch
@echo off
echo ====================================
echo    Yaqout Build
echo ====================================

:: Check for gcc
where gcc >nul 2>nul
if %ERRORLEVEL% neq 0 (
    echo [ERROR] GCC not found! Install MinGW-w64
    pause
    exit /b 1
)

echo [1/3] Cleaning old files...
if exist yaqout.exe del yaqout.exe
if exist *.o del *.o

echo [2/3] Compiling sources...
gcc -O2 -std=c99 -DLUA_USE_WINDOWS -o yaqout.exe ^
    lua.c lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c ^
    lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c ^
    lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c ^
    lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c ^
    liolib.c lmathlib.c loslib.c lstrlib.c ltablib.c ^
    lutf8lib.c loadlib.c linit.c -lm

if %ERRORLEVEL% neq 0 (
    echo [ERROR] Build failed!
    pause
    exit /b 1
)

echo [3/3] Verifying output...
if exist yaqout.exe (
    echo.
    echo ====================================
    echo    Build succeeded!
    echo ====================================
    echo.
    yaqout.exe -v
) else (
    echo [ERROR] Binary not found!
)

pause
```

---

## Build on Linux

### Method 1: GCC

Install requirements:

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install build-essential

# Fedora
sudo dnf groupinstall "Development Tools"

# Arch Linux
sudo pacman -S base-devel

# openSUSE
sudo zypper install -t pattern devel_basis
```

Build:

```bash
cd ~/yaqout

# Simple build
gcc -O2 -std=c99 -DLUA_USE_LINUX -o yaqout \
    lua.c lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c \
    lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c \
    lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c \
    lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c \
    liolib.c lmathlib.c loslib.c lstrlib.c ltablib.c \
    lutf8lib.c loadlib.c linit.c -lm -ldl

# Or with make
make
```

### Method 2: Make

The `makefile` is included:

```bash
# Full build
make

# Clean
make clean

# Debug build
make MYCFLAGS="-g -DLUAI_ASSERT"
```

### Method 3: Build script

Create `build.sh`:

```bash
#!/bin/bash

echo "===================================="
echo "   Yaqout Build"
echo "===================================="

# Check for gcc
if ! command -v gcc &> /dev/null; then
    echo "[ERROR] GCC not found!"
    echo "Install it: sudo apt install build-essential"
    exit 1
fi

# Detect platform
UNAME=$(uname -s)
case "$UNAME" in
    Linux*)  PLATFORM="-DLUA_USE_LINUX"; LIBS="-lm -ldl";;
    Darwin*) PLATFORM="-DLUA_USE_MACOSX"; LIBS="-lm";;
    *)       PLATFORM=""; LIBS="-lm";;
esac

echo "[1/3] Cleaning old files..."
rm -f yaqout *.o

echo "[2/3] Compiling sources..."
gcc -O2 -std=c99 $PLATFORM -o yaqout \
    lua.c lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c \
    lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c \
    lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c \
    lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c \
    liolib.c lmathlib.c loslib.c lstrlib.c ltablib.c \
    lutf8lib.c loadlib.c linit.c $LIBS

if [ $? -ne 0 ]; then
    echo "[ERROR] Build failed!"
    exit 1
fi

echo "[3/3] Verifying output..."
if [ -f yaqout ]; then
    echo ""
    echo "===================================="
    echo "   Build succeeded!"
    echo "===================================="
    echo ""
    chmod +x yaqout
    ./yaqout -v
else
    echo "[ERROR] Binary not found!"
    exit 1
fi
```

```bash
chmod +x build.sh
./build.sh
```

---

## Build on macOS

Install requirements:

```bash
# Xcode Command Line Tools
xcode-select --install

# Or GCC via Homebrew
brew install gcc
```

Build:

```bash
cd ~/yaqout

# With Clang (default)
clang -O2 -std=c99 -DLUA_USE_MACOSX -o yaqout \
    lua.c lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c \
    lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c \
    lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c \
    lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c \
    liolib.c lmathlib.c loslib.c lstrlib.c ltablib.c \
    lutf8lib.c loadlib.c linit.c -lm

# Or with make
make macosx
```

---

## Advanced build options

### Optimization flags

| Flag | Description | Use |
|------|-------------|-----|
| `-O0` | No optimization | Debugging |
| `-O1` | Light optimization | Balance |
| `-O2` | Standard optimization | **Recommended** |
| `-O3` | Max optimization | High performance |
| `-Os` | Size optimization | Small binary |

### Debug flags

```bash
# Debug build
gcc -g -O0 -DLUAI_ASSERT -std=c99 -o yaqout_debug ...

# Full debug info
gcc -g3 -ggdb -O0 -DLUAI_ASSERT -DLUA_USE_APICHECK -std=c99 -o yaqout_debug ...
```

### Platform defines

| Define | Platform |
|--------|----------|
| `-DLUA_USE_WINDOWS` | Windows |
| `-DLUA_USE_LINUX` | Linux |
| `-DLUA_USE_MACOSX` | macOS |
| `-DLUA_USE_POSIX` | Generic POSIX |
| `-DLUA_USE_C89` | C89 compatibility |

### Special defines

```bash
# All internal checks
-DLUAI_ASSERT

# API check
-DLUA_USE_APICHECK

# Hard memory tests
-DHARDMEMTESTS

# Hard stack tests
-DHARDSTACKTESTS

# Lua 5.3 compatibility
-DLUA_COMPAT_5_3
```

### 32-bit vs 64-bit

```bash
# 32-bit
gcc -m32 -O2 -std=c99 -o yaqout32 ...

# 64-bit (default on 64-bit systems)
gcc -m64 -O2 -std=c99 -o yaqout64 ...
```

---

## Source file structure

### Core files

```
Core
├── lua.c          # Main entry point
├── lua.h          # Public header
├── luaconf.h      # Build config
├── lualib.h       # Library definitions
├── lauxlib.c      # Auxiliary library
└── lauxlib.h
```

### Language files (lexer and parser)

```
Lexer and parser
├── llex.c         # Lexer (Arabic keywords)
├── llex.h
├── lctype.c       # Character types (Arabic support)
├── lctype.h
├── lparser.c      # Parser
├── lparser.h
├── lcode.c        # Bytecode generation
└── lcode.h
```

### Virtual machine

```
VM
├── lvm.c          # Instruction execution
├── lvm.h
├── lopcodes.c     # Opcode definitions
├── lopcodes.h
├── lopnames.h     # Opcode names
└── ljumptab.h     # Jump table
```

### Memory management

```
Memory
├── lmem.c         # Memory management
├── lmem.h
├── lgc.c          # Garbage collector
├── lgc.h
├── lstate.c       # Interpreter state
└── lstate.h
```

### Standard libraries (localized)

```
Libraries (localized)
├── lbaselib.c     # Base functions (print, type...)
├── lmathlib.c     # Math library
├── lstrlib.c      # String library
├── ltablib.c      # Table library
├── liolib.c       # IO
├── loslib.c       # OS library
├── lcorolib.c     # Coroutines
├── ldblib.c       # Debug library
├── lutf8lib.c     # UTF-8 library
├── loadlib.c      # Library loading
└── linit.c        # Library init
```

### Other files

```
Other
├── lobject.c / lobject.h
├── lstring.c / lstring.h
├── ltable.c / ltable.h
├── lfunc.c / lfunc.h
├── ltm.c / ltm.h
├── ldebug.c / ldebug.h
├── ldo.c / ldo.h
├── ldump.c / lundump.c / lundump.h
├── lzio.c / lzio.h
├── llimits.h
├── lprefix.h
└── ltests.c       # Internal tests
```

---

## Testing the build

### Quick test

```bash
# Check version
./yaqout -v
# Windows:
yaqout.exe -v

# Expected output:
# Yaqout 5.5 (based on Lua 5.5)
```

### Interactive test

```bash
./yaqout
# Then type:
اطبع("Hello world!")
# Ctrl+D to exit (Linux/Mac) or Ctrl+Z (Windows)
```

### File test

```bash
# Create a test file
echo 'اطبع("Build works!")' > test.yq

# Run it
./yaqout test.yq
```

### Full tests

```bash
# All tests
./yaqout testes/all.lua

# Single suites
./yaqout testes/strings.lua
./yaqout testes/math.lua
./yaqout testes/api.lua
```

### Arabic keyword test

Create `test_arabic.yq`:

```lua
-- Arabic keyword test
محلي س = 10
محلي ص = 20

دالة جمع(أ, ب)
    ارجع أ + ب
نهاية

إذا س < ص إذن
    اطبع("س is smaller than ص")
نهاية

لكل ي = 1, 5 افعل
    اطبع("Number: " .. ي)
نهاية

اطبع("Sum: " .. جمع(س, ص))
اطبع("Test passed!")
```

```bash
./yaqout test_arabic.yq
```

---

## Troubleshooting

### Error: `gcc: command not found`

```bash
# Windows: add MinGW\bin to PATH
# Linux:
sudo apt install build-essential
# macOS:
xcode-select --install
```

### Error: `undefined reference to 'dlopen'`

```bash
# Add -ldl
gcc ... -lm -ldl
```

### Error: `cannot find -lm`

```bash
# Linux
sudo apt install libc6-dev
ls /usr/lib/x86_64-linux-gnu/libm.*
```

### Error: `llex.c: invalid multibyte character`

```bash
# Check UTF-8 encoding
file llex.c
# Expected: UTF-8 Unicode text

# Fix wrong encoding:
iconv -f ISO-8859-1 -t UTF-8 llex.c > llex_utf8.c
mv llex_utf8.c llex.c
```

### Error: `Windows.h not found` (MSVC)

```batch
:: Use Developer Command Prompt, not plain PowerShell/CMD
```

### Warning: `-Wconversion`

```bash
# Normal warnings in Lua code, safe to ignore or:
gcc -Wno-conversion ...
```

### Arabic letters do not display

```bash
# Windows CMD
chcp 65001

# Windows PowerShell
[Console]::OutputEncoding = [Text.UTF8Encoding]::UTF8

# Linux/Mac
export LANG=en_US.UTF-8
```

---

## Building the static library

### Build libyaqout.a

```bash
# Step 1: object files
gcc -c -O2 -std=c99 -DLUA_USE_LINUX \
    lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c \
    lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c \
    lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c \
    lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c \
    liolib.c lmathlib.c loslib.c lstrlib.c ltablib.c \
    lutf8lib.c loadlib.c linit.c

# Step 2: static library
ar rcs libyaqout.a *.o

# Step 3: link test
gcc -o yaqout lua.c -L. -lyaqout -lm -ldl
```

### Shared library

```bash
# Linux
gcc -shared -fPIC -O2 -std=c99 -DLUA_USE_LINUX \
    -o libyaqout.so \
    lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c \
    lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c \
    lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c \
    lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c \
    liolib.c lmathlib.c loslib.c lstrlib.c ltablib.c \
    lutf8lib.c loadlib.c linit.c -lm -ldl

# Windows (DLL)
gcc -shared -O2 -std=c99 -DLUA_USE_WINDOWS -DLUA_BUILD_AS_DLL \
    -o yaqout.dll \
    lapi.c lcode.c ... -lm
```

---

## Release packaging

### Package layout

```
yaqout-1.0-win64/
├── yaqout.exe           # Binary
├── library.yq           # Extra libraries
├── README.md            # Docs
├── LICENSE              # License
├── examples/            # Examples
│   ├── hello.yq
│   ├── calculator.yq
│   └── game.yq
└── vscode-yaqout/       # VS Code extension
```

### Packaging script

```bash
#!/bin/bash
VERSION="1.0"
PLATFORM="linux64"

mkdir -p "yaqout-${VERSION}-${PLATFORM}"
cd "yaqout-${VERSION}-${PLATFORM}"

cp ../yaqout .
cp ../library.yq .
cp ../README.md .
cp ../LICENSE .
cp -r ../examples .
cp -r ../vscode-yaqout .

cd ..
tar -czvf "yaqout-${VERSION}-${PLATFORM}.tar.gz" "yaqout-${VERSION}-${PLATFORM}"

echo "Package created: yaqout-${VERSION}-${PLATFORM}.tar.gz"
```

---

## Build command summary

| System | Command |
|--------|---------|
| **Windows (MinGW)** | `gcc -O2 -std=c99 -DLUA_USE_WINDOWS -o yaqout.exe *.c -lm` |
| **Linux** | `gcc -O2 -std=c99 -DLUA_USE_LINUX -o yaqout *.c -lm -ldl` |
| **macOS** | `clang -O2 -std=c99 -DLUA_USE_MACOSX -o yaqout *.c -lm` |
| **Make** | `make` |

---

## Summary

Building Yaqout needs:

1. A C compiler (GCC/Clang/MSVC)
2. One build command
3. No external dependencies

**Help or bug reports:**

- Open a GitHub Issue
- See CONTRIBUTING.md

---

**Prepared by:**
**Islam Al-Nashar - Al-Nashar Studio**
**Version: 1.0 | February 2026**
