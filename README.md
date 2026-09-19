# Yaqout Language

### A Full Arabic Programming Language Based on Lua 5.5

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-blue)]()
[![Language](https://img.shields.io/badge/Language-Arabic%20%2B%20English-green)]()

---

## Table of Contents

- [Overview](#overview)
- [Why Yaqout](#why-yaqout)
- [Key Features](#key-features)
- [Limitations](#limitations)
- [Installation and Quick Start](#installation-and-quick-start)
- [Code Examples](#code-examples)
- [Standard Libraries](#standard-libraries)
- [Keyword Table](#keyword-table)
- [Comparison with Other Languages](#comparison-with-other-languages)
- [FAQ](#faq)
- [Contributing](#contributing)
- [Developer](#developer)
- [License](#license)

---

## Overview

**Yaqout** is a powerful and fast scripting language built as a complete Arabic version of the well-known Lua language. It enables Arab developers to write code in their native language while keeping the high performance and flexibility of Lua.

Code examples below keep the original Arabic keywords because that is the point of the language — all explanations are in English.

### Why Yaqout?

- **Educational**: ideal for teaching programming to Arabic-speaking beginners
- **Practical**: usable for game and application development
- **Fast**: keeps the famous Lua performance
- **Open source**: free to use and modify under MIT

---

## Key Features

### 1. Fully Arabic keywords

Readable Arabic control flow:

```lua
if age >= 18 then
-- in Yaqout:
إذا العمر >= 18 إذن
    اطبع("أنت بالغ")
وإلا
    اطبع("أنت قاصر")
نهاية
```

### 2. Unicode identifiers

Variables and functions can use native Arabic names:

```lua
محلي اسم_المستخدم = "أحمد"
محلي عمر_المستخدم = 25

دالة حساب_العمر_بالأيام(سنوات)
    ارجع سنوات * 365
نهاية
```

### 3. Localized standard libraries

Math, string, table, and OS functions with Arabic names:

```lua
محلي الجذر = رياضيات.جذر(16)  -- 4
محلي النص = نصوص.عكس("مرحبا")
جدول.إدراج(قائمتي, "عنصر جديد")
```

### 4. Custom file extensions

Supports `.yaqout` and `.yq` files:

```bash
yaqout.exe my_program.yq
yaqout.exe app.ياقوت
```

### 5. Lightweight and fast

Same fast Lua engine:

- Binary size: ~200KB
- Memory usage: very low
- Execution speed: close to C

### 6. VS Code support

Syntax highlighting extension with a custom icon for `.yq` files:

- Arabic keyword highlighting
- Autocomplete support
- Custom file icon

### 7. Advanced libraries

`yaqout.files` and `yaqout.web` helpers:

```lua
استدعي("library.yq")
ياقوت.ملفات.كتابة("notes.txt", "hello")
ياقوت.ويب.جلب("https://example.com")
```

### 8. Lua compatible

English and Arabic can be mixed — any Lua code runs as-is:

```lua
local x = 10
محلي ص = 20
if x > ص then
    اطبع("x is bigger")
end
```

---

## Limitations

### 1. C extension compatibility

- C libraries may not support Arabic function names
- Use English names for external interfaces

### 2. Editors

- Old editors may not support right-to-left text
- Some fonts have issues with Arabic

### 3. Encoding

- Save files as UTF-8
- Some terminals need special setup for Arabic display (Windows: `chcp 65001`)

### 4. Documentation and community

- Docs are still evolving
- The Arabic community is smaller than the English Lua community, so searching for solutions in Arabic is harder

---

## Installation and Quick Start

### Quick install (Windows)

```bash
# 1. Download yaqout.exe from the Releases page
# 2. Put it in a folder and add it to PATH
# 3. Test it:
yaqout.exe -v
```

### Build from source

Requirements: GCC or MinGW, C99.

```bash
gcc -O2 -std=c99 -DLUA_USE_WINDOWS -o yaqout.exe ^
    lua.c lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c ^
    lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c ^
    lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c ^
    lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c ^
    liolib.c lmathlib.c loslib.c lstrlib.c ltablib.c ^
    lutf8lib.c loadlib.c linit.c -lm
```

Linux:

```bash
gcc -O2 -std=c99 -DLUA_USE_LINUX -o yaqout \
    lua.c lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c \
    lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c \
    lparser.c lstate.c lstring.c ltable.c ltm.c lundump.c \
    lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c \
    liolib.c lmathlib.c loslib.c lstrlib.c ltablib.c \
    lutf8lib.c loadlib.c linit.c -lm -ldl
```

### Install the VS Code extension

```bash
install_extension.bat
```

See `build.md` for the full build guide (Windows / Linux / macOS, static and shared libraries, troubleshooting).

---

## Code Examples

### Example 1: Hello

```lua
-- Simple greeting program
محلي الاسم = "زائر"

دالة ترحيب(نص)
    اطبع("أهلاً بك يا " .. نص .. " في لغة ياقوت!")
نهاية

ترحيب(الاسم)
```

### Example 2: Average

```lua
-- Average of student grades
محلي درجات = {85, 92, 78, 95, 88}
محلي المجموع = 0

لكل ي, درجة في أزواج(درجات) افعل
    المجموع = المجموع + درجة
نهاية

محلي المتوسط = المجموع / #درجات
اطبع("متوسط الدرجات: " .. المتوسط)
```

### Example 3: Multiplication table

```lua
دالة جدول_الضرب(رقم)
    اطبع("جدول ضرب العدد " .. رقم .. ":")
    لكل ي = 1, 10 افعل
        محلي النتيجة = رقم * ي
        اطبع(رقم .. " × " .. ي .. " = " .. النتيجة)
    نهاية
نهاية

جدول_الضرب(7)
```

### Example 4: Tables (records)

```lua
محلي طالب = {
    اسم = "سارة",
    عمر = 20,
    تخصص = "هندسة البرمجيات",
    درجات = {
        رياضيات = 95,
        برمجة = 98,
        فيزياء = 88
    }
}

دالة احسب_المعدل(ط)
    محلي مجموع = 0
    محلي عدد = 0
    لكل مادة, درجة في أزواج(ط.درجات) افعل
        مجموع = مجموع + درجة
        عدد = عدد + 1
    نهاية
    ارجع مجموع / عدد
نهاية

اطبع("اسم الطالب: " .. طالب.اسم)
اطبع("المعدل: " .. احسب_المعدل(طالب))
```

### Example 5: Files

```lua
استدعي("library.yq")

-- Write a file
ياقوت.ملفات.كتابة("notes.txt", "my notes")

-- Read a file
محلي ملف = دخل_خرج.فتح("notes.txt", "r")
إذا ملف إذن
    محلي محتوى = ملف:قراءة("*all")
    اطبع(محتوى)
    ملف:إغلاق()
نهاية
```

---

## Standard Libraries

### Math (`رياضيات`)

| Function | Description | Example |
|----------|-------------|---------|
| `رياضيات.جذر(x)` | Square root | `رياضيات.جذر(16)` -> `4` |
| `رياضيات.جيب(x)` | Sine | `رياضيات.جيب(0)` -> `0` |
| `رياضيات.جتا(x)` | Cosine | `رياضيات.جتا(0)` -> `1` |
| `رياضيات.ظل(x)` | Tangent | `رياضيات.ظل(0)` -> `0` |
| `رياضيات.أرض(x)` | Floor | `رياضيات.أرض(3.7)` -> `3` |
| `رياضيات.سقف(x)` | Ceil | `رياضيات.سقف(3.2)` -> `4` |
| `رياضيات.قيمة_مطلقة(x)` | Absolute value | `رياضيات.قيمة_مطلقة(-5)` -> `5` |
| `رياضيات.أقصى(...)` | Max | `رياضيات.أقصى(1,5,3)` -> `5` |
| `رياضيات.أدنى(...)` | Min | `رياضيات.أدنى(1,5,3)` -> `1` |
| `رياضيات.عشوائي(m,n)` | Random number | `رياضيات.عشوائي(1,100)` |
| `رياضيات.ط` | Pi | `3.14159...` |

### Strings (`نصوص`)

| Function | Description | Example |
|----------|-------------|---------|
| `نصوص.طول(s)` | Length | `نصوص.طول("مرحبا")` -> `5` |
| `نصوص.عكس(s)` | Reverse | `نصوص.عكس("abc")` -> `"cba"` |
| `نصوص.تكبير(s)` | Uppercase | `نصوص.تكبير("abc")` -> `"ABC"` |
| `نصوص.تصغير(s)` | Lowercase | `نصوص.تصغير("ABC")` -> `"abc"` |
| `نصوص.تنسيق(...)` | Format | `نصوص.تنسيق("%d", 42)` |

### Tables (`جدول`)

| Function | Description |
|----------|-------------|
| `جدول.إدراج(t,v)` | Insert element |
| `جدول.حذف(t,i)` | Remove element |
| `جدول.ترتيب(t)` | Sort table |
| `جدول.دمج(t,sep)` | Join as string |

### System (`نظام`)

| Function | Description |
|----------|-------------|
| `نظام.وقت()` | Current time |
| `نظام.تاريخ(f)` | Formatted date |
| `نظام.خرج(c)` | Exit program |
| `نظام.تنفيذ(cmd)` | Execute shell command |

### IO (`دخل_خرج`)

| Function | Description |
|----------|-------------|
| `دخل_خرج.فتح(file,mode)` | Open file |
| `دخل_خرج.قراءة()` | Read from input |
| `دخل_خرج.كتابة(...)` | Write to output |

---

## Keyword Table

### Core keywords

| Arabic | English | Description |
|--------|---------|-------------|
| `محلي` | `local` | Define a local variable |
| `دالة` | `function` | Define a function |
| `نهاية` | `end` | Close a block |
| `ارجع` | `return` | Return a value |
| `إذا` | `if` | Condition |
| `إذن` | `then` | Start of condition block |
| `وإلا` | `else` | Alternative branch |
| `وإلا_إذا` | `elseif` | Alternative condition |
| `لكل` | `for` | Loop |
| `طالما` | `while` | While loop |
| `افعل` | `do` | Start of loop block |
| `كرر` | `repeat` | Repeat loop |
| `حتى` | `until` | Repeat-until condition |
| `اكسر` | `break` | Break loop |
| `في` | `in` | In (for loops) |

### Boolean values

| Arabic | English | Description |
|--------|---------|-------------|
| `صح` | `true` | True |
| `خطأ` | `false` | False |
| `لاشيء` | `nil` | Nil / empty |

### Logical operators

| Arabic | English | Description |
|--------|---------|-------------|
| `و` | `and` | Logical and |
| `أو` | `or` | Logical or |
| `ليس` | `not` | Negation |

### Built-in functions

| Arabic | English | Description |
|--------|---------|-------------|
| `اطبع` | `print` | Print to screen |
| `نوع` | `type` | Variable type |
| `تحويل_لرقم` | `tonumber` | Convert to number |
| `تحويل_لنص` | `tostring` | Convert to string |
| `أزواج` | `pairs` | Iterate over table |
| `أزواج_رقمية` | `ipairs` | Numeric iteration |

---

## Comparison with Other Languages

### Yaqout vs Python

| Feature | Yaqout | Python |
|---------|--------|--------|
| Learning curve | Easy | Easy |
| Arabic keywords | Yes | No |
| Localized libraries | Yes | No |
| Performance | High | Medium |
| Binary size | ~200KB | ~30MB |
| Game embedding | Yes | Partial |
| Community | Small | Very large |

### Yaqout vs JavaScript

| Feature | Yaqout | JavaScript |
|---------|--------|------------|
| Learning curve | Easy | Medium |
| Arabic keywords | Yes | No |
| Web support | No | Yes |
| Performance | High | High |
| Complexity | Low | Medium |

### Yaqout vs Lua

| Feature | Yaqout | Lua |
|---------|--------|-----|
| Same engine | Yes | Yes |
| Arabic keywords | Yes | No |
| Localized libraries | Yes | No |
| Compatibility | 100% with Lua | - |
| Community | Small | Large |

---

## FAQ

### Q1: Is Yaqout free?

Yes, open source and free under MIT.

### Q2: Can I use it commercially?

Yes, MIT allows commercial use.

### Q3: Is it compatible with plain Lua code?

Yes, 100% compatible. Any Lua code runs.

### Q4: How do I learn it?

1. `YAQOUT_BOOK.md` — full learning book (being translated to English)
2. `build.md` — build guide
3. `testes/` folder — examples and tests

### Q5: Arabic letters do not display correctly?

Make sure:

- Files are saved as UTF-8
- Terminal supports UTF-8
- On Windows CMD: `chcp 65001`

### Q6: Can I contribute?

Yes, see `CONTRIBUTING.md`.

### Q7: Where do I report issues?

Open a new GitHub Issue with details.

### Q8: Does it work on Linux/Mac?

Yes, it builds with GCC on any system.

---

## Contributing

All contributions are welcome:

- Localize more libraries
- Write docs and examples
- Report and fix bugs
- Star and share the project

See CONTRIBUTING.md for details.

---

## Developer

- **Lead developer**: Islam Al-Nashar
- **Organization**: Al-Nashar Studio
- **Year**: 2026

---

## License

Open source under the **MIT License**.

```
MIT License

Copyright (c) 2026 Islam Al-Nashar (Al-Nashar Studio)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.
```

---

## Tags

`arabic-programming-language` `lua-arabic` `yaqout-lang` `arabic-coding`
`programming-in-arabic` `language-localization` `scripting-language`
`compilers` `open-source` `education`

---

**Let's build the future of Arabic programming together!**
