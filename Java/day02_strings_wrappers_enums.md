# 📘 Day 2 — Strings, Wrapper Classes, Enums & Inner Classes

**Date**: Aug 19, 2026 | **Duration**: ~4.5 hours
**Goal**: Master Strings (the most asked topic in Java interviews), Wrapper Classes, Enums, and Inner Classes

---

## 📑 Table of Contents

1. [Strings — The Complete Story](#1-strings--the-complete-story)
   - 1.1 How Strings Work Internally
   - 1.2 String Pool (String Intern Pool)
   - 1.3 Why Strings Are Immutable
   - 1.4 String vs StringBuilder vs StringBuffer
   - 1.5 String Concatenation — What Really Happens
   - 1.6 All Important String Methods
   - 1.7 String Comparison — All Ways
   - 1.8 String Conversion
2. [Wrapper Classes & Autoboxing](#2-wrapper-classes--autoboxing)
   - 2.1 What Are Wrapper Classes
   - 2.2 Autoboxing & Unboxing
   - 2.3 Integer Cache (Trap!)
   - 2.4 Parsing & Converting
   - 2.5 Common Traps
3. [Enums — More Than Constants](#3-enums--more-than-constants)
   - 3.1 Why Enums Exist
   - 3.2 Enum Basics
   - 3.3 Enum with Fields, Constructors & Methods
   - 3.4 Enum with Abstract Methods
   - 3.5 EnumSet & EnumMap
   - 3.6 Enum as Singleton
4. [Inner Classes — Classes Inside Classes](#4-inner-classes--classes-inside-classes)
   - 4.1 Why Inner Classes
   - 4.2 Member Inner Class
   - 4.3 Static Nested Class
   - 4.4 Local Inner Class
   - 4.5 Anonymous Inner Class
   - 4.6 Anonymous Class vs Lambda
5. [Interview Questions & Answers (55+)](#5-interview-questions--answers)

---

## 1. Strings — The Complete Story

> Strings are the **#1 most asked topic** in Java interviews. Every interview will have at least 2-3 String questions. Master this section thoroughly.

### 1.1 How Strings Work Internally

A `String` in Java is an **object** of class `java.lang.String`. Internally, it is backed by a character array (or byte array since Java 9).

```
Before Java 9:    private final char[] value;     // UTF-16, 2 bytes per char
Since Java 9:     private final byte[] value;     // Compact Strings — uses 1 byte for Latin-1 characters
                  private final byte coder;       // 0 = Latin-1 (1 byte), 1 = UTF-16 (2 bytes)
```

> [!NOTE]
> **Java 9 Compact Strings**: Java 9 introduced an optimization. If a string contains only ASCII/Latin-1 characters (English, digits, etc.), it uses 1 byte per character instead of 2. This saves ~50% memory for most applications. This happens automatically — you don't need to do anything.

The key word in the declaration is **`final`** — the array reference can never be changed once assigned. This is part of what makes Strings immutable.

### 1.2 String Pool (String Intern Pool)

The String Pool is a **special memory area inside the Heap** (moved from PermGen to Heap in Java 7) where Java stores string literals to save memory.

**How it works — Visualized**:

```
HEAP MEMORY
┌──────────────────────────────────────────────┐
│                                              │
│   ┌──────────── STRING POOL ──────────────┐  │
│   │                                       │  │
│   │   ┌─────────┐   ┌─────────┐          │  │
│   │   │ "Hello" │   │ "World" │          │  │
│   │   └────▲────┘   └────▲────┘          │  │
│   │        │             │                │  │
│   └────────│─────────────│────────────────┘  │
│            │             │                    │
│   s1 ──────┘             │                    │
│   s2 ──────┘   (same!)   │                    │
│   s3 ────────────────────┘                    │
│                                              │
│   ┌─────────┐    ┌─────────┐                │
│   │ "Hello" │    │ "Hello" │   (Outside Pool)│
│   └────▲────┘    └────▲────┘                │
│        │              │                      │
│   s4 ──┘         s5 ──┘   (different objects)│
│                                              │
└──────────────────────────────────────────────┘
```

```java
// String LITERALS → go into the String Pool
String s1 = "Hello";     // Creates "Hello" in pool
String s2 = "Hello";     // Reuses same "Hello" from pool — NO new object!

// Using 'new' → creates object OUTSIDE the pool (on regular heap)
String s4 = new String("Hello");    // New object on heap (NOT in pool)
String s5 = new String("Hello");    // Another new object on heap

// Comparison
System.out.println(s1 == s2);       // true  — same reference (pool)
System.out.println(s1 == s4);       // false — different locations
System.out.println(s4 == s5);       // false — two different heap objects
System.out.println(s1.equals(s4));  // true  — same content
```

**The `intern()` method** — Forces a string into the pool:

```java
String s4 = new String("Hello");
String s6 = s4.intern();    // Checks pool: "Hello" exists? Yes → return pool reference

System.out.println(s1 == s6);    // true  — s6 now points to pool
System.out.println(s4 == s6);    // false — s4 is still on heap
```

> [!IMPORTANT]
> **Classic Interview Question**: How many objects are created by `String s = new String("Hello");`?
>
> **Answer**: Potentially **2 objects**:
> 1. One in the String Pool (for the literal `"Hello"` — if it doesn't already exist)
> 2. One on the regular Heap (because of `new`)
>
> If `"Hello"` already exists in the pool, then only **1 object** is created (the one on the heap).

### 1.3 Why Strings Are Immutable — 5 Reasons

Once a `String` object is created, its content **cannot be changed**. Any "modification" creates a **new String**.

```java
String s = "Hello";
s.concat(" World");           // Creates new String, but s still points to "Hello"
System.out.println(s);        // "Hello" — unchanged!

s = s.concat(" World");       // Now s points to the NEW string "Hello World"
System.out.println(s);        // "Hello World"
// The original "Hello" is still in the pool, just no longer referenced by s
```

**Why did Java make Strings immutable?** Five important reasons:

| # | Reason | Explanation |
|---|--------|-------------|
| 1 | **String Pool Optimization** | Multiple references can safely share the same String. If strings were mutable, changing one would affect all references — disaster! |
| 2 | **Security** | Strings are used for file paths, database URLs, network connections, class loading. If an attacker could modify a string after validation but before use, it's a security hole. |
| 3 | **Thread Safety** | Immutable objects are inherently thread-safe. Multiple threads can read the same String without synchronization. |
| 4 | **Hashcode Caching** | `String` caches its hashcode (lazy calculation, stored in a field). Since the string never changes, the hashcode never changes. This makes `HashMap` lookups faster. |
| 5 | **Class Loading Safety** | The JVM uses strings to load classes (`Class.forName("com.example.MyClass")`). If someone could modify the string between the security check and the actual loading, they could load malicious classes. |

Think of it like a **printed book** 📖 — you can't erase and rewrite the words. If you want different words, you create a new book.

### 1.4 String vs StringBuilder vs StringBuffer — The Trilogy

This is asked in **almost every interview**. Know this table cold:

| Feature | `String` | `StringBuilder` | `StringBuffer` |
|---------|----------|-----------------|----------------|
| **Mutability** | ❌ Immutable | ✅ Mutable | ✅ Mutable |
| **Thread-Safe** | ✅ (inherently) | ❌ Not thread-safe | ✅ Thread-safe (synchronized) |
| **Performance** | Slowest (creates new objects) | 🚀 Fastest | Medium (sync overhead) |
| **Storage** | String Pool + Heap | Heap only | Heap only |
| **Since** | JDK 1.0 | JDK 1.5 | JDK 1.0 |
| **Use When** | Content won't change | Single-threaded mutations | Multi-threaded mutations |

```java
// String — each concat creates a NEW object ❌ (bad for loops)
String result = "";
for (int i = 0; i < 10000; i++) {
    result = result + i;     // Creates ~10,000 String objects! SLOW 🐌
}

// StringBuilder — modifies SAME object ✅ (fast)
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 10000; i++) {
    sb.append(i);            // Modifies same object. FAST 🚀
}
String result = sb.toString();
```

**StringBuilder Internal Working**:

```java
// StringBuilder internally uses a resizable char array (byte array in Java 9+)
// Default capacity: 16 characters
StringBuilder sb = new StringBuilder();     // capacity = 16
sb.append("Hello");                         // length = 5, capacity = 16

// When capacity is exceeded:
// newCapacity = (oldCapacity * 2) + 2
// 16 → 34 → 70 → 142 → ...

// You can set initial capacity to avoid resizing:
StringBuilder sb = new StringBuilder(1000);  // capacity = 1000 (good if you know approximate size)
```

**Important StringBuilder / StringBuffer Methods**:

```java
StringBuilder sb = new StringBuilder("Hello");

sb.append(" World");          // "Hello World"           — add at end
sb.insert(5, ",");            // "Hello, World"          — insert at position
sb.replace(0, 5, "Hi");      // "Hi, World"             — replace range
sb.delete(2, 4);              // "Hi World"              — delete range
sb.reverse();                 // "dlroW iH"              — reverse
sb.charAt(0);                 // 'd'                     — character at index
sb.length();                  // 8                       — current length
sb.capacity();                // 21                      — internal capacity (16 + 5 original)
sb.setCharAt(0, 'D');         // "DlroW iH"              — set character at index
sb.deleteCharAt(0);           // "lroW iH"               — delete single character
sb.substring(0, 4);           // "lroW"                  — returns String (not StringBuilder!)
sb.indexOf("oW");             // 2                       — find substring position
sb.toString();                // Convert to String
```

> [!TIP]
> **Interview Rule of Thumb**:
> - Use `String` for constants and when the value won't change
> - Use `StringBuilder` in 99% of mutable string scenarios (single-threaded)
> - Use `StringBuffer` only when you specifically need thread-safe mutable strings (rare — most prefer `StringBuilder` + external synchronization)

### 1.5 String Concatenation — What Really Happens Behind the Scenes

Understanding this shows deep knowledge in interviews:

```java
String s = "Hello" + " " + "World";
```

**Before Java 9**: The compiler transformed `+` concatenation into `StringBuilder` operations:
```java
// Compiler transforms the above into:
String s = new StringBuilder().append("Hello").append(" ").append("World").toString();
```

**Java 9+**: The compiler uses `invokedynamic` with `StringConcatFactory`, which allows the JVM to choose the best strategy at runtime. This is more efficient because:
- The JVM can pre-size the StringBuilder
- It can use different strategies for different scenarios
- It avoids creating intermediate objects

**However**, in a **loop**, the compiler **cannot** optimize well:

```java
// ❌ BAD — compiler creates a new StringBuilder for EACH iteration
String result = "";
for (int i = 0; i < 1000; i++) {
    result = result + i;     // Each iteration: new StringBuilder → append old → append i → toString
}

// ✅ GOOD — single StringBuilder used throughout
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);            // Same StringBuilder, just appending
}
String result = sb.toString();
```

> [!IMPORTANT]
> **Interview Answer**: "For simple concatenations like `"Hello" + name`, using `+` is fine because the compiler optimizes it. But for concatenation inside loops, I always use `StringBuilder` because the compiler creates a new `StringBuilder` per iteration, which is very inefficient."

### 1.6 All Important String Methods

I've organized these by category for easy revision. Know at least the bolded ones for interviews.

#### Creating / Converting

```java
// Creating
String s1 = "Hello";                              // Literal (pool)
String s2 = new String("Hello");                   // Object (heap)
String s3 = new String(new char[]{'H','i'});       // From char array
String s4 = String.valueOf(123);                   // "123" — int to String
String s5 = String.valueOf(true);                  // "true"
String s6 = String.join(", ", "A", "B", "C");     // "A, B, C"
String s7 = "Hi".repeat(3);                        // "HiHiHi" (Java 11)
```

#### Querying / Inspecting

```java
String s = "Hello World";

s.length();                  // 11        — number of characters
s.isEmpty();                 // false     — true if length is 0
s.isBlank();                 // false     — true if empty or only whitespace (Java 11)
s.charAt(0);                 // 'H'       — character at index
s.indexOf('o');              // 4         — first occurrence of 'o'
s.indexOf("World");          // 6         — first occurrence of substring
s.indexOf('o', 5);           // 7         — first 'o' starting from index 5
s.lastIndexOf('o');          // 7         — last occurrence
s.contains("World");         // true      — checks if substring exists
s.startsWith("Hello");       // true
s.endsWith("World");         // true
```

#### Comparing

```java
String s = "Hello";

s.equals("Hello");                  // true    — content comparison (case-sensitive)
s.equalsIgnoreCase("hello");        // true    — content comparison (case-insensitive)
s.compareTo("Hello");               // 0       — lexicographic (0 = equal, <0 = before, >0 = after)
s.compareToIgnoreCase("hello");     // 0
```

#### Extracting

```java
String s = "Hello World";

s.substring(6);              // "World"         — from index 6 to end
s.substring(0, 5);           // "Hello"         — from index 0 to 4 (end is exclusive!)
s.toCharArray();             // {'H','e','l','l','o',' ','W','o','r','l','d'}
```

> [!CAUTION]
> `substring(start, end)` — the `end` index is **exclusive**! This trips up many people.
> `"Hello".substring(1, 3)` returns `"el"` (characters at index 1 and 2, NOT 3).

#### Modifying (returns NEW String — original unchanged!)

```java
String s = "  Hello World  ";

s.trim();                    // "Hello World"    — removes leading/trailing whitespace (ASCII ≤ 32)
s.strip();                   // "Hello World"    — removes whitespace (Unicode-aware) (Java 11)
s.stripLeading();            // "Hello World  "  — removes leading only (Java 11)
s.stripTrailing();           // "  Hello World"  — removes trailing only (Java 11)

s = "Hello World";
s.toUpperCase();             // "HELLO WORLD"
s.toLowerCase();             // "hello world"
s.replace('l', 'L');         // "HeLLo WorLd"    — replaces ALL occurrences of char
s.replace("World", "Java");  // "Hello Java"     — replaces ALL occurrences of CharSequence
s.replaceAll("[aeiou]", "*");// "H*ll* W*rld"    — regex-based replacement
s.replaceFirst("[aeiou]","*");// "H*llo World"   — only first match
```

> [!TIP]
> **`trim()` vs `strip()`**: Both remove whitespace, but `strip()` (Java 11) is Unicode-aware and handles special whitespace characters like `\u2000`. For most cases, they behave the same. Prefer `strip()` if on Java 11+.

#### Splitting & Joining

```java
String csv = "Angooj,28,Kolkata,Engineer";

String[] parts = csv.split(",");       // {"Angooj", "28", "Kolkata", "Engineer"}
String[] limit = csv.split(",", 3);    // {"Angooj", "28", "Kolkata,Engineer"} — max 3 parts

String joined = String.join("-", parts);  // "Angooj-28-Kolkata-Engineer"

// Java 11 — split by lines
String multi = "Line1\nLine2\nLine3";
multi.lines().forEach(System.out::println);   // Stream of lines
```

#### Java 11 Additions (Important — often asked)

```java
"  ".isBlank();                // true  — empty or only whitespace
"  Hello  ".strip();           // "Hello" — Unicode-aware trim
"Ha".repeat(3);                // "HaHaHa"
"Line1\nLine2".lines().count(); // 2 — returns Stream<String>
```

### 1.7 String Comparison — All Ways (A Complete Guide)

This is critical for interviews. Here are ALL the ways to compare Strings:

```java
String s1 = "Hello";
String s2 = "Hello";
String s3 = new String("Hello");
String s4 = "HELLO";
```

| Method | What it Compares | s1 vs s2 | s1 vs s3 | s1 vs s4 |
|--------|-----------------|----------|----------|----------|
| `==` | Reference (memory address) | `true` ✅ | `false` ❌ | `false` |
| `.equals()` | Content (case-sensitive) | `true` | `true` ✅ | `false` |
| `.equalsIgnoreCase()` | Content (case-insensitive) | `true` | `true` | `true` ✅ |
| `.compareTo()` | Lexicographic order | `0` (equal) | `0` (equal) | `32` (positive) |
| `Objects.equals()` | Null-safe `.equals()` | `true` | `true` | `false` |

> [!IMPORTANT]
> **Golden Rule**: ALWAYS use `.equals()` for String comparison, NEVER `==`.
> The only time `==` returns `true` for Strings is when both references point to the same object (like two literals with the same value).

### 1.8 String Conversion — Every Direction

```java
// Primitive → String
String s1 = String.valueOf(42);          // "42"        — preferred way
String s2 = Integer.toString(42);        // "42"
String s3 = "" + 42;                     // "42"        — works but less clean

// String → Primitive
int num = Integer.parseInt("42");        // 42
double d = Double.parseDouble("3.14");   // 3.14
boolean b = Boolean.parseBoolean("true");// true

// String → char array → String
char[] chars = "Hello".toCharArray();    // {'H','e','l','l','o'}
String s = new String(chars);            // "Hello"
String s2 = String.valueOf(chars);       // "Hello"

// byte array
byte[] bytes = "Hello".getBytes();       // UTF-8 bytes
String s = new String(bytes, StandardCharsets.UTF_8);   // "Hello"
```

---

## 2. Wrapper Classes & Autoboxing

### 2.1 What Are Wrapper Classes & Why Do We Need Them?

Java has 8 primitives (`int`, `char`, etc.) and corresponding **wrapper classes** that wrap them in objects.

**Why do we need them?** Because:
1. **Collections** (`ArrayList`, `HashMap`) can only store **objects**, not primitives
2. **Generics** (`List<T>`) require objects
3. **Null handling** — primitives can't be `null`, wrappers can
4. **Utility methods** — wrappers provide parsing, conversion, comparison methods

| Primitive | Wrapper | Size | Parent Class |
|-----------|---------|------|-------------|
| `byte` | `Byte` | 1 byte | `Number` |
| `short` | `Short` | 2 bytes | `Number` |
| `int` | `Integer` | 4 bytes | `Number` |
| `long` | `Long` | 8 bytes | `Number` |
| `float` | `Float` | 4 bytes | `Number` |
| `double` | `Double` | 8 bytes | `Number` |
| `char` | `Character` | 2 bytes | `Object` |
| `boolean` | `Boolean` | ~1 byte | `Object` |

> [!NOTE]
> All numeric wrappers (`Byte`, `Short`, `Integer`, `Long`, `Float`, `Double`) extend **`Number`**, which provides methods like `intValue()`, `doubleValue()`, `longValue()`, etc.

```java
// Wrapper class hierarchy:
// Object
//   ├── Number (abstract)
//   │     ├── Byte
//   │     ├── Short
//   │     ├── Integer
//   │     ├── Long
//   │     ├── Float
//   │     └── Double
//   ├── Character
//   └── Boolean
```

### 2.2 Autoboxing & Unboxing

**Autoboxing** = Automatic conversion from primitive → wrapper (introduced in Java 5)
**Unboxing** = Automatic conversion from wrapper → primitive

```java
// Before Java 5 — manual boxing
Integer obj = new Integer(10);         // ❌ Deprecated since Java 9
Integer obj2 = Integer.valueOf(10);    // Manual boxing

// Java 5+ — autoboxing (automatic)
Integer obj = 10;                      // Autoboxing: int → Integer (compiler does valueOf())
int num = obj;                         // Unboxing: Integer → int (compiler does intValue())

// Works with all types
Double d = 3.14;          // double → Double
Boolean b = true;         // boolean → Boolean
Character c = 'A';        // char → Character

// Works in expressions
Integer x = 10;
Integer y = 20;
int sum = x + y;          // Both unboxed → int + int → result is int
Integer result = x + y;   // Both unboxed → added → result autoboxed to Integer
```

**Where autoboxing happens automatically**:
```java
// 1. Assignment
Integer x = 5;                          // Autoboxing

// 2. Method arguments
public void process(Integer num) { }
process(42);                             // 42 autoboxed to Integer

// 3. Collections
List<Integer> list = new ArrayList<>();
list.add(10);                            // 10 autoboxed to Integer
int val = list.get(0);                   // Integer unboxed to int

// 4. Comparison operators
Integer a = 100;
if (a > 50) { }                          // a unboxed to int for comparison

// 5. Arithmetic operations
Integer a = 10, b = 20;
Integer c = a + b;                        // Unbox → add → autobox
```

### 2.3 Integer Cache — The Famous Interview Trap 🎯

This is one of the **most commonly asked tricky questions**. Understand it deeply.

**Java caches Integer objects** in the range **-128 to 127**. When you create an Integer within this range (via autoboxing or `valueOf()`), Java returns the **cached instance** instead of creating a new object.

```java
Integer a = 127;           // Cached
Integer b = 127;           // Same cached object!
System.out.println(a == b);         // true ✅ — SAME object from cache

Integer c = 128;           // NOT cached (outside -128 to 127)
Integer d = 128;           // Different object
System.out.println(c == d);         // false ❌ — DIFFERENT objects!

Integer e = -128;          // Cached
Integer f = -128;          // Same cached object
System.out.println(e == f);         // true ✅

Integer g = -129;          // NOT cached
Integer h = -129;          // Different object
System.out.println(g == h);         // false ❌
```

**Visualized**:
```
INTEGER CACHE (shared static array)
┌──────────────────────────────────────────┐
│  [-128] [-127] ... [0] [1] ... [126] [127]  │
│    ▲                        ▲              │
│    │                        │              │
│  Integer a = -128        Integer b = 127    │
│  Integer c = -128 ──────►  (same!)         │
└──────────────────────────────────────────┘

OUTSIDE CACHE — new object every time
Integer x = 128  → new Integer(128)
Integer y = 128  → new Integer(128)   ← DIFFERENT object
```

**Why does this cache exist?**
- Small integers (-128 to 127) are used very frequently in programs
- Caching them saves memory and improves performance
- `Integer.valueOf(int)` checks the cache first; `new Integer(int)` always creates a new object (now deprecated)

**Which wrappers have caching?**

| Wrapper | Cached Range |
|---------|-------------|
| `Byte` | All (-128 to 127 — the entire range!) |
| `Short` | -128 to 127 |
| `Integer` | -128 to 127 (upper limit configurable via JVM flag) |
| `Long` | -128 to 127 |
| `Character` | 0 to 127 |
| `Boolean` | `TRUE` and `FALSE` (only 2 values) |
| `Float` | ❌ No cache |
| `Double` | ❌ No cache |

> [!IMPORTANT]
> **Interview Best Practice**: Always use `.equals()` to compare wrapper objects, never `==`.
> ```java
> Integer a = 200, b = 200;
> System.out.println(a == b);          // false ❌ (unreliable!)
> System.out.println(a.equals(b));     // true  ✅ (always correct!)
> ```

### 2.4 Parsing & Converting

```java
// String → Primitive (parseXxx)
int i = Integer.parseInt("42");           // 42
long l = Long.parseLong("123456789");     // 123456789
double d = Double.parseDouble("3.14");    // 3.14
boolean b = Boolean.parseBoolean("true"); // true
boolean b2 = Boolean.parseBoolean("yes"); // false! (only "true" → true, case-insensitive)

// String → Wrapper (valueOf)
Integer obj = Integer.valueOf("42");      // Integer object
Integer obj2 = Integer.valueOf(42);       // Integer object (from int)

// Primitive → String
String s1 = String.valueOf(42);           // "42" — preferred
String s2 = Integer.toString(42);         // "42"
String s3 = "" + 42;                      // "42" — works but creates temporary objects

// Different bases
int binary = Integer.parseInt("1010", 2);  // 10 (binary to decimal)
int hex = Integer.parseInt("FF", 16);      // 255 (hex to decimal)
String hexStr = Integer.toHexString(255);  // "ff"
String binStr = Integer.toBinaryString(10);// "1010"
String octStr = Integer.toOctalString(8);  // "10"
```

### 2.5 Common Wrapper Class Traps ⚠️

**Trap 1: NullPointerException on Unboxing**

```java
Integer x = null;
int y = x;           // ❌ NullPointerException!
                      // Compiler inserts x.intValue() → NPE because x is null

// This is VERY common in real projects:
Map<String, Integer> map = new HashMap<>();
int count = map.get("missing_key");   // ❌ NPE! get() returns null

// Safe way:
int count = map.getOrDefault("missing_key", 0);
// Or:
Integer count = map.get("missing_key");
if (count != null) { ... }
```

> [!CAUTION]
> **From Your Project**: In your Healthcare project, when retrieving values from database columns that might be NULL, always use `Integer` (wrapper) instead of `int` (primitive) to handle nulls safely. Use `Optional<Integer>` or null-checks before unboxing.

**Trap 2: Performance in Loops**

```java
// ❌ BAD — autoboxing in every iteration creates thousands of Integer objects
Long sum = 0L;
for (long i = 0; i < 100000; i++) {
    sum += i;     // Unbox sum → add → autobox result → assign
}

// ✅ GOOD — use primitive
long sum = 0L;
for (long i = 0; i < 100000; i++) {
    sum += i;     // Pure primitive operation — fast!
}
```

**Trap 3: == vs equals() with Mixed Types**

```java
Integer a = 10;
int b = 10;
System.out.println(a == b);     // true! → a is UNBOXED to int, then compared as primitives

Long x = 10L;
Integer y = 10;
// System.out.println(x == y);  // ❌ Compile error — can't compare Long and Integer with ==
System.out.println(x.equals(y));// false! — different types (Long vs Integer)
System.out.println(x.equals(10L)); // true — same type and value
```

**Trap 4: Method Overloading Ambiguity**

```java
public class Test {
    void print(int x) { System.out.println("primitive"); }
    void print(Integer x) { System.out.println("wrapper"); }

    public static void main(String[] args) {
        Test t = new Test();
        t.print(5);              // "primitive" — prefers exact match (int)
        t.print(Integer.valueOf(5)); // "wrapper" — explicit Integer
    }
}
```

The compiler **prefers widening over autoboxing**: `int` matches `int` directly, no need to autobox. If only `print(long)` existed, `5` would be widened to `long`.

---

## 3. Enums — More Than Constants

### 3.1 Why Enums Exist — The Problem They Solve

**Before Enums (Java < 5)** — We used `int` constants:
```java
// ❌ OLD WAY — many problems
public class Status {
    public static final int ACTIVE = 1;
    public static final int INACTIVE = 2;
    public static final int SUSPENDED = 3;
}

int status = Status.ACTIVE;
status = 999;          // ❌ Compiles! But 999 is not a valid status
status = -42;          // ❌ Compiles! No type safety at all
printStatus(42);       // ❌ Compiles! Any int is accepted
```

Problems with `int` constants:
1. **No type safety** — any `int` can be passed
2. **No namespace** — risk of name conflicts
3. **Brittle** — if values change, all clients must recompile
4. **No meaningful print** — `System.out.println(1)` doesn't tell you it's "ACTIVE"
5. **Can't iterate** — no way to loop through all values

**With Enums (Java 5+)** — All problems solved:
```java
// ✅ NEW WAY — type-safe, self-documenting
public enum Status {
    ACTIVE, INACTIVE, SUSPENDED
}

Status status = Status.ACTIVE;
// status = 999;       // ❌ Compile error — type safety!
// status = "hello";   // ❌ Compile error
System.out.println(status);  // "ACTIVE" — meaningful print
```

### 3.2 Enum Basics

```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
```

```java
// Using enum
Day today = Day.MONDAY;

// Get name as String
today.name();           // "MONDAY" — exact name
today.toString();       // "MONDAY" — same as name() by default

// Get ordinal (position, 0-indexed)
today.ordinal();        // 0 (MONDAY=0, TUESDAY=1, ...)

// Get all values
Day[] allDays = Day.values();   // Array of all enum constants
for (Day d : Day.values()) {
    System.out.println(d + " = " + d.ordinal());
}

// Convert String to Enum
Day d = Day.valueOf("MONDAY");  // Day.MONDAY
// Day d2 = Day.valueOf("monday"); // ❌ IllegalArgumentException — case-sensitive!

// Enum in switch (very clean!)
switch (today) {
    case MONDAY:
    case TUESDAY:
    case WEDNESDAY:
    case THURSDAY:
    case FRIDAY:
        System.out.println("Weekday");
        break;
    case SATURDAY:
    case SUNDAY:
        System.out.println("Weekend");
        break;
}
```

### 3.3 Enum with Fields, Constructors & Methods

This is where enums get powerful and where interviews go deeper.

```java
public enum Planet {
    // Each constant calls the constructor with these values
    MERCURY(3.303e+23, 2.4397e6),
    VENUS  (4.869e+24, 6.0518e6),
    EARTH  (5.976e+24, 6.37814e6),
    MARS   (6.421e+23, 3.3972e6);
    
    // Fields
    private final double mass;     // in kilograms
    private final double radius;   // in meters

    // Constructor — ALWAYS private (implicitly or explicitly)
    // Can NEVER be public or protected
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }

    // Methods
    public double getMass() { return mass; }
    public double getRadius() { return radius; }
    
    // Can have custom methods
    public double surfaceGravity() {
        final double G = 6.67300E-11;
        return G * mass / (radius * radius);
    }
    
    public double surfaceWeight(double otherMass) {
        return otherMass * surfaceGravity();
    }
}
```

```java
double earthWeight = 75.0;
double mass = earthWeight / Planet.EARTH.surfaceGravity();

for (Planet p : Planet.values()) {
    System.out.printf("Your weight on %s is %6.2f%n", p, p.surfaceWeight(mass));
}
```

**Real-World Example — From Your Healthcare Project:**

```java
public enum AdmissionStatus {
    PENDING("Pending Review", 1),
    ADMITTED("Patient Admitted", 2),
    DISCHARGED("Patient Discharged", 3),
    TRANSFERRED("Transferred to Another Facility", 4),
    CANCELLED("Admission Cancelled", 5);
    
    private final String displayName;
    private final int code;
    
    AdmissionStatus(String displayName, int code) {
        this.displayName = displayName;
        this.code = code;
    }
    
    public String getDisplayName() { return displayName; }
    public int getCode() { return code; }
    
    // Reverse lookup — code to enum
    public static AdmissionStatus fromCode(int code) {
        for (AdmissionStatus status : values()) {
            if (status.code == code) return status;
        }
        throw new IllegalArgumentException("Unknown code: " + code);
    }
}
```

> [!TIP]
> **Interview Tip**: Enums in Java are NOT simple constants like in C/C++. They are **full-fledged classes** that can have fields, constructors, methods, and even implement interfaces. This is a key differentiator that shows deep Java knowledge.

### 3.4 Enum with Abstract Methods (Constant-Specific Body)

Each enum constant can have its **own implementation** of a method:

```java
public enum Operation {
    ADD {
        @Override
        public double apply(double x, double y) { return x + y; }
    },
    SUBTRACT {
        @Override
        public double apply(double x, double y) { return x - y; }
    },
    MULTIPLY {
        @Override
        public double apply(double x, double y) { return x * y; }
    },
    DIVIDE {
        @Override
        public double apply(double x, double y) {
            if (y == 0) throw new ArithmeticException("Cannot divide by zero");
            return x / y;
        }
    };

    // Abstract method — each constant MUST implement it
    public abstract double apply(double x, double y);
}
```

```java
double result = Operation.ADD.apply(10, 5);      // 15.0
double result2 = Operation.MULTIPLY.apply(3, 4); // 12.0

// Iterate and apply all operations
for (Operation op : Operation.values()) {
    System.out.printf("%.1f %s %.1f = %.1f%n", 10.0, op, 3.0, op.apply(10, 3));
}
```

### 3.5 Enum Implementing Interface

```java
public interface Printable {
    void print();
}

public enum Color implements Printable {
    RED("#FF0000"),
    GREEN("#00FF00"),
    BLUE("#0000FF");
    
    private final String hexCode;
    
    Color(String hexCode) {
        this.hexCode = hexCode;
    }
    
    @Override
    public void print() {
        System.out.println(name() + " = " + hexCode);
    }
}
```

### 3.6 EnumSet & EnumMap — High-Performance Collections for Enums

**EnumSet** — A `Set` implementation specialized for enums. Internally uses **bit vectors** — extremely fast and memory-efficient.

```java
// Creating EnumSet
EnumSet<Day> weekend = EnumSet.of(Day.SATURDAY, Day.SUNDAY);
EnumSet<Day> weekdays = EnumSet.range(Day.MONDAY, Day.FRIDAY);
EnumSet<Day> allDays = EnumSet.allOf(Day.class);
EnumSet<Day> noDays = EnumSet.noneOf(Day.class);
EnumSet<Day> notWeekend = EnumSet.complementOf(weekend);   // All days except weekend

// Operations
weekend.contains(Day.SATURDAY);   // true
weekdays.add(Day.SATURDAY);       // Add to set
weekdays.remove(Day.MONDAY);      // Remove from set
```

**EnumMap** — A `Map` implementation with enum keys. Internally uses a **simple array** (index = ordinal) — very fast.

```java
EnumMap<Day, String> schedule = new EnumMap<>(Day.class);
schedule.put(Day.MONDAY, "Team meeting");
schedule.put(Day.WEDNESDAY, "Code review");
schedule.put(Day.FRIDAY, "Sprint demo");

String activity = schedule.get(Day.MONDAY);   // "Team meeting"

// Iterating — always in enum declaration order
for (Map.Entry<Day, String> entry : schedule.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
```

> [!TIP]
> **When should you use EnumSet/EnumMap?**
> Whenever you have a collection keyed by an enum, prefer `EnumMap` over `HashMap` and `EnumSet` over `HashSet`. They are significantly faster and use less memory because they use arrays/bit-vectors internally instead of hash tables.

### 3.7 Enum as Singleton Pattern

This is considered the **best way** to implement Singleton in Java (as recommended by Joshua Bloch in *Effective Java*):

```java
public enum DatabaseConnection {
    INSTANCE;    // Single constant = single instance
    
    private Connection connection;
    
    DatabaseConnection() {
        // Initialize connection
        connection = createConnection();
    }
    
    public Connection getConnection() {
        return connection;
    }
    
    private Connection createConnection() {
        // Create and return database connection
        return null;
    }
}

// Usage
DatabaseConnection.INSTANCE.getConnection();
```

**Why enum Singleton is the best?**
1. **Thread-safe**: Enum constants are guaranteed to be created once by the JVM
2. **Serialization-safe**: Enum serialization is handled by the JVM — no risk of creating a second instance
3. **Reflection-safe**: The JVM prevents instantiation of enums via reflection
4. **Simple**: No boilerplate code

---

## 4. Inner Classes — Classes Inside Classes

### 4.1 Why Inner Classes?

Inner classes allow you to **logically group classes** that are used in only one place. They have the special ability to **access the enclosing class's members** (including private).

**Real-World Analogy**: Think of a university (outer class) and its departments (inner classes). Departments logically belong inside the university and need access to university resources.

Java has **4 types** of inner classes:

```
Inner Classes
├── 1. Member Inner Class      (non-static, tied to an outer object)
├── 2. Static Nested Class     (static, independent of outer object)
├── 3. Local Inner Class       (defined inside a method)
└── 4. Anonymous Inner Class   (no name, defined + instantiated in one statement)
```

### 4.2 Member Inner Class (Non-Static Inner Class)

A class defined inside another class **without** the `static` keyword. Each inner class instance is tied to an outer class instance.

```java
public class Hospital {
    private String name;
    private int capacity;
    
    public Hospital(String name, int capacity) {
        this.name = name;
        this.capacity = capacity;
    }
    
    // Member inner class
    public class Department {
        private String deptName;
        
        public Department(String deptName) {
            this.deptName = deptName;
        }
        
        public void display() {
            // Can access PRIVATE members of outer class!
            System.out.println("Department: " + deptName);
            System.out.println("Hospital: " + name);              // Outer class field
            System.out.println("Capacity: " + capacity);          // Outer class field
            System.out.println("Outer this: " + Hospital.this);   // Reference to outer object
        }
    }
}
```

```java
// To create inner class object, you NEED an outer class object first
Hospital hospital = new Hospital("AIIMS", 1000);
Hospital.Department dept = hospital.new Department("Cardiology");
dept.display();

// Or in one line:
Hospital.Department dept2 = new Hospital("Apollo", 500).new Department("Neurology");
```

**Key Points**:
- Can access **all members** of outer class (including `private`)
- Each inner object has an implicit reference to its outer object
- **Cannot** have `static` members (except `static final` constants)
- Created using: `outerObject.new InnerClass()`

### 4.3 Static Nested Class

A class defined inside another class **with** the `static` keyword. It does **not** need an outer class instance.

```java
public class Hospital {
    private String name;
    private static int totalHospitals = 0;
    
    public Hospital(String name) {
        this.name = name;
        totalHospitals++;
    }
    
    // Static nested class
    public static class Statistics {
        public void showTotal() {
            // Can access STATIC members of outer class
            System.out.println("Total hospitals: " + totalHospitals);
            
            // CANNOT access instance members directly
            // System.out.println(name);   // ❌ Compile error — name is instance, not static
        }
        
        public void showHospitalName(Hospital h) {
            // CAN access instance members through an object reference
            System.out.println("Hospital: " + h.name);   // ✅ Even private!
        }
    }
}
```

```java
// No outer object needed!
Hospital.Statistics stats = new Hospital.Statistics();
stats.showTotal();

Hospital h = new Hospital("AIIMS");
stats.showHospitalName(h);
```

**Key Points**:
- Can only access **static members** of outer class directly
- Can access instance members **through an object reference**
- **Can** have static members
- Created using: `new OuterClass.StaticNestedClass()`
- Behaves like a top-level class but is nested for organizational purposes

### Member Inner Class vs Static Nested Class

| Feature | Member Inner Class | Static Nested Class |
|---------|-------------------|-------------------|
| `static` keyword | ❌ No | ✅ Yes |
| Needs outer instance | ✅ Yes | ❌ No |
| Access outer instance members | ✅ Yes (directly) | ❌ No (needs reference) |
| Access outer static members | ✅ Yes | ✅ Yes |
| Can have static members | ❌ No | ✅ Yes |
| Creation | `outer.new Inner()` | `new Outer.Nested()` |
| Use when | Logically tied to outer instance | Independent of outer instance |

> [!TIP]
> **Prefer static nested classes** unless you specifically need access to the outer instance. Static nested classes have less overhead (no implicit outer reference) and are easier to understand.

### 4.4 Local Inner Class

A class defined **inside a method**. It exists only within that method's scope.

```java
public class Hospital {
    
    public void processAdmission(String patientName) {
        
        final String ward = "General";    // Must be final or effectively final
        
        // Local inner class — only visible inside this method
        class AdmissionProcessor {
            void process() {
                System.out.println("Processing: " + patientName);  // Access method param
                System.out.println("Ward: " + ward);               // Access local variable
            }
        }
        
        AdmissionProcessor processor = new AdmissionProcessor();
        processor.process();
    }
}
```

**Key Points**:
- Visible only within the method where it's defined
- Can access **effectively final** (or explicitly `final`) local variables and parameters
- Rarely used in practice — anonymous classes or lambdas are preferred
- Cannot have access modifiers (`public`, `private`, etc.)
- Cannot be `static`

> [!NOTE]
> **What is "effectively final"?** A variable is effectively final if its value never changes after initialization — even if you don't declare it as `final`. Java 8 introduced this concept so lambdas and local inner classes don't require the `final` keyword explicitly.
> ```java
> String name = "Angooj";  // Never reassigned → effectively final
> // name = "John";         // If you uncomment this → no longer effectively final → compile error in lambda
> Runnable r = () -> System.out.println(name);  // Works because name is effectively final
> ```

### 4.5 Anonymous Inner Class

A class with **no name** — defined and instantiated in a single expression. Used to create a one-time implementation of an interface or extend a class.

```java
// Regular approach — create a named class
class MyComparator implements Comparator<String> {
    @Override
    public int compare(String a, String b) {
        return a.length() - b.length();
    }
}
List<String> names = Arrays.asList("Angooj", "Rahul", "Jo");
Collections.sort(names, new MyComparator());

// Anonymous inner class approach — inline, no separate class needed
Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.length() - b.length();    // Sort by length
    }
});
```

**More Examples**:

```java
// 1. Implementing an interface anonymously
Runnable task = new Runnable() {
    @Override
    public void run() {
        System.out.println("Running anonymously!");
    }
};
new Thread(task).start();

// 2. Extending a class anonymously
Thread thread = new Thread() {    // Anonymous subclass of Thread
    @Override
    public void run() {
        System.out.println("Custom thread!");
    }
};
thread.start();

// 3. Anonymous class with abstract class
abstract class Animal {
    abstract void sound();
}

Animal dog = new Animal() {       // Anonymous subclass of Animal
    @Override
    void sound() {
        System.out.println("Woof!");
    }
};
dog.sound();                       // "Woof!"
```

**Key Points**:
- No name, no reuse — used only once
- Can implement an interface **or** extend a class (but not both simultaneously)
- Can access effectively final local variables
- Cannot have explicit constructors (no name → no constructor name)
- Creates a `.class` file with a name like `OuterClass$1.class`, `OuterClass$2.class`

### 4.6 Anonymous Class vs Lambda — The Evolution

Java 8 lambdas replaced anonymous classes in many scenarios. Understanding the differences shows modern Java knowledge:

```java
// Anonymous inner class (pre-Java 8 way)
Comparator<String> comp1 = new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.length() - b.length();
    }
};

// Lambda (Java 8 way) — much cleaner!
Comparator<String> comp2 = (a, b) -> a.length() - b.length();

// Method reference (even cleaner!)
Comparator<String> comp3 = Comparator.comparingInt(String::length);
```

| Feature | Anonymous Inner Class | Lambda Expression |
|---------|----------------------|-------------------|
| Syntax | Verbose | Concise |
| `this` | Refers to anonymous class itself | Refers to enclosing class |
| Can implement multiple methods | ✅ Yes | ❌ No (single abstract method only) |
| Can extend a class | ✅ Yes | ❌ No |
| Can have state (fields) | ✅ Yes | ❌ No |
| Generates `.class` file | ✅ Yes | ❌ No (uses `invokedynamic`) |
| Performance | Slower (new class + object) | Faster (no extra class) |
| Use when | Multiple methods or need class features | Single method (functional interface) |

> [!IMPORTANT]
> **When Lambda Can't Replace Anonymous Class**:
> 1. When implementing an interface with **more than one abstract method**
> 2. When extending a **concrete or abstract class**
> 3. When you need to reference `this` as the anonymous class instance itself
> 4. When you need instance fields in the anonymous class

---

## 5. Interview Questions & Answers

### Category A: String Questions (20 Questions)

---

**Q1: Why is `String` immutable in Java?**

**Answer**: String is immutable for 5 reasons:
1. **String Pool**: Multiple references share the same string. Mutation would corrupt other references.
2. **Security**: Strings used in file paths, URLs, credentials. Modification after validation is a security risk.
3. **Thread Safety**: Immutable objects don't need synchronization.
4. **Hashcode Caching**: String caches its hash. Immutability guarantees the hash never becomes stale.
5. **Class Loading**: JVM uses strings for class names. Mutability would break class loading.

Internally, `String` is `final class` (can't be subclassed) with `private final char[] value` (or `byte[]` in Java 9+), so the value can't be reassigned, and since the class is final, no subclass can expose the internal array.

---

**Q2: How many objects are created by: `String s = new String("Hello");`?**

**Answer**: **Up to 2 objects**:
1. `"Hello"` as a **string literal** → placed in the String Pool (if not already there)
2. `new String(...)` → creates a **new object on the Heap** (outside the pool)

If `"Hello"` already exists in the pool from a previous statement, then only **1 object** (the heap one) is created.

---

**Q3: What is the String Pool? Where is it stored?**

**Answer**: The String Pool (also called String Intern Pool) is a special storage area where Java stores string literals. When you create a string literal, Java checks the pool first — if it exists, the existing reference is returned; if not, a new string is created in the pool.

**Location**:
- Java 6 and earlier: PermGen space (fixed size → could cause `OutOfMemoryError: PermGen space`)
- **Java 7+**: Moved to the **main Heap** (benefits from garbage collection, dynamically sized)

---

**Q4: Explain the difference between `String`, `StringBuilder`, and `StringBuffer`.**

**Answer**:
- **`String`**: Immutable. Any "change" creates a new object. Thread-safe inherently. Use when value won't change.
- **`StringBuilder`**: Mutable. Modifies in-place. **NOT** thread-safe. Fastest. Use for single-threaded string manipulation (99% of cases).
- **`StringBuffer`**: Mutable. Modifies in-place. **Thread-safe** (all methods are `synchronized`). Slower than StringBuilder. Use only when multiple threads modify the same string.

Performance example: Concatenating 10,000 strings in a loop:
- String: ~10,000 objects created → very slow
- StringBuilder: 1 object, modified in place → very fast
- StringBuffer: 1 object, with synchronization overhead → fast but slower than StringBuilder

---

**Q5: What is the `intern()` method?**

**Answer**: `intern()` checks if the string exists in the String Pool. If yes, it returns the pool reference. If no, it adds the string to the pool and returns the pool reference.

```java
String s1 = new String("Hello");   // On heap
String s2 = s1.intern();           // Returns pool reference to "Hello"
String s3 = "Hello";               // Pool reference

System.out.println(s2 == s3);      // true — both point to pool
System.out.println(s1 == s2);      // false — s1 is on heap, s2 is in pool
```

Use case: When you have many duplicate strings (e.g., reading from a file), `intern()` can save memory by deduplicating them.

---

**Q6: Predict the output:**
```java
String s1 = "Hello";
String s2 = "Hel" + "lo";
String s3 = "Hel";
String s4 = s3 + "lo";

System.out.println(s1 == s2);   // ?
System.out.println(s1 == s4);   // ?
```

**Answer**:
```
true
false
```
- `s1 == s2` is `true` because `"Hel" + "lo"` is a **compile-time constant expression** — the compiler resolves it to `"Hello"` and uses the same pool reference.
- `s1 == s4` is `false` because `s3 + "lo"` involves a **variable** (`s3`), so it's resolved at runtime using `StringBuilder`, creating a new object on the heap.

**Exception**: If `s3` were declared `final String s3 = "Hel"`, then `s3 + "lo"` WOULD be a compile-time constant, and `s1 == s4` would be `true`.

```java
final String s3 = "Hel";
String s4 = s3 + "lo";
System.out.println(s1 == s4);   // true! — s3 is a compile-time constant
```

---

**Q7: Predict the output:**
```java
String s1 = "abc";
String s2 = "abc";
String s3 = new String("abc");
String s4 = new String("abc").intern();

System.out.println(s1 == s2);     // ?
System.out.println(s1 == s3);     // ?
System.out.println(s1 == s4);     // ?
System.out.println(s1.equals(s3));// ?
```

**Answer**:
```
true     — both literals, same pool reference
false    — s3 is on heap, s1 is in pool
true     — intern() returns pool reference, which is same as s1
true     — same content
```

---

**Q8: Is `String` a keyword in Java?**

**Answer**: **No**. `String` is a **class** (`java.lang.String`), not a keyword. It just looks special because:
- It's imported by default (`java.lang` package)
- It has literal syntax (`"..."`)
- It has `+` operator support for concatenation

Keywords are lowercase (`class`, `int`, `if`, etc.). `String` starts with uppercase — it's a class.

---

**Q9: Why is `String` declared as `final` class?**

**Answer**: If `String` were not final, a malicious subclass could:
- Override methods to modify behavior
- Bypass immutability
- Compromise security (strings used in class loading, security checks)
- Break the String Pool mechanism
- Invalidate hashcode caching

Making it `final` ensures no subclass can undermine String's guarantees.

---

**Q10: What is the difference between `trim()` and `strip()`?**

**Answer**:
- `trim()` (since Java 1.0): Removes characters with ASCII value ≤ 32 (space, tab, newline). Does NOT handle Unicode whitespace.
- `strip()` (since Java 11): Uses `Character.isWhitespace()` which handles Unicode whitespace characters like `\u2000` (En Quad), `\u3000` (Ideographic Space), etc.

```java
String s = "\u2000Hello\u2000";   // Unicode whitespace
s.trim();       // "\u2000Hello\u2000" — NOT removed (trim doesn't know Unicode)
s.strip();      // "Hello" — removed! (strip understands Unicode)
```

Also: `stripLeading()` and `stripTrailing()` exist for one-sided stripping.

---

**Q11: How does `String` achieve thread-safety?**

**Answer**: Through **immutability**. Since String content cannot change after creation:
- No thread can modify it while another reads it
- No `synchronized` block is needed
- Multiple threads can safely share the same String reference

This is the most elegant form of thread safety — no locks, no synchronization, no performance overhead.

---

**Q12: What happens when you use `+` for String concatenation in a loop?**

**Answer**: Each `+` creates a new `StringBuilder` internally, performs the concatenation, calls `toString()`, and discards the `StringBuilder`. In a loop with N iterations, this creates N intermediate `String` objects and N `StringBuilder` objects — very wasteful.

```java
// ❌ Behind the scenes for each iteration:
// new StringBuilder(result).append(i).toString() → assigned back to result

// ✅ Use StringBuilder explicitly for loops:
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);
}
String result = sb.toString();  // ONE StringBuilder, ONE final String
```

---

**Q13: Can we use `String` in switch statements?**

**Answer**: **Yes**, since **Java 7**. Before that, only `byte`, `short`, `char`, `int`, and enums were allowed.

```java
String command = "START";
switch (command) {
    case "START":   System.out.println("Starting..."); break;
    case "STOP":    System.out.println("Stopping..."); break;
    case "RESTART": System.out.println("Restarting..."); break;
    default:        System.out.println("Unknown command");
}
```

Internally, Java uses the string's `hashCode()` for the switch, then verifies with `equals()`.

---

**Q14: How to convert a `String` to a `char` array and vice versa?**

**Answer**:
```java
// String → char array
String s = "Hello";
char[] chars = s.toCharArray();         // {'H', 'e', 'l', 'l', 'o'}

// char array → String
String s1 = new String(chars);          // "Hello"
String s2 = String.valueOf(chars);      // "Hello"
String s3 = String.copyValueOf(chars);  // "Hello"

// Partial char array → String
String s4 = new String(chars, 1, 3);    // "ell" (offset=1, count=3)
```

---

**Q15: What is the difference between `replace()` and `replaceAll()`?**

**Answer**:
- `replace(char, char)` / `replace(CharSequence, CharSequence)` — Literal replacement. Replaces ALL occurrences, but the search term is treated as a **plain string**.
- `replaceAll(String, String)` — **Regex-based** replacement. The first argument is a regular expression.

```java
String s = "a.b.c";
s.replace(".", "-");       // "a-b-c"    — '.' treated as literal dot
s.replaceAll(".", "-");    // "-----"    — '.' is regex "any character"!
s.replaceAll("\\.", "-");  // "a-b-c"    — escaped dot in regex
```

> [!CAUTION]
> **Common bug**: Using `replaceAll()` when you mean `replace()`. If your search string contains regex special characters (`[ ] . * + ? { } ( ) ^ $ | \`), use `replace()` or escape them with `Pattern.quote()`.

---

**Q16: How to check if a `String` is a palindrome?**

**Answer**:
```java
// Approach 1: Using StringBuilder.reverse()
public boolean isPalindrome(String s) {
    return s.equals(new StringBuilder(s).reverse().toString());
}

// Approach 2: Two-pointer (more efficient, no extra object)
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) return false;
        left++;
        right--;
    }
    return true;
}
```

---

**Q17: Predict the output:**
```java
String s1 = "Hello";
String s2 = "Hello";
s1 = s1.concat(" World");

System.out.println(s1);       // ?
System.out.println(s2);       // ?
System.out.println(s1 == s2); // ?
```

**Answer**:
```
Hello World
Hello
false
```
- `s1.concat(" World")` creates a **new String** `"Hello World"` and `s1` now points to it
- `s2` still points to the original `"Hello"` in the pool — **completely unaffected**
- `s1` and `s2` now point to different objects

This perfectly demonstrates String immutability and why it's safe for the String Pool.

---

**Q18: What is the time complexity of `String.substring()` in Java 7+?**

**Answer**: **O(n)** where n is the length of the substring.

In Java 6, `substring()` was O(1) because it shared the underlying `char[]` with the original string (just stored a different offset and length). But this caused **memory leaks** — a small substring could keep a very large char array alive.

From Java 7+, `substring()` creates a **new char array** — O(n) time, but no memory leak risk.

---

**Q19: What is the `compareTo()` method in String?**

**Answer**: `compareTo()` performs **lexicographic comparison** (dictionary order) based on Unicode values.

Returns:
- `0` if strings are equal
- **Negative** if calling string comes before the argument
- **Positive** if calling string comes after the argument

```java
"apple".compareTo("banana");     // negative (a < b)
"banana".compareTo("apple");     // positive (b > a)
"apple".compareTo("apple");      // 0 (equal)
"Apple".compareTo("apple");      // negative (A=65 < a=97)
```

Used by `TreeSet`, `TreeMap`, and `Collections.sort()` for natural ordering of strings.

---

**Q20: Can you create a `String` without using `new` keyword and without using a literal?**

**Answer**: Yes, several ways:
```java
// 1. Using String.valueOf()
String s1 = String.valueOf(42);              // "42"

// 2. Using StringBuilder/StringBuffer
String s2 = new StringBuilder("Hi").toString();

// 3. Using char array
String s3 = String.valueOf(new char[]{'H', 'i'});

// 4. Using concat
String s4 = "".concat("Hello");

// 5. Using String.format()
String s5 = String.format("Hello %s", "World");

// 6. Using String.join()
String s6 = String.join("-", "A", "B", "C");
```

---

### Category B: Wrapper Class Questions (12 Questions)

---

**Q21: What is autoboxing and unboxing?**

**Answer**: 
- **Autoboxing**: Automatic conversion of primitive → wrapper (`int` → `Integer`)
- **Unboxing**: Automatic conversion of wrapper → primitive (`Integer` → `int`)

Introduced in Java 5. The compiler inserts `Integer.valueOf(n)` for autoboxing and `obj.intValue()` for unboxing.

```java
List<Integer> list = new ArrayList<>();
list.add(10);              // Autoboxing: 10 → Integer.valueOf(10)
int val = list.get(0);     // Unboxing: Integer → list.get(0).intValue()
```

---

**Q22: What is the Integer Cache? Why does it exist?**

**Answer**: Java caches `Integer` objects for values **-128 to 127**. When you create an Integer in this range via autoboxing or `valueOf()`, the cached instance is returned instead of creating a new object.

```java
Integer a = 127, b = 127;
a == b;    // true — same cached object

Integer c = 128, d = 128;
c == d;    // false — different objects (outside cache)
```

**Why?** Small integers are used extremely frequently in typical programs. Caching them saves memory and reduces garbage collection pressure.

The upper limit can be increased via JVM flag: `-XX:AutoBoxCacheMax=<size>`.

---

**Q23: Predict the output:**
```java
Integer a = 1000, b = 1000;
Integer c = 100, d = 100;
System.out.println(a == b);
System.out.println(c == d);
```

**Answer**:
```
false    — 1000 is outside cache range (-128 to 127), different objects
true     — 100 is within cache range, same cached object
```

---

**Q24: What happens when you unbox a `null` wrapper?**

**Answer**: **`NullPointerException`**.

```java
Integer x = null;
int y = x;              // NPE! Compiler inserts x.intValue() → calls method on null

// Common real-world scenario:
Map<String, Integer> map = new HashMap<>();
int count = map.get("key");    // NPE! get() returns null when key is absent
```

**Prevention**:
```java
int count = map.getOrDefault("key", 0);                // Safe default
Integer value = map.get("key");
if (value != null) { int count = value; }              // Null check
int count = Optional.ofNullable(map.get("key")).orElse(0); // Optional
```

---

**Q25: Why can't we use primitives with generics? (e.g., `List<int>` is illegal)**

**Answer**: Generics in Java work through **type erasure** — at runtime, `List<Integer>` becomes just `List<Object>`. Since primitives are NOT objects and don't extend `Object`, they can't be used as type parameters.

```java
List<int> list;           // ❌ Compile error
List<Integer> list;       // ✅ Must use wrapper

// Java solves this with autoboxing:
List<Integer> list = new ArrayList<>();
list.add(5);              // Autoboxing: int → Integer
int val = list.get(0);    // Unboxing: Integer → int
```

---

**Q26: What is the difference between `Integer.parseInt()` and `Integer.valueOf()`?**

**Answer**:
- `parseInt(String)` → Returns **`int`** (primitive)
- `valueOf(String)` → Returns **`Integer`** (object) — may use cache

```java
int a = Integer.parseInt("42");      // int (primitive)
Integer b = Integer.valueOf("42");   // Integer (object, cached if -128 to 127)
Integer c = Integer.valueOf(42);     // Integer from int (may be cached)
```

**When to use**: If you need a primitive, use `parseInt()`. If you need an object, use `valueOf()` (takes advantage of caching).

---

**Q27: `Double d1 = 0.1 + 0.2;` — What is the value? Is it 0.3?**

**Answer**: **No!** It's `0.30000000000000004`.

Floating-point numbers use binary representation (IEEE 754), and 0.1 and 0.2 cannot be represented exactly in binary — just like 1/3 can't be represented exactly in decimal.

```java
System.out.println(0.1 + 0.2);           // 0.30000000000000004
System.out.println(0.1 + 0.2 == 0.3);    // false!
```

**For precise calculations** (financial, medical), use `BigDecimal`:
```java
BigDecimal a = new BigDecimal("0.1");
BigDecimal b = new BigDecimal("0.2");
BigDecimal c = a.add(b);
System.out.println(c);                    // 0.3 — exact!
```

> [!TIP]
> **From Your Project**: In your Healthcare project, if you deal with billing, medication dosages, or any financial calculations, always use `BigDecimal`, never `double` or `float`.

---

**Q28: Can wrapper classes be used as keys in `HashMap`?**

**Answer**: **Yes**, and they work perfectly because:
1. All wrapper classes properly override `equals()` and `hashCode()` (following the contract)
2. All wrapper classes are **immutable** — their hashcode never changes after being used as a key
3. They implement `Comparable` — can also be used in `TreeMap`

```java
Map<Integer, String> map = new HashMap<>();
map.put(1, "One");
map.put(2, "Two");
map.get(1);           // "One" — works perfectly
```

---

### Category C: Enum Questions (10 Questions)

---

**Q29: What is an Enum in Java? How is it different from a class?**

**Answer**: An Enum is a **special type of class** that represents a fixed set of constants. It is more than a simple collection of named constants — it's a full class with fields, constructors, and methods.

Key differences from regular classes:
- Constants are implicitly `public static final`
- Constructor is always **private** (can't create instances with `new`)
- Implicitly extends `java.lang.Enum` (so can't extend other classes)
- Can implement interfaces
- Has built-in methods: `values()`, `valueOf()`, `name()`, `ordinal()`
- Guaranteed to be **singleton** per constant — thread-safe by JVM guarantee

---

**Q30: Can an Enum extend a class?**

**Answer**: **No**. Every enum implicitly extends `java.lang.Enum`. Since Java doesn't support multiple inheritance, an enum cannot extend any other class. However, an enum **can implement interfaces**.

```java
// ❌ Not possible
// enum Color extends SomeClass { }

// ✅ Possible
enum Color implements Serializable, Comparable<Color> {
    RED, GREEN, BLUE;
}
```

---

**Q31: Can we create an instance of Enum using `new`?**

**Answer**: **No**. Enum constructors are implicitly `private`. You cannot instantiate an enum using `new`, even from within the enum class itself (outside the constant declarations). The JVM creates enum instances when the class is loaded.

```java
// Color c = new Color();   // ❌ Compile error — enum type cannot be instantiated
Color c = Color.RED;        // ✅ Use the predefined constants
```

---

**Q32: Can Enum have a constructor? If yes, what are the rules?**

**Answer**: **Yes**. Rules:
1. Constructor must be **`private`** (or package-private, but `private` is recommended)
2. Cannot be `public` or `protected`
3. Constructor is called **automatically** for each enum constant
4. Called exactly once per constant when the class is loaded

```java
enum Size {
    SMALL(10), MEDIUM(20), LARGE(30);   // Each calls Size(int)
    
    private final int value;
    
    private Size(int value) {     // private constructor
        this.value = value;
    }
    
    public int getValue() { return value; }
}
```

---

**Q33: How to iterate over all enum constants?**

**Answer**: Use the `values()` method (compiler-generated):
```java
for (Day d : Day.values()) {
    System.out.println(d.name() + " at position " + d.ordinal());
}

// Or using EnumSet
EnumSet.allOf(Day.class).forEach(System.out::println);

// Or using Stream
Arrays.stream(Day.values()).filter(d -> d.ordinal() > 4).forEach(System.out::println);
```

---

**Q34: What is the difference between `name()` and `toString()` in Enum?**

**Answer**:
- `name()`: Returns the **exact name** as declared. Cannot be overridden. Always returns the constant name.
- `toString()`: Returns the name by default, but **can be overridden** to return a custom string.

```java
enum Status {
    ACTIVE, INACTIVE;
    
    @Override
    public String toString() {
        return name().charAt(0) + name().substring(1).toLowerCase();
    }
}

Status s = Status.ACTIVE;
s.name();        // "ACTIVE" — always exact
s.toString();    // "Active" — our custom format

// Reverse lookup — always use name(), never toString()
Status s2 = Status.valueOf("ACTIVE");     // ✅ Works
// Status s3 = Status.valueOf("Active");  // ❌ IllegalArgumentException
```

---

**Q35: Can Enum implement the Singleton pattern? Why is it considered the best approach?**

**Answer**: **Yes**, and it's the best Singleton implementation (recommended by Joshua Bloch, author of *Effective Java*).

```java
public enum Singleton {
    INSTANCE;
    
    private int count = 0;
    
    public void increment() { count++; }
    public int getCount() { return count; }
}

// Usage
Singleton.INSTANCE.increment();
```

**Why best?**
1. **Thread-safe**: JVM guarantees single instantiation
2. **Serialization-safe**: JVM handles enum serialization — no extra `readResolve()` needed
3. **Reflection-safe**: `Constructor.newInstance()` throws `IllegalArgumentException` for enums
4. **No boilerplate**: No `private` constructor, `volatile` instance, double-checked locking, etc.

---

**Q36: What is `EnumSet`? Why prefer it over `HashSet` for enums?**

**Answer**: `EnumSet` is a specialized `Set` for enum types. It uses a **bit-vector** internally — each bit represents an enum constant (present or absent).

```java
EnumSet<Day> weekend = EnumSet.of(Day.SATURDAY, Day.SUNDAY);
```

Why prefer over `HashSet`:
- **Space**: Uses one bit per constant vs. full object references in HashSet
- **Speed**: Bit operations (`&`, `|`) vs. hash computation and collision handling
- **Iteration**: Guaranteed to iterate in enum declaration order

---

**Q37: Predict the output:**
```java
enum Fruit {
    APPLE, BANANA, CHERRY;
}

Fruit f1 = Fruit.APPLE;
Fruit f2 = Fruit.APPLE;
Fruit f3 = Fruit.valueOf("APPLE");

System.out.println(f1 == f2);           // ?
System.out.println(f1 == f3);           // ?
System.out.println(f1.equals(f2));      // ?
System.out.println(f1.ordinal());       // ?
```

**Answer**:
```
true     — enum constants are singletons
true     — valueOf returns the same singleton instance
true     — equals also returns true (uses == internally)
0        — APPLE is the first constant (0-indexed)
```

**Key insight**: For enums, `==` and `.equals()` behave identically because each constant is a singleton. In fact, `Enum.equals()` is implemented as `return this == obj`. Using `==` for enums is perfectly fine and even preferred (null-safe, faster).

---

**Q38: Can we use `==` to compare Enums? Is it safe?**

**Answer**: **Yes, and it's recommended!** Unlike wrapper classes and Strings where `==` compares references and can give wrong results, enum constants are **singletons** guaranteed by the JVM. Each constant exists exactly once, so `==` always works correctly for enums.

```java
Status s = Status.ACTIVE;

// Both are correct for enums
s == Status.ACTIVE       // ✅ Preferred — null-safe, fast
s.equals(Status.ACTIVE)  // ✅ Also works, but unnecessary

// Bonus: == is null-safe!
Status s = null;
s == Status.ACTIVE        // false — no NPE
s.equals(Status.ACTIVE)   // ❌ NPE! Calling method on null
```

---

### Category D: Inner Class Questions (10 Questions)

---

**Q39: What are the 4 types of inner classes in Java?**

**Answer**:

| Type | Static? | Where Defined | Needs Outer Instance? | Example Use Case |
|------|---------|---------------|-----------------------|-----------------|
| Member Inner Class | No | Inside class | ✅ Yes | Iterator implementation |
| Static Nested Class | Yes | Inside class | ❌ No | Builder pattern, entry in Map |
| Local Inner Class | No | Inside method | ❌ (but needs effectively final vars) | One-off helper in a method |
| Anonymous Inner Class | No | Inline expression | ❌ | Event listeners, Comparators |

---

**Q40: What is the difference between a member inner class and a static nested class?**

**Answer**: The key difference is the **relationship with the outer class**:

- **Member inner class**: Has an implicit reference to the outer class instance. Each inner object is tied to a specific outer object. Can access all outer class members (including private instance members).
  
- **Static nested class**: No reference to any outer class instance. It's essentially a top-level class nested inside another for organizational purposes. Can only access static members of the outer class directly.

```java
// Member inner class — needs outer object
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();

// Static nested class — independent
Outer.StaticNested nested = new Outer.StaticNested();
```

**When to choose**: Use static nested class by default. Only use member inner class when you specifically need access to the outer instance's state.

---

**Q41: Can an inner class access the private members of its outer class?**

**Answer**: **Yes!** This is one of the main reasons inner classes exist. All 4 types of inner classes can access private members of their enclosing class.

```java
class Outer {
    private int secret = 42;
    
    class Inner {
        void reveal() {
            System.out.println(secret);   // ✅ Accesses outer's private field
        }
    }
}
```

The compiler achieves this by generating synthetic accessor methods (package-private bridge methods) in the outer class.

---

**Q42: Can a local inner class access local variables of its enclosing method?**

**Answer**: Yes, but only if the variables are **`final` or effectively final** (never reassigned after initialization).

```java
void process() {
    int x = 10;          // Effectively final (never reassigned)
    int y = 20;
    y = 30;              // Reassigned → NOT effectively final
    
    class Local {
        void test() {
            System.out.println(x);   // ✅ x is effectively final
            // System.out.println(y); // ❌ Compile error — y is not effectively final
        }
    }
}
```

**Why this restriction?** The local variable lives on the stack (destroyed when method returns), but the inner class object may outlive the method. Java copies the variable's value into the inner class. If the variable could change after copying, the copy and original would go out of sync — confusing behavior. Making it `final`/effectively final ensures consistency.

---

**Q43: What is an anonymous inner class? When would you use it?**

**Answer**: An anonymous inner class is a class without a name that is declared and instantiated in a single expression. It's used for one-time implementations.

Use cases:
1. Implementing an interface with a single method (pre-Java 8)
2. Creating event listeners (Swing/Android)
3. Providing custom Comparator
4. Extending a class with small modifications

```java
// Before Java 8
Collections.sort(list, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
});

// After Java 8 — Lambda replaces this in most cases
Collections.sort(list, (a, b) -> a.compareTo(b));
```

**Still needed when**: The interface has multiple methods, you need to extend a class, or you need instance state.

---

**Q44: Can a lambda replace every anonymous inner class?**

**Answer**: **No**. Lambdas can only implement **functional interfaces** (interfaces with exactly one abstract method). Anonymous classes are still needed when:

1. The interface has **multiple abstract methods**
2. You need to **extend a class** (abstract or concrete)
3. You need **instance variables** in the anonymous class
4. You need `this` to refer to the **anonymous class itself** (in lambdas, `this` refers to the enclosing class)

---

**Q45: Predict the output:**
```java
public class Test {
    int x = 10;
    
    void test() {
        int x = 20;
        
        Runnable r = new Runnable() {
            int x = 30;
            
            @Override
            public void run() {
                System.out.println(x);            // ?
                System.out.println(this.x);       // ?
                System.out.println(Test.this.x);  // ?
            }
        };
        r.run();
    }
    
    public static void main(String[] args) {
        new Test().test();
    }
}
```

**Answer**:
```
30     — inner class's own x (closest scope)
30     — 'this' refers to the anonymous inner class → this.x = 30
10     — Test.this refers to the outer class → outer x = 10
```

The local variable `x = 20` is **shadowed** by the anonymous class's field `x = 30`. It cannot be accessed from within the anonymous class.

---

**Q46: How many `.class` files are generated for inner classes?**

**Answer**: Each inner class generates its own `.class` file:

| Type | File Name |
|------|-----------|
| Outer class | `Outer.class` |
| Member inner class | `Outer$Inner.class` |
| Static nested class | `Outer$StaticNested.class` |
| Local inner class | `Outer$1Local.class` |
| Anonymous inner class | `Outer$1.class`, `Outer$2.class`, etc. |

You can verify this by running `javac` and checking the output directory.

---

**Q47: Can an inner class be `private`?**

**Answer**: **Yes!** Unlike top-level classes (which can only be `public` or package-private), inner classes can have **any access modifier**: `public`, `protected`, `default`, or `private`.

A `private` inner class can only be accessed from within its outer class — perfect for implementation details that shouldn't be exposed.

```java
public class LinkedList<E> {
    // Private inner class — implementation detail
    private static class Node<E> {
        E data;
        Node<E> next;
    }
}
```

`HashMap.Entry`, `ArrayList`'s internal `Itr` (Iterator) class — these are all real-world examples of inner classes in the JDK.

---

### Category E: Mixed Tricky Questions (8 Questions)

---

**Q48: Predict the output:**
```java
String s1 = "Java";
String s2 = "Java";
StringBuilder sb1 = new StringBuilder("Java");
StringBuilder sb2 = new StringBuilder("Java");

System.out.println(s1 == s2);           // ?
System.out.println(s1.equals(s2));      // ?
System.out.println(sb1 == sb2);         // ?
System.out.println(sb1.equals(sb2));    // ?
```

**Answer**:
```
true     — same String Pool reference
true     — String.equals() compares content
false    — different objects on heap
false    — StringBuilder does NOT override equals()! Uses Object.equals() which is ==
```

**Key insight**: `StringBuilder` does **NOT** override `equals()` and `hashCode()`. Comparing StringBuilders with `equals()` gives the same result as `==`. To compare content: `sb1.toString().equals(sb2.toString())`.

---

**Q49: Why are Strings preferred as `HashMap` keys?**

**Answer**: Strings are ideal HashMap keys because:
1. **Immutable** — hashcode can't change after insertion (changing hashcode would "lose" the entry)
2. **Caches hashcode** — `String` caches its hash in a field, so `hashCode()` is computed only once, even if called multiple times
3. **Proper `equals()` and `hashCode()`** — String correctly overrides both methods, following the contract
4. **Human-readable** — easy to debug and log

If you use a mutable object as a key and modify it after insertion, its hashcode changes, and you can never retrieve the entry again — it's effectively "lost" in the wrong bucket.

---

**Q50: What is the output of `"abc".toUpperCase() == "ABC"`?**

**Answer**: **`false`**

`toUpperCase()` creates a **new String object** on the heap, not in the pool. So `==` compares references and finds they're different. Use `equals()`:

```java
"abc".toUpperCase() == "ABC";           // false
"abc".toUpperCase().equals("ABC");      // true
```

---

**Q51: Can we extend the `String` class and override its methods?**

**Answer**: **No**. `String` is declared as `final class`, so it cannot be extended. This is by design to ensure immutability and security guarantees can never be broken by a subclass.

---

**Q52: What is the difference between `String.valueOf(null)` and `null.toString()`?**

**Answer**:
```java
String.valueOf(null);   // Returns the string "null" (handles null safely)
String s = null;
s.toString();           // ❌ NullPointerException!
```

`String.valueOf()` has a null check: `return (obj == null) ? "null" : obj.toString();`

---

**Q53: How to count the frequency of each character in a String?**

**Answer**: Multiple approaches:
```java
String s = "programming";

// Approach 1: HashMap
Map<Character, Integer> freq = new HashMap<>();
for (char c : s.toCharArray()) {
    freq.put(c, freq.getOrDefault(c, 0) + 1);
}

// Approach 2: Java 8 Streams
Map<Character, Long> freq2 = s.chars()
    .mapToObj(c -> (char) c)
    .collect(Collectors.groupingBy(c -> c, Collectors.counting()));

// Approach 3: int array (if only lowercase letters)
int[] freq3 = new int[26];
for (char c : s.toCharArray()) {
    freq3[c - 'a']++;
}
```

---

**Q54: What is the output? Why?**
```java
Boolean b1 = Boolean.valueOf("true");
Boolean b2 = Boolean.valueOf("TRUE");
Boolean b3 = Boolean.valueOf("yes");
Boolean b4 = Boolean.valueOf("1");
Boolean b5 = Boolean.valueOf(null);

System.out.println(b1 + " " + b2 + " " + b3 + " " + b4 + " " + b5);
```

**Answer**: `true true false false false`

`Boolean.valueOf(String)` returns `true` ONLY if the string is `"true"` (case-insensitive). Everything else — including `"yes"`, `"1"`, `null`, `"false"`, `"anything"` — returns `false`.

---

**Q55: What is `String.format()` and `System.out.printf()`?**

**Answer**: Both use format specifiers to create formatted strings:

```java
String name = "Angooj";
int age = 28;
double salary = 75000.50;

// String.format() — returns formatted String
String result = String.format("Name: %s, Age: %d, Salary: %.2f", name, age, salary);
// "Name: Angooj, Age: 28, Salary: 75000.50"

// printf — prints formatted output directly
System.out.printf("Name: %-10s Age: %03d%n", name, age);
// "Name: Angooj     Age: 028"
```

Common format specifiers:

| Specifier | Type | Example |
|-----------|------|---------|
| `%s` | String | `"Hello"` |
| `%d` | Integer (decimal) | `42` |
| `%f` | Floating-point | `3.140000` |
| `%.2f` | Float with 2 decimals | `3.14` |
| `%n` | Line separator (platform-independent) | newline |
| `%b` | Boolean | `true` |
| `%c` | Character | `'A'` |
| `%x` | Hexadecimal | `ff` |
| `%o` | Octal | `17` |
| `%-10s` | Left-aligned, 10 chars wide | `"Hello     "` |
| `%010d` | Zero-padded, 10 digits wide | `0000000042` |

---

> [!TIP]
> **Day 2 Completion Checklist** ✅
> - [ ] Can explain String Pool with a diagram
> - [ ] Know all 5 reasons why String is immutable
> - [ ] Can differentiate String vs StringBuilder vs StringBuffer with use cases
> - [ ] Know all important String methods by category
> - [ ] Understand `==` vs `.equals()` for Strings and when each gives what result
> - [ ] Can explain Integer Cache with range and predict `==` behavior
> - [ ] Know autoboxing/unboxing and the null-unboxing trap
> - [ ] Can create enums with fields, constructors, and methods
> - [ ] Know why enum Singleton is the best implementation
> - [ ] Can explain all 4 types of inner classes
> - [ ] Know when anonymous class is needed vs lambda
> - [ ] Can predict output for all tricky questions in this document

---

**Tomorrow (Day 3)**: Exception Handling (Complete) — from basics to custom exceptions, try-with-resources, and all the tricky interview scenarios 🚀
