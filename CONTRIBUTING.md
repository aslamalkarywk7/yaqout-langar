# Contributing to Yaqout

## How to contribute to the first professional Arabic programming language

---

## Table of Contents

- [Introduction](#introduction)
- [Why contribute to Yaqout](#why-contribute-to-yaqout)
- [Technical structure](#technical-structure)
- [Development setup](#development-setup)
- [GitHub contribution steps](#github-contribution-steps)
- [Needed contribution types](#needed-contribution-types)
- [Code style](#code-style)
- [FAQ](#faq)
- [Common errors](#common-errors)
- [Known issues](#known-issues)
- [Contact and support](#contact-and-support)

---

## Introduction

**Yaqout** is not just a translation of Lua — it is an ambitious project to build a complete Arabic programming environment. Every Arab developer has something to offer, whether it is:

- Improving translation and localization
- Adding new libraries
- Writing docs and examples
- Testing the language and reporting bugs
- Improving performance and fixing vulnerabilities

---

## Why contribute to Yaqout?

### What you gain:

1. **Compiler experience**: you learn how programming languages work internally
2. **Open-source credit**: you can add this experience to your CV
3. **Arab community support**: you help break the language barrier for beginners
4. **C practice**: the project is fully built in C
5. **Real codebase work**: you work with the world-famous Lua code

### Project stats:

- **Core language**: C99
- **Source files**: 50+ files
- **Code size**: 400+ KB
- **Localized libraries**: 7 standard libraries

---

## Technical structure

### Main file layout:

```
yarout/
├── Core files
│   ├── lua.c          # Main entry point
│   ├── lua.h          # Main header
│   ├── luaconf.h      # Config
│   └── lualib.h       # Library definitions
│
├── Lexer
│   ├── llex.c         # Arabic keywords
│   ├── llex.h
│   └── lctype.c       # Arabic character support
│
├── Parser
│   ├── lparser.c      # Syntax analysis
│   ├── lparser.h
│   ├── lcode.c        # Intermediate code generation
│   └── lcode.h
│
├── VM
│   ├── lvm.c          # Instruction execution
│   ├── lvm.h
│   ├── lopcodes.c     # VM opcodes
│   └── lopcodes.h
│
├── Localized libraries
│   ├── lbaselib.c     # Base functions
│   ├── lmathlib.c     # Math library
│   ├── lstrlib.c      # String library
│   ├── ltablib.c      # Table library
│   ├── liolib.c       # IO library
│   ├── loslib.c       # OS library
│   └── lcorolib.c     # Coroutine library
│
├── Memory management
│   ├── lmem.c         # Memory management
│   ├── lgc.c          # Garbage collector
│   └── lstate.c       # Interpreter state
│
├── Docs
│   ├── README.md
│   ├── CONTRIBUTING.md
│   ├── YAQOUT_BOOK.md
│   └── build.md
│
└── Tests
    └── testes/        # Test files
```

### How does Arabic translation work?

#### 1. Keywords (in `llex.c`):

```c
static const char *const luaX_tokens [] = {
    "و", "اكسر", "افعل", "وإلا", "وإلا_إذا",
    "نهاية", "خطأ", "لكل", "دالة", "عام", "اذهب_إلى", "إذا",
    "في", "محلي", "لاشيء", "ليس", "أو", "كرر",
    "رجع", "إذن", "صح", "حتى", "طالما",
    // ... operators
};
```

#### 2. Arabic character support (in `lctype.c`):

Arabic letters are recognized as valid identifiers.

#### 3. Localized functions (in `lbaselib.c`):

```c
static const luaL_Reg base_funcs[] = {
    {"اطبع", luaB_print},
    {"نوع", luaB_type},
    {"تحويل_لرقم", luaB_tonumber},
    {"تحويل_لنص", luaB_tostring},
    // ...
};
```

---

## Development setup

### Requirements:

| Tool | Description | Download |
|------|-------------|----------|
| **GCC/MinGW** | C compiler | [mingw-w64.org](https://www.mingw-w64.org/) |
| **Git** | Version control | [git-scm.com](https://git-scm.com/) |
| **VS Code** | Code editor (optional) | [code.visualstudio.com](https://code.visualstudio.com/) |

### Setup on Windows:

```bash
# 1. Install MinGW-w64 and add it to PATH

# 2. Verify installation
gcc --version

# 3. Clone the project
git clone https://github.com/aslamalkarywk7/yaqout-langar.git
cd yaqout-langar

# 4. Build the project
gcc -O2 -std=c99 -DLUA_USE_WINDOWS -o yaqout.exe ^
    lua.c lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c ^
    lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c ^
    lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c ^
    lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c ^
    liolib.c lmathlib.c loslib.c lstrlib.c ltablib.c ^
    lutf8lib.c loadlib.c linit.c -lm

# 5. Test the build
.\yaqout.exe -v
```

### Setup on Linux/Mac:

```bash
# 1. Install requirements
sudo apt install build-essential  # Ubuntu/Debian
# or
brew install gcc  # macOS

# 2. Clone the project
git clone https://github.com/aslamalkarywk7/yaqout-langar.git
cd yaqout-langar

# 3. Build with make
make

# 4. Test
./yaqout -v
```

---

## GitHub contribution steps

### The right way to contribute:

#### Step 1: Fork the project

1. Go to the GitHub project page
2. Click **Fork** at the top right
3. Choose your personal account

#### Step 2: Clone the project

```bash
git clone https://github.com/[your-account]/yaqout-langar.git
cd yaqout-langar
```

#### Step 3: Create a new branch

```bash
# Naming: type/short-description (English, kebab-case)
git checkout -b feature/add-new-function
# or
git checkout -b fix/printing-bug
# or
git checkout -b docs/improve-docs
```

#### Step 4: Make changes

```bash
# Edit the needed files
# ...

# Stage changes
git add .

# Commit with a clear message
git commit -m "feat: add area calculation helper"
```

#### Step 5: Push changes

```bash
git push origin feature/add-new-function
```

#### Step 6: Create a Pull Request

1. Go to your project page on GitHub
2. Click **Compare & pull request**
3. Write a detailed description
4. Click **Create pull request**

### Ideal Pull Request template:

```markdown
## Description
[Explain what you changed and why]

## Change type
- [ ] New feature
- [ ] Bug fix
- [ ] Performance improvement
- [ ] Documentation improvement

## Changed files
- `lbaselib.c` - new function
- `README.md` - document the function

## How to test
1. Build the project
2. Run: `yaqout.exe test.yq`
3. Expected result: ...
```

---

## Needed contribution types

### 1. Library localization (priority: high)

Libraries needing localization:

- `lcorolib.c` - coroutine library
- `ldblib.c` - debug library

Localization example:

```c
// Before
{"create", luaB_cocreate},

// After
{"إنشاء", luaB_cocreate},
{"create", luaB_cocreate}, // for compatibility
```

### 2. Documentation (priority: high)

- Document localized functions
- Write tutorials and examples
- Translate error messages

### 3. Tests (priority: medium)

- Test Arabic keywords
- Test localized libraries
- Test `.yq` files

### 4. Bug fixes (priority: high)

- Check GitHub Issues
- Fix reported bugs

### 5. Performance (priority: low)

- Improve interpreter speed
- Reduce memory usage

### 6. VS Code extension (priority: medium)

- Improve syntax highlighting
- Add autocomplete

---

## Code style

### C style:

```c
// Correct
static int luaB_myfunction(lua_State *L) {
    // code here
    return 1;
}

// Wrong
static int luaB_myfunction(lua_State *L){
// code here
return 1;
}
```

### Naming rules:

| Type | Rule | Example |
|------|------|---------|
| C functions | snake_case | `luaB_print` |
| Yaqout functions | Arabic with underscores | `حساب_المساحة` |
| Constants | UPPER_CASE | `LUA_VERSION` |
| Variables | camelCase | `lineNumber` |

### Comments:

```c
/*
** Function description: prints a value to the screen
** Params: L - state pointer
** Returns: number of returned values
*/
static int luaB_print(lua_State *L) {
    // ...
}
```

---

## FAQ

### Q1: Do I need to know Lua to contribute?

Not necessarily. You can contribute docs and translations without deep Lua knowledge. For source changes, basic Lua and C help.

### Q2: How do I add a new keyword?

1. Open `llex.h` and add the token definition
2. Open `llex.c` and add the word to `luaX_tokens`
3. Open `lparser.c` and handle the keyword

### Q3: How do I add a new library function?

```c
// 1. Write the function
static int my_function(lua_State *L) {
    // code
    return 1;
}

// 2. Add it to the array
static const luaL_Reg my_funcs[] = {
    {"function_name", my_function},
    {NULL, NULL}
};
```

### Q4: Arabic letters do not work in variable names?

Make sure:

- File is saved as UTF-8
- You use the latest Yaqout build
- No BOM at the start of the file

### Q5: How do I test my changes?

```bash
# Build
gcc -O2 -std=c99 -o yaqout.exe [files]

# Simple test
echo 'اطبع("مرحبا")' > test.yq
.\yaqout.exe test.yq

# Full tests
.\yaqout.exe testes/all.lua
```

### Q6: What is the difference between `.yq` and `.ياقوت`?

Both are supported. `.yq` is short, `.ياقوت` is explicit. Prefer `.yq` for system compatibility.

---

## Common errors

### Error 1: `gcc: command not found`

**Cause:** GCC not installed or not in PATH
**Fix:**

```bash
# Windows: add MinGW\bin to System PATH
# Linux:
sudo apt install build-essential
```

### Error 2: `undefined reference to 'luaB_print'`

**Cause:** forgot a file in the build command
**Fix:** include all `.c` files

### Error 3: unfinished string

**Cause:** unclosed quote
**Fix:** close every `"` properly

### Error 4: invalid long string delimiter

**Cause:** wrong use of `[[` and `]]`
**Fix:** use `[[long text]]` correctly

### Error 5: Arabic letters look broken

**Cause:** wrong file encoding
**Fix:**

- Save as UTF-8
- CMD: `chcp 65001`
- PowerShell: `[Console]::OutputEncoding = [Text.UTF8Encoding]::UTF8`

### Error 6: `attempt to call a nil value`

**Cause:** function undefined or misspelled
**Fix:** check the function name and required library

---

## Known issues

### Issue 1: Encoding overlap

**Description:** some Unicode chars may confuse the lexer
**Status:** Known - needs fix
**Workaround:** avoid unused special chars

### Issue 2: Identifier length limit

**Description:** very long Arabic identifiers may exceed the limit
**Status:** Low priority
**Workaround:** use shorter names

### Issue 3: External C library compatibility

**Description:** some libraries do not support Arabic function names
**Status:** Under review
**Workaround:** use English names for external interfaces

---

## Yaqout advantages vs alternatives

| Feature | Yaqout | Arabic Python | Arabic JavaScript |
|---------|--------|---------------|-------------------|
| Arabic keywords | Yes | No | No |
| Arabic variable names | Yes | Yes | Yes |
| Localized libraries | Yes | No | No |
| Lightweight | Yes | No | No |
| Easy to learn | Yes | Yes | Partial |
| Game embedding | Yes | No | Partial |

---

## Contact and support

### Channels:

- **GitHub Issues**: bug reports and proposals
- **GitHub Discussions**: general discussion

### Lead developer:

- **Islam Al-Nashar**
- **Organization**: Al-Nashar Studio

---

## License

This project is licensed under **MIT**, which means:

- You can use it for free
- You can modify it
- You can distribute it
- You can use it commercially
- Keep the copyright notice

---

## Special thanks

Thanks to everyone contributing to Yaqout. Every line of code, doc, and suggestion builds the future of Arabic programming.

**Let's build the future of programming in our language together!**

---

*Last updated: February 2026*
*Version: 1.0*
