# 📘 Day 1 — Java Basics + OOP Fundamentals

**Date**: Aug 18, 2026 | **Duration**: ~4.5 hours
**Goal**: Master Java basics and all 4 OOP pillars with real-world examples

---

## 📑 Table of Contents

1. [Data Types & Variables](#1-data-types--variables)
2. [Operators](#2-operators)
3. [Control Flow](#3-control-flow)
4. [OOP Pillar 1 — Encapsulation](#4-oop-pillar-1--encapsulation)
5. [OOP Pillar 2 — Inheritance](#5-oop-pillar-2--inheritance)
6. [OOP Pillar 3 — Polymorphism](#6-oop-pillar-3--polymorphism)
7. [OOP Pillar 4 — Abstraction](#7-oop-pillar-4--abstraction)
8. [Keywords Deep Dive — this, super, static, final](#8-keywords-deep-dive)
9. [Constructors](#9-constructors)
10. [Interview Questions & Answers (50+)](#10-interview-questions--answers)

---

## 1. Data Types & Variables

### 1.1 Primitive Data Types

Java has **8 primitive data types**. Think of them as the building blocks — everything else is built on top of these.

| Type | Size | Default | Range | Example |
|------|------|---------|-------|---------|
| `byte` | 1 byte (8 bits) | `0` | -128 to 127 | `byte age = 25;` |
| `short` | 2 bytes (16 bits) | `0` | -32,768 to 32,767 | `short year = 2026;` |
| `int` | 4 bytes (32 bits) | `0` | -2.1B to 2.1B | `int salary = 500000;` |
| `long` | 8 bytes (64 bits) | `0L` | Very large | `long population = 8000000000L;` |
| `float` | 4 bytes (32 bits) | `0.0f` | ~6-7 decimal digits | `float pi = 3.14f;` |
| `double` | 8 bytes (64 bits) | `0.0d` | ~15 decimal digits | `double price = 99.99;` |
| `char` | 2 bytes (16 bits) | `'\u0000'` | 0 to 65,535 (Unicode) | `char grade = 'A';` |
| `boolean` | ~1 bit* | `false` | `true` or `false` | `boolean active = true;` |

> [!TIP]
> **Memory trick**: **B**oys **S**hould **I**nherit **L**ong **F**amily **D**ynasty **C**arefully — **B**yte, **S**hort, **I**nt, **L**ong, **F**loat, **D**ouble, **C**har, **B**oolean

### 1.2 Type Casting

**Widening (Implicit)** — Smaller → Larger (automatic, no data loss)
```
byte → short → int → long → float → double
         char ↗
```

```java
int num = 100;
double d = num;   // Widening: int → double (automatic)
System.out.println(d);  // 100.0
```

**Narrowing (Explicit)** — Larger → Smaller (manual cast required, possible data loss)

```java
double d = 99.99;
int num = (int) d;   // Narrowing: double → int (manual cast)
System.out.println(num);  // 99  ← decimal part is LOST, not rounded!
```

### 1.3 Type Promotion in Expressions ⚠️

This is a **favourite interview trick question**:

```java
byte a = 10;
byte b = 20;
// byte c = a + b;    // ❌ COMPILE ERROR! 
// Why? Because a + b is automatically promoted to int

int c = a + b;        // ✅ Correct
byte c2 = (byte)(a + b);  // ✅ Also correct — explicit cast
```

**Rule**: In any arithmetic expression, `byte`, `short`, and `char` are **automatically promoted to `int`** before the operation.

```java
byte b = 50;
b = b * 2;      // ❌ Error — b * 2 becomes int
b *= 2;          // ✅ Works! Compound assignment does implicit casting
```

> [!IMPORTANT]
> **Compound assignment operators** (`+=`, `-=`, `*=`, `/=`) include an **implicit cast**. This is a common interview trick.

### 1.4 Variables

| Type | Where Declared | Default Value | Lifetime |
|------|----------------|---------------|----------|
| **Local variable** | Inside method/block | ❌ No default (must initialize) | Method execution |
| **Instance variable** | Inside class, outside method | ✅ Has defaults (0, null, false) | Object lifetime |
| **Static variable** | Inside class with `static` | ✅ Has defaults | Class lifetime (shared) |

```java
public class Patient {
    // Instance variable — each Patient object has its own copy
    String name;              // default: null
    int age;                  // default: 0
    boolean isAdmitted;       // default: false
    
    // Static variable — shared across ALL Patient objects
    static int totalPatients = 0;
    
    public void display() {
        // Local variable — MUST be initialized before use
        int tempId = 100;     // ✅
        // int x;
        // System.out.println(x);  // ❌ Compile error — not initialized
    }
}
```

**`transient` variable**: Excluded from serialization (covered in Day 7).
**`volatile` variable**: Always read from main memory, not thread's cache (covered in Day 6).

---

## 2. Operators

### 2.1 All Operator Types

| Category | Operators | Example |
|----------|-----------|---------|
| **Arithmetic** | `+`, `-`, `*`, `/`, `%` | `10 % 3 = 1` |
| **Relational** | `==`, `!=`, `<`, `>`, `<=`, `>=` | `5 > 3` → `true` |
| **Logical** | `&&` (short-circuit AND), `\|\|` (short-circuit OR), `!` (NOT) | `true && false` → `false` |
| **Bitwise** | `&` (AND), `\|` (OR), `^` (XOR), `~` (NOT) | `5 & 3` → `1` |
| **Shift** | `<<` (left), `>>` (signed right), `>>>` (unsigned right) | `8 >> 1` → `4` |
| **Assignment** | `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `<<=`, `>>=` | `x += 5` |
| **Unary** | `++`, `--`, `+`, `-`, `!`, `~` | `x++`, `--y` |
| **Ternary** | `? :` | `(a > b) ? a : b` |
| **instanceof** | `instanceof` | `obj instanceof String` |

### 2.2 Short-Circuit Evaluation ⚠️

```java
int a = 5, b = 0;

// && → if first is false, second is NOT evaluated
if (b != 0 && a / b > 2) {  // Safe! Second part skipped
    System.out.println("OK");
}

// & → BOTH sides are ALWAYS evaluated
if (b != 0 & a / b > 2) {   // ❌ ArithmeticException: / by zero
    System.out.println("OK");
}
```

> **Interview Point**: `&&` and `||` are **short-circuit** (lazy). `&` and `|` are **non-short-circuit** (eager). When used with boolean values, `&` and `|` also work as logical operators — but they evaluate both sides.

### 2.3 Pre-increment vs Post-increment ⚠️

```java
int a = 5;
int b = a++;    // Post: b = 5 (assign first, then increment a to 6)
int c = ++a;    // Pre: a becomes 7 first, then c = 7

System.out.println("a=" + a + " b=" + b + " c=" + c);  
// Output: a=7 b=5 c=7
```

### 2.4 Operator Precedence (Most Important Ones)

```
Highest → Lowest:
  ()  →  ++ --  →  * / %  →  + -  →  << >> >>>  →  < > <= >= instanceof
  →  == !=  →  &  →  ^  →  |  →  &&  →  ||  →  ?:  →  = += -= etc.
```

> [!TIP]
> You don't need to memorize the full table. Just remember: **arithmetic > relational > logical > assignment**. Use parentheses `()` when in doubt.

---

## 3. Control Flow

### 3.1 if-else

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
```

### 3.2 switch (Traditional + Enhanced)

**Traditional switch**:
```java
int day = 3;
switch (day) {
    case 1: System.out.println("Monday"); break;
    case 2: System.out.println("Tuesday"); break;
    case 3: System.out.println("Wednesday"); break;   // ← Executes
    default: System.out.println("Other");
}
// Without break → "fall-through" to next case!
```

**Enhanced switch (Java 14+)** — No `break` needed, can return values:
```java
String result = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";     // ← Returns "Wednesday"
    case 6, 7 -> "Weekend";   // Multiple values
    default -> "Other";
};
```

### 3.3 Loops

```java
// for loop
for (int i = 0; i < 5; i++) { ... }

// while loop — check first, then execute
int i = 0;
while (i < 5) { i++; }

// do-while — execute first, then check (runs at least once)
int j = 10;
do {
    System.out.println(j);   // Prints 10 even though j > 5
} while (j < 5);

// for-each (enhanced for)
int[] nums = {1, 2, 3, 4, 5};
for (int num : nums) { System.out.println(num); }
```

### 3.4 break, continue, labeled break ⚠️

```java
// Labeled break — break out of outer loop
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break outer;   // Breaks OUTER loop, not just inner
        }
        System.out.println(i + "," + j);
    }
}
// Output: 0,0  0,1  0,2  1,0
```

---

## 4. OOP Pillar 1 — Encapsulation

### What is it?

> **Encapsulation** = Wrapping data (variables) and methods into a single unit (class) + hiding internal details.

Think of it like a **medicine capsule** 💊 — the medicine (data) is wrapped inside, and you can only interact with it through defined ways (methods).

### How to Implement

1. Make variables `private` (hide data)
2. Provide `public` getter/setter methods (controlled access)

```java
public class Patient {
    // Step 1: Private variables — can't access directly from outside
    private String name;
    private int age;
    
    // Step 2: Public getters — controlled READ access
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    // Step 3: Public setters — controlled WRITE access with validation
    public void setName(String name) {
        if (name != null && !name.isEmpty()) {
            this.name = name;
        }
    }
    
    public void setAge(int age) {
        if (age > 0 && age < 150) {   // Validation!
            this.age = age;
        } else {
            throw new IllegalArgumentException("Invalid age: " + age);
        }
    }
}
```

```java
Patient p = new Patient();
// p.age = -5;           // ❌ Compile error — age is private
p.setAge(-5);            // ❌ Throws exception — validation catches it
p.setAge(30);            // ✅ Valid
System.out.println(p.getAge());  // 30
```

### Access Modifiers

| Modifier | Same Class | Same Package | Subclass (diff pkg) | Other Package |
|----------|-----------|--------------|---------------------|---------------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| `default` (no keyword) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

> [!TIP]
> **Memory trick**: Think of expanding circles:
> `private` → just ME
> `default` → my NEIGHBOURHOOD (package)
> `protected` → my FAMILY (package + children)
> `public` → the whole WORLD

### Why Encapsulation?

1. **Data Protection**: Prevent invalid data (negative age, null name)
2. **Flexibility**: Change internal implementation without breaking external code
3. **Read-only / Write-only**: Provide only getter (read-only) or only setter (write-only)

---

## 5. OOP Pillar 2 — Inheritance

### What is it?

> **Inheritance** = A child class (subclass) acquires properties and behaviours of a parent class (superclass). It represents an **"IS-A"** relationship.

Think of it like **genetics** 🧬 — a child inherits traits from parents.

### Types of Inheritance in Java

```
1. Single:       A → B               (B extends A)
2. Multilevel:   A → B → C           (C extends B, B extends A)
3. Hierarchical: A → B, A → C        (B & C both extend A)
4. ❌ Multiple:  A → C, B → C        NOT supported with classes (but supported with interfaces)
```

> [!IMPORTANT]
> Java does **NOT** support multiple inheritance with classes to avoid the **Diamond Problem** (ambiguity when two parents have the same method). But you CAN implement multiple interfaces.

### Basic Example

```java
// Parent class (Superclass)
public class Person {
    String name;
    int age;
    
    public void introduce() {
        System.out.println("Hi, I'm " + name + ", age " + age);
    }
}

// Child class (Subclass) — inherits from Person
public class Patient extends Person {
    String disease;
    
    public void showDetails() {
        // Can access parent's fields and methods directly
        introduce();   // Inherited from Person
        System.out.println("Disease: " + disease);
    }
}
```

```java
Patient p = new Patient();
p.name = "Angooj";       // Inherited from Person
p.age = 28;              // Inherited from Person
p.disease = "Flu";       // Own field
p.introduce();           // Inherited method — "Hi, I'm Angooj, age 28"
p.showDetails();         // Own method
```

### Method Overriding

When a child class provides its **own implementation** of a method already defined in the parent class.

```java
public class Person {
    public void introduce() {
        System.out.println("I am a Person");
    }
}

public class Doctor extends Person {
    @Override    // Good practice — compiler checks correctness
    public void introduce() {
        System.out.println("I am a Doctor");
    }
}
```

```java
Person p = new Doctor();
p.introduce();   // Output: "I am a Doctor" (runtime polymorphism — explained in next section)
```

### Method Overriding Rules ⚠️

| Rule | Detail |
|------|--------|
| Method signature | Must be **exactly same** (name + parameters) |
| Return type | Same or **covariant** (subtype of original return type) |
| Access modifier | Same or **wider** (e.g., protected → public ✅, public → private ❌) |
| Exceptions | Can throw **same, subclass, or fewer** checked exceptions |
| `static` methods | **Cannot** be overridden (can be hidden) |
| `final` methods | **Cannot** be overridden |
| `private` methods | **Cannot** be overridden (not visible to subclass) |
| Constructors | **Cannot** be overridden (not inherited) |

### `super` keyword (basic — detailed in Section 8)

```java
public class Doctor extends Person {
    @Override
    public void introduce() {
        super.introduce();                   // Call parent's version first
        System.out.println("I am also a Doctor");
    }
}
// Output:
// I am a Person
// I am also a Doctor
```

### What IS inherited, what is NOT

| Inherited ✅ | NOT Inherited ❌ |
|-------------|-----------------|
| public & protected members | private members |
| default members (same package) | Constructors |
| Methods | | 
| Nested classes | |

> [!NOTE]
> `private` members **exist** in the child object (memory is allocated), but they are **not accessible** directly. They can be accessed through inherited public/protected methods (getters/setters).

---

## 6. OOP Pillar 3 — Polymorphism

### What is it?

> **Polymorphism** = "Many forms". The same method/action behaves differently based on context.

Think of it like the **"+"** button on a calculator — it adds numbers, but in a word processor, it concatenates text. Same symbol, different behavior.

### Two Types

### 6.1 Compile-Time Polymorphism (Method Overloading)

**Same method name, different parameters** — decided at compile time.

```java
public class Calculator {
    // Same name "add", different parameters
    
    public int add(int a, int b) {              // 2 int params
        return a + b;
    }
    
    public int add(int a, int b, int c) {       // 3 int params
        return a + b + c;
    }
    
    public double add(double a, double b) {     // 2 double params
        return a + b;
    }
    
    public String add(String a, String b) {     // 2 String params
        return a + b;
    }
}
```

```java
Calculator calc = new Calculator();
calc.add(5, 10);          // calls add(int, int) → 15
calc.add(5, 10, 15);      // calls add(int, int, int) → 30
calc.add(1.5, 2.5);       // calls add(double, double) → 4.0
calc.add("Hello", " World"); // calls add(String, String) → "Hello World"
```

### Overloading Rules

| Basis | Overloading? |
|-------|-------------|
| Different number of parameters | ✅ Yes |
| Different type of parameters | ✅ Yes |
| Different order of parameter types | ✅ Yes |
| Different return type ONLY | ❌ No — compile error |
| Different access modifier ONLY | ❌ No |

### Overloading Ambiguity Trap ⚠️

```java
public class Tricky {
    void test(int a, long b) {
        System.out.println("int-long");
    }
    
    void test(long a, int b) {
        System.out.println("long-int");
    }
}

Tricky t = new Tricky();
t.test(5, 10);   // ❌ COMPILE ERROR — Ambiguous! 
                  // Both methods match equally (5 can be int or widened to long)
```

### 6.2 Runtime Polymorphism (Method Overriding + Dynamic Method Dispatch)

**Same method name and parameters in parent and child** — decided at runtime based on the **actual object type**.

```java
public class Shape {
    public void draw() {
        System.out.println("Drawing a Shape");
    }
}

public class Circle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Circle");
    }
}

public class Rectangle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Rectangle");
    }
}
```

```java
// Reference type is Shape, but actual object is Circle/Rectangle
Shape s1 = new Circle();
Shape s2 = new Rectangle();
Shape s3 = new Shape();

s1.draw();   // "Drawing a Circle"     ← Circle's version at runtime
s2.draw();   // "Drawing a Rectangle"  ← Rectangle's version at runtime
s3.draw();   // "Drawing a Shape"      ← Shape's version at runtime
```

This is called **Dynamic Method Dispatch** — the JVM decides which method to call at runtime, based on the actual object type (not the reference type).

### Upcasting & Downcasting

```java
// UPCASTING — child → parent reference (implicit, always safe)
Shape s = new Circle();     // Circle "upcasted" to Shape
s.draw();                    // Circle's draw() — runtime polymorphism

// DOWNCASTING — parent → child reference (explicit, risky)
// Shape s = new Circle();
Circle c = (Circle) s;      // ✅ Works — actual object IS a Circle
c.draw();

Shape s2 = new Shape();
// Circle c2 = (Circle) s2; // ❌ ClassCastException at runtime!
//                           // Actual object is NOT a Circle

// Safe downcasting with instanceof
if (s instanceof Circle) {
    Circle c3 = (Circle) s;  // Safe!
}

// Java 16+ pattern matching
if (s instanceof Circle circle) {
    circle.draw();   // No explicit cast needed!
}
```

### Covariant Return Type

A child class can override a method and return a **subtype** of the parent's return type:

```java
public class AnimalFactory {
    public Animal create() {
        return new Animal();
    }
}

public class DogFactory extends AnimalFactory {
    @Override
    public Dog create() {    // Returns Dog (subtype of Animal) — Covariant!
        return new Dog();
    }
}
```

---

## 7. OOP Pillar 4 — Abstraction

### What is it?

> **Abstraction** = Showing only essential details while hiding implementation complexity.

Think of an **ATM machine** 🏧 — you see buttons for "Withdraw", "Balance", "Transfer". You don't see the complex banking logic behind it.

### Two Ways to Achieve Abstraction

### 7.1 Abstract Classes (0% to 100% abstraction)

```java
// Cannot be instantiated directly
public abstract class Vehicle {
    String brand;
    
    // Regular method — has implementation
    public void honk() {
        System.out.println("Beep beep!");
    }
    
    // Abstract method — NO implementation (child MUST implement)
    public abstract void start();
    
    // Abstract method
    public abstract double getFuelEfficiency();
}
```

```java
public class Car extends Vehicle {
    @Override
    public void start() {           // MUST implement
        System.out.println("Car starting with key ignition");
    }
    
    @Override
    public double getFuelEfficiency() {   // MUST implement
        return 15.5;
    }
}

public class ElectricCar extends Vehicle {
    @Override
    public void start() {           // Different implementation
        System.out.println("Electric car starting silently");
    }
    
    @Override
    public double getFuelEfficiency() {   // Different implementation
        return 0;  // No fuel
    }
}
```

```java
// Vehicle v = new Vehicle();   // ❌ Cannot instantiate abstract class
Vehicle v = new Car();           // ✅ Upcasting
v.start();                       // "Car starting with key ignition"
v.honk();                        // "Beep beep!" (inherited regular method)
```

### Abstract Class Rules

| Rule | Detail |
|------|--------|
| `abstract` keyword | Required on class and abstract methods |
| Instantiation | ❌ Cannot create object directly |
| Constructors | ✅ CAN have constructors (called via `super()` from child) |
| Abstract methods | 0 or more (can have none!) |
| Regular methods | ✅ CAN have concrete methods with body |
| Variables | ✅ Can have instance variables, static variables |
| `final` | ❌ Cannot be both `abstract` and `final` |

### 7.2 Interfaces (100% abstraction — pre-Java 8)

```java
// All methods are implicitly public abstract (before Java 8)
// All variables are implicitly public static final (constants)
public interface Treatable {
    int MAX_TREATMENTS = 10;   // public static final (implicitly)
    
    void treat(String medication);        // public abstract (implicitly)
    boolean isRecovered();                // public abstract (implicitly)
    
    // Java 8: default method (has body)
    default void printStatus() {
        System.out.println("Treatment in progress");
    }
    
    // Java 8: static method
    static void guidelines() {
        System.out.println("Follow WHO guidelines");
    }
    
    // Java 9: private method (helper for default methods)
    private void logInternal() {
        System.out.println("Internal log");
    }
}
```

```java
// A class IMPLEMENTS an interface (can implement MULTIPLE)
public class Patient implements Treatable, Serializable {
    @Override
    public void treat(String medication) {
        System.out.println("Treating with " + medication);
    }
    
    @Override
    public boolean isRecovered() {
        return true;
    }
    
    // Can optionally override default method
}
```

### 7.3 Abstract Class vs Interface — Complete Comparison

| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| Keyword | `extends` | `implements` |
| Multiple | ❌ Single inheritance | ✅ Multiple interfaces |
| Methods | Abstract + concrete | Abstract + default (Java 8) + static (Java 8) + private (Java 9) |
| Variables | Any type | Only `public static final` (constants) |
| Constructors | ✅ Yes | ❌ No |
| Access modifiers | Any | Methods: `public` (or `private` in Java 9) |
| Speed | Slightly faster | Slightly slower (vtable lookup) |

### When to Use Which?

| Use **Abstract Class** when... | Use **Interface** when... |
|-------------------------------|--------------------------|
| Classes share common state (fields) | You need multiple inheritance |
| You want to provide some default behavior | You define a contract / capability |
| There's an "IS-A" relationship | There's a "CAN-DO" relationship |
| Example: `Vehicle` → `Car`, `Bike` | Example: `Flyable`, `Swimmable`, `Serializable` |

> [!TIP]
> **Interview Answer**: "I use abstract classes when I want to share code among related classes, and interfaces when I want to define a contract that unrelated classes can implement. For example, in my Healthcare project, I might have an abstract `MedicalRecord` class with shared fields like `recordId` and `date`, while having a `Printable` interface that any class can implement."

---

## 8. Keywords Deep Dive

### 8.1 `this` keyword — 6 Uses

`this` refers to the **current object instance**.

```java
public class Patient {
    private String name;
    private int age;
    
    // USE 1: Refer to instance variable (resolve ambiguity)
    public void setName(String name) {
        this.name = name;          // this.name = instance variable, name = parameter
    }
    
    // USE 2: Call another method of current object
    public void display() {
        this.validate();           // Can also just write validate()
        System.out.println(name);
    }
    
    // USE 3: Call another constructor (constructor chaining)
    public Patient() {
        this("Unknown", 0);        // Calls the 2-arg constructor — MUST be first line!
    }
    
    public Patient(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // USE 4: Pass current object as method argument
    public void register(Hospital hospital) {
        hospital.addPatient(this);   // Pass current Patient object
    }
    
    // USE 5: Return current object (method chaining / Builder pattern)
    public Patient setNameChain(String name) {
        this.name = name;
        return this;                 // Return current object for chaining
    }
    
    // USE 6: Used with synchronized (lock on current object)
    public void safeMethod() {
        synchronized(this) {         // Lock current object
            // thread-safe code
        }
    }
    
    private void validate() { }
}

// Method chaining example:
Patient p = new Patient()
    .setNameChain("Angooj")
    .setNameChain("Updated");    // Fluent API pattern
```

### 8.2 `super` keyword — 3 Uses

`super` refers to the **parent class**.

```java
public class Person {
    String name = "Person";
    
    public Person(String name) {
        this.name = name;
    }
    
    public void greet() {
        System.out.println("Hello from Person");
    }
}

public class Doctor extends Person {
    String name = "Doctor";    // Hides parent's name
    
    // USE 1: Call parent's constructor
    public Doctor(String name) {
        super(name);            // MUST be first line in constructor!
    }
    
    // USE 2: Call parent's method
    @Override
    public void greet() {
        super.greet();          // "Hello from Person"
        System.out.println("Hello from Doctor");
    }
    
    // USE 3: Access parent's variable (when hidden by child)
    public void showNames() {
        System.out.println(this.name);    // "Doctor"
        System.out.println(super.name);   // "Person" (parent's variable)
    }
}
```

> [!IMPORTANT]
> - `super()` must be the **first statement** in a constructor
> - `this()` must also be the **first statement** in a constructor
> - Therefore, you **CANNOT** use both `this()` and `super()` in the same constructor

### 8.3 `static` keyword — 4 Uses

`static` means **belongs to the class, not to any specific object**.

```java
public class Patient {
    // USE 1: Static variable — shared by ALL objects
    static int totalPatients = 0;
    String name;
    
    // USE 2: Static method — called on class, not on object
    public static int getTotalPatients() {
        // System.out.println(name);    // ❌ Can't access instance variable
        // this.name;                    // ❌ Can't use 'this'
        return totalPatients;            // ✅ Can only access static members
    }
    
    public Patient(String name) {
        this.name = name;
        totalPatients++;    // Shared counter
    }
    
    // USE 3: Static block — runs once when class is loaded
    static {
        System.out.println("Patient class loaded");
        // Initialize static variables, load config, etc.
    }
    
    // USE 4: Static nested class (covered in inner classes)
    static class PatientStats {
        // Can exist independently of Patient object
    }
}
```

```java
// Static members accessed via CLASS name (not object)
System.out.println(Patient.getTotalPatients());  // 0

Patient p1 = new Patient("Angooj");
Patient p2 = new Patient("Rahul");

System.out.println(Patient.getTotalPatients());  // 2 — shared!
System.out.println(p1.totalPatients);            // 2 — same value (but bad practice)
```

### Static Rules ⚠️

| From Static Context (static method/block) | Allowed? |
|-------------------------------------------|----------|
| Access static variable | ✅ |
| Call static method | ✅ |
| Access instance variable | ❌ |
| Call instance method | ❌ |
| Use `this` | ❌ |
| Use `super` | ❌ |

```java
// Why main() is static?
// JVM calls main() without creating an object → so it must be static
public static void main(String[] args) { }
```

### Static Imports

```java
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;

// Now you can use PI and sqrt directly
double area = PI * r * r;        // instead of Math.PI
double root = sqrt(25);          // instead of Math.sqrt(25)
```

### 8.4 `final` keyword — 3 Uses

`final` means **"cannot be changed"**.

```java
// USE 1: Final variable — value cannot be changed (constant)
final int MAX_AGE = 150;
// MAX_AGE = 200;          // ❌ Compile error

// Blank final — assigned later (once only)
final int id;
id = 100;
// id = 200;               // ❌ Cannot reassign

// Final reference — reference can't change, but object content CAN change
final List<String> names = new ArrayList<>();
names.add("Angooj");       // ✅ Modifying the object is OK
// names = new ArrayList<>();  // ❌ Can't reassign the reference

// Final with method parameter
public void process(final int value) {
    // value = 10;          // ❌ Cannot modify parameter
}


// USE 2: Final method — cannot be overridden by child class
public class Animal {
    public final void breathe() {     // All animals breathe the same way
        System.out.println("Breathing...");
    }
}

public class Dog extends Animal {
    // @Override
    // public void breathe() { }   // ❌ Compile error — cannot override final method
}


// USE 3: Final class — cannot be extended (no child class)
public final class String { }       // Java's String class is final!
// public class MyString extends String { }  // ❌ Cannot extend final class

// Other final classes: Integer, Double, Boolean (all wrapper classes)
```

### `final` vs `finally` vs `finalize()` — Classic Interview Question

| Keyword | What | Where | Purpose |
|---------|------|-------|---------|
| `final` | Keyword | Variable, method, class | Prevent modification/override/extension |
| `finally` | Block | After try-catch | Code that ALWAYS executes (cleanup) |
| `finalize()` | Method | Object class | Called by GC before destroying object (⚠️ deprecated since Java 9) |

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Error: " + e.getMessage());
} finally {
    System.out.println("This ALWAYS executes");   // Cleanup: close files, connections
}
```

---

## 9. Constructors

### What is a Constructor?

> A **constructor** is a special method that is called when an object is created. It initializes the object.

### Rules
- Same name as the class
- No return type (not even `void`)
- Called automatically with `new`
- If you don't write any constructor, Java provides a **default no-arg constructor**
- If you write ANY constructor, default constructor is **NOT provided**

### Types

```java
public class Patient {
    String name;
    int age;
    
    // 1. DEFAULT CONSTRUCTOR (provided by Java if you write none)
    //    Patient() { }   ← implicit
    
    // 2. NO-ARG CONSTRUCTOR (you write it explicitly)
    public Patient() {
        this.name = "Unknown";
        this.age = 0;
    }
    
    // 3. PARAMETERIZED CONSTRUCTOR
    public Patient(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // 4. COPY CONSTRUCTOR (Java doesn't provide — you write it)
    public Patient(Patient other) {
        this.name = other.name;
        this.age = other.age;
    }
}
```

### Constructor Chaining

```java
public class Patient {
    String name;
    int age;
    String disease;
    
    public Patient() {
        this("Unknown", 0);        // Calls 2-arg constructor
    }
    
    public Patient(String name, int age) {
        this(name, age, "None");   // Calls 3-arg constructor
    }
    
    public Patient(String name, int age, String disease) {
        // this() or super() would go here — FIRST LINE only
        this.name = name;
        this.age = age;
        this.disease = disease;
    }
}
```

### Constructor Chaining with Inheritance

```java
public class Person {
    String name;
    
    public Person(String name) {
        this.name = name;
        System.out.println("Person constructor");
    }
}

public class Patient extends Person {
    int age;
    
    public Patient(String name, int age) {
        super(name);    // MUST be first line — calls Parent constructor
        this.age = age;
        System.out.println("Patient constructor");
    }
}

Patient p = new Patient("Angooj", 28);
// Output:
// Person constructor        ← Parent first
// Patient constructor       ← Then child
```

> [!IMPORTANT]
> If you don't explicitly call `super(...)`, Java automatically inserts `super()` (no-arg) as the first line. If the parent doesn't have a no-arg constructor, you get a **compile error**.

### Constructor vs Method

| Feature | Constructor | Method |
|---------|------------|--------|
| Name | Same as class | Any name |
| Return type | None | Required |
| Called by | `new` keyword | Object reference |
| Inherited? | ❌ No | ✅ Yes |
| Can be overridden? | ❌ No | ✅ Yes |
| `this()` / `super()` | ✅ First line | ❌ Not allowed |

---

## 10. Interview Questions & Answers

### Category A: Data Types & Variables (8 Questions)

---

**Q1: What are the 8 primitive data types in Java?**

**Answer**: Java has 8 primitive types divided into 4 categories:
- **Integer**: `byte` (1 byte), `short` (2 bytes), `int` (4 bytes), `long` (8 bytes)
- **Floating-point**: `float` (4 bytes), `double` (8 bytes)
- **Character**: `char` (2 bytes — Unicode)
- **Boolean**: `boolean` (true/false)

All other types in Java are reference types (objects). Primitives are stored on the stack, while objects are on the heap.

---

**Q2: What is the difference between `int` and `Integer`?**

**Answer**:
- `int` is a **primitive type** — stores raw value, no methods, stored on stack, faster
- `Integer` is a **wrapper class** — wraps `int` in an object, has methods like `parseInt()`, `valueOf()`, stored on heap

Java provides **autoboxing** (int → Integer) and **unboxing** (Integer → int) for automatic conversion.

```java
int a = 5;
Integer b = a;          // Autoboxing: int → Integer
int c = b;              // Unboxing: Integer → int
Integer d = null;
// int e = d;           // ❌ NullPointerException on unboxing null!
```

---

**Q3: Why is `char` 2 bytes in Java, while it is 1 byte in C/C++?**

**Answer**: Java uses **Unicode** (UTF-16) to represent characters, which supports international characters (Chinese, Arabic, Hindi, etc.). Unicode needs 2 bytes. C/C++ uses ASCII which only needs 1 byte (128 characters).

---

**Q4: What is type promotion in expressions? Predict the output:**

```java
byte a = 10;
byte b = 30;
byte c = (byte)(a * b);
System.out.println(c);
```

**Answer**: `a * b = 300`, but byte range is -128 to 127. When cast to byte, 300 overflows and wraps around. `300 % 256 = 44`. Output: **44**.

This is because:
1. `a * b` is promoted to `int` → gives 300
2. Casting `(byte)300`: 300 in binary = `1 0010 1100`. Byte takes last 8 bits = `0010 1100` = 44

---

**Q5: What is the difference between `float` and `double`?**

**Answer**:
| Feature | `float` | `double` |
|---------|---------|----------|
| Size | 4 bytes (32-bit) | 8 bytes (64-bit) |
| Precision | ~6-7 decimal digits | ~15 decimal digits |
| Default | Not default for decimals | ✅ Default for decimal literals |
| Suffix | Must use `f` → `3.14f` | Optional `d` → `3.14` or `3.14d` |

Use `double` for most calculations. Use `float` only when memory is critical (large arrays).

---

**Q6: What happens if you don't initialize a local variable?**

**Answer**: You get a **compile error**. Local variables do NOT get default values. You must explicitly assign a value before using them.

```java
public void test() {
    int x;
    // System.out.println(x);  // ❌ Compile error: variable x might not have been initialized
    
    int y = 0;
    System.out.println(y);     // ✅ Fine
}
```

However, instance and static variables DO get default values (0, null, false).

---

**Q7: What is the difference between `=`, `==`, and `equals()`?**

**Answer**:
- `=` is the **assignment operator** — assigns a value
- `==` is the **comparison operator** — for primitives, compares values; for objects, compares **references** (memory addresses)
- `.equals()` is a **method** — for objects, compares **content** (if properly overridden)

```java
String s1 = new String("hello");
String s2 = new String("hello");
System.out.println(s1 == s2);       // false — different objects in memory
System.out.println(s1.equals(s2));  // true — same content
```

---

**Q8: What is the `var` keyword (Java 10)?**

**Answer**: `var` enables **local variable type inference** — the compiler infers the type from the assigned value.

```java
var name = "Angooj";          // Compiler infers: String
var list = new ArrayList<String>();  // Compiler infers: ArrayList<String>
var x = 10;                   // Compiler infers: int
```

Restrictions: Only for local variables with initializers. Cannot use for method parameters, return types, instance variables, or without initialization.

---

### Category B: OOP Concepts (15 Questions)

---

**Q9: What are the 4 pillars of OOP? Explain each with a real-world example.**

**Answer**:

1. **Encapsulation**: Bundling data and methods into a class, hiding internal state.
   - *Example*: A bank account — you can't directly change the balance; you must use deposit/withdraw methods that enforce rules.

2. **Inheritance**: Child class inherits properties and behaviors of parent class (IS-A relationship).
   - *Example*: A savings account IS-A bank account. It inherits common features and adds interest calculation.

3. **Polymorphism**: Same action behaving differently based on context.
   - *Example*: A "draw()" method — Circle draws a circle, Rectangle draws a rectangle. Same method name, different behavior.

4. **Abstraction**: Showing essential features while hiding complexity.
   - *Example*: Car steering wheel — you turn it left/right without knowing the internal mechanics of the steering system.

---

**Q10: What is the difference between method overloading and method overriding?**

**Answer**:

| Feature | Overloading | Overriding |
|---------|-------------|------------|
| Definition | Same name, different parameters | Same name AND same parameters |
| Where | Same class (or inherited) | Parent class and child class |
| Binding | Compile-time (static) | Runtime (dynamic) |
| Return type | Can be different | Must be same or covariant |
| Access modifier | Can be different | Same or wider |
| `static` methods | Can be overloaded | Cannot be overridden (hidden) |
| Example | `add(int)`, `add(int, int)` | Parent's `draw()` → Child's `draw()` |

---

**Q11: Can we override a `static` method in Java?**

**Answer**: **No**. Static methods belong to the class, not to objects, so they are not subject to runtime polymorphism. However, if a child class defines a static method with the same signature, it's called **method hiding** (not overriding).

```java
class Parent {
    static void show() { System.out.println("Parent"); }
}
class Child extends Parent {
    static void show() { System.out.println("Child"); }  // Method HIDING
}

Parent p = new Child();
p.show();   // Output: "Parent" — static method resolved by reference type, not object type
```

---

**Q12: Can we override a `private` method?**

**Answer**: **No**. Private methods are not visible to the child class, so they cannot be overridden. If a child class defines a method with the same name, it's treated as a **completely new method**, not an override.

---

**Q13: Can we overload the `main()` method?**

**Answer**: **Yes**, we can overload it. But the JVM will only call `public static void main(String[] args)` as the entry point.

```java
public class Test {
    public static void main(String[] args) {
        System.out.println("Standard main");
        main(5);   // Calling overloaded main
    }
    
    public static void main(int num) {
        System.out.println("Overloaded main: " + num);
    }
}
```

---

**Q14: What is the difference between abstract class and interface?**

**Answer**: *(See the detailed comparison table in Section 7.3 above)*

Key points:
- Abstract class: partial abstraction, can have constructors, state (instance variables), single inheritance
- Interface: full abstraction (pre-Java 8), no constructors, no state (only constants), multiple inheritance
- Since Java 8: interfaces can have `default` and `static` methods
- Since Java 9: interfaces can have `private` methods

**When to choose**:
- Use abstract class when classes share common code/state (IS-A)
- Use interface to define a contract/capability (CAN-DO)

---

**Q15: Can an abstract class have a constructor? Why?**

**Answer**: **Yes**. Even though you can't instantiate an abstract class directly, its constructor is called when a child class is instantiated (via `super()`). It's used to initialize common fields.

```java
abstract class Animal {
    String name;
    Animal(String name) {      // Constructor
        this.name = name;
    }
}

class Dog extends Animal {
    Dog(String name) {
        super(name);           // Calls Animal's constructor
    }
}
```

---

**Q16: Can an abstract class have no abstract methods?**

**Answer**: **Yes**. A class can be declared `abstract` even without any abstract methods. This prevents the class from being instantiated directly while still providing concrete methods. This is sometimes used as a design decision.

```java
abstract class Utility {
    public void doSomething() {
        System.out.println("Doing something");
    }
    // No abstract methods — but still can't do new Utility()
}
```

---

**Q17: What is the Diamond Problem? How does Java solve it?**

**Answer**: The Diamond Problem occurs when a class inherits from two classes that both extend the same base class, causing ambiguity about which version of a method to use.

```
       A
      / \
     B   C     ← Both B and C have method foo()
      \ /
       D       ← Which foo() does D get?
```

Java **prevents this with classes** by not allowing multiple class inheritance.

With **interfaces** (Java 8+ default methods), if two interfaces have the same default method, the implementing class **must override it** to resolve ambiguity:

```java
interface A { default void foo() { System.out.println("A"); } }
interface B { default void foo() { System.out.println("B"); } }

class C implements A, B {
    @Override
    public void foo() {           // MUST override — resolve ambiguity
        A.super.foo();            // Can choose to call A's version
    }
}
```

---

**Q18: What is `instanceof`? How is it used?**

**Answer**: `instanceof` checks if an object is an instance of a specific class or implements a specific interface. Returns `boolean`.

```java
Object obj = "Hello";
System.out.println(obj instanceof String);    // true
System.out.println(obj instanceof Integer);   // false
System.out.println(obj instanceof Object);    // true (everything is Object)
System.out.println(null instanceof String);   // false (null is never instanceof anything)
```

Java 16+ pattern matching:
```java
if (obj instanceof String s) {     // s is automatically cast
    System.out.println(s.length());  // No explicit cast needed
}
```

---

**Q19: Why does Java not support multiple inheritance with classes?**

**Answer**: To avoid **ambiguity** (Diamond Problem). If class C extends both A and B, and both have a method `foo()`, the compiler can't decide which `foo()` to inherit. 

Java's solution:
- Single class inheritance (avoids ambiguity)
- Multiple interface implementation (interfaces originally had no implementation, so no ambiguity; Java 8+ requires explicit override for conflicts)

---

**Q20: Explain upcasting and downcasting with examples.**

**Answer**:
- **Upcasting**: Child → Parent reference. Always safe, implicit. Enables polymorphism.
  ```java
  Animal a = new Dog();   // Dog is upcasted to Animal
  a.eat();                // Works — eat() is in Animal
  // a.bark();            // ❌ Can't access Dog-specific methods
  ```

- **Downcasting**: Parent → Child reference. Risky, explicit. Must verify with `instanceof`.
  ```java
  Animal a = new Dog();
  Dog d = (Dog) a;        // ✅ Works — actual object IS a Dog
  d.bark();               // ✅ Now can access Dog methods
  
  Animal a2 = new Cat();
  Dog d2 = (Dog) a2;      // ❌ ClassCastException at runtime!
  ```

---

**Q21: What is dynamic method dispatch?**

**Answer**: Dynamic method dispatch is the mechanism by which the JVM decides at **runtime** which overridden method to call, based on the **actual object type** (not the reference type).

```java
Animal a = new Dog();    // Reference: Animal, Object: Dog
a.sound();               // Calls Dog's sound() — decided at runtime
```

The JVM checks the actual object's class → looks up the method in that class → executes it. This is the foundation of **runtime polymorphism**.

---

**Q22: What is covariant return type?**

**Answer**: When overriding a method, the child class can return a **subtype** of the parent's return type. This is called covariant return type (introduced in Java 5).

```java
class Parent {
    Parent get() { return this; }
}
class Child extends Parent {
    @Override
    Child get() { return this; }   // Returns Child (subtype of Parent) — ✅
}
```

---

**Q23: Can we make a constructor `private`? Why would we?**

**Answer**: **Yes**. Common use cases:
1. **Singleton pattern** — prevent external instantiation, control object creation
2. **Factory pattern** — objects created via factory methods only
3. **Utility class** — class with only static methods (like `java.lang.Math`)

```java
public class Singleton {
    private static Singleton instance;
    
    private Singleton() { }    // Private constructor
    
    public static Singleton getInstance() {
        if (instance == null) instance = new Singleton();
        return instance;
    }
}
```

---

### Category C: Keywords — this, super, static, final (12 Questions)

---

**Q24: What are all the uses of `this` keyword?**

**Answer**: `this` refers to the current object and has 6 uses:
1. **Refer to instance variable** (when parameter name shadows it): `this.name = name;`
2. **Invoke current class method**: `this.validate();`
3. **Invoke current class constructor** (constructor chaining): `this(name, age);` — must be first line
4. **Pass as argument**: `method(this);`
5. **Return current object**: `return this;` (for method chaining / Builder pattern)
6. **Synchronized block**: `synchronized(this) { }`

---

**Q25: What are the uses of `super` keyword?**

**Answer**: `super` refers to the parent class and has 3 uses:
1. **Call parent constructor**: `super(name);` — must be first line
2. **Call parent method**: `super.display();` — useful when overriding
3. **Access parent variable**: `super.name` — when hidden by child's variable with same name

---

**Q26: Can `this()` and `super()` be used in the same constructor?**

**Answer**: **No**. Both must be the first statement in a constructor, so only one can be used. They are mutually exclusive in the same constructor.

---

**Q27: What is the execution order of static blocks, instance blocks, and constructors?**

**Answer**:
```java
class Parent {
    static { System.out.println("1. Parent static block"); }
    { System.out.println("3. Parent instance block"); }
    Parent() { System.out.println("4. Parent constructor"); }
}

class Child extends Parent {
    static { System.out.println("2. Child static block"); }
    { System.out.println("5. Child instance block"); }
    Child() { System.out.println("6. Child constructor"); }
}

new Child();
```

**Output order**:
```
1. Parent static block       ← Static blocks first (parent → child), only ONCE
2. Child static block
3. Parent instance block      ← Instance blocks before constructor (parent → child)
4. Parent constructor
5. Child instance block
6. Child constructor
```

**Rule**: Static blocks (once, parent→child) → Instance block → Constructor (parent→child, for each `new`)

---

**Q28: Can we access instance variables from a static method?**

**Answer**: **No**, not directly. Static methods belong to the class, not any object. They don't have a `this` reference.

```java
public class Test {
    int x = 10;              // Instance variable
    static int y = 20;       // Static variable
    
    public static void main(String[] args) {
        // System.out.println(x);   // ❌ Cannot access instance from static
        System.out.println(y);       // ✅ Static can access static
        
        Test obj = new Test();
        System.out.println(obj.x);   // ✅ Access through object reference
    }
}
```

---

**Q29: What is a `static` import?**

**Answer**: Static import allows you to access static members of a class directly, without specifying the class name.

```java
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;

double result = sqrt(PI * 10);   // Instead of Math.sqrt(Math.PI * 10)
```

Use sparingly — can reduce readability if overused.

---

**Q30: What is a `final` variable? What is a blank final variable?**

**Answer**:
- **Final variable**: Assigned at declaration, cannot be changed later.
  ```java
  final int MAX = 100;
  // MAX = 200;   // ❌ Compile error
  ```

- **Blank final variable**: Declared without initialization, but MUST be initialized either in instance initializer block or in **every constructor**.
  ```java
  class Patient {
      final int id;        // Blank final
      
      Patient(int id) {
          this.id = id;     // Must initialize here
      }
  }
  ```

- **Static blank final variable**: Must be initialized in a static block.
  ```java
  static final int CODE;
  static {
      CODE = loadFromConfig();
  }
  ```

---

**Q31: Can a `final` method be overloaded?**

**Answer**: **Yes**. `final` prevents **overriding**, not **overloading**. These are independent concepts.

```java
class Parent {
    public final void display(int x) { }        // Final method
    public final void display(int x, int y) { } // Overloaded — ✅ allowed
}

class Child extends Parent {
    // public void display(int x) { }   // ❌ Cannot override final method
    public void display(String s) { }   // ✅ This is OVERLOADING, not overriding
}
```

---

**Q32: Why is the `String` class `final`?**

**Answer**: String is final to ensure:
1. **Security**: Strings are used in class loading, network connections, file paths. If someone could extend and modify String behavior, it would be a security risk.
2. **Thread Safety**: Immutable Strings are inherently thread-safe.
3. **Hashcode Caching**: String caches its hashcode. If it could be subclassed and modified, the cached hashcode would become invalid.
4. **String Pool**: The String Pool optimization relies on immutability. If Strings were mutable, one reference could change the value that other references point to.

---

**Q33: What is the difference between `final`, `finally`, and `finalize()`?**

**Answer**:

| | `final` | `finally` | `finalize()` |
|---|---------|-----------|-------------|
| **Type** | Keyword | Block | Method |
| **Used with** | Variable, method, class | try-catch | Object class |
| **Purpose** | Restrict modification | Ensure cleanup code runs | Called by GC before destruction |
| **Status** | ✅ Active | ✅ Active | ⚠️ Deprecated (Java 9) |

```java
// final
final int x = 10;

// finally — always executes (even after return/exception)
try { riskyOperation(); }
catch (Exception e) { log(e); }
finally { closeConnection(); }   // ALWAYS runs

// finalize() — deprecated, unreliable, don't use
@Override
protected void finalize() {
    // Cleanup before GC destroys this object
    // DON'T rely on this — use try-with-resources instead
}
```

---

**Q34: If `finally` always executes, when does it NOT execute?**

**Answer**: `finally` does NOT execute only in these rare cases:
1. `System.exit(0)` is called before reaching `finally`
2. JVM crashes (fatal error)
3. The thread executing the code is killed/interrupted
4. Infinite loop or `Thread.sleep()` forever in try/catch

```java
try {
    System.out.println("Try");
    System.exit(0);          // JVM exits immediately
} finally {
    System.out.println("Finally");   // ❌ This DOES NOT execute
}
```

---

**Q35: Why is `main()` method `public static void`?**

**Answer**:
- `public` — accessible from anywhere (JVM needs to call it from outside the class)
- `static` — JVM calls it without creating an object (no object exists yet when program starts)
- `void` — it doesn't return anything to the JVM
- `main` — name convention that JVM looks for as the entry point
- `String[] args` — command line arguments

---

### Category D: Constructors (8 Questions)

---

**Q36: What is a constructor? How is it different from a method?**

**Answer**: A constructor is a special method used to initialize objects. Key differences:

| Feature | Constructor | Method |
|---------|------------|--------|
| Name | Must match class name | Any valid name |
| Return type | No return type (not even void) | Must have return type |
| Invocation | Called via `new` keyword | Called on object reference |
| Inheritance | Not inherited | Inherited |
| `this()` / `super()` | Allowed (first line) | Not allowed |
| Purpose | Initialize object | Define behavior |
| Default provided? | Yes (if none written) | No |

---

**Q37: What is the default constructor? When is it provided?**

**Answer**: The default constructor is a **no-argument constructor** automatically provided by the Java compiler when you don't write ANY constructor in your class. It:
- Takes no parameters
- Has an empty body (just calls `super()`)
- Has the same access modifier as the class

**Important**: If you define even ONE constructor (any kind), the default constructor is **NOT provided**.

```java
class Patient { }                    // Compiler adds: Patient() { super(); }

class Patient {
    Patient(String name) { }        // Default constructor NOT available
    // new Patient();               // ❌ Compile error
}
```

---

**Q38: Can a constructor be `final`, `static`, or `abstract`?**

**Answer**: **No** to all three.
- `final` — constructors can't be inherited, so preventing override is meaningless
- `static` — constructors are inherently tied to object creation; `static` would contradict this
- `abstract` — constructors must have a body (you can't leave object initialization abstract)

---

**Q39: What is constructor chaining? Explain with `this()` and `super()`.**

**Answer**: Constructor chaining is calling one constructor from another.

- `this()` — calls another constructor in the **same class**
- `super()` — calls a constructor in the **parent class**

```java
class Employee {
    String name;
    int age;
    String dept;
    
    Employee() {
        this("Unknown", 0, "General");     // Chain to 3-arg
    }
    
    Employee(String name) {
        this(name, 0, "General");          // Chain to 3-arg
    }
    
    Employee(String name, int age, String dept) {
        super();                           // Chain to Object()
        this.name = name;
        this.age = age;
        this.dept = dept;
    }
}
```

---

**Q40: What happens if parent has no no-arg constructor and child doesn't call `super()`?**

**Answer**: **Compile error**. The compiler automatically inserts `super()` (no-arg) as the first line of every constructor. If the parent doesn't have a no-arg constructor, this fails.

```java
class Parent {
    Parent(int x) { }    // Only parameterized constructor — no default!
}

class Child extends Parent {
    Child() {
        // Compiler inserts super() here → ❌ No matching constructor in Parent!
    }
}

// Fix:
class Child extends Parent {
    Child() {
        super(10);        // Explicitly call parent's parameterized constructor
    }
}
```

---

**Q41: Can a constructor return a value?**

**Answer**: A constructor **doesn't have a return type**, so it can't use `return value;`. However, you can use `return;` (empty return) to exit early.

**Tricky interview question**: What if you write a method with the same name as the class?

```java
class Test {
    void Test() {       // This is a METHOD, not a constructor! (has void return type)
        System.out.println("Method");
    }
    
    Test() {            // THIS is the constructor
        System.out.println("Constructor");
    }
}

new Test();   // Calls the constructor → "Constructor"
```

---

**Q42: Can we have both `this()` and `super()` in the same constructor?**

**Answer**: **No**. Both must be the first statement, so they are mutually exclusive. You can have `this()` → which chains to another constructor → which eventually calls `super()`.

---

**Q43: What is the order of constructor execution in inheritance?**

**Answer**: **Parent first, then child** (top-down). Always.

```java
class A { A() { System.out.println("A"); } }
class B extends A { B() { System.out.println("B"); } }
class C extends B { C() { System.out.println("C"); } }

new C();
// Output:
// A     ← Topmost parent first
// B
// C     ← Current class last
```

This is because every constructor implicitly calls `super()` as its first line, which calls the parent's constructor before executing its own body.

---

### Category E: Tricky Output-Based Questions (10 Questions)

---

**Q44: Predict the output:**
```java
public class Test {
    public static void main(String[] args) {
        System.out.println(10 + 20 + "Hello");
        System.out.println("Hello" + 10 + 20);
    }
}
```

**Answer**:
```
30Hello
Hello1020
```
- Line 1: `10 + 20` = 30 (int addition), then `30 + "Hello"` = `"30Hello"` (string concat)
- Line 2: `"Hello" + 10` = `"Hello10"` (string concat), then `"Hello10" + 20` = `"Hello1020"` (string concat)

**Rule**: Evaluation is **left to right**. Once a `String` is encountered, everything after is concatenation.

---

**Q45: Predict the output:**
```java
public class Test {
    static int x = 10;
    
    static {
        x = 20;
    }
    
    public static void main(String[] args) {
        System.out.println(x);
    }
    
    static {
        x = 30;
    }
}
```

**Answer**: `30`

Static blocks execute in order from top to bottom when the class is loaded:
1. `x = 10` (static variable initialization)
2. First static block: `x = 20`
3. Second static block: `x = 30`
4. `main()` prints 30

---

**Q46: Predict the output:**
```java
class Parent {
    int x = 10;
    Parent() {
        display();
    }
    void display() {
        System.out.println("Parent x = " + x);
    }
}

class Child extends Parent {
    int x = 20;
    void display() {
        System.out.println("Child x = " + x);
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
    }
}
```

**Answer**: `Child x = 0`

Explanation:
1. `new Child()` calls `Child()`, which first calls `super()` → `Parent()`
2. Inside `Parent()`, `display()` is called — but `display()` is overridden in `Child`
3. Due to runtime polymorphism, `Child.display()` runs
4. But `Child`'s instance variable `x` is **not yet initialized** (Parent constructor is still running)
5. So `x` has its default value `0`

> [!CAUTION]
> Never call overridable methods from a constructor! The child's fields may not be initialized yet.

---

**Q47: Predict the output:**
```java
public class Test {
    public static void main(String[] args) {
        int i = 1;
        i = i++ + ++i;
        System.out.println(i);
    }
}
```

**Answer**: `4`

Step-by-step:
1. `i++` → uses current value 1, then increments i to 2. Expression so far: `1 + ...`
2. `++i` → increments i to 3, then uses value 3. Expression: `1 + 3`
3. `i = 1 + 3 = 4`

---

**Q48: Can you override `equals()` without overriding `hashCode()`? What happens?**

**Answer**: You **can** but you **should NOT**. It violates the contract:

> If two objects are equal according to `equals()`, they MUST have the same `hashCode()`.

If you break this:
- `HashMap` / `HashSet` will malfunction
- You could put an object in a set but then not be able to find it

```java
// BAD: Override equals but not hashCode
class Patient {
    String id;
    
    @Override
    public boolean equals(Object o) {
        return this.id.equals(((Patient)o).id);
    }
    // Missing hashCode() override!
}

Patient p1 = new Patient("P001");
Patient p2 = new Patient("P001");
p1.equals(p2);                    // true ✅

Set<Patient> set = new HashSet<>();
set.add(p1);
set.contains(p2);                 // false ❌ — WRONG! Because different hashCodes
```

---

**Q49: Predict the output:**
```java
public class Test {
    public static void main(String[] args) {
        try {
            System.out.println("try");
            return;
        } finally {
            System.out.println("finally");
        }
    }
}
```

**Answer**:
```
try
finally
```

`finally` executes **even after a `return` statement**. The `return` is actually deferred until after `finally` completes.

---

**Q50: Predict the output:**
```java
class Animal {
    String name = "Animal";
    static String type = "Creature";
    
    void display() { System.out.println(name); }
    static void showType() { System.out.println(type); }
}

class Dog extends Animal {
    String name = "Dog";
    static String type = "Pet";
    
    void display() { System.out.println(name); }
    static void showType() { System.out.println(type); }
}

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();
        System.out.println(a.name);    // ?
        a.display();                    // ?
        a.showType();                   // ?
    }
}
```

**Answer**:
```
Animal
Dog
Creature
```

- `a.name` → **"Animal"** — Variables are resolved by **reference type** (no polymorphism for fields)
- `a.display()` → **"Dog"** — Instance methods use **runtime polymorphism** (actual object type)
- `a.showType()` → **"Creature"** — Static methods are resolved by **reference type** (no polymorphism — method hiding)

> [!IMPORTANT]
> **Polymorphism applies ONLY to instance methods, NOT to variables or static methods.**

---

**Q51: What happens when you serialize an object whose parent is not Serializable?**

**Answer**: During deserialization, the **non-serializable parent's constructor** is called (to re-initialize parent fields to defaults). The child's serialized fields are restored. Parent fields will have their default/constructor-initialized values, not the values they had during serialization.

*(This is a preview question for Day 7 — Serialization)*

---

**Q52: Can we have an interface without any methods?**

**Answer**: **Yes**. It's called a **marker interface** (or tag interface). It doesn't define any methods — it just "marks" a class with a capability. Examples:
- `Serializable` — marks objects that can be serialized
- `Cloneable` — marks objects that can be cloned
- `Remote` — marks objects for RMI

```java
public interface Serializable { }    // No methods!

class Patient implements Serializable {
    // Now Patient objects can be serialized
}
```

Modern alternative: annotations (`@Entity`, `@Service`) have largely replaced marker interfaces.

---

**Q53: What are the SOLID principles? Give a brief example of each.**

**Answer**: *(Preview for Day 20 — but commonly asked alongside OOP)*

| Principle | Meaning | Example |
|-----------|---------|---------|
| **S**ingle Responsibility | One class = one reason to change | `PatientService` handles business logic only, not email sending |
| **O**pen/Closed | Open for extension, closed for modification | Add new `Shape` types without changing existing `AreaCalculator` |
| **L**iskov Substitution | Subtypes must be substitutable for base types | A `Square` should behave correctly when used as a `Rectangle` |
| **I**nterface Segregation | Don't force unused methods on clients | Separate `Printable`, `Scannable` instead of one fat `Machine` interface |
| **D**ependency Inversion | Depend on abstractions, not concretions | `OrderService` depends on `PaymentGateway` interface, not `StripePayment` |

---

> [!TIP]
> **Day 1 Completion Checklist** ✅
> - [ ] Can explain all 8 primitive types with ranges
> - [ ] Understand type casting and type promotion traps
> - [ ] Can explain all 4 OOP pillars with real examples
> - [ ] Know the difference between overloading and overriding
> - [ ] Can list all method overriding rules
> - [ ] Know when to use abstract class vs interface
> - [ ] Can list all 6 uses of `this` keyword
> - [ ] Can list all 3 uses of `super` keyword
> - [ ] Understand `static` restrictions (can't access instance from static)
> - [ ] Know `final` vs `finally` vs `finalize()`
> - [ ] Can explain constructor chaining with `this()` and `super()`
> - [ ] Can predict output for tricky questions (static blocks, polymorphism, string concat)
> - [ ] Can answer all 53 questions confidently

---

**Tomorrow (Day 2)**: Strings Deep Dive, Wrapper Classes, Enums & Inner Classes 🚀
