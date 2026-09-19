# Book: Mastering Programming with Yaqout
## The Complete Guide to Programming in Arabic
**Author: Islam Al-Nashar (Al-Nashar Studio)**
**Version: 1.0 (2026)**

---

## Introduction

Welcome to the world of Arabic programming. **Yaqout** is not just a translation of Lua — it is a complete environment designed to remove the language barrier for creative minds in the Arab world. This book is a tutorial reference that takes you from zero to building complex software systems.

All code samples keep the original Arabic keywords. All explanations are in English.

---

## Index

1. **Chapter 1**: Setup and first greeting.
2. **Chapter 2**: Building blocks (variables and data types).
3. **Chapter 3**: Logic and decisions (conditionals).
4. **Chapter 4**: Repetition and power (loops).
5. **Chapter 5**: Code architecture (functions).
6. **Chapter 6**: Data structures (tables and maps).
7. **Chapter 7**: Standard libraries (system and math).
8. **Chapter 8**: Advanced programming (coroutines and metatables).

---

## Chapter 1: First Greeting

Yaqout is an easy-to-learn scripting language. Let's write your first code:

```lua
اطبع("مرحباً بك في لغة ياقوت")
```

File name: `start.yq`
Run: `yaqout.exe start.yq`

---

## Chapter 2: Building Blocks (Variables)

Variables are storage for information.

### Data types:

1. **Number**: (e.g. `10` or `3.14`).
2. **String**: (e.g. `"ياقوت"`).
3. **Boolean**: (`صح` for true or `خطأ` for false).
4. **Nil**: (`لاشيء` means nothing).
5. **Table**: (the single powerful data structure).

```lua
محلي العمر = 25
محلي الاسم = "إسلام"
محلي هل_محب_للبرمجة = صح
```

---

## Chapter 3: Decisions

Programming is the ability to choose a path.

```lua
محلي درجة_الحرارة = 30

إذا درجة_الحرارة > 40 إذن
    اطبع("الجو حار جداً")
وإلا_إذا درجة_الحرارة > 20 إذن
    اطبع("الجو معتدل")
وإلا
    اطبع("الجو بارد")
نهاية
```

---

## Chapter 4: Loops

To run code multiple times.

### "لكل" (for) loop:

```lua
اطبع("العد التنازلي:")
لكل ر = 5, 1, -1 افعل
    اطبع(ر)
نهاية
اطبع("انطلاق!")
```

---

## Chapter 5: Code Architecture (Functions)

A function is reusable code.

```lua
دالة حساب_المساحة(الطول, العرض)
    ارجع الطول * العرض
نهاية

محلي مساحة_الغرفة = حساب_المساحة(5, 4)
اطبع("المساحة تساوي: " .. مساحة_الغرفة)
```

---

## Chapter 6: Tables

A table in Yaqout is an array, dictionary, and object at once.

```lua
محلي طالب = {
    اسم = "أحمد",
    عمر = 20,
    درجات = {90, 85, 95}
}

اطبع(طالب.اسم)
جدول.إدراج(طالب.درجات, 88)
```

---

## Chapter 7: Localized Libraries

Yaqout ships with powerful ready-to-use libraries in Arabic:

* **نصوص.عكس(s)**: reverse a string.
* **رياضيات.جذر(x)**: square root.
* **نظام.تاريخ()**: get the date.

Full example:

```lua
محلي تاريخ_اليوم = نظام.تاريخ("%Y-%m-%d")
اطبع("تاريخ اليوم هو: " .. تاريخ_اليوم)
```

See README.md for the full standard-library tables.

---

## Chapter 8: Advanced Programming

Yaqout lets you change language behavior with **metatables**.

```lua
محلي جدول_محمي = {}
تعيين_الجدول_الوصفي(جدول_محمي, {
    __index = دالة(ط, مفتاح)
        ارجع "المفتاح [" .. مفتاح .. "] غير موجود!"
    نهاية
})

اطبع(جدول_محمي.بيانات)
```

---

## Conclusion

You now hold the basic keys to programming with Yaqout. The road is long and fun, and creativity has no limits when you code in your own language.

**Best regards:**
**Developer Islam Al-Nashar**
**Al-Nashar Studio**
