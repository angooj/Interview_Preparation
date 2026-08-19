# 📘 Day 1 — Java Basics + OOP Fundamentals (Improved Edition)

**Date**: Aug 18, 2026 | **Duration**: ~5 hours
**Goal**: Master Java basics and all 4 OOP pillars with real-world examples

---

## 📑 Table of Contents

1. [JDK vs JRE vs JVM — The Big Picture](#1-jdk-vs-jre-vs-jvm--the-big-picture)
2. [Data Types & Variables](#2-data-types--variables)
3. [Operators](#3-operators)
4. [Control Flow](#4-control-flow)
5. [Arrays](#5-arrays)
6. [Packages & Imports](#6-packages--imports)
7. [OOP — Introduction & Key Concepts](#7-oop--introduction--key-concepts)
8. [OOP Pillar 1 — Encapsulation](#8-oop-pillar-1--encapsulation)
9. [OOP Pillar 2 — Inheritance](#9-oop-pillar-2--inheritance)
10. [OOP Pillar 3 — Polymorphism](#10-oop-pillar-3--polymorphism)
11. [OOP Pillar 4 — Abstraction](#11-oop-pillar-4--abstraction)
12. [Object Class — The Root of Everything](#12-object-class--the-root-of-everything)
13. [Relationships — IS-A vs HAS-A](#13-relationships--is-a-vs-has-a)
14. [Keywords Deep Dive — this, super, static, final](#14-keywords-deep-dive--this-super-static-final)
15. [Constructors](#15-constructors)
16. [Memory Model — Stack vs Heap](#16-memory-model--stack-vs-heap)
17. [Interview Questions & Answers (65+)](#17-interview-questions--answers)

---

## 1. JDK vs JRE vs JVM — The Big Picture

Before diving into Java code, understand the platform. This is asked in almost every fresher/experienced interview.

### Visual Diagram

```
┌─────────────────────────────────────────────────────┐
│                  JDK (Java Development Kit)          │
│  ┌───────────────────────────────────────────────┐  │
│  │              JRE (Java Runtime Environment)    │  │
│  │  ┌─────────────────────────────────────────┐  │  │
│  │  │          JVM (Java Virtual Machine)      │  │  │
│  │  │                                          │  │  │
│  │  │  ┌──────────┐  ┌──────────┐            │  │  │
│  │  │  │ClassLoader│  │Execution │            │  │  │
│  │  │  │ Subsystem │  │  Engine  │            │  │  │
│  │  │  └──────────┘  │(Interpret│            │  │  │
│  │  │                 │ er + JIT)│            │  │  │
│  │  │  ┌──────────┐  └──────────┘            │  │  │
│  │  │  │  Runtime  │  ┌──────────┐            │  │  │
│  │  │  │Data Areas │  │  Native  │            │  │  │
│  │  │  │(Heap,Stack│  │ Method   │            │  │  │
│  │  │  │ etc.)     │  │Interface │            │  │  │
│  │  │  └──────────┘  └──────────┘            │  │  │
│  │  └─────────────────────────────────────────┘  │  │
│  │                                                │  │
│  │  ┌──────────────────────────────────────────┐ │  │
│  │  │     Class Libraries (rt.jar / modules)    │ │  │
│  │  │  java.lang, java.util, java.io, etc.      │ │  │
│  │  └──────────────────────────────────────────┘ │  │
│  └───────────────────────────────────────────────┘  │
│                                                      │
│  ┌──────────────────────────────────────────────┐   │
│  │         Development Tools                     │   │
│  │   javac (compiler), java (launcher),          │   │
│  │   javadoc, jar, jdb (debugger), jshell        │   │
│  └──────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

| Component | What It Is | Contains | Analogy |
|-----------|-----------|----------|---------|
| **JVM** | Virtual machine that **runs** bytecode | ClassLoader, Execution Engine, Memory areas | The **engine** of a car |
| **JRE** | JVM + **libraries** needed to run Java apps | JVM + class libraries (rt.jar) | Engine + **fuel system** |
| **JDK** | JRE + **development tools** | JRE + compiler (javac), debugger (jdb), etc. | Complete **car factory** |

### How Java Code Runs — The Complete Flow

```
 ┌──────────┐     javac      ┌──────────┐      JVM       ┌──────────┐
 │ Hello.java│  ──────────►  │Hello.class│  ──────────►  │  Output  │
 │(Source    │  (Compiler)   │(Bytecode) │  (Interprets  │  on      │
 │ Code)    │               │           │   + JIT)       │  Screen  │
 └──────────┘               └──────────┘               └──────────┘
     
  Human-readable          Platform-independent        Platform-dependent
                          "Write Once"               "Run Anywhere"
```

1. **Write**: `Hello.java` (source code)
2. **Compile**: `javac Hello.java` → produces `Hello.class` (bytecode)
3. **Load**: JVM's ClassLoader loads the `.class` file
4. **Verify**: Bytecode verifier checks for security violations
5. **Execute**: Execution Engine interprets bytecode (or JIT-compiles to native code for speed)

> [!NOTE]
> **Why "Write Once, Run Anywhere"?** Because the bytecode (`.class` file) is platform-independent. The JVM is platform-dependent (different JVM for Windows, Mac, Linux), but it interprets the same bytecode on every platform. So you write code once and it runs on any OS that has a JVM installed.

### Key Interview Points

- **Java is both compiled AND interpreted**: Source → bytecode (compiled), bytecode → machine code (interpreted/JIT)
- **JIT (Just-In-Time) Compiler**: Part of JVM that compiles frequently-used bytecode into native machine code at runtime for better performance. "Hot" methods get compiled to native code.
- **Platform independence**: Bytecode is platform-independent, JVM is platform-dependent

---

## 2. Data Types & Variables

### 2.1 Primitive Data Types

Java has **8 primitive data types**. Think of them as the building blocks — everything else is built on top of these.

| Type | Size | Default Value | Min Value | Max Value | Example |
|------|------|---------------|-----------|-----------|---------|
| `byte` | 1 byte (8 bits) | `0` | -128 | 127 | `byte age = 25;` |
| `short` | 2 bytes (16 bits) | `0` | -32,768 | 32,767 | `short year = 2026;` |
| `int` | 4 bytes (32 bits) | `0` | -2,147,483,648 | 2,147,483,647 | `int salary = 500000;` |
| `long` | 8 bytes (64 bits) | `0L` | -9.2 × 10¹⁸ | 9.2 × 10¹⁸ | `long pop = 8000000000L;` |
| `float` | 4 bytes (32 bits) | `0.0f` | ±1.4 × 10⁻⁴⁵ | ±3.4 × 10³⁸ | `float pi = 3.14f;` |
| `double` | 8 bytes (64 bits) | `0.0d` | ±4.9 × 10⁻³²⁴ | ±1.8 × 10³⁰⁸ | `double price = 99.99;` |
| `char` | 2 bytes (16 bits) | `'\u0000'` | 0 | 65,535 | `char grade = 'A';` |
| `boolean` | ~1 bit* | `false` | — | — | `boolean active = true;` |

> [!TIP]
> **Memory trick for sizes**: **B**oys **S**hould **I**nherit **L**ong **F**amily **D**ynasty **C**arefully — **B**yte(1), **S**hort(2), **I**nt(4), **L**ong(8), **F**loat(4), **D**ouble(8), **C**har(2), **B**oolean(~1)
>
> Integer sizes double: 1 → 2 → 4 → 8 bytes

**Why does Java have specific sizes?** Unlike C/C++ where `int` can be 2 or 4 bytes depending on the platform, Java **fixes** the size of each type across all platforms. This guarantees consistent behavior — part of "Write Once, Run Anywhere."

### 2.2 Literals (How You Write Values in Code)

```java
// Integer literals
int decimal = 42;           // Decimal (base 10) — default
int binary = 0b101010;      // Binary (base 2) — prefix 0b
int octal = 052;            // Octal (base 8) — prefix 0
int hex = 0x2A;             // Hexadecimal (base 16) — prefix 0x
long big = 42L;             // Long literal — suffix L (lowercase l looks like 1, so use L)

// Underscore in literals (Java 7+) — for readability
int million = 1_000_000;    // Same as 1000000
long card = 1234_5678_9012_3456L;
int binary = 0b1010_1010;

// Floating-point literals
double d = 3.14;            // Default is double
float f = 3.14f;            // Must add f/F suffix for float
double scientific = 1.5e3;  // 1500.0 — scientific notation

// Character literals
char c1 = 'A';              // Character
char c2 = 65;               // Unicode value (65 = 'A')
char c3 = '\u0041';         // Unicode escape (0041 = 'A')
char newline = '\n';        // Escape character

// Boolean literal
boolean flag = true;        // Only true or false (not 0 or 1 like C/C++)
```

> [!IMPORTANT]
> **Java has NO unsigned types** (unlike C/C++). All integer types are signed. Java 8 added some unsigned utility methods (`Integer.toUnsignedLong()`, `Integer.divideUnsigned()`), but the types themselves are still signed.

### 2.3 Type Casting

**Widening (Implicit)** — Smaller → Larger (automatic, no data loss)

```
byte → short → int → long → float → double
         char ↗
```

```java
int num = 100;
double d = num;          // ✅ Widening: int → double (automatic)
System.out.println(d);   // 100.0

char c = 'A';
int ascii = c;           // ✅ Widening: char → int
System.out.println(ascii); // 65
```

**Narrowing (Explicit)** — Larger → Smaller (manual cast required, possible data loss)

```java
double d = 99.99;
int num = (int) d;          // ✅ Narrowing: double → int (truncates, does NOT round!)
System.out.println(num);    // 99  ← decimal part is LOST

int big = 130;
byte small = (byte) big;   // ✅ Narrowing: int → byte (overflow!)
System.out.println(small);  // -126  ← overflows because 130 > 127

// Narrowing with precision loss
long l = 123456789123456789L;
float f = l;                // ✅ Widening? Actually LOSES precision!
System.out.println(f);      // 1.23456792E17 (not exact!)
```

> [!CAUTION]
> **Tricky**: `long → float` is considered **widening** (no explicit cast needed) even though `float` has only 6-7 digits of precision while `long` can hold 19 digits. You can **lose precision** without any compiler warning!

### 2.4 Type Promotion in Expressions ⚠️

This is a **favourite interview trick question**. Understand this deeply:

**Rule**: In any arithmetic expression involving `byte`, `short`, or `char`, they are **automatically promoted to `int`** before the operation.

```java
byte a = 10;
byte b = 20;
// byte c = a + b;         // ❌ COMPILE ERROR! 
// Why? Because: a(byte) → promoted to int, b(byte) → promoted to int
//               int + int = int, but you're assigning to byte

int c = a + b;              // ✅ Correct
byte c2 = (byte)(a + b);   // ✅ Also correct — explicit cast
```

**More Type Promotion Rules**:
```java
byte b = 50;
b = b * 2;           // ❌ Error — b * 2 is int (b promoted, 2 is int)
b *= 2;              // ✅ Works! Compound assignment does implicit casting

short s = 10;
s = s + 1;           // ❌ Error — s + 1 is int
s += 1;              // ✅ Works! Same reason — implicit cast
s++;                 // ✅ Works! ++ also has implicit cast

// If one operand is double, result is double
int x = 5;
double y = 2.0;
// int z = x / y;    // ❌ Error — x/y is double
double z = x / y;    // ✅ 2.5

// Integer division vs floating division
int a = 5, b = 2;
System.out.println(a / b);        // 2   ← integer division (truncates)
System.out.println((double)a / b); // 2.5 ← cast one operand to double
System.out.println(a / (double)b); // 2.5 ← same effect
```

> [!IMPORTANT]
> **Why do compound assignment operators have implicit casting?** The Java Language Specification defines `x += y` as `x = (type of x)(x + y)`. The cast is built into the definition. This is a deliberate design choice for convenience, but it can hide bugs:
> ```java
> byte b = 127;
> b += 1;          // No error! But b is now -128 (overflow, silently)
> ```

### 2.5 Variables — Four Types

| Type | Where Declared | Default Value | Lifetime | Scope |
|------|----------------|---------------|----------|-------|
| **Local** | Inside method/block | ❌ None (must initialize) | Method execution | Method/block only |
| **Instance** | Inside class, outside method | ✅ 0/null/false | Object lifetime | Entire class |
| **Static** | Inside class with `static` | ✅ 0/null/false | Class lifetime (shared) | Entire class |
| **Parameter** | Method signature | ❌ None (caller provides) | Method execution | Method only |

```java
public class Patient {
    // Instance variable — each Patient object has its own copy
    String name;              // default: null
    int age;                  // default: 0
    boolean isAdmitted;       // default: false
    
    // Static variable — shared across ALL Patient objects (one copy in memory)
    static int totalPatients = 0;
    
    // Parameter — provided by caller
    public void setAge(int newAge) {   // newAge is a parameter
        // Local variable — MUST be initialized before use
        int tempId = generateId();
        
        // int x;
        // System.out.println(x);  // ❌ Compile error — not initialized
        
        this.age = newAge;
    }
    
    private int generateId() { return totalPatients++; }
}
```

**Special Variable Keywords**:

| Keyword | Purpose | Example |
|---------|---------|---------|
| `transient` | Excluded from serialization | `transient String password;` |
| `volatile` | Always read from main memory (visibility across threads) | `volatile boolean running;` |

> [!TIP]
> **From Your Project**: In your Healthcare project's `Patient` entity, fields like `patientId`, `name`, `age` are **instance variables**. A counter like `totalAdmissions` could be a **static variable**. Inside a service method, temporary calculations use **local variables**.

---

## 3. Operators

### 3.1 All Operator Types

| Category | Operators | Example | Notes |
|----------|-----------|---------|-------|
| **Arithmetic** | `+`, `-`, `*`, `/`, `%` | `10 % 3 = 1` | `%` is modulo (remainder) |
| **Relational** | `==`, `!=`, `<`, `>`, `<=`, `>=` | `5 > 3 → true` | Returns boolean |
| **Logical** | `&&`, `\|\|`, `!` | `true && false → false` | Short-circuit |
| **Bitwise Logical** | `&`, `\|`, `^`, `~` | `5 & 3 → 1` | Non-short-circuit for boolean |
| **Shift** | `<<`, `>>`, `>>>` | `8 >> 1 → 4` | Multiply/divide by 2 |
| **Assignment** | `=`, `+=`, `-=`, `*=`, `/=`, `%=` | `x += 5` | Includes implicit cast |
| **Unary** | `++`, `--`, `+`, `-`, `!`, `~` | `x++`, `!true` | Pre/post increment |
| **Ternary** | `? :` | `(a>b) ? a : b` | Inline if-else |
| **instanceof** | `instanceof` | `obj instanceof String` | Type checking |

### 3.2 Short-Circuit Evaluation ⚠️

Understanding short-circuit is crucial — it's used in real code daily and is a frequent interview topic.

```java
// && (Short-circuit AND) — if first is false, second is NOT evaluated
int a = 5, b = 0;
if (b != 0 && a / b > 2) {   // ✅ Safe! a/b never executes because b != 0 is false
    System.out.println("OK");
}

// || (Short-circuit OR) — if first is true, second is NOT evaluated
String name = null;
if (name == null || name.isEmpty()) {  // ✅ Safe! name.isEmpty() never executes because null check passes
    System.out.println("Name is missing");
}

// & (Non-short-circuit AND) — BOTH sides ALWAYS evaluated
if (b != 0 & a / b > 2) {    // ❌ ArithmeticException! a/b is evaluated even though b is 0
    System.out.println("OK");
}
```

**When to use non-short-circuit (`&`, `|`)?**
- When both sides have **side effects** that must execute:
```java
boolean result = validateName(name) & validateAge(age);
// Both validation methods run even if first fails → collect all errors
```

### 3.3 Bitwise Operators — How They Work

These operate on individual bits. Understanding them helps with certain interview problems (check power of 2, swap without temp, etc.).

```java
// Visualized:
//   5 = 0101
//   3 = 0011
//   ────────
// & = 0001 = 1   (AND: both bits must be 1)
// | = 0111 = 7   (OR: at least one bit is 1)
// ^ = 0110 = 6   (XOR: bits must be different)
// ~5= 1010 = -6  (NOT: flip all bits — two's complement)

int a = 5, b = 3;
System.out.println(a & b);   // 1
System.out.println(a | b);   // 7
System.out.println(a ^ b);   // 6
System.out.println(~a);      // -6

// Shift operators
System.out.println(8 << 1);  // 16  — left shift = multiply by 2
System.out.println(8 >> 1);  // 4   — right shift = divide by 2
System.out.println(8 << 3);  // 64  — multiply by 2³ = 8

// Useful tricks:
boolean isPowerOf2 = (n & (n - 1)) == 0;  // Check if n is power of 2
int swapped = a ^ b;                       // XOR swap (without temp variable)
```

### 3.4 Pre-increment vs Post-increment ⚠️

```java
int a = 5;
int b = a++;    // Post: b = 5 (use THEN increment → a becomes 6)
int c = ++a;    // Pre:  a becomes 7 FIRST, then c = 7

System.out.println("a=" + a + " b=" + b + " c=" + c);  
// Output: a=7 b=5 c=7
```

**Tricky combination** (common interview question):
```java
int x = 10;
x = x++;        // What is x?
// Step 1: temp = x (10)
// Step 2: x = x + 1 (11)
// Step 3: x = temp (10)  ← Assignment from step 1's saved value!
System.out.println(x);  // 10! Not 11!
```

### 3.5 instanceof Operator

```java
Object obj = "Hello";
System.out.println(obj instanceof String);    // true
System.out.println(obj instanceof Integer);   // false
System.out.println(obj instanceof Object);    // true (everything is Object)
System.out.println(null instanceof String);   // false (null is never instanceof anything)
System.out.println(null instanceof Object);   // false

// Java 16+ Pattern Matching (important for modern interviews)
if (obj instanceof String str) {     // Cast + assign in one step
    System.out.println(str.length());  // No explicit cast needed!
}
```

### 3.6 Operator Precedence (Simplified)

You don't need to memorize the full table. Just remember this hierarchy:

```
Highest Priority
  ↓  ()                              Parentheses (always wins)
  ↓  ++ -- ! ~ (unary)              Unary operators
  ↓  * / %                           Multiplication, division, modulo
  ↓  + -                             Addition, subtraction
  ↓  << >> >>>                       Shift operators
  ↓  < > <= >= instanceof           Relational
  ↓  == !=                           Equality
  ↓  & → ^ → |                      Bitwise (AND, XOR, OR)
  ↓  && → ||                         Logical (AND, OR)
  ↓  ? :                             Ternary
  ↓  = += -= *= /= etc.             Assignment
Lowest Priority
```

> [!TIP]
> **Golden Rule**: When in doubt, use **parentheses** `()` to make your intent clear. It's also better for readability.

---

## 4. Control Flow

### 4.1 if-else

```java
int score = 85;

if (score >= 90) {
    System.out.println("Grade A");
} else if (score >= 80) {
    System.out.println("Grade B");     // ← This executes
} else if (score >= 70) {
    System.out.println("Grade C");
} else {
    System.out.println("Grade D");
}

// Ternary — concise if-else for simple cases
String result = (score >= 60) ? "Pass" : "Fail";
```

### 4.2 switch (Traditional + Enhanced)

**Traditional switch**:
```java
int day = 3;
switch (day) {
    case 1: System.out.println("Monday"); break;
    case 2: System.out.println("Tuesday"); break;
    case 3: System.out.println("Wednesday"); break;   // ← Executes
    default: System.out.println("Other");
}
// ⚠️ Without break → "fall-through" to next case! (Common bug AND common interview question)
```

**Enhanced switch (Java 14+)** — No `break` needed, can return values:
```java
String dayName = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    case 6, 7 -> "Weekend";      // Multiple values in one case
    default -> {
        String msg = "Unknown day: " + day;
        yield msg;                // 'yield' for multi-line blocks
    }
};
```

**What types can switch use?**

| Type | Supported? | Since |
|------|-----------|-------|
| `byte`, `short`, `char`, `int` | ✅ | Java 1.0 |
| `Byte`, `Short`, `Character`, `Integer` (wrappers) | ✅ | Java 5 |
| `enum` | ✅ | Java 5 |
| `String` | ✅ | **Java 7** |
| `long`, `float`, `double`, `boolean` | ❌ | — |

### 4.3 Loops

```java
// for loop — know exactly how many times
for (int i = 0; i < 5; i++) {
    System.out.println(i);    // 0, 1, 2, 3, 4
}

// while loop — check condition FIRST, then execute
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}

// do-while loop — execute FIRST, then check (runs at LEAST once)
int j = 10;
do {
    System.out.println(j);    // Prints 10 even though j > 5
} while (j < 5);              // Condition is false, but loop ran once!

// for-each (enhanced for) — iterate collections/arrays cleanly
int[] nums = {1, 2, 3, 4, 5};
for (int num : nums) {
    System.out.println(num);   // Can't access index, can't modify array
}
```

> [!NOTE]
> **for-each limitations**: You cannot access the index, cannot modify the original array/collection, and cannot iterate backwards. Use a regular `for` loop when you need these features.

### 4.4 break, continue, labeled break ⚠️

```java
// break — exit the loop entirely
for (int i = 0; i < 10; i++) {
    if (i == 5) break;            // Stops at 5
    System.out.print(i + " ");    // 0 1 2 3 4
}

// continue — skip current iteration, go to next
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) continue;    // Skip even numbers
    System.out.print(i + " ");    // 1 3 5 7 9
}

// Labeled break — break out of OUTER loop (common interview question)
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break outer;           // Breaks the OUTER loop, not just inner
        }
        System.out.println(i + "," + j);
    }
}
// Output: 0,0  0,1  0,2  1,0   (stops at i=1, j=1)

// Without label, break would only exit inner loop:
// Output would be: 0,0  0,1  0,2  1,0  2,0  2,1  2,2
```

---

## 5. Arrays

### 5.1 What is an Array?

An array is a **fixed-size**, **contiguous memory** container that holds elements of the **same type**. Arrays in Java are **objects** (stored on the heap).

```java
// Declaration (no memory allocated yet)
int[] nums;              // Preferred style
int nums2[];             // C-style (valid but discouraged)

// Initialization (memory allocated)
nums = new int[5];       // Array of 5 ints, default value 0
String[] names = new String[3];   // Array of 3 Strings, default null

// Declaration + initialization together
int[] scores = {90, 85, 78, 92, 88};          // Array literal
int[] scores2 = new int[]{90, 85, 78, 92, 88}; // Explicit new

// Accessing elements (0-indexed)
System.out.println(scores[0]);    // 90 (first element)
System.out.println(scores[4]);    // 88 (last element)
// System.out.println(scores[5]); // ❌ ArrayIndexOutOfBoundsException!

System.out.println(scores.length); // 5 — length is a FIELD, not a method (no parentheses!)
```

### 5.2 Multi-Dimensional Arrays

```java
// 2D Array (matrix)
int[][] matrix = new int[3][4];     // 3 rows, 4 columns
matrix[0][0] = 1;

int[][] matrix2 = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Iterating 2D array
for (int i = 0; i < matrix2.length; i++) {            // rows
    for (int j = 0; j < matrix2[i].length; j++) {     // columns
        System.out.print(matrix2[i][j] + " ");
    }
    System.out.println();
}

// Jagged Array — rows have different lengths!
int[][] jagged = new int[3][];      // 3 rows, column count unspecified
jagged[0] = new int[]{1, 2};        // Row 0: 2 elements
jagged[1] = new int[]{3, 4, 5};     // Row 1: 3 elements
jagged[2] = new int[]{6};           // Row 2: 1 element
```

### 5.3 Arrays Utility Class (`java.util.Arrays`)

```java
import java.util.Arrays;

int[] arr = {5, 2, 8, 1, 9, 3};

// Sorting
Arrays.sort(arr);                            // [1, 2, 3, 5, 8, 9]
Arrays.sort(arr, 1, 4);                      // Sort only index 1 to 3

// Searching (array MUST be sorted first)
int index = Arrays.binarySearch(arr, 5);     // Returns index of 5

// Printing
System.out.println(Arrays.toString(arr));    // [1, 2, 3, 5, 8, 9]
System.out.println(Arrays.deepToString(matrix2));  // For 2D arrays

// Copying
int[] copy = Arrays.copyOf(arr, arr.length);       // Full copy
int[] partial = Arrays.copyOfRange(arr, 1, 4);     // Copy index 1 to 3

// Filling
int[] filled = new int[5];
Arrays.fill(filled, 42);                           // [42, 42, 42, 42, 42]

// Comparing
int[] a = {1, 2, 3};
int[] b = {1, 2, 3};
System.out.println(a == b);               // false — different objects
System.out.println(Arrays.equals(a, b));  // true — same content!

// Converting to List (⚠️ returns fixed-size list!)
String[] names = {"Angooj", "Rahul", "Priya"};
List<String> list = Arrays.asList(names);
// list.add("New");   // ❌ UnsupportedOperationException — fixed size!
list.set(0, "Updated");  // ✅ Modification is OK
// The original array is ALSO modified! They share the same backing array
```

> [!CAUTION]
> **`Arrays.asList()` trap**: It returns a **fixed-size** list backed by the original array. You cannot `add()` or `remove()`. Changes to the list affect the original array and vice versa. For a mutable copy, use: `new ArrayList<>(Arrays.asList(names))`.

### Array vs ArrayList — Quick Comparison

| Feature | Array | ArrayList |
|---------|-------|-----------|
| Size | Fixed at creation | Dynamic (grows automatically) |
| Type | Primitives + Objects | Objects only (uses wrappers for primitives) |
| Performance | Faster (no boxing) | Slightly slower (autoboxing for primitives) |
| Methods | Just `length` field | Rich API: `add()`, `remove()`, `contains()`, etc. |
| Syntax | `int[] arr = new int[5];` | `List<Integer> list = new ArrayList<>();` |
| Thread-safe | No | No (use `Collections.synchronizedList()` or `CopyOnWriteArrayList`) |

---

## 6. Packages & Imports

### What are Packages?

Packages are **namespaces** that organize classes and prevent name conflicts. Think of them as **folders** in a file system.

```java
// Package declaration — MUST be the first line (before imports)
package com.cognizant.healthcare.service;

// Import specific class
import java.util.ArrayList;
import java.util.HashMap;

// Import all classes from a package (avoid in production — can cause name conflicts)
import java.util.*;

// Static import — import static members directly
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;

// Usage without class prefix:
double area = PI * r * r;          // Instead of Math.PI
double root = sqrt(25);            // Instead of Math.sqrt(25)
```

### Key Packages in Java

| Package | Purpose | Example Classes |
|---------|---------|----------------|
| `java.lang` | Core classes (auto-imported) | `String`, `Object`, `System`, `Math`, `Thread`, wrappers |
| `java.util` | Collections, utilities | `ArrayList`, `HashMap`, `Date`, `Scanner`, `Optional` |
| `java.io` | Input/Output | `File`, `InputStream`, `BufferedReader` |
| `java.nio` | New I/O (channels, buffers) | `Path`, `Files`, `Channels` |
| `java.sql` | Database access | `Connection`, `Statement`, `ResultSet` |
| `java.time` | Date/Time (Java 8) | `LocalDate`, `LocalDateTime`, `Duration` |
| `java.util.concurrent` | Concurrency | `ExecutorService`, `CompletableFuture`, `ConcurrentHashMap` |

> [!NOTE]
> **`java.lang` is automatically imported** in every Java file. That's why you can use `String`, `System`, `Object`, `Math`, etc. without an import statement.

---

## 7. OOP — Introduction & Key Concepts

### Why OOP?

**Before OOP (Procedural Programming)**: Programs were organized as a sequence of functions operating on data. As programs grew, managing data flow became chaotic — functions could modify any data, making bugs hard to track.

**OOP Solution**: Organize code around **objects** that combine data AND behavior. Each object is responsible for its own data.

| Procedural | Object-Oriented |
|-----------|----------------|
| Functions + Data (separate) | Objects = Data + Behavior (together) |
| Global/shared data | Encapsulated data |
| Hard to maintain at scale | Easier to maintain, extend, test |
| C, Pascal, FORTRAN | Java, C++, Python, C# |

### Key OOP Terminology

| Term | Meaning | Real-World Analogy |
|------|---------|-------------------|
| **Class** | Blueprint / template for creating objects | Blueprint of a house |
| **Object** | Instance of a class — actual entity in memory | An actual house built from the blueprint |
| **Method** | Behavior / action an object can perform | Functions of the house (open door, switch light) |
| **Field/Attribute** | Data / state of an object | Properties of the house (color, rooms, area) |
| **Constructor** | Special method to create and initialize an object | The construction process of building a house |

```java
// Class = Blueprint
public class Patient {
    // Fields = State / Data
    String name;
    int age;
    String disease;
    
    // Constructor = Initialization
    public Patient(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Method = Behavior
    public void admit() {
        System.out.println(name + " admitted to hospital");
    }
}

// Objects = Instances (actual patients)
Patient p1 = new Patient("Angooj", 28);     // Object 1
Patient p2 = new Patient("Rahul", 32);      // Object 2 — different data, same blueprint
p1.admit();   // "Angooj admitted to hospital"
p2.admit();   // "Rahul admitted to hospital"
```

---

## 8. OOP Pillar 1 — Encapsulation

### What is it?

> **Encapsulation** = Wrapping data (variables) and code (methods) into a single unit (class) + restricting direct access to internal details.

**Real-world analogy**: A **medicine capsule** 💊 — the medicine (data) is wrapped inside a shell, and you can only interact through defined ways. Or think of a **TV remote** 📺 — you press buttons (public methods), but the internal circuits (private data) are hidden.

### Why is Encapsulation Important?

1. **Data Protection**: Prevents invalid states (negative age, null names)
2. **Controlled Access**: Validation in setters catches bad data at the gate
3. **Flexibility to Change**: You can change internal implementation without breaking external code
4. **Read-only / Write-only fields**: Provide only getter or only setter
5. **Debugging**: If data is wrong, only the setter could have changed it — one place to look

### How to Implement (with real-world validation)

```java
public class Patient {
    // Step 1: Make ALL fields private — hide the data
    private String name;
    private int age;
    private String email;
    private String bloodGroup;
    
    // Step 2: Public getters — controlled READ access
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    // Step 3: Public setters — controlled WRITE access WITH validation
    public void setName(String name) {
        if (name == null || name.trim().isEmpty()) {
            throw new IllegalArgumentException("Patient name cannot be empty");
        }
        this.name = name.trim();
    }
    
    public void setAge(int age) {
        if (age < 0 || age > 150) {
            throw new IllegalArgumentException("Age must be between 0 and 150, got: " + age);
        }
        this.age = age;
    }
    
    public void setEmail(String email) {
        if (email != null && !email.matches("^[\\w.-]+@[\\w.-]+\\.\\w{2,}$")) {
            throw new IllegalArgumentException("Invalid email format: " + email);
        }
        this.email = email;
    }
    
    // Read-only field — only getter, no setter (set only via constructor)
    public String getBloodGroup() {
        return bloodGroup;
    }
    
    public Patient(String name, int age, String bloodGroup) {
        setName(name);           // Use setter for validation even in constructor!
        setAge(age);
        this.bloodGroup = bloodGroup;  // Set once, never changed
    }
}
```

```java
Patient p = new Patient("Angooj", 28, "B+");
// p.age = -5;               // ❌ Compile error — age is private
p.setAge(-5);                 // ❌ Throws IllegalArgumentException
p.setAge(30);                 // ✅ Valid
p.setEmail("bad-email");      // ❌ Throws IllegalArgumentException
p.setEmail("angooj@mail.com"); // ✅ Valid
// p.setBloodGroup("A-");    // ❌ No setter — blood group is read-only
```

> [!TIP]
> **From Your Project**: In your Healthcare project's Patient E-Chart module, encapsulation ensures that patient data (medical records, admission info) can only be modified through validated service methods — critical for healthcare data integrity and compliance.

### Access Modifiers — The Gatekeepers

| Modifier | Same Class | Same Package | Subclass (diff pkg) | Other Package |
|----------|-----------|--------------|---------------------|---------------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| `default` (no keyword) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

**Memory trick** — Think of expanding circles:
```
         ┌──────────────── public ─────────────────┐
         │   ┌──────────── protected ───────────┐  │
         │   │   ┌──────── default ──────────┐  │  │
         │   │   │   ┌──── private ──────┐   │  │  │
         │   │   │   │    Same Class     │   │  │  │
         │   │   │   └───────────────────┘   │  │  │
         │   │   │     Same Package          │  │  │
         │   │   └───────────────────────────┘  │  │
         │   │       Subclass (other package)    │  │
         │   └──────────────────────────────────┘  │
         │              Entire World                │
         └──────────────────────────────────────────┘
```

---

## 9. OOP Pillar 2 — Inheritance

### What is it?

> **Inheritance** = A child class (subclass) acquires properties and behaviours of a parent class (superclass). It represents an **"IS-A"** relationship.

**Real-world analogy**: **Genetics** 🧬 — a child inherits traits from parents. Or: **Vehicle** → **Car**, **Bike**, **Truck**. A car IS-A vehicle.

### Types of Inheritance in Java

```
1. Single:        A → B                B extends A
                  
2. Multilevel:    A → B → C            C extends B, B extends A
                  
3. Hierarchical:  A → B                B & C both extend A
                  A → C
                  
4. ❌ Multiple:   A ──┐                NOT supported with classes
                       ├→ C            (supported with interfaces)
                  B ──┘
                  
5. Hybrid:        Combination           Not directly supported with classes
```

> [!IMPORTANT]
> Java does **NOT** support multiple inheritance with classes to avoid the **Diamond Problem** (ambiguity when two parents have the same method). But you CAN implement **multiple interfaces**.

### Detailed Example

```java
// Parent class (Superclass)
public class Person {
    protected String name;
    protected int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void introduce() {
        System.out.println("Hi, I'm " + name + ", age " + age);
    }
    
    public void eat() {
        System.out.println(name + " is eating");
    }
}

// Child class (Subclass)
public class Patient extends Person {
    private String disease;
    private String doctorName;
    
    public Patient(String name, int age, String disease) {
        super(name, age);          // MUST call parent constructor (first line!)
        this.disease = disease;
    }
    
    // NEW method — specific to Patient
    public void showDiagnosis() {
        System.out.println(name + " diagnosed with: " + disease);
    }
    
    // OVERRIDDEN method — custom version of parent's method
    @Override
    public void introduce() {
        super.introduce();         // Can still call parent's version
        System.out.println("I'm currently being treated for " + disease);
    }
}
```

```java
Patient p = new Patient("Angooj", 28, "Flu");
p.introduce();       // Overridden — calls Patient's version (which also calls super)
p.eat();             // Inherited from Person — works as-is
p.showDiagnosis();   // Patient's own method
```

### Method Overriding Rules ⚠️ (Complete)

| Rule | Valid Example | Invalid Example |
|------|-------------|----------------|
| **Same method signature** | `void draw()` → `void draw()` | `void draw()` → `void draw(int x)` (overloading, not overriding) |
| **Return type: same or covariant** | `Animal get()` → `Dog get()` ✅ | `Dog get()` → `Animal get()` ❌ |
| **Access: same or wider** | `protected void m()` → `public void m()` ✅ | `public void m()` → `protected void m()` ❌ |
| **Exceptions: same, narrower, or none** | `throws IOException` → `throws FileNotFoundException` ✅ | `throws Exception` → `throws IOException, SQLException` ❌ (more) |
| **static methods: cannot override** | — | Static methods are **hidden**, not overridden |
| **final methods: cannot override** | — | Compile error |
| **private methods: not visible** | — | Child's same-name method is a completely new method |
| **Constructors: not inherited** | — | Cannot override what you don't inherit |

### Method Hiding vs Method Overriding

This subtle difference is often tested:

```java
class Parent {
    static void staticMethod() { System.out.println("Parent static"); }   // Static
    void instanceMethod()      { System.out.println("Parent instance"); } // Instance
}

class Child extends Parent {
    static void staticMethod() { System.out.println("Child static"); }    // HIDING
    @Override
    void instanceMethod()      { System.out.println("Child instance"); }  // OVERRIDING
}

Parent p = new Child();
p.staticMethod();    // "Parent static"  ← HIDING: decided by REFERENCE type
p.instanceMethod();  // "Child instance" ← OVERRIDING: decided by OBJECT type
```

| | Method Overriding | Method Hiding |
|---|---|---|
| Applies to | Instance methods | Static methods |
| Resolved at | Runtime (dynamic dispatch) | Compile time (reference type) |
| `@Override` | ✅ Can use | ❌ Cannot use (not technically overriding) |
| Polymorphism | ✅ Yes | ❌ No |

### What IS and IS NOT Inherited

| Inherited ✅ | NOT Inherited ❌ |
|-------------|-----------------|
| `public` methods and fields | `private` methods and fields |
| `protected` methods and fields | Constructors |
| `default` (package-private) — same package only | — |

> [!NOTE]
> **Private members EXIST in child objects** — memory is allocated for them. But the child class **cannot access** them directly. They can be accessed through inherited public/protected methods (getters/setters) of the parent class.

---

## 10. OOP Pillar 3 — Polymorphism

### What is it?

> **Polymorphism** = "Many forms". The same entity (method, operator, reference) behaves differently based on context.

**Real-world analogy**: A person can be a **developer** at work, a **son** at home, a **friend** at a party — same person, different behavior based on context.

### Two Types

### 10.1 Compile-Time Polymorphism (Method Overloading)

**Same method name, different parameters** — the compiler decides which version to call at compile time.

```java
public class MathHelper {
    public int add(int a, int b) {                  return a + b; }
    public int add(int a, int b, int c) {           return a + b + c; }
    public double add(double a, double b) {         return a + b; }
    public String add(String a, String b) {         return a + b; }
}
```

**Overloading Resolution Rules** (how compiler picks which method to call):

```
1. Exact match             →  add(int) called with int → exact match
2. Widening                →  add(long) called with int → int widened to long
3. Autoboxing              →  add(Integer) called with int → autoboxed
4. Var-args                →  add(int...) called with int → last resort
```

**Priority**: Exact match > Widening > Autoboxing > Var-args

```java
class Overloaded {
    void test(int x)     { System.out.println("int"); }
    void test(long x)    { System.out.println("long"); }
    void test(Integer x) { System.out.println("Integer"); }
    void test(int... x)  { System.out.println("varargs"); }
}

new Overloaded().test(5);
// Calls: test(int) — exact match wins
// If test(int) didn't exist → test(long) — widening
// If test(long) didn't exist → test(Integer) — autoboxing
// If test(Integer) didn't exist → test(int...) — var-args
```

**Overloading Ambiguity Trap** ⚠️:
```java
class Tricky {
    void test(int a, long b) { System.out.println("int-long"); }
    void test(long a, int b) { System.out.println("long-int"); }
}

new Tricky().test(5, 10);   // ❌ COMPILE ERROR — Ambiguous!
// Both match equally: 5 can stay int or widen to long
```

### 10.2 Runtime Polymorphism (Method Overriding + Dynamic Method Dispatch)

The JVM decides which overridden method to call at **runtime**, based on the **actual object type**.

```java
class Shape {
    void draw()    { System.out.println("Drawing Shape"); }
    void area()    { System.out.println("Calculating area of generic shape"); }
}

class Circle extends Shape {
    @Override
    void draw()    { System.out.println("Drawing Circle ⭕"); }
    @Override
    void area()    { System.out.println("π × r²"); }
}

class Rectangle extends Shape {
    @Override
    void draw()    { System.out.println("Drawing Rectangle ▬"); }
    @Override
    void area()    { System.out.println("length × width"); }
}
```

```java
// The magic of polymorphism:
Shape[] shapes = { new Circle(), new Rectangle(), new Shape() };

for (Shape s : shapes) {
    s.draw();    // Each calls ITS OWN version!
}

// Output:
// Drawing Circle ⭕      ← Circle's draw()
// Drawing Rectangle ▬    ← Rectangle's draw()
// Drawing Shape           ← Shape's draw()
```

**Why is this powerful?** Because you can write code that works with the **base type** and it automatically works with ALL subtypes — even ones that haven't been written yet! This is the foundation of **extensible, maintainable code**.

> [!TIP]
> **From Your Project**: In your Healthcare project, you might have different types of assessments (Admission Assessment, Discharge Assessment, Follow-up Assessment) all extending a base `Assessment` class. A `processAssessment(Assessment a)` method works with any type — runtime polymorphism handles calling the correct logic.

### Upcasting & Downcasting

```java
// UPCASTING — child → parent reference (implicit, ALWAYS safe)
Shape s = new Circle();         // Circle "upcasted" to Shape reference
s.draw();                        // Circle's draw() — runtime polymorphism still works!
// s.getRadius();                // ❌ Can't access Circle-specific methods through Shape reference

// DOWNCASTING — parent → child reference (explicit, RISKY)
Shape s = new Circle();
Circle c = (Circle) s;          // ✅ Works — actual object IS a Circle
c.getRadius();                   // ✅ Now can access Circle-specific methods

Shape s2 = new Rectangle();
// Circle c2 = (Circle) s2;     // ❌ ClassCastException at runtime! Object is Rectangle, not Circle

// SAFE downcasting — always check first
if (s2 instanceof Circle) {
    Circle c3 = (Circle) s2;     // Safe!
}

// Java 16+ Pattern Matching — even cleaner
if (s2 instanceof Circle circle) {
    circle.getRadius();          // No explicit cast needed!
}
```

### Covariant Return Type

A child class can override a method and return a **subtype** of the parent's return type:

```java
class AnimalFactory {
    Animal create() { return new Animal(); }
}

class DogFactory extends AnimalFactory {
    @Override
    Dog create() { return new Dog(); }    // Returns Dog (subtype of Animal) — ✅ Covariant!
}
```

> [!IMPORTANT]
> **Key Polymorphism Rules to Remember**:
> - Polymorphism works for **instance methods** only
> - It does **NOT** work for **fields** (variables) — resolved by reference type
> - It does **NOT** work for **static methods** — resolved by reference type (method hiding)
> ```java
> class Parent { int x = 10; }
> class Child extends Parent { int x = 20; }
> Parent p = new Child();
> System.out.println(p.x);  // 10 — Parent's x (NO polymorphism for fields!)
> ```

---

## 11. OOP Pillar 4 — Abstraction

### What is it?

> **Abstraction** = Showing only **essential details** while **hiding implementation complexity**.

**Real-world analogy**: An **ATM machine** 🏧 — you see "Withdraw", "Balance", "Transfer" buttons. You don't see the complex banking logic, network calls, security protocols happening behind the scenes. Another example: When you call `list.sort()`, you don't need to know the sorting algorithm used internally.

### Two Ways to Achieve Abstraction

### 11.1 Abstract Classes (0% to 100% abstraction)

An abstract class is a class that **cannot be instantiated** and may contain abstract methods (methods without a body).

```java
public abstract class PaymentProcessor {
    // Regular field
    protected String transactionId;
    
    // Regular constructor
    public PaymentProcessor(String transactionId) {
        this.transactionId = transactionId;
    }
    
    // CONCRETE method — has implementation (shared by all subclasses)
    public void logTransaction() {
        System.out.println("Transaction " + transactionId + " logged at " + LocalDateTime.now());
    }
    
    // ABSTRACT methods — NO implementation (child MUST implement)
    public abstract boolean processPayment(double amount);
    public abstract String getPaymentMethod();
    
    // Template method pattern (combines concrete + abstract)
    public final void executePayment(double amount) {
        System.out.println("Starting " + getPaymentMethod() + " payment...");
        boolean success = processPayment(amount);
        if (success) {
            logTransaction();
            System.out.println("Payment of ₹" + amount + " successful!");
        } else {
            System.out.println("Payment failed!");
        }
    }
}

public class CreditCardProcessor extends PaymentProcessor {
    public CreditCardProcessor(String txnId) { super(txnId); }
    
    @Override
    public boolean processPayment(double amount) {
        System.out.println("Charging credit card...");
        return amount <= 100000;    // Limit check
    }
    
    @Override
    public String getPaymentMethod() { return "Credit Card"; }
}

public class UPIProcessor extends PaymentProcessor {
    public UPIProcessor(String txnId) { super(txnId); }
    
    @Override
    public boolean processPayment(double amount) {
        System.out.println("Processing UPI...");
        return amount <= 200000;
    }
    
    @Override
    public String getPaymentMethod() { return "UPI"; }
}
```

```java
PaymentProcessor processor = new CreditCardProcessor("TXN001");
processor.executePayment(5000);
// Starting Credit Card payment...
// Charging credit card...
// Transaction TXN001 logged at 2026-08-18T10:30:00
// Payment of ₹5000.0 successful!
```

### Abstract Class Rules

| Rule | Detail |
|------|--------|
| `abstract` keyword | Required on class; required on methods without body |
| Instantiation | ❌ Cannot create object directly (`new AbstractClass()` fails) |
| Constructors | ✅ CAN have constructors (called via `super()`) |
| Abstract methods | 0 or more (can have none — just prevents instantiation) |
| Concrete methods | ✅ CAN have methods with body |
| Variables | ✅ Any type (instance, static, final, etc.) |
| `final` | ❌ Cannot be both `abstract` and `final` (contradictory) |
| `static` methods | ✅ Can have static methods (they can't be abstract though) |
| `main()` method | ✅ Can even have `main()` and be run directly! |

### 11.2 Interfaces (100% abstraction — pre-Java 8)

An interface defines a **contract** — a set of methods that implementing classes must provide.

```java
public interface Treatable {
    // Variables are implicitly: public static final (constants)
    int MAX_TREATMENTS = 10;
    
    // Methods are implicitly: public abstract (before Java 8)
    void treat(String medication);
    boolean isRecovered();
    
    // Java 8: default method — has body, can be overridden
    default void printStatus() {
        logInternal("Status check");
        System.out.println("Treatment in progress");
    }
    
    // Java 8: static method — belongs to interface, NOT inherited
    static void guidelines() {
        System.out.println("Follow WHO guidelines");
    }
    
    // Java 9: private method — helper for default methods (not visible to implementors)
    private void logInternal(String msg) {
        System.out.println("[LOG] " + msg);
    }
}
```

### Interface Evolution Across Java Versions

| Java Version | What Interfaces Can Have | Impact |
|-------------|------------------------|--------|
| **Java 7** (and before) | Only `public abstract` methods + `public static final` constants | Pure contracts |
| **Java 8** | + `default` methods (with body) + `static` methods | Added behavior without breaking implementations |
| **Java 9** | + `private` methods (helper for defaults) | Better code reuse within interface |

> **Why were `default` methods added in Java 8?** To enable adding new methods to interfaces (like `forEach()` to `Iterable`, `stream()` to `Collection`) **without breaking** all existing implementations. Without default methods, adding a method to an interface would force ALL implementors to add it — breaking millions of lines of code.

### 11.3 Abstract Class vs Interface — Complete Comparison

| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| Keyword | `extends` | `implements` |
| Multiple | ❌ Single class only | ✅ Multiple interfaces |
| Methods | Abstract + concrete | Abstract + default (Java 8) + static (Java 8) + private (Java 9) |
| Variables | Any type | Only `public static final` |
| Constructors | ✅ Yes | ❌ No |
| Access modifiers (methods) | Any | `public` only (or `private` in Java 9) |
| Access modifiers (fields) | Any | `public static final` only |
| State (instance variables) | ✅ Yes | ❌ No (only constants) |
| `this` reference | ✅ Yes | ❌ No |
| Speed | Slightly faster | Slightly slower (dynamic lookup) |

### When to Use Which? (Interview-Ready Answer)

| Use **Abstract Class** when... | Use **Interface** when... |
|-------------------------------|--------------------------|
| Classes share common **state** (fields) | Defining a **contract** / **capability** |
| You want shared default **behavior** | Unrelated classes need the same feature |
| There's a clear **IS-A** relationship | There's a **CAN-DO** relationship |
| You need constructors | You need **multiple inheritance** |
| Example: `Vehicle` → `Car`, `Bike` | Example: `Serializable`, `Comparable`, `Runnable` |

> [!TIP]
> **Interview Answer Template**: "I use abstract classes when I want to share code among closely related classes that have a common state, like a base `MedicalRecord` class with shared fields. I use interfaces to define capabilities that unrelated classes can have, like a `Printable` interface that both `Patient` and `Invoice` can implement."

### Marker Interfaces (Tagging Interfaces)

A marker interface has **no methods** — it just "marks" a class with a capability.

```java
public interface Serializable { }    // No methods!
public interface Cloneable { }       // No methods!
public interface Remote { }          // No methods!

class Patient implements Serializable {
    // Patient objects can now be serialized — JVM checks for the Serializable marker
}
```

**Modern alternative**: Annotations have largely replaced marker interfaces:
```java
@Entity          // JPA marker — equivalent to a marker interface
@Component       // Spring marker
@FunctionalInterface  // Java 8 marker
```

---

## 12. Object Class — The Root of Everything

**Every class in Java** implicitly extends `java.lang.Object`. It's the root of the entire class hierarchy.

```java
class Patient { }
// is equivalent to:
class Patient extends Object { }
```

### All 11 Methods of Object Class

| Method | Purpose | When to Override |
|--------|---------|-----------------|
| `toString()` | String representation | Always (for logging/debugging) |
| `equals(Object)` | Content equality | When you need logical equality (not reference equality) |
| `hashCode()` | Hash value for hash-based collections | Always override with equals() |
| `getClass()` | Returns runtime class | Never (it's `final`) |
| `clone()` | Creates a copy | When you need object copying |
| `finalize()` | Called before GC (**deprecated**) | Never — use try-with-resources |
| `wait()` | Thread waits for notification | Thread communication scenarios |
| `wait(long)` | Thread waits with timeout | Thread communication scenarios |
| `wait(long, int)` | Thread waits with precise timeout | Thread communication scenarios |
| `notify()` | Wakes up one waiting thread | Thread communication scenarios |
| `notifyAll()` | Wakes up all waiting threads | Thread communication scenarios |

### The equals() and hashCode() Contract ⚠️

This is **one of the most asked interview topics**. Understand it deeply:

```java
public class Patient {
    private String patientId;
    private String name;
    
    // Default equals() from Object: compares references (==)
    // We override to compare by patientId
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;                        // Same reference
        if (o == null || getClass() != o.getClass()) return false;  // Null or different class
        Patient patient = (Patient) o;
        return Objects.equals(patientId, patient.patientId);  // Compare by ID
    }
    
    // THE CONTRACT: if equals() returns true, hashCode() MUST return same value
    @Override
    public int hashCode() {
        return Objects.hash(patientId);    // Based on same fields as equals()
    }
    
    @Override
    public String toString() {
        return "Patient{id='" + patientId + "', name='" + name + "'}";
    }
}
```

**The Contract Rules**:
1. If `a.equals(b)` is `true`, then `a.hashCode() == b.hashCode()` **MUST** be true
2. If `a.hashCode() != b.hashCode()`, then `a.equals(b)` **MUST** be false
3. If `a.hashCode() == b.hashCode()`, `a.equals(b)` **MAY** be true or false (hash collision)
4. `equals()` must be: **reflexive** (`a.equals(a)`), **symmetric** (`a.equals(b) ↔ b.equals(a)`), **transitive** (`a=b, b=c → a=c`), **consistent** (multiple calls return same result), **null-safe** (`a.equals(null)` returns false)

> [!CAUTION]
> **What breaks if you override equals() without hashCode()?** HashMap and HashSet will malfunction:
> ```java
> Patient p1 = new Patient("P001", "Angooj");
> Patient p2 = new Patient("P001", "Angooj");
> p1.equals(p2);  // true (we overrode equals)
> 
> Set<Patient> set = new HashSet<>();
> set.add(p1);
> set.contains(p2);  // false! ← WRONG because hashCode is different
>                     // Different hashCode → different bucket → never compared with equals()
> ```

---

## 13. Relationships — IS-A vs HAS-A

Understanding relationships between classes is important for design discussions in interviews.

### IS-A Relationship (Inheritance)

```java
// Dog IS-A Animal
class Animal { }
class Dog extends Animal { }

// Car IS-A Vehicle
class Vehicle { }
class Car extends Vehicle { }
```

### HAS-A Relationship (Composition / Aggregation)

An object **contains** another object as a field.

```java
// Patient HAS-A Address
class Address {
    String street, city, state;
}

class Patient {
    String name;
    Address address;      // HAS-A relationship
}
```

### Three Types of HAS-A Relationships

| Relationship | Strength | Can Child Exist Without Parent? | Example |
|-------------|----------|-------------------------------|---------|
| **Association** | Weakest | ✅ Yes (both independent) | Doctor ↔ Patient (doctor exists without patient and vice versa) |
| **Aggregation** | Medium | ✅ Yes (child can exist independently) | Department → Professor (professor can exist without department) |
| **Composition** | Strongest | ❌ No (child dies with parent) | House → Room (room can't exist without house) |

```java
// COMPOSITION — strong ownership (Room dies when House is destroyed)
class House {
    private List<Room> rooms;
    
    public House() {
        rooms = new ArrayList<>();
        rooms.add(new Room("Living Room"));   // House CREATES rooms
        rooms.add(new Room("Bedroom"));
    }
    // If House is destroyed, Rooms are also destroyed — they were created by House
}

// AGGREGATION — weak ownership (Engine can exist independently)
class Car {
    private Engine engine;
    
    public Car(Engine engine) {
        this.engine = engine;    // Car RECEIVES engine from outside — doesn't create it
    }
    // If Car is destroyed, Engine still exists — it was created externally
}

// ASSOCIATION — just a relationship, no ownership
class Doctor {
    private List<Patient> patients;    // Doctor knows about patients
}
class Patient {
    private Doctor primaryDoctor;       // Patient knows about doctor
}
// Neither owns the other — both exist independently
```

> [!TIP]
> **Interview Tip**: "In my Healthcare project, Hospital and Department have a **composition** relationship — departments don't exist without a hospital. Doctor and Patient have an **association** — both exist independently. Patient and MedicalRecord have **composition** — records belong to and die with the patient record."

### Composition over Inheritance (Design Principle)

**Prefer composition over inheritance** when there's no clear IS-A relationship.

```java
// ❌ WRONG — Stack extends ArrayList? Stack IS-A ArrayList? No!
class Stack extends ArrayList {
    // Now Stack has methods like get(index), set(index) which break stack semantics
}

// ✅ RIGHT — Stack HAS-A list internally (composition)
class Stack<T> {
    private List<T> elements = new ArrayList<>();
    
    public void push(T item) { elements.add(item); }
    public T pop() { return elements.remove(elements.size() - 1); }
    public T peek() { return elements.get(elements.size() - 1); }
    // Only stack operations are exposed — clean API
}
```

---

## 14. Keywords Deep Dive — this, super, static, final

### 14.1 `this` keyword — 6 Uses

`this` refers to the **current object instance**. It's a reference that the JVM passes implicitly to every instance method.

```java
public class Patient {
    private String name;
    private int age;
    
    // USE 1: Distinguish instance variable from parameter (resolve shadowing)
    public void setName(String name) {
        this.name = name;          // this.name = instance field, name = parameter
    }
    
    // USE 2: Call another method of current class
    public void display() {
        this.validate();           // Equivalent to just validate() — this is implicit
        System.out.println(name);
    }
    
    // USE 3: Call another constructor (constructor chaining) — MUST be first line
    public Patient() {
        this("Unknown", 0);        // Calls the 2-arg constructor
        // Any other code AFTER this()
    }
    
    public Patient(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // USE 4: Pass current object as argument
    public void register(Hospital hospital) {
        hospital.addPatient(this);   // "Add ME to the hospital"
    }
    
    // USE 5: Return current object (enables fluent API / method chaining)
    public Patient withName(String name) {
        this.name = name;
        return this;                 // Return current object
    }
    public Patient withAge(int age) {
        this.age = age;
        return this;
    }
    
    // USE 6: Synchronized block
    public void threadSafeMethod() {
        synchronized(this) {         // Lock on current object
            // Thread-safe code
        }
    }
    
    private void validate() { }
}

// Fluent API / Method chaining (USE 5):
Patient p = new Patient()
    .withName("Angooj")
    .withAge(28);
```

### 14.2 `super` keyword — 3 Uses

`super` refers to the **parent class**.

```java
public class Person {
    protected String name = "Person";
    
    public Person(String name) { this.name = name; }
    public void greet() { System.out.println("Hello from Person"); }
}

public class Doctor extends Person {
    private String name = "Doctor";    // Hides parent's name
    
    // USE 1: Call parent's constructor — MUST be first line
    public Doctor(String name) {
        super(name);                   // Calls Person(String name)
    }
    
    // USE 2: Call parent's method (when overriding)
    @Override
    public void greet() {
        super.greet();                 // "Hello from Person"
        System.out.println("Hello from Doctor");
    }
    
    // USE 3: Access parent's variable (when hidden by child's variable)
    public void showNames() {
        System.out.println(this.name);    // "Doctor" — child's variable
        System.out.println(super.name);   // "Person" — parent's variable
    }
}
```

> [!IMPORTANT]
> - `super()` must be the **first statement** in a constructor
> - `this()` must also be the **first statement** in a constructor
> - Therefore, **CANNOT** use both `this()` and `super()` in the same constructor
> - If you don't write `super()` or `this()`, compiler inserts `super()` automatically

### 14.3 `static` keyword — 4 Uses

`static` means **belongs to the class**, not to any specific object.

```java
public class Patient {
    // USE 1: Static variable — ONE copy shared by ALL objects
    static int totalPatients = 0;
    String name;                      // Each object has its own copy
    
    // USE 2: Static method — called on CLASS, not on object
    public static int getTotalPatients() {
        // Can only access static members directly
        return totalPatients;           // ✅ Static variable
        // return name;                 // ❌ Can't access instance variable
        // this.name;                   // ❌ Can't use 'this'
        // super.something;            // ❌ Can't use 'super'
    }
    
    // USE 3: Static block — runs ONCE when class is first loaded
    static {
        System.out.println("Patient class loaded into memory");
        totalPatients = 0;  // Initialize static variables
    }
    
    // USE 4: Static nested class
    static class PatientStatistics {
        static void report() {
            System.out.println("Total patients: " + totalPatients);
        }
    }
    
    public Patient(String name) {
        this.name = name;
        totalPatients++;    // Shared counter incremented
    }
}
```

```java
Patient p1 = new Patient("Angooj");
Patient p2 = new Patient("Rahul");
System.out.println(Patient.getTotalPatients());  // 2 — accessed via CLASS name ✅
System.out.println(p1.totalPatients);            // 2 — works but bad practice ⚠️
```

**What static methods CAN'T do**:

| From Static Context | Allowed? | Why? |
|---------------------|----------|------|
| Access static variable | ✅ | Belongs to class |
| Call static method | ✅ | Belongs to class |
| Access instance variable | ❌ | No `this` — which object's variable? |
| Call instance method | ❌ | No `this` — on which object? |
| Use `this` | ❌ | No current object in static context |
| Use `super` | ❌ | `super` implies an instance |

**Why is `main()` method static?** Because the JVM needs to call it **before any object exists**. When your program starts, no objects have been created yet — so the entry point must be callable without an object → `static`.

### 14.4 `final` keyword — 3 Uses

`final` means **"cannot be changed/extended/overridden"**.

```java
// USE 1: Final variable — value cannot be reassigned
final int MAX_AGE = 150;
// MAX_AGE = 200;             // ❌ Compile error

// Blank final — initialized later (but only ONCE)
final int id;
id = 100;
// id = 200;                  // ❌ Cannot reassign

// ⚠️ IMPORTANT: final reference ≠ immutable object
final List<String> names = new ArrayList<>();
names.add("Angooj");          // ✅ Modifying object's CONTENT is fine
names.add("Rahul");           // ✅ Still fine
// names = new ArrayList<>(); // ❌ Can't change the REFERENCE

// USE 2: Final method — cannot be overridden by child class
class Animal {
    public final void breathe() {    // All animals breathe the same way
        System.out.println("Breathing...");
    }
}
class Dog extends Animal {
    // @Override
    // public void breathe() { }  // ❌ Compile error — cannot override final method
}

// USE 3: Final class — cannot be extended (no subclass allowed)
public final class String { }       // Java's String class is final!
// class MyString extends String { } // ❌ Cannot extend final class

// Other final classes: Integer, Double, Boolean, all wrapper classes
```

### `final` vs `finally` vs `finalize()` — Classic Interview Question

| | `final` | `finally` | `finalize()` |
|---|---------|-----------|-------------|
| **What** | Keyword | Block | Method |
| **Where** | Variable, method, class | After try-catch | Object class |
| **Purpose** | Prevent modification | Ensure cleanup code ALWAYS runs | Called by GC before destroying object |
| **Status** | ✅ Active | ✅ Active | ⚠️ **Deprecated** (Java 9) |

```java
// finally — ALWAYS executes (even after return!)
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Error: " + e.getMessage());
} finally {
    System.out.println("This ALWAYS executes");  // Close files, connections
}
```

**When does `finally` NOT execute?**
1. `System.exit(0)` is called
2. JVM crashes
3. Thread is killed
4. Infinite loop in try/catch

---

## 15. Constructors

### What is a Constructor?

> A **constructor** is a special block of code called when an object is created with `new`. Its purpose is to **initialize the object's state**.

### Rules
- Same name as the class
- No return type (not even `void`)
- Called automatically with `new`
- If you don't write any constructor, Java provides a **default no-arg constructor**
- If you write **ANY** constructor, the default is **NOT provided**
- Can be `private` (Singleton, Factory, Utility classes)
- Can be overloaded (multiple constructors)
- Cannot be `abstract`, `static`, `final`, or `synchronized`

### Types

```java
public class Patient {
    String name;
    int age;
    String bloodGroup;
    
    // 1. NO-ARG CONSTRUCTOR
    public Patient() {
        this("Unknown", 0, "Unknown");    // Chains to 3-arg constructor
    }
    
    // 2. PARAMETERIZED CONSTRUCTOR
    public Patient(String name, int age) {
        this(name, age, "Unknown");        // Chains to 3-arg constructor
    }
    
    // 3. FULL PARAMETERIZED CONSTRUCTOR (all fields)
    public Patient(String name, int age, String bloodGroup) {
        this.name = name;
        this.age = age;
        this.bloodGroup = bloodGroup;
    }
    
    // 4. COPY CONSTRUCTOR (Java doesn't provide — you write it)
    public Patient(Patient other) {
        this.name = other.name;
        this.age = other.age;
        this.bloodGroup = other.bloodGroup;
    }
}
```

### Constructor Chaining

Constructors can call other constructors to avoid code duplication:

```java
// Within same class — using this()
public Patient() {
    this("Unknown", 0);        // Calls 2-arg constructor — MUST be first line!
}

// Across classes (inheritance) — using super()
public class Doctor extends Person {
    String specialization;
    
    public Doctor(String name, int age, String specialization) {
        super(name, age);              // Calls Person's constructor — MUST be first line!
        this.specialization = specialization;
    }
}
```

### Constructor Execution Order in Inheritance

```java
class A {
    A() { System.out.println("A constructor"); }
}
class B extends A {
    B() { System.out.println("B constructor"); }
}
class C extends B {
    C() { System.out.println("C constructor"); }
}

new C();
// Output: (Parent FIRST, then child — top-down)
// A constructor
// B constructor
// C constructor
```

**Complete execution order with everything**:
```java
class Parent {
    static { System.out.println("1. Parent STATIC block"); }
    { System.out.println("4. Parent INSTANCE block"); }
    Parent() { System.out.println("5. Parent CONSTRUCTOR"); }
}

class Child extends Parent {
    static { System.out.println("2. Child STATIC block"); }
    { System.out.println("6. Child INSTANCE block"); }
    Child() { System.out.println("7. Child CONSTRUCTOR"); }
}

// First time: new Child();
// Output:
// 1. Parent STATIC block       ← Static blocks first (parent → child), ONCE only
// 2. Child STATIC block
// 3. (static blocks done — won't run again for new Child())
// 4. Parent INSTANCE block      ← Instance block BEFORE constructor
// 5. Parent CONSTRUCTOR          ← Parent constructor
// 6. Child INSTANCE block        ← Child instance block BEFORE child constructor
// 7. Child CONSTRUCTOR           ← Finally, child constructor
```

### Constructor vs Method

| Feature | Constructor | Method |
|---------|------------|--------|
| Name | MUST match class name | Any valid name |
| Return type | None (not even void) | Required |
| Called by | `new` keyword | Object reference |
| Inherited? | ❌ No | ✅ Yes |
| Overridden? | ❌ No | ✅ Yes |
| Overloaded? | ✅ Yes | ✅ Yes |
| `this()`/`super()` | ✅ First line | ❌ Not allowed |
| Default provided? | ✅ (if none written) | ❌ No |
| Can be `private`? | ✅ Yes (Singleton) | ✅ Yes |
| Can be `final`? | ❌ No | ✅ Yes |
| Can be `static`? | ❌ No | ✅ Yes |
| Can be `abstract`? | ❌ No | ✅ Yes |

---

## 16. Memory Model — Stack vs Heap

Understanding where data lives in memory is crucial for interviews and real debugging.

### Visual Diagram

```
┌────────── JVM MEMORY ──────────┐
│                                │
│  ┌──── STACK (per thread) ───┐ │     ┌──── HEAP (shared) ──────────────────┐
│  │                           │ │     │                                      │
│  │  main() frame:            │ │     │   ┌─────────────────┐               │
│  │    p ──────────────────────│─│────►│   │  Patient Object  │               │
│  │    x = 10                 │ │     │   │  name ───────────│───┐           │
│  │    y = 20.5               │ │     │   │  age = 28        │   │           │
│  │                           │ │     │   └─────────────────┘   │           │
│  │  setAge() frame:          │ │     │                          │           │
│  │    newAge = 30            │ │     │   ┌─────────────────┐   │           │
│  │                           │ │     │   │  String "Angooj" │◄──┘           │
│  │  (Popped after method     │ │     │   └─────────────────┘               │
│  │   returns)                │ │     │                                      │
│  └───────────────────────────┘ │     │   ┌── String Pool ──────────────┐   │
│                                │     │   │  "Hello"  "World"  "Angooj" │   │
│                                │     │   └─────────────────────────────┘   │
│                                │     └──────────────────────────────────────┘
└────────────────────────────────┘
```

### Stack vs Heap Comparison

| Feature | Stack | Heap |
|---------|-------|------|
| **Stores** | Primitives, method frames, references | Objects, arrays |
| **Access** | LIFO (Last In, First Out) | Random access |
| **Speed** | Very fast | Slower |
| **Size** | Small (per thread) | Large (shared) |
| **Lifetime** | Method scope (auto-cleaned) | Until GC collects |
| **Thread** | Each thread has its own stack | Shared across all threads |
| **Error** | `StackOverflowError` (deep recursion) | `OutOfMemoryError` (too many objects) |

```java
public void example() {
    int x = 10;                      // x (primitive) → STACK
    double y = 20.5;                 // y (primitive) → STACK
    
    Patient p = new Patient("Angooj", 28);
    //     ↑ reference (p) → STACK
    //                       Patient object → HEAP
    //                       "Angooj" string → HEAP (String Pool)
    
    int[] arr = new int[5];
    //    ↑ reference (arr) → STACK
    //                        array object → HEAP
}
// Method returns → x, y, p, arr references are all POPPED from stack
// Patient and array objects remain on HEAP until GC collects them
```

> [!TIP]
> **Interview Gold**: When asked "where is X stored?", remember:
> - **Primitives** inside methods → Stack
> - **Objects** (created with `new`) → Heap
> - **References** (variables that point to objects) → Stack (if local) or Heap (if inside another object)
> - **Static variables** → Metaspace (method area)
> - **String literals** → String Pool (inside Heap)

---

## 16.5 Common Mistakes & Anti-Patterns

These are mistakes that Java developers commonly make. Interviewers sometimes ask about these directly, and avoiding them in your code demonstrates maturity.

### Mistake 1: Using `==` to Compare Objects
```java
// ❌ WRONG
String s1 = new String("Hello");
String s2 = new String("Hello");
if (s1 == s2) { }              // Compares REFERENCES, not content

// ✅ CORRECT
if (s1.equals(s2)) { }         // Compares CONTENT
```

### Mistake 2: Not Overriding `hashCode()` When Overriding `equals()`
```java
// ❌ WRONG — breaks HashMap/HashSet
@Override
public boolean equals(Object o) { ... }
// Missing hashCode()!

// ✅ CORRECT — always override both
@Override
public boolean equals(Object o) { ... }
@Override
public int hashCode() { return Objects.hash(field1, field2); }
```

### Mistake 3: Calling Overridable Methods from Constructor
```java
// ❌ DANGEROUS — child's fields not initialized yet
class Parent {
    Parent() { display(); }      // display() is overridden in Child
    void display() { }
}
class Child extends Parent {
    int x = 10;
    @Override
    void display() {
        System.out.println(x);   // Prints 0, not 10!
    }
}

// ✅ SAFE — use final or private methods in constructors
class Parent {
    Parent() { init(); }
    private void init() { }       // Can't be overridden
}
```

### Mistake 4: Ignoring Access Modifiers (Making Everything Public)
```java
// ❌ WRONG — exposes internal implementation
public class Patient {
    public String name;           // Anyone can set to anything!
    public int age;               // No validation possible
}

// ✅ CORRECT — proper encapsulation
public class Patient {
    private String name;
    private int age;
    public void setAge(int age) {
        if (age < 0 || age > 150) throw new IllegalArgumentException();
        this.age = age;
    }
}
```

### Mistake 5: Confusing Method Overriding with Method Hiding
```java
// ❌ COMMON CONFUSION
class Parent {
    static void greet() { System.out.println("Parent"); }
}
class Child extends Parent {
    static void greet() { System.out.println("Child"); }  // This is HIDING, not overriding!
}
Parent p = new Child();
p.greet();   // "Parent" — no polymorphism for static methods!

// ✅ UNDERSTAND: Polymorphism works ONLY for instance methods
```

### Mistake 6: Using Abstract Class When Interface is More Appropriate
```java
// ❌ OVER-ENGINEERING — forces single inheritance
abstract class Printable {
    abstract void print();
}

// ✅ BETTER — allows multiple capabilities
interface Printable {
    void print();
}
interface Exportable {
    void export();
}
// A class can implement both!
class Report implements Printable, Exportable { ... }
```

### Mistake 7: Integer Division Surprise
```java
// ❌ UNEXPECTED
int a = 5, b = 2;
double result = a / b;        // 2.0, not 2.5!
// Integer / Integer = Integer (truncated), THEN converted to double

// ✅ CORRECT
double result = (double) a / b;  // 2.5 — cast one operand first
```

### Mistake 8: Not Understanding `final` Reference vs Immutability
```java
final List<String> list = new ArrayList<>();
// ❌ THINKING: "list is immutable"
list.add("Hello");               // ✅ This WORKS! Content can change
// list = new ArrayList<>();     // ❌ Only the REFERENCE is final

// For true immutability:
List<String> immutable = List.of("A", "B", "C");   // Java 9+
// immutable.add("D");         // ❌ UnsupportedOperationException
```

## 17. Interview Questions & Answers (65+)

### Category A: Java Platform (5 Questions)

---

**Q1 🟢: What is the difference between JDK, JRE, and JVM?**

**Answer**:
- **JVM** (Java Virtual Machine): Abstract machine that executes bytecode. Contains ClassLoader, Execution Engine (Interpreter + JIT), and runtime memory areas. It's platform-dependent (different JVM for different OS).
- **JRE** (Java Runtime Environment): JVM + standard class libraries (java.lang, java.util, etc.). Needed to **run** Java programs.
- **JDK** (Java Development Kit): JRE + development tools (javac compiler, jdb debugger, jar tool, javadoc). Needed to **develop** Java programs.

**Analogy**: JVM = engine, JRE = engine + fuel system, JDK = complete car factory.

---

**Q2 🟢: Why is Java called "platform-independent"?**

**Answer**: Java source code is compiled into **bytecode** (`.class` files) which is platform-independent — the same bytecode runs on any OS. The JVM (which IS platform-dependent — different JVM for Windows, Mac, Linux) interprets this bytecode. So: "Write Once, Run Anywhere."

The bytecode acts as a **middle layer** between the source code and the native machine code of each platform.

---

**Q3 🟡: What is the JIT compiler?**

**Answer**: JIT (Just-In-Time) compiler is part of the JVM's Execution Engine. It compiles frequently executed bytecode ("hot spots") into **native machine code** at runtime for better performance.

Without JIT, the Interpreter converts bytecode to machine code **line by line** (slow). JIT identifies "hot" methods and compiles them entirely to native code, which runs directly on the CPU (fast). Subsequent calls skip interpretation entirely.

Modern JVMs use **tiered compilation**: C1 (quick compile, basic optimizations) → C2 (slower compile, aggressive optimizations).

---

**Q4 🟢: What is `public static void main(String[] args)` — explain each word.**

**Answer**:
- `public`: Accessible from anywhere (JVM needs to call it from outside)
- `static`: Called without creating an object (no object exists when program starts)
- `void`: Doesn't return anything to the caller (JVM)
- `main`: Method name the JVM looks for as the entry point (convention)
- `String[] args`: Command-line arguments passed when running the program

```java
// Running: java MyApp Hello World
// args = {"Hello", "World"}
```

**Variations that work**: `public static void main(String[] args)`, `public static void main(String args[])`, `public static void main(String... args)`.

---

**Q5 🟡: Can we run a Java program without the `main()` method?**

**Answer**:
- **Java 6 and earlier**: Yes, using a static initializer block (the JVM loaded the class and ran static blocks before looking for main). But the program would end with a "Main method not found" error.
- **Java 7+**: No. The JVM checks for `main()` **first**, before running static blocks. If main is missing, it throws `Error: Main method not found`.

---

### Category B: Data Types & Variables (8 Questions)

---

**Q6 🟢: What are the 8 primitive data types in Java?**

**Answer**: Organized by category:
- **Integer**: `byte` (1B), `short` (2B), `int` (4B), `long` (8B)
- **Floating-point**: `float` (4B), `double` (8B)
- **Character**: `char` (2B — Unicode UTF-16)
- **Boolean**: `boolean` (true/false)

All are stored on the stack (when local), have fixed sizes across all platforms, and have default values when used as instance/static variables.

---

**Q7 🟢: What is the difference between `int` and `Integer`?**

**Answer**:
| Feature | `int` | `Integer` |
|---------|-------|-----------|
| Type | Primitive | Wrapper class (Object) |
| Memory | Stack (4 bytes) | Heap (16+ bytes) |
| Default | `0` | `null` |
| Nullable | ❌ | ✅ |
| Methods | None | `parseInt()`, `valueOf()`, `compareTo()`, etc. |
| Collections | ❌ Can't use | ✅ `List<Integer>` |
| Performance | Faster | Slower (heap allocation, GC) |

Java 5 introduced **autoboxing/unboxing** for automatic conversion between them.

---

**Q8 🟡: Why is `char` 2 bytes in Java?**

**Answer**: Java uses **Unicode** (UTF-16) to represent characters, supporting international scripts (Chinese, Arabic, Hindi, Bengali, etc.). Unicode needs 2 bytes per character. C/C++ uses ASCII which only needs 1 byte but is limited to 128 characters.

---

**Q9 🟡: What is type promotion? Predict the output:**
```java
byte a = 10, b = 30;
byte c = (byte)(a * b);
System.out.println(c);
```

**Answer**: Output: **44**

`a * b = 300`. Both are promoted to `int`, result is `int` 300. Casting to `byte`: 300 in binary is `100101100`. Byte takes last 8 bits: `00101100` = 44. (300 % 256 = 44)

---

**Q10 🟢: What is the difference between `=`, `==`, and `.equals()`?**

**Answer**:
- `=`: **Assignment** operator
- `==`: **Reference comparison** for objects (same memory address?), **value comparison** for primitives
- `.equals()`: **Content comparison** for objects (if properly overridden)

```java
String s1 = new String("Hi"), s2 = new String("Hi");
s1 == s2;          // false — different objects
s1.equals(s2);     // true — same content
```

---

**Q11 🟡: What is the `var` keyword? (Java 10+)**

**Answer**: `var` enables local variable type inference — the compiler determines the type from the initializer.

```java
var name = "Angooj";               // Inferred: String
var list = new ArrayList<String>(); // Inferred: ArrayList<String>
```

**Restrictions**: Only for local variables with initializers. Cannot use for: parameters, return types, fields, or without initialization.

---

**Q12 🟡: What happens if you don't initialize a local variable?**

**Answer**: **Compile error**. Local variables have no default values — you must explicitly assign before use. Instance and static variables DO get defaults (0, null, false).

---

**Q13 🟡: What are the default values of instance variables?**

**Answer**: `byte/short/int` = 0, `long` = 0L, `float` = 0.0f, `double` = 0.0, `char` = '\u0000', `boolean` = false, any Object reference = null.

---

### Category C: OOP Concepts (20 Questions)

---

**Q14 🟢: What are the 4 pillars of OOP? Explain with real-world examples.**

**Answer**:
1. **Encapsulation** (Data Hiding): Wrapping data + methods in a class, hiding internals. *Example*: Bank account — can't modify balance directly, must use deposit/withdraw methods with rules.
2. **Inheritance** (Code Reuse): Child class inherits from parent. *Example*: Savings Account IS-A Bank Account — inherits common features, adds interest.
3. **Polymorphism** (Many Forms): Same action, different behavior. *Example*: `draw()` on Circle draws a circle, on Rectangle draws a rectangle.
4. **Abstraction** (Hide Complexity): Show essential details, hide implementation. *Example*: ATM shows Withdraw/Balance buttons, hides complex banking logic.

---

**Q15 🟢: What is the difference between method overloading and overriding?**

**Answer**:
| Feature | Overloading | Overriding |
|---------|-------------|------------|
| Definition | Same name, **different parameters** | Same name **AND** same parameters |
| Where | Same class (or inherited) | Parent and child class |
| Binding | Compile-time (static) | Runtime (dynamic) |
| Return type | Can differ | Same or covariant |
| Access | Can differ | Same or wider |
| `static` | Can be overloaded | Cannot be overridden (hidden) |
| `private` | Can be overloaded | Cannot be overridden (not visible) |
| Polymorphism | Compile-time | Runtime |

---

**Q16 🟡: Can we override a static method?**

**Answer**: **No**. Static methods are bound at compile time based on the reference type. If a child defines a static method with the same signature, it's called **method hiding**, not overriding. The method called depends on the **reference type**, not the actual object type — no runtime polymorphism.

---

**Q17 🟡: Can we override a private method?**

**Answer**: **No**. Private methods are not visible to child classes, so there's nothing to override. If a child defines a method with the same name, it's a **completely new method**.

---

**Q18 🟢: Can we overload the `main()` method?**

**Answer**: **Yes**. But only `public static void main(String[] args)` is the entry point. Other overloaded versions are just regular static methods.

---

**Q19 🟢: What is the difference between abstract class and interface?**

**Answer**: *(See detailed table in Section 11.3)* Key points: abstract class = partial abstraction + state + single inheritance; interface = contract + no state + multiple inheritance.

---

**Q20 🟡: Can an abstract class have a constructor?**

**Answer**: **Yes**. Called via `super()` from child constructors. Used to initialize common fields inherited by all subclasses.

---

**Q21 🟡: Can an abstract class have no abstract methods?**

**Answer**: **Yes**. Declaring a class `abstract` just prevents direct instantiation. Useful when you want to force subclassing.

---

**Q22 🔴: What is the Diamond Problem? How does Java handle it?**

**Answer**: When a class inherits from two parents that both have the same method — which version to use?

Java prevents it with classes (single inheritance only). With interfaces (Java 8+ default methods), if two interfaces have the same default method, the implementing class **MUST override** it to resolve ambiguity.

---

**Q23 🟡: Why doesn't Java support multiple inheritance with classes?**

**Answer**: To avoid ambiguity (Diamond Problem). Instead, Java provides multiple interface implementation, which originally had no method bodies (no ambiguity). Java 8+ added default methods with mandatory conflict resolution.

---

**Q24 🟡: What is dynamic method dispatch?**

**Answer**: The mechanism by which JVM decides at **runtime** which overridden method to call, based on the actual object type (not reference type). Foundation of runtime polymorphism.

```java
Animal a = new Dog();    // Reference: Animal, Object: Dog
a.sound();               // Calls Dog's sound() — decided at RUNTIME
```

---

**Q25 🔴: Explain upcasting vs downcasting.**

**Answer**: 
- **Upcasting** (child → parent): Implicit, safe. `Animal a = new Dog();`
- **Downcasting** (parent → child): Explicit, risky. `Dog d = (Dog) a;` — may throw `ClassCastException`.

Always check with `instanceof` before downcasting.

---

**Q26 🟡: What is covariant return type?**

**Answer**: When overriding, the child can return a **subtype** of the parent's return type. E.g., parent returns `Animal`, child can return `Dog`.

---

**Q27 🔴: Does polymorphism work for fields (instance variables)?**

**Answer**: **No**! Polymorphism only works for **instance methods**. Fields and static methods are resolved by the **reference type** at compile time.

```java
class Parent { int x = 10; }
class Child extends Parent { int x = 20; }
Parent p = new Child();
System.out.println(p.x);  // 10 — Parent's x! (No polymorphism for fields)
```

---

**Q28 🟡: What is a marker interface? Give examples.**

**Answer**: An interface with **no methods** — just marks a class with a capability. JVM checks for the marker at runtime. Examples: `Serializable`, `Cloneable`, `Remote`. Modern Java uses annotations as markers instead (`@Entity`, `@Component`).

---

**Q29 🟡: What are `default` methods in interfaces? Why were they added?**

**Answer**: Methods with a body in interfaces (Java 8). Added so that new methods (like `stream()`, `forEach()`) could be added to existing interfaces without breaking all implementations.

---

**Q30 🟡: Can we make a constructor private? Why?**

**Answer**: **Yes**. Used for: Singleton (one instance), Factory (controlled creation), Utility classes (only static methods — `Math`).

---

**Q31 🟢: What is the `Object` class? Name its methods.**

**Answer**: Root of all Java classes. Every class implicitly extends `Object`. 11 methods: `toString()`, `equals()`, `hashCode()`, `getClass()`, `clone()`, `finalize()`, `wait()` (3 overloads), `notify()`, `notifyAll()`.

---

**Q32 🟡: Explain the `equals()` and `hashCode()` contract.**

**Answer**: If `a.equals(b)` is `true`, then `a.hashCode() == b.hashCode()` **MUST** be true. Breaking this contract causes HashMap/HashSet to malfunction — an object can be added but never found.

---

**Q33 🔴: What is the difference between Association, Aggregation, and Composition?**

**Answer**:
- **Association**: Two independent objects interact. Neither owns the other. (Doctor ↔ Patient)
- **Aggregation**: One contains the other, but the contained object **CAN exist independently**. (Department ∘─ Professor)
- **Composition**: One contains the other, and the contained object **CANNOT exist independently**. (House ●─ Room)

---

### Category D: Keywords & Constructors (12 Questions)

---

**Q34 🟡: What are all uses of `this` keyword?**

**Answer**: 6 uses: (1) Refer to instance variable, (2) Invoke method, (3) Invoke constructor (`this()`), (4) Pass as argument, (5) Return current object (fluent API), (6) Synchronized block.

---

**Q35 🟡: What are all uses of `super` keyword?**

**Answer**: 3 uses: (1) Call parent constructor, (2) Call parent method, (3) Access parent variable (when hidden).

---

**Q36 🟡: Can `this()` and `super()` be used in the same constructor?**

**Answer**: **No**. Both must be the first statement — mutually exclusive.

---

**Q37 🔴: What is the execution order of static blocks, instance blocks, and constructors?**

**Answer**: Static blocks (parent→child, once) → Instance block → Constructor (parent→child, per `new`).

---

**Q38 🟡: Can you access instance variables from a static method?**

**Answer**: Not directly. Static methods don't have `this`. You can access through an object reference: `new Obj().field`.

---

**Q39 🟢: What is the difference between `final`, `finally`, and `finalize()`?**

**Answer**: `final` = keyword (prevent change/override/extend), `finally` = block (always executes after try/catch), `finalize()` = deprecated method (GC cleanup).

---

**Q40 🟡: Can a `final` method be overloaded?**

**Answer**: **Yes**. `final` prevents overriding, not overloading.

---

**Q41 🟢: Why is `String` class `final`?**

**Answer**: Security (class loading, credentials), thread safety, hashcode caching, String Pool integrity. Prevents subclasses from breaking immutability.

---

**Q42 🟡: What happens if parent has no no-arg constructor and child doesn't call `super(args)`?**

**Answer**: **Compile error**. Compiler inserts `super()` automatically → parent has no no-arg constructor → fail.

---

**Q43 🟡: What is constructor chaining?**

**Answer**: Calling one constructor from another using `this()` (same class) or `super()` (parent class). Avoids code duplication.

---

**Q44 🟡: Can a constructor return a value?**

**Answer**: No return type (not even void). However, a **method** with the same name as the class IS valid (but it's a method, not a constructor).

---

**Q45 🟡: What is the order of constructor execution in inheritance?**

**Answer**: Parent first, then child (top-down). Every constructor calls `super()` first (implicitly or explicitly).

---

### Category E: Memory & Arrays (5 Questions)

---

**Q46 🟡: What is the difference between Stack and Heap memory?**

**Answer**:
| Feature | Stack | Heap |
|---------|-------|------|
| Stores | Primitives, references, method frames | Objects, arrays |
| Access | LIFO, per thread | Shared, GC managed |
| Speed | Very fast | Slower |
| Error | StackOverflowError | OutOfMemoryError |
| Size | Small, fixed | Large, dynamic |

---

**Q47 🟡: Where are String literals stored?**

**Answer**: In the **String Pool**, which is inside the **Heap** (since Java 7). Previously it was in PermGen space (Java 6 and earlier).

---

**Q48 🟡: What is `StackOverflowError`? When does it occur?**

**Answer**: Occurs when the call stack exceeds its size limit — typically from **infinite or very deep recursion**.

```java
void recursive() {
    recursive();    // No base case → StackOverflowError!
}
```

---

**Q49 🟡: What is the difference between `length`, `length()`, and `size()`?**

**Answer**:
- `length` — **field** of **arrays**: `int[] arr; arr.length`
- `length()` — **method** of **String**: `"Hello".length()`
- `size()` — **method** of **Collections**: `list.size()`

---

**Q50 🟡: What is the difference between `Arrays.asList()` and `List.of()`?**

**Answer**:
| Feature | `Arrays.asList()` | `List.of()` (Java 9) |
|---------|-------------------|---------------------|
| Mutable | Partially (can `set()`, can't `add()`/`remove()`) | ❌ Completely immutable |
| Null elements | ✅ Allows | ❌ Throws NPE |
| Backed by array | ✅ Changes reflect in array | ❌ Independent copy |

---

### Category F: Tricky Output Questions (15 Questions)

---

**Q51 🟢: Predict the output:**
```java
System.out.println(10 + 20 + "Hello");
System.out.println("Hello" + 10 + 20);
```

**Answer**: `30Hello` and `Hello1020`

Left to right: `10 + 20` = int addition = 30, then `30 + "Hello"` = string concat. In line 2, `"Hello" + 10` = string concat immediately, then continues as concat.

---

**Q52 🔴: Predict the output:**
```java
class Parent {
    int x = 10;
    Parent() { display(); }
    void display() { System.out.println("Parent x = " + x); }
}
class Child extends Parent {
    int x = 20;
    void display() { System.out.println("Child x = " + x); }
}
public class Test {
    public static void main(String[] args) { new Child(); }
}
```

**Answer**: `Child x = 0`

Parent constructor calls `display()` → overridden → Child's `display()` runs → but Child's `x` isn't initialized yet (still default 0). **Never call overridable methods from constructors!**

---

**Q53 🟡: Predict the output:**
```java
int i = 1;
i = i++ + ++i;
System.out.println(i);
```

**Answer**: `4`. `i++` = use 1 then i→2. `++i` = i→3 then use 3. `1 + 3 = 4`.

---

**Q54 🟡: Predict the output:**
```java
static int x = 10;
static { x = 20; }
public static void main(String[] args) { System.out.println(x); }
static { x = 30; }
```

**Answer**: `30`. Static blocks execute top to bottom when class loads: x=10 → x=20 → x=30.

---

**Q55 🟢: Predict the output:**
```java
try {
    System.out.println("try");
    return;
} finally {
    System.out.println("finally");
}
```

**Answer**: `try` then `finally`. `finally` executes even after `return`.

---

**Q56 🟢: Predict the output:**
```java
Animal a = new Dog();
System.out.println(a.name);    // field
a.display();                    // instance method
a.showType();                   // static method
```
Where `name="Animal"/"Dog"`, `display()` prints class name, `showType()` is static.

**Answer**: `Animal` (field → reference type), `Dog` (instance method → object type), `Animal` (static method → reference type). **Polymorphism only for instance methods!**

---

**Q57 🟡: Predict the output:**
```java
String s1 = "Hello";
String s2 = "Hel" + "lo";
String s3 = "Hel";
String s4 = s3 + "lo";
System.out.println(s1 == s2);
System.out.println(s1 == s4);
```

**Answer**: `true`, `false`. `"Hel" + "lo"` is a compile-time constant → same pool reference. `s3 + "lo"` uses variable → runtime StringBuilder → new heap object.

---

**Q58 🟡: What prints?**
```java
System.out.println(1 == 1.0);
System.out.println('A' == 65);
System.out.println('A' == 65.0);
```

**Answer**: `true`, `true`, `true`. Type promotion: int→double, char→int, char→double. All compare values.

---

**Q59 🟡: Predict the output:**
```java
int x = 10;
x = x++;
System.out.println(x);
```

**Answer**: `10`. Post-increment saves old value (10), increments x to 11, then assigns saved value (10) back. The increment is lost!

---

**Q60 🟡: What is the output?**
```java
final int a = 10;
int b = 20;
System.out.println(a + b == 30);   // compile-time?
```

**Answer**: `true`. `a` is a compile-time constant (`final` + initialized). `a + b` is evaluated normally. Both sides are `int`, comparison works.

---

**Q61 🟡: Can you have an interface method that is both `default` and `static`?**

**Answer**: **No**. A method is either `default` (instance-level, overridable) or `static` (class-level, not overridable). They are mutually exclusive.

---

**Q62 🟡: Predict the output:**
```java
Integer a = new Integer(10);
Integer b = new Integer(10);
System.out.println(a == b);
System.out.println(a.equals(b));
```

**Answer**: `false`, `true`. `new` always creates distinct objects (no cache). `equals()` compares values.

---

**Q63 🟢: What is the difference between `break` and `continue`?**

**Answer**: `break` exits the loop entirely. `continue` skips the current iteration and moves to the next. Both can be labeled to affect outer loops.

---

**Q64 🟡: What is a `static` import?**

**Answer**: Allows using static members without class prefix: `import static java.lang.Math.PI;` → use `PI` directly instead of `Math.PI`.

---

**Q65 🟡: Can an interface extend another interface?**

**Answer**: **Yes**! An interface can `extend` one or more interfaces (multiple inheritance of type is allowed).

```java
interface A { void methodA(); }
interface B { void methodB(); }
interface C extends A, B { void methodC(); }  // ✅ Valid — extends multiple interfaces
```

---

> [!TIP]
> **Day 1 Completion Checklist** ✅
> - [ ] Can explain JDK vs JRE vs JVM with diagram
> - [ ] Know all 8 primitives with sizes, ranges, and defaults
> - [ ] Understand type casting, type promotion, and compound assignment traps
> - [ ] Can declare, initialize, and manipulate 1D, 2D, and jagged arrays
> - [ ] Can explain all 4 OOP pillars with real examples
> - [ ] Know method overloading rules and resolution priority
> - [ ] Know all 7 method overriding rules
> - [ ] Understand method hiding vs method overriding
> - [ ] Know abstract class vs interface differences (pre and post Java 8)
> - [ ] Can list all 11 Object class methods
> - [ ] Understand equals/hashCode contract
> - [ ] Know Association vs Aggregation vs Composition
> - [ ] Can list all 6 uses of `this`, 3 uses of `super`
> - [ ] Understand static restrictions and `final` keyword uses
> - [ ] Can explain constructor chaining and execution order
> - [ ] Understand Stack vs Heap memory with diagram
> - [ ] Can predict output for all tricky questions

---

**Next (Day 2)**: Strings Deep Dive, Wrapper Classes, Enums & Inner Classes 🚀
