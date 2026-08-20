# 📘 Day 3 — Exception Handling (Complete) + Object Class Deep Dive

**Date**: Aug 20, 2026 | **Duration**: ~4.5 hours
**Goal**: Master Exception Handling from basics to advanced (most asked topic after Strings) + Object class methods

---

## 📑 Table of Contents

1. [Exception Hierarchy — The Complete Picture](#1-exception-hierarchy--the-complete-picture)
   - 1.1 What is an Exception?
   - 1.2 Throwable Hierarchy
   - 1.3 Error vs Exception
   - 1.4 Checked vs Unchecked Exceptions
   - 1.5 Common Exceptions You Must Know
2. [Exception Handling Mechanisms](#2-exception-handling-mechanisms)
   - 2.1 try-catch-finally
   - 2.2 Execution Flow in All Scenarios
   - 2.3 throw vs throws
   - 2.4 Exception Propagation
   - 2.5 Multi-catch (Java 7)
   - 2.6 try-with-resources (Java 7)
   - 2.7 Exception Chaining
3. [Custom Exceptions & Best Practices](#3-custom-exceptions--best-practices)
   - 3.1 When to Create Custom Exceptions
   - 3.2 Creating Custom Checked Exception
   - 3.3 Creating Custom Unchecked Exception
   - 3.4 Building a Real Exception Hierarchy
   - 3.5 Best Practices (12 Rules)
4. [Object Class — The Root of Everything](#4-object-class--the-root-of-everything)
   - 4.1 All 11 Methods
   - 4.2 toString()
   - 4.3 equals() — Deep Dive
   - 4.4 hashCode() — Deep Dive
   - 4.5 The equals/hashCode Contract
   - 4.6 clone() — Shallow vs Deep Copy
   - 4.7 finalize(), getClass(), wait/notify
5. [Common Mistakes & Anti-Patterns](#5-common-mistakes--anti-patterns)
6. [Interview Questions & Answers (60+)](#6-interview-questions--answers)

---

## 1. Exception Hierarchy — The Complete Picture

### 1.1 What is an Exception?

> An **exception** is an abnormal event that disrupts the normal flow of a program at **runtime**. Java provides a robust mechanism to handle these events gracefully instead of crashing.

**Real-world analogy**: Think of driving a car 🚗. The normal flow is: start → drive → reach destination. Exceptions are like: flat tire, engine overheating, road blocked. You don't ignore them — you handle them (change tire, cool engine, take detour). If you don't handle them, the journey (program) stops.

### 1.2 Throwable Hierarchy — The Complete Tree

This diagram is asked in **every** interview. Know it cold.

```
                        java.lang.Object
                              │
                      java.lang.Throwable          ← Root of all errors/exceptions
                       ┌──────┴──────┐
                       │             │
                 java.lang.Error   java.lang.Exception
                       │             │
              ┌────────┴────┐    ┌───┴──────────────────┐
              │             │    │                       │
      StackOverflow   OutOfMemory  RuntimeException   IOException
      Error           Error        (UNCHECKED)        (CHECKED)
              │                    │                       │
      VirtualMachine     ┌────────┼────────┐         ┌────┼────┐
      Error              │        │        │         │         │
                   NullPointer  ClassCast  Index   FileNot   SQL
                   Exception   Exception  OutOf   Found     Exception
                                          Bounds  Exception
                         │
                   ┌─────┼──────┐
                   │     │      │
              Arithmetic Illegal  NumberFormat
              Exception  Argument  Exception
                         Exception
```

**Key Insight**: Everything extends `Throwable`. Only `Throwable` and its subclasses can be thrown with `throw` and caught with `catch`.

### 1.3 Error vs Exception

| Feature | Error | Exception |
|---------|-------|-----------|
| **Package** | `java.lang.Error` | `java.lang.Exception` |
| **Caused by** | **JVM/System** — out of your control | **Application/Programmer** — in your control |
| **Recovery** | ❌ Usually NOT recoverable | ✅ Usually recoverable |
| **Should you catch?** | ❌ No (almost never) | ✅ Yes |
| **Examples** | `StackOverflowError`, `OutOfMemoryError`, `VirtualMachineError` | `NullPointerException`, `IOException`, `SQLException` |
| **Checked?** | ❌ Unchecked (extends `Error`) | Both checked and unchecked |

```java
// Error — JVM problem, you can't fix this
public void infinite() {
    infinite();    // StackOverflowError — infinite recursion, stack space exhausted
}

// Exception — programmer problem, you CAN handle this
public void divide() {
    int result = 10 / 0;    // ArithmeticException — handle with try-catch
}
```

> [!CAUTION]
> **Never catch `Error`** in production code (except in very rare cases like monitoring/logging tools). If you get `OutOfMemoryError`, catching it won't help — the JVM is in an unstable state. Fix the root cause instead (memory leak, incorrect configuration).

### 1.4 Checked vs Unchecked Exceptions ⚠️

This distinction is **one of the most asked topics**. Understand it deeply.

```
                    Throwable
                   ┌────┴────┐
                   │         │
                 Error    Exception
              (UNCHECKED) ┌────┴────────┐
                          │             │
                   RuntimeException   ALL OTHER
                    (UNCHECKED)      EXCEPTIONS
                                     (CHECKED)
```

| Feature | Checked Exception | Unchecked Exception |
|---------|------------------|---------------------|
| **Inherits from** | `Exception` (but NOT `RuntimeException`) | `RuntimeException` or `Error` |
| **Compiler checks?** | ✅ Yes — MUST handle or declare | ❌ No — compiler doesn't force handling |
| **When?** | **Recoverable** situations (file not found, DB down) | **Programming errors** (null pointer, bad cast) |
| **Handle with** | `try-catch` OR `throws` declaration | Optional — can use try-catch if needed |
| **Examples** | `IOException`, `SQLException`, `ClassNotFoundException`, `InterruptedException` | `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ClassCastException`, `ArithmeticException` |

```java
// CHECKED — compiler forces you to handle
public void readFile() {
    FileReader fr = new FileReader("test.txt");    // ❌ Won't compile!
    // FileNotFoundException is CHECKED — must handle or declare
}

// Option 1: Handle with try-catch
public void readFile() {
    try {
        FileReader fr = new FileReader("test.txt");
    } catch (FileNotFoundException e) {
        System.out.println("File not found: " + e.getMessage());
    }
}

// Option 2: Declare with throws (pass responsibility to caller)
public void readFile() throws FileNotFoundException {
    FileReader fr = new FileReader("test.txt");     // ✅ Compiles — caller must handle
}

// UNCHECKED — compiler doesn't complain
public void divide() {
    int result = 10 / 0;    // ✅ Compiles fine! Crashes at RUNTIME with ArithmeticException
}
```

> [!IMPORTANT]
> **Why does Java have both?**
> - **Checked**: For situations the programmer should anticipate and recover from (file missing → ask user for another path, network down → retry). The compiler FORCES you to think about it.
> - **Unchecked**: For programming bugs that should be FIXED, not caught (null access → fix the null check, bad array index → fix the loop). Forcing try-catch for these would clutter every line of code.

### 1.5 Common Exceptions You Must Know

**Unchecked (RuntimeException subclasses)**:

| Exception | When it Occurs | Example |
|-----------|---------------|---------|
| `NullPointerException` | Calling method/field on `null` | `String s = null; s.length();` |
| `ArrayIndexOutOfBoundsException` | Invalid array index | `int[] a = {1,2}; a[5];` |
| `StringIndexOutOfBoundsException` | Invalid string index | `"Hi".charAt(10);` |
| `ClassCastException` | Invalid type cast | `Object o = "Hi"; Integer i = (Integer) o;` |
| `ArithmeticException` | Math error (division by zero) | `10 / 0` |
| `IllegalArgumentException` | Invalid method argument | `Thread.sleep(-1)` |
| `NumberFormatException` | Invalid number parse (extends `IllegalArgumentException`) | `Integer.parseInt("abc")` |
| `IllegalStateException` | Method called at wrong time | Calling `next()` without `hasNext()` on Iterator |
| `ConcurrentModificationException` | Modifying collection during iteration | Removing from ArrayList inside for-each |
| `UnsupportedOperationException` | Unsupported operation | `Arrays.asList(1,2).add(3)` |
| `StackOverflowError` | Deep/infinite recursion | Recursive method without base case |

**Checked (Exception subclasses, not RuntimeException)**:

| Exception | When it Occurs | Example |
|-----------|---------------|---------|
| `IOException` | I/O operation fails | File read/write failure |
| `FileNotFoundException` | File doesn't exist (extends `IOException`) | `new FileReader("missing.txt")` |
| `SQLException` | Database operation fails | Bad SQL query, connection lost |
| `ClassNotFoundException` | Class not found at runtime | `Class.forName("com.Missing")` |
| `InterruptedException` | Thread is interrupted while sleeping/waiting | `Thread.sleep()` interrupted |
| `ParseException` | Parsing fails | `new SimpleDateFormat("dd/MM").parse("abc")` |
| `CloneNotSupportedException` | `clone()` on non-Cloneable class | Object doesn't implement `Cloneable` |

---

## 2. Exception Handling Mechanisms

### 2.1 try-catch-finally — The Foundation

```java
try {
    // Code that MIGHT throw an exception
    // This is the "risky" code
    int result = 10 / 0;
    System.out.println("After division");    // SKIPPED if exception occurs
    
} catch (ArithmeticException e) {
    // Runs ONLY if the matching exception occurs in try block
    System.out.println("Error: " + e.getMessage());    // "/ by zero"
    
} finally {
    // ALWAYS runs — whether exception occurred or not
    // Use for cleanup: close files, connections, release resources
    System.out.println("Cleanup done");
}
```

**Valid Combinations**:
```java
// 1. try-catch (most common)
try { } catch (Exception e) { }

// 2. try-finally (no catch — exception propagates, but cleanup still happens)
try { } finally { }

// 3. try-catch-finally (complete)
try { } catch (Exception e) { } finally { }

// 4. try with multiple catches (order matters!)
try { }
catch (FileNotFoundException e) { }    // More specific FIRST
catch (IOException e) { }              // Less specific AFTER
catch (Exception e) { }               // Most general LAST

// ❌ INVALID — try alone
// try { }      // Compile error — need catch or finally
```

> [!CAUTION]
> **Catch order matters!** Specific exceptions must come **before** general ones. Otherwise, the specific catch is unreachable (compile error).
> ```java
> // ❌ COMPILE ERROR — IOException catches everything before FileNotFoundException can
> catch (IOException e) { }
> catch (FileNotFoundException e) { }    // Unreachable!
> 
> // ✅ CORRECT — specific first
> catch (FileNotFoundException e) { }    // Handles file-specific issues
> catch (IOException e) { }              // Handles other I/O issues
> ```

### 2.2 Execution Flow in ALL Scenarios ⚠️

This is tested with **output prediction questions** in every interview. Trace through each carefully.

**Scenario 1: No Exception**
```java
try {
    System.out.println("1. try");          // ✅ Executes
} catch (Exception e) {
    System.out.println("2. catch");        // ❌ Skipped — no exception
} finally {
    System.out.println("3. finally");      // ✅ Always executes
}
System.out.println("4. after");            // ✅ Executes
// Output: 1. try → 3. finally → 4. after
```

**Scenario 2: Exception IS Caught**
```java
try {
    System.out.println("1. try");          // ✅ Executes
    int x = 10 / 0;                        // 💥 Exception!
    System.out.println("2. after divide"); // ❌ Skipped — exception jumped out
} catch (ArithmeticException e) {
    System.out.println("3. catch");        // ✅ Executes — exception caught
} finally {
    System.out.println("4. finally");      // ✅ Always executes
}
System.out.println("5. after");            // ✅ Executes — exception was handled
// Output: 1. try → 3. catch → 4. finally → 5. after
```

**Scenario 3: Exception NOT Caught (wrong catch type)**
```java
try {
    System.out.println("1. try");          // ✅ Executes
    int x = 10 / 0;                        // 💥 ArithmeticException!
    System.out.println("2. after");        // ❌ Skipped
} catch (NullPointerException e) {         // Wrong type — doesn't match!
    System.out.println("3. catch");        // ❌ Skipped
} finally {
    System.out.println("4. finally");      // ✅ STILL executes!
}
System.out.println("5. after");            // ❌ Skipped — exception uncaught, propagates up
// Output: 1. try → 4. finally → [CRASH: ArithmeticException]
```

**Scenario 4: Exception in catch block**
```java
try {
    throw new ArithmeticException("oops");
} catch (ArithmeticException e) {
    System.out.println("1. catch");           // ✅ Executes
    throw new RuntimeException("in catch");   // 💥 New exception!
} finally {
    System.out.println("2. finally");         // ✅ STILL executes before propagation!
}
// Output: 1. catch → 2. finally → [CRASH: RuntimeException("in catch")]
```

**Scenario 5: Return in try, code in finally ⚠️ (Classic interview trap)**
```java
public static int getValue() {
    try {
        return 1;                              // Return value 1 is "saved"
    } finally {
        return 2;                              // ⚠️ OVERRIDES the try's return!
    }
}
System.out.println(getValue());               // Output: 2
```

> [!CAUTION]
> **Never return from finally!** It silently swallows the try/catch return value AND any exceptions. This is a severe anti-pattern that makes debugging impossible.

**Scenario 6: Return in try, modification in finally**
```java
public static int getValue() {
    int x = 10;
    try {
        return x;                    // Saves value 10 to return
    } finally {
        x = 20;                      // Modifies x, but return value already saved!
    }
}
System.out.println(getValue());     // Output: 10 (NOT 20!)
// The return value was already "captured" before finally modified x
```

### 2.3 throw vs throws

| Feature | `throw` | `throws` |
|---------|---------|----------|
| **What** | Statement that **throws** an exception object | Declaration that a method **might throw** exceptions |
| **Where** | Inside method body | In method signature |
| **Followed by** | Exception **object** (`new`) | Exception **class names** |
| **Count** | One exception at a time | Multiple, comma-separated |
| **Purpose** | Actually create and throw the exception | Inform the caller about possible exceptions |

```java
// throws — declaration (in method signature)
public void readFile(String path) throws FileNotFoundException, IOException {
    // tells caller: "I might throw these, YOU handle them"
    
    // throw — actually throwing an exception (inside method body)
    if (path == null) {
        throw new IllegalArgumentException("Path cannot be null");
    }
    
    FileReader fr = new FileReader(path);    // This might throw FileNotFoundException
}
```

```java
// throw with custom message
throw new NullPointerException("Patient name cannot be null");

// throw with cause (exception chaining)
try {
    // some code
} catch (SQLException e) {
    throw new ServiceException("Failed to save patient", e);  // 'e' is the cause
}

// Re-throwing an exception
try {
    riskyOperation();
} catch (Exception e) {
    logger.error("Operation failed", e);
    throw e;    // Re-throw the SAME exception after logging
}
```

### 2.4 Exception Propagation

When an exception occurs, it travels **up the call stack** until it finds a matching catch block. If none is found, the JVM prints the stack trace and terminates the thread.

```java
public void method3() {
    System.out.println(10 / 0);       // 💥 ArithmeticException created HERE
}

public void method2() {
    method3();                         // No catch → propagates UP to method1
}

public void method1() {
    try {
        method2();                     // Exception propagates here
    } catch (ArithmeticException e) {
        System.out.println("Caught!"); // ✅ Caught here — stops propagating
    }
}

public static void main(String[] args) {
    new Test().method1();              // Calls method1
}
```

**Propagation Flow**:
```
main() → method1() → method2() → method3()
                                    💥 ArithmeticException!
                              ← propagates (no catch in method2)
           ← propagates to method1's try-catch
           ✅ CAUGHT! Execution continues normally after catch
```

**For CHECKED exceptions**, the propagation must be **declared**:
```java
// Every method in the chain must either catch OR declare with throws
public void method3() throws IOException {
    throw new IOException("file error");       // Checked — must declare
}

public void method2() throws IOException {     // Must declare — doesn't catch
    method3();
}

public void method1() {
    try {
        method2();
    } catch (IOException e) {                  // Finally caught
        System.out.println("Handled: " + e.getMessage());
    }
}
```

### 2.5 Multi-catch (Java 7+)

Catch multiple unrelated exception types in a single catch block:

```java
// BEFORE Java 7 — repetitive code
try {
    // code
} catch (IOException e) {
    logger.error("Error: " + e.getMessage());
    throw new ServiceException(e);
} catch (SQLException e) {
    logger.error("Error: " + e.getMessage());    // Same handling — code duplication!
    throw new ServiceException(e);
}

// AFTER Java 7 — multi-catch with pipe (|)
try {
    // code
} catch (IOException | SQLException e) {
    // 'e' is effectively final — cannot reassign it
    logger.error("Error: " + e.getMessage());
    throw new ServiceException(e);
}
```

**Rules for multi-catch**:
1. Exception types must be **unrelated** (neither can be a subclass of the other)
2. The variable `e` is **implicitly final** — cannot be reassigned
3. Catches are checked left to right

```java
// ❌ COMPILE ERROR — FileNotFoundException is subclass of IOException
catch (FileNotFoundException | IOException e) { }    // Redundant!

// ✅ CORRECT — unrelated exceptions
catch (IOException | SQLException | ParseException e) { }
```

### 2.6 try-with-resources (Java 7+) — Essential!

**The Problem**: Resources like files, database connections, and streams must be **closed** after use. Forgetting to close causes resource leaks (file handles, DB connections exhaust).

```java
// ❌ OLD WAY — manual closing with finally (verbose, error-prone)
FileReader fr = null;
BufferedReader br = null;
try {
    fr = new FileReader("data.txt");
    br = new BufferedReader(fr);
    String line = br.readLine();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    try {
        if (br != null) br.close();       // Must null-check and handle close exception!
        if (fr != null) fr.close();
    } catch (IOException e) {
        e.printStackTrace();               // Close itself can fail!
    }
}
```

```java
// ✅ NEW WAY — try-with-resources (Java 7+) — automatic closing!
try (FileReader fr = new FileReader("data.txt");
     BufferedReader br = new BufferedReader(fr)) {
     
    String line = br.readLine();
    System.out.println(line);
    
} catch (IOException e) {
    e.printStackTrace();
}
// Resources are AUTOMATICALLY closed when try block exits — even if exception occurs!
// Close order: REVERSE of declaration (br first, then fr)
```

**How it works**: The resource must implement `AutoCloseable` (or `Closeable`) interface:

```java
public interface AutoCloseable {
    void close() throws Exception;
}

// Many JDK classes implement it:
// FileReader, BufferedReader, InputStream, OutputStream,
// Connection, Statement, ResultSet, Scanner, etc.
```

**Creating your own AutoCloseable resource**:

```java
public class DatabaseConnection implements AutoCloseable {
    private Connection conn;
    
    public DatabaseConnection(String url) throws SQLException {
        this.conn = DriverManager.getConnection(url);
        System.out.println("Connection opened");
    }
    
    public void query(String sql) {
        // Execute query
    }
    
    @Override
    public void close() throws SQLException {
        if (conn != null && !conn.isClosed()) {
            conn.close();
            System.out.println("Connection closed automatically!");
        }
    }
}

// Usage:
try (DatabaseConnection db = new DatabaseConnection("jdbc:mysql://localhost/hospital")) {
    db.query("SELECT * FROM patients");
}   // close() called automatically!
```

> [!TIP]
> **From Your Project**: In your Healthcare project, every `Connection`, `PreparedStatement`, and `ResultSet` should use try-with-resources. This prevents the common production bug of database connection pool exhaustion caused by unclosed connections.

**Suppressed Exceptions** (Java 7+):

What if both the try block AND the close() method throw exceptions?

```java
try (MyResource res = new MyResource()) {
    throw new Exception("from try");       // Primary exception
}
// MyResource.close() throws: "from close"  — this becomes SUPPRESSED

// The primary exception ("from try") is thrown.
// The close exception is added as a SUPPRESSED exception.
// You can access it via: e.getSuppressed()
```

```java
catch (Exception e) {
    System.out.println(e.getMessage());                    // "from try"
    Throwable[] suppressed = e.getSuppressed();
    for (Throwable t : suppressed) {
        System.out.println("Suppressed: " + t.getMessage()); // "from close"
    }
}
```

**Java 9 Enhancement**: You can use effectively final variables in try-with-resources:
```java
// Java 7/8 — must declare in try()
FileReader fr = new FileReader("test.txt");
try (FileReader fr2 = fr) { }               // Needed a new variable

// Java 9+ — use existing effectively final variable
FileReader fr = new FileReader("test.txt");
try (fr) { }                                 // Direct use! Cleaner
```

### 2.7 Exception Chaining (Wrapping)

Wrapping a low-level exception inside a higher-level one preserves the original cause while giving the caller a more meaningful exception:

```java
// Without chaining — original cause is LOST
try {
    connection.execute(sql);
} catch (SQLException e) {
    throw new ServiceException("Failed to save patient");
    // ❌ Original SQLException details are lost!
}

// With chaining — original cause is PRESERVED
try {
    connection.execute(sql);
} catch (SQLException e) {
    throw new ServiceException("Failed to save patient", e);
    // ✅ 'e' is the CAUSE — accessible via getCause()
}
```

```java
// Accessing the chain
catch (ServiceException e) {
    System.out.println(e.getMessage());                    // "Failed to save patient"
    System.out.println(e.getCause().getMessage());         // Original SQL error message
    System.out.println(e.getCause().getClass().getName()); // java.sql.SQLException
}

// Alternative: initCause() method
RuntimeException re = new RuntimeException("wrapper");
re.initCause(originalException);
throw re;
```

> [!IMPORTANT]
> **Always chain exceptions** when wrapping. Losing the original cause makes debugging in production nearly impossible. When you see an error log with no root cause, it means someone swallowed or didn't chain the exception.

---

## 3. Custom Exceptions & Best Practices

### 3.1 When to Create Custom Exceptions

Create custom exceptions when:
1. **Domain-specific errors** need distinct handling — `PatientNotFoundException`, `DuplicateAdmissionException`
2. You need to **carry additional data** — error codes, field names, severity levels
3. **Existing Java exceptions** don't convey the business meaning
4. You want to **decouple layers** — service throws business exceptions, not SQL exceptions

### 3.2 Creating Custom Checked Exception

```java
// Checked — caller MUST handle or declare
public class PatientNotFoundException extends Exception {
    
    private final String patientId;
    
    // Constructor with message
    public PatientNotFoundException(String message) {
        super(message);
        this.patientId = null;
    }
    
    // Constructor with message and cause (for chaining)
    public PatientNotFoundException(String message, Throwable cause) {
        super(message, cause);
        this.patientId = null;
    }
    
    // Constructor with additional data
    public PatientNotFoundException(String patientId, String message) {
        super(message);
        this.patientId = patientId;
    }
    
    public String getPatientId() {
        return patientId;
    }
}
```

### 3.3 Creating Custom Unchecked Exception

```java
// Unchecked — caller MAY handle (optional)
public class InvalidAssessmentException extends RuntimeException {
    
    private final String fieldName;
    private final String errorCode;
    
    public InvalidAssessmentException(String message) {
        super(message);
        this.fieldName = null;
        this.errorCode = "VALIDATION_ERROR";
    }
    
    public InvalidAssessmentException(String fieldName, String message) {
        super(message);
        this.fieldName = fieldName;
        this.errorCode = "VALIDATION_ERROR";
    }
    
    public InvalidAssessmentException(String message, Throwable cause) {
        super(message, cause);
        this.fieldName = null;
        this.errorCode = "VALIDATION_ERROR";
    }
    
    public String getFieldName() { return fieldName; }
    public String getErrorCode() { return errorCode; }
}
```

### 3.4 Building a Real Exception Hierarchy — Healthcare Project

> [!TIP]
> **From Your Project**: Here's how a clean exception hierarchy looks for the Healthcare application:

```java
// Base exception for all healthcare business exceptions
public abstract class HealthcareException extends RuntimeException {
    private final String errorCode;
    private final LocalDateTime timestamp;
    
    protected HealthcareException(String errorCode, String message) {
        super(message);
        this.errorCode = errorCode;
        this.timestamp = LocalDateTime.now();
    }
    
    protected HealthcareException(String errorCode, String message, Throwable cause) {
        super(message, cause);
        this.errorCode = errorCode;
        this.timestamp = LocalDateTime.now();
    }
    
    public String getErrorCode() { return errorCode; }
    public LocalDateTime getTimestamp() { return timestamp; }
}

// Specific exceptions
public class PatientNotFoundException extends HealthcareException {
    public PatientNotFoundException(String patientId) {
        super("PATIENT_NOT_FOUND", "Patient not found with ID: " + patientId);
    }
}

public class DuplicateAdmissionException extends HealthcareException {
    public DuplicateAdmissionException(String patientId) {
        super("DUPLICATE_ADMISSION", "Patient " + patientId + " is already admitted");
    }
}

public class InvalidAssessmentException extends HealthcareException {
    public InvalidAssessmentException(String field, String reason) {
        super("INVALID_ASSESSMENT", "Assessment validation failed for '" + field + "': " + reason);
    }
}
```

```
Exception Hierarchy:
RuntimeException
  └── HealthcareException (abstract base)
        ├── PatientNotFoundException
        ├── DuplicateAdmissionException
        ├── InvalidAssessmentException
        └── DocuSignIntegrationException
```

**Using it with Spring's @ControllerAdvice**:
```java
@RestControllerAdvice
public class GlobalExceptionHandler {
    
    @ExceptionHandler(PatientNotFoundException.class)
    public ResponseEntity<ErrorResponse> handlePatientNotFound(PatientNotFoundException ex) {
        ErrorResponse error = new ErrorResponse(
            ex.getErrorCode(), ex.getMessage(), ex.getTimestamp()
        );
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
    }
    
    @ExceptionHandler(HealthcareException.class)   // Catch-all for business exceptions
    public ResponseEntity<ErrorResponse> handleBusinessException(HealthcareException ex) {
        ErrorResponse error = new ErrorResponse(
            ex.getErrorCode(), ex.getMessage(), ex.getTimestamp()
        );
        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(error);
    }
    
    @ExceptionHandler(Exception.class)   // Catch-all safety net
    public ResponseEntity<ErrorResponse> handleUnexpected(Exception ex) {
        ErrorResponse error = new ErrorResponse(
            "INTERNAL_ERROR", "An unexpected error occurred", LocalDateTime.now()
        );
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(error);
    }
}
```

### 3.5 Best Practices — 12 Rules

| # | Rule | Bad Example | Good Example |
|---|------|------------|--------------|
| 1 | **Catch specific exceptions** | `catch (Exception e)` | `catch (IOException e)` |
| 2 | **Never swallow exceptions** | `catch (Exception e) { }` (empty catch) | `catch (Exception e) { logger.error("msg", e); }` |
| 3 | **Use try-with-resources** | Manual close in finally | `try (var conn = getConn())` |
| 4 | **Don't use exceptions for flow control** | Catch NPE to check if null | `if (obj != null)` |
| 5 | **Log OR throw, never both** | Log then throw (double logging) | Throw and let the caller decide |
| 6 | **Chain exceptions** | `throw new X("msg")` | `throw new X("msg", cause)` |
| 7 | **Declare specific in throws** | `throws Exception` | `throws IOException, SQLException` |
| 8 | **Prefer unchecked for bugs** | Checked for null args | `throw new IllegalArgumentException(...)` |
| 9 | **Prefer checked for recoverable** | Unchecked for external failures | Checked `IOException` for file operations |
| 10 | **Document with @throws** | No documentation | `@throws PatientNotFoundException if ID is invalid` |
| 11 | **Never return from finally** | `finally { return x; }` | Remove the return from finally |
| 12 | **Catch early, throw late** | Catch low-level errors at low level | Let exceptions bubble up to appropriate handler |

```java
// RULE 4 — Don't use exceptions for flow control
// ❌ BAD
try {
    int value = Integer.parseInt(input);
} catch (NumberFormatException e) {
    value = 0;    // Using exception as an if-check
}

// ✅ GOOD — check BEFORE calling
if (input != null && input.matches("\\d+")) {
    int value = Integer.parseInt(input);
} else {
    int value = 0;
}

// RULE 5 — Log OR throw, not both
// ❌ BAD — double logging when caller also logs
catch (SQLException e) {
    logger.error("DB error", e);
    throw new ServiceException("Failed", e);    // Caller will also log!
}

// ✅ GOOD — just throw, let the handler log
catch (SQLException e) {
    throw new ServiceException("Failed to save patient", e);
}
```

### Checked vs Unchecked — When to Create Which?

| Create **Checked** Exception When... | Create **Unchecked** Exception When... |
|--------------------------------------|---------------------------------------|
| Caller CAN recover from it | It's a programming bug |
| Caller SHOULD be forced to handle | Caller shouldn't be forced (99% catch doesn't help) |
| External system failure (file, DB, API) | Invalid argument, illegal state |
| Example: `InsufficientFundsException` | Example: `InvalidPatientIdException` |

> [!NOTE]
> **Modern trend**: Most Java frameworks (Spring, Hibernate) use **unchecked exceptions** by default. Spring wraps all checked exceptions (like `SQLException`) into unchecked ones (`DataAccessException`). This is because most checked exceptions in practice are logged and re-thrown — the `throws` declaration adds noise without value.

---

## 4. Object Class — The Root of Everything

**Every class in Java** implicitly extends `java.lang.Object`. This means every object has access to Object's 11 methods.

```java
class Patient { }
// is equivalent to:
class Patient extends Object { }
```

### 4.1 All 11 Methods of Object Class

| Method | Returns | Purpose | Override? |
|--------|---------|---------|-----------|
| `toString()` | `String` | String representation of object | ✅ Always |
| `equals(Object)` | `boolean` | Logical equality comparison | ✅ When needed |
| `hashCode()` | `int` | Hash value for hash-based collections | ✅ Always with equals() |
| `getClass()` | `Class<?>` | Runtime class of the object | ❌ `final` — cannot |
| `clone()` | `Object` | Creates a copy | ✅ Rarely (use copy constructor) |
| `finalize()` | `void` | Called before GC (⚠️ **deprecated** Java 9) | ❌ Never |
| `wait()` | `void` | Thread waits for notification | ❌ Rarely directly |
| `wait(long)` | `void` | Thread waits with timeout | ❌ Rarely directly |
| `wait(long, int)` | `void` | Thread waits with precise timeout | ❌ Rarely directly |
| `notify()` | `void` | Wakes up one waiting thread | ❌ Rarely directly |
| `notifyAll()` | `void` | Wakes up all waiting threads | ❌ Rarely directly |

### 4.2 toString()

**Default**: Returns `ClassName@hexHashCode` — useless for debugging.

```java
Patient p = new Patient("Angooj", 28);
System.out.println(p);          // Default: Patient@1b6d3586 ← meaningless!
```

**Override for meaningful output**:
```java
@Override
public String toString() {
    return "Patient{name='" + name + "', age=" + age + ", id='" + patientId + "'}";
}

System.out.println(p);          // Patient{name='Angooj', age=28, id='P001'}
```

> [!TIP]
> `toString()` is called automatically by: `System.out.println(obj)`, `"" + obj`, `String.valueOf(obj)`, logger statements, debugger displays. Always override it for better debugging.
>
> In production, use **Lombok's `@ToString`** to auto-generate:
> ```java
> @ToString
> public class Patient {
>     private String name;
>     private int age;
> }
> // Auto-generates: Patient(name=Angooj, age=28)
> ```

### 4.3 equals() — Deep Dive

**Default behavior**: Same as `==` — compares **references** (memory addresses).

```java
Patient p1 = new Patient("P001", "Angooj");
Patient p2 = new Patient("P001", "Angooj");

p1.equals(p2);     // false! ← Default equals() checks if p1 and p2 are the SAME object
p1 == p2;           // false  ← Same thing
```

**Overriding equals() — The Correct Way** (5-step recipe):

```java
public class Patient {
    private String patientId;
    private String name;
    private int age;
    
    @Override
    public boolean equals(Object o) {
        // Step 1: Same reference? → true (optimization)
        if (this == o) return true;
        
        // Step 2: Null check → false
        if (o == null) return false;
        
        // Step 3: Same class? (NOT instanceof — explained below)
        if (getClass() != o.getClass()) return false;
        
        // Step 4: Cast to our type
        Patient patient = (Patient) o;
        
        // Step 5: Compare significant fields
        return age == patient.age &&
               Objects.equals(patientId, patient.patientId) &&
               Objects.equals(name, patient.name);
    }
}
```

**`getClass()` vs `instanceof` in equals()**:

| | `getClass() != o.getClass()` | `!(o instanceof Patient)` |
|---|---|---|
| Behavior | Exact same class required | Allows subclasses to be equal |
| Symmetry | ✅ Always symmetric | ⚠️ Can break symmetry |
| When to use | Default — most cases | When subclass should be "equal" to parent |

```java
// Symmetry problem with instanceof:
class Patient { }
class VIPPatient extends Patient { }

Patient p = new Patient("P001");
VIPPatient vip = new VIPPatient("P001");

// With instanceof in Patient.equals():
p.equals(vip);    // true  — vip instanceof Patient
vip.equals(p);    // false — p NOT instanceof VIPPatient
// ❌ Breaks symmetry! a.equals(b) should equal b.equals(a)
```

**The 5 Contracts of equals()**:

| Contract | Meaning | Example |
|----------|---------|---------|
| **Reflexive** | `x.equals(x)` must be `true` | Every object equals itself |
| **Symmetric** | If `a.equals(b)` then `b.equals(a)` | Both directions must agree |
| **Transitive** | If `a.equals(b)` and `b.equals(c)`, then `a.equals(c)` | Equality chains |
| **Consistent** | Multiple calls return same result (if objects unchanged) | No randomness |
| **Null** | `x.equals(null)` must be `false` | Nothing equals null |

### 4.4 hashCode() — Deep Dive

**What is a hashCode?** An integer value computed from an object's data, used by hash-based collections (`HashMap`, `HashSet`, `Hashtable`) to quickly locate objects.

```java
// Default hashCode() — based on memory address (different for every object)
Patient p1 = new Patient("P001", "Angooj");
Patient p2 = new Patient("P001", "Angooj");
p1.hashCode();    // e.g., 123456
p2.hashCode();    // e.g., 789012 ← Different! (different objects in memory)
```

**Override to match equals()**:
```java
@Override
public int hashCode() {
    return Objects.hash(patientId, name, age);
    // Uses same fields as equals() — this is THE RULE
}

// Now:
p1.hashCode();    // e.g., 54321
p2.hashCode();    // e.g., 54321 ← Same! (same data)
```

### 4.5 The equals/hashCode Contract ⚠️

This is **one of the most critical contracts** in Java and is asked in almost every interview.

**The Rules**:
1. If `a.equals(b)` is `true` → `a.hashCode() == b.hashCode()` **MUST** be true
2. If `a.hashCode() != b.hashCode()` → `a.equals(b)` **MUST** be false
3. If `a.hashCode() == b.hashCode()` → `a.equals(b)` **MAY** be true or false (hash collision is OK)

**Visual — What happens inside HashMap**:

```
HashMap with 16 buckets:

Bucket Index = hashCode(key) & (16 - 1)    ← determines which bucket

Bucket 0: ┌─────┐
           │     │ → null
           └─────┘
Bucket 1: ┌─────┐
           │     │ → null
           └─────┘
Bucket 3: ┌─────┐    ┌──────────┐    ┌──────────┐
           │     │ →  │ K1 → V1  │ →  │ K2 → V2  │ → null
           └─────┘    └──────────┘    └──────────┘
                      K1.hashCode() & 15 == 3
                      K2.hashCode() & 15 == 3    ← Collision! Same bucket

When searching for K2:
  1. Compute K2.hashCode() → get bucket index (3)
  2. Go to bucket 3
  3. Compare K2.equals(K1) → false → move to next node
  4. Compare K2.equals(K2) → true → FOUND! Return V2
```

**What BREAKS if you override equals() without hashCode()?**

```java
// Override only equals(), NOT hashCode()
Patient p1 = new Patient("P001", "Angooj");
Patient p2 = new Patient("P001", "Angooj");  // Same data

p1.equals(p2);    // true ✅

Set<Patient> set = new HashSet<>();
set.add(p1);
set.contains(p2); // false! ❌ WHY?
// p2.hashCode() differs from p1.hashCode() (default = memory address)
// p2 goes to a DIFFERENT bucket → never compared with p1 using equals()
// The set "can't find" p2 even though an equal object exists!

Map<Patient, String> map = new HashMap<>();
map.put(p1, "Found");
map.get(p2);      // null! ❌ Same problem — different bucket
```

> [!IMPORTANT]
> **Golden Rule**: If you override `equals()`, you **MUST** override `hashCode()`. If you override `hashCode()`, you **SHOULD** override `equals()`. They always go together.
>
> Use the same fields in both methods. If `equals()` compares `patientId` and `name`, then `hashCode()` must use `patientId` and `name`.

### 4.6 clone() — Shallow vs Deep Copy

**Shallow Copy**: Copies the object's fields. For primitive fields, copies the value. For reference fields, copies the **reference** (both original and clone point to the SAME nested object).

**Deep Copy**: Creates new copies of all nested objects too. Completely independent objects.

```
SHALLOW COPY:
Original Patient          Cloned Patient
┌─────────────┐           ┌─────────────┐
│ name: ──────│──────┐    │ name: ──────│──────┐
│ age: 28     │      │    │ age: 28     │      │
│ address: ───│──┐   │    │ address: ───│──┐   │
└─────────────┘  │   │    └─────────────┘  │   │
                 │   │                      │   │
                 │   └──────►"Angooj"◄──────┘   │
                 │                              │
                 └──────────►Address◄───────────┘
                          (SAME object!)

DEEP COPY:
Original Patient          Cloned Patient
┌─────────────┐           ┌─────────────┐
│ name: ──────│──► "Angooj"  │ name: ──────│──► "Angooj" (new)
│ age: 28     │           │ age: 28     │
│ address: ───│──► Addr1  │ address: ───│──► Addr2 (new copy!)
└─────────────┘           └─────────────┘
```

```java
// Implementing clone (shallow)
public class Patient implements Cloneable {
    private String name;
    private int age;
    private Address address;   // Reference type
    
    @Override
    public Patient clone() {
        try {
            return (Patient) super.clone();   // Shallow copy
            // name → shared (but String is immutable, so OK)
            // age → copied (primitive)
            // address → shared reference! (PROBLEM for mutable objects)
        } catch (CloneNotSupportedException e) {
            throw new RuntimeException(e);    // Should never happen
        }
    }
    
    // Deep copy version
    public Patient deepClone() {
        try {
            Patient cloned = (Patient) super.clone();
            cloned.address = new Address(this.address);   // Create new Address copy
            return cloned;
        } catch (CloneNotSupportedException e) {
            throw new RuntimeException(e);
        }
    }
}
```

> [!TIP]
> **Modern Java practice**: Avoid `clone()`. Use **copy constructors** or **static factory methods** instead — they're cleaner and don't require `Cloneable` interface:
> ```java
> // Copy constructor — preferred approach
> public Patient(Patient other) {
>     this.name = other.name;
>     this.age = other.age;
>     this.address = new Address(other.address);   // Deep copy
> }
> 
> // Usage
> Patient original = new Patient("Angooj", 28);
> Patient copy = new Patient(original);   // Clean, no Cloneable needed
> ```

### 4.7 finalize(), getClass(), wait/notify

**finalize()** — ⚠️ **DEPRECATED since Java 9**:
```java
// Called by GC before destroying the object — DO NOT USE
@Override
protected void finalize() throws Throwable {
    // Cleanup resources
    super.finalize();
}
// Problems: no guarantee it runs, delays GC, performance hit
// Use try-with-resources or explicit close() instead
```

**getClass()** — Returns the runtime class:
```java
Patient p = new Patient();
Class<?> clazz = p.getClass();

clazz.getName();           // "com.hospital.Patient"
clazz.getSimpleName();     // "Patient"
clazz.getSuperclass();     // class java.lang.Object

// Useful for runtime type checking
if (obj.getClass() == Patient.class) { }   // Exact match (no subclasses)
if (obj instanceof Patient) { }            // Includes subclasses
```

**wait() / notify() / notifyAll()** — Thread communication:
```java
// These must be called from within a synchronized block
synchronized (lock) {
    while (conditionNotMet) {
        lock.wait();          // Release lock, thread sleeps until notified
    }
    // Condition is now met, proceed
}

// Another thread:
synchronized (lock) {
    // Change the condition
    lock.notify();            // Wake up ONE waiting thread
    // lock.notifyAll();      // Wake up ALL waiting threads
}
```

These are covered in detail on Day 6 (Multithreading).

---

## 5. Common Mistakes & Anti-Patterns

### Mistake 1: Empty Catch Block (Swallowing Exceptions)

```java
// ❌ THE WORST — exception is silently lost, bugs become invisible
try {
    patient = patientRepository.findById(id);
} catch (Exception e) {
    // Nothing here! The error is swallowed.
    // Production bug: "Why is patient null? No error in logs!"
}

// ✅ At minimum, LOG the exception
try {
    patient = patientRepository.findById(id);
} catch (Exception e) {
    logger.error("Failed to find patient {}", id, e);
    throw new PatientNotFoundException(id);
}
```

### Mistake 2: Catching `Exception` or `Throwable` Broadly

```java
// ❌ TOO BROAD — catches everything including bugs you should fix
try {
    processPatient(patient);
} catch (Exception e) {
    System.out.println("Something went wrong");
    // This catches NullPointerException too — hiding a real bug!
}

// ✅ CATCH SPECIFIC — handle what you expect, let bugs crash loudly
try {
    processPatient(patient);
} catch (PatientNotFoundException e) {
    return ResponseEntity.notFound().build();
} catch (DuplicateAdmissionException e) {
    return ResponseEntity.status(CONFLICT).body(e.getMessage());
}
// NullPointerException will propagate — as it should (it's a bug to fix)
```

### Mistake 3: Using Exceptions for Flow Control

```java
// ❌ BAD — exceptions are expensive (stack trace capture)
public boolean isNumeric(String str) {
    try {
        Integer.parseInt(str);
        return true;
    } catch (NumberFormatException e) {
        return false;    // Using exception as if-else — 10x slower
    }
}

// ✅ GOOD — check before calling
public boolean isNumeric(String str) {
    if (str == null || str.isEmpty()) return false;
    return str.chars().allMatch(Character::isDigit);
}
```

### Mistake 4: Losing the Original Cause When Wrapping

```java
// ❌ CAUSE LOST — impossible to debug in production
catch (SQLException e) {
    throw new ServiceException("Database error");
    // WHERE was the SQL error? What query? What table? ALL LOST.
}

// ✅ CAUSE PRESERVED — full chain visible in stack trace
catch (SQLException e) {
    throw new ServiceException("Failed to save patient record", e);
    // Stack trace shows: ServiceException → caused by: SQLException → actual DB error
}
```

### Mistake 5: Log AND Throw (Double Logging)

```java
// ❌ DOUBLE LOGGING — same error appears twice in logs
catch (IOException e) {
    logger.error("File read failed", e);      // Logged here
    throw new ServiceException("Failed", e);  // Handler will ALSO log it!
}

// ✅ CHOOSE ONE — either log OR throw
// Option A: Handle here (log + recover)
catch (IOException e) {
    logger.warn("File read failed, using default config", e);
    return getDefaultConfig();    // Recovered!
}

// Option B: Propagate (throw — let caller decide)
catch (IOException e) {
    throw new ServiceException("Failed to read config", e);
}
```

### Mistake 6: Not Overriding hashCode() with equals()

```java
// ❌ BROKEN HashMap/HashSet behavior
public class Patient {
    private String id;
    
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Patient)) return false;
        return Objects.equals(id, ((Patient) o).id);
    }
    // Missing hashCode()!
}

Set<Patient> set = new HashSet<>();
set.add(new Patient("P001"));
set.contains(new Patient("P001"));   // false! ← WRONG, should be true

// ✅ ALWAYS override both together
@Override
public int hashCode() {
    return Objects.hash(id);
}
```

### Mistake 7: Returning from finally Block

```java
// ❌ SILENTLY SWALLOWS exceptions and overrides return values
public int calculate() {
    try {
        return 10 / 0;           // ArithmeticException thrown!
    } catch (ArithmeticException e) {
        throw e;                  // Exception re-thrown...
    } finally {
        return -1;                // ...but finally's return OVERRIDES everything!
    }
}
// Returns -1, exception is silently lost. NO crash, NO error log. A silent bug.

// ✅ Never put return in finally
```

### Mistake 8: Catching CloneNotSupportedException Wrong

```java
// ❌ Forgetting to implement Cloneable
public class Patient {
    @Override
    public Patient clone() {
        return (Patient) super.clone();   // CloneNotSupportedException at runtime!
    }
}

// ✅ Implement Cloneable OR use copy constructor instead
public class Patient implements Cloneable {
    @Override
    public Patient clone() { ... }
}
// Even better: just use a copy constructor (no Cloneable needed)
```

---

## 6. Interview Questions & Answers

### Category A: Exception Basics (15 Questions)

---

**Q1 🟢: What is an exception in Java?**

**Answer**: An exception is an abnormal event that disrupts normal program flow at runtime. Java provides a mechanism (`try-catch-finally`) to handle these events gracefully. All exceptions extend `java.lang.Throwable`. Exceptions are objects — they carry information about what went wrong (message, stack trace, cause).

---

**Q2 🟢: What is the difference between Error and Exception?**

**Answer**:
- **Error**: Caused by the JVM/system — not recoverable. Examples: `StackOverflowError`, `OutOfMemoryError`. You should NOT catch errors.
- **Exception**: Caused by the application/programmer — usually recoverable. Examples: `NullPointerException`, `IOException`. You SHOULD handle exceptions.

Both extend `Throwable`, but Error indicates serious problems that a reasonable application should not try to handle.

---

**Q3 🟢: What is the difference between checked and unchecked exceptions?**

**Answer**:
- **Checked**: Compiler forces you to handle (try-catch or throws). Extends `Exception` but NOT `RuntimeException`. Represents recoverable situations. Examples: `IOException`, `SQLException`.
- **Unchecked**: Compiler doesn't force handling. Extends `RuntimeException` or `Error`. Represents programming bugs. Examples: `NullPointerException`, `ArrayIndexOutOfBoundsException`.

**Key rule**: Everything that extends `RuntimeException` or `Error` is unchecked. Everything else under `Exception` is checked.

---

**Q4 🟡: Can we catch `Error` in Java? Should we?**

**Answer**: **Can we?** Yes, technically — `Error` extends `Throwable`, so it can be caught. **Should we?** Almost never. Errors indicate severe JVM problems (out of memory, stack overflow). Catching them usually doesn't help because the JVM is in an unstable state. Exception: monitoring tools sometimes catch `OutOfMemoryError` to send an alert before dying.

---

**Q5 🟡: What is the difference between `throw` and `throws`?**

**Answer**:
| `throw` | `throws` |
|---------|----------|
| Used inside method body | Used in method signature |
| Followed by an exception **object** | Followed by exception **class names** |
| Throws one exception at a time | Can declare multiple exceptions |
| Actually creates and throws | Just declares the possibility |

```java
public void validate(String id) throws PatientNotFoundException {    // throws = declaration
    if (id == null) {
        throw new PatientNotFoundException("ID is null");             // throw = action
    }
}
```

---

**Q6 🟢: What is the `finally` block? When does it execute?**

**Answer**: `finally` is a block that **always executes** after try-catch, regardless of whether an exception occurred, was caught, or not. Used for cleanup (closing files, connections).

**When it does NOT execute** (rare):
1. `System.exit()` is called before finally
2. JVM crashes
3. The thread running the try-catch is killed
4. Infinite loop in try or catch

---

**Q7 🟡: Predict the output:**
```java
public static int test() {
    try {
        return 1;
    } catch (Exception e) {
        return 2;
    } finally {
        return 3;
    }
}
System.out.println(test());
```

**Answer**: **`3`**. The finally block's `return` overrides the try block's `return`. The value 1 is "saved" by the try's return, but finally's return replaces it with 3 before the method actually returns. **Never return from finally — it silently swallows exceptions and return values.**

---

**Q8 🟡: Predict the output:**
```java
try {
    System.out.println("A");
    throw new RuntimeException();
} catch (Exception e) {
    System.out.println("B");
} catch (RuntimeException e) {    // ← What happens?
    System.out.println("C");
} finally {
    System.out.println("D");
}
```

**Answer**: **Compile error!** `RuntimeException` extends `Exception`, so the `catch (Exception e)` already catches `RuntimeException`. The second catch is unreachable. Specific exceptions must come **before** general ones.

---

**Q9 🟡: What is exception propagation? How does it work?**

**Answer**: When an exception occurs in a method and is not caught there, it propagates (travels) up the **call stack** to the calling method. This continues until a matching catch block is found. If no catch block is found in the entire call stack, the JVM prints the stack trace and terminates the thread.

For unchecked exceptions, propagation is automatic. For checked exceptions, each method in the chain must either catch OR declare with `throws`.

---

**Q10 🟡: What is `try-with-resources`? Why was it introduced?**

**Answer**: A Java 7 feature that automatically closes resources when the try block exits. The resource must implement `AutoCloseable`. It was introduced to eliminate resource leak bugs caused by forgetting to close resources in finally blocks.

```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line = br.readLine();
}
// br.close() is called automatically — even if exception occurs!
```

Benefits: cleaner code, no resource leaks, handles close() exceptions via suppression mechanism.

---

**Q11 🟡: What are suppressed exceptions in try-with-resources?**

**Answer**: When both the try block AND the `close()` method throw exceptions, the try block's exception is the "primary" one, and the close() exception is "suppressed" (attached to the primary). This prevents the close exception from hiding the real error.

```java
catch (Exception e) {
    e.getMessage();                    // Primary exception
    e.getSuppressed();                 // Array of suppressed exceptions from close()
}
```

---

**Q12 🟡: What is multi-catch? What are its rules?**

**Answer**: Java 7 allows catching multiple unrelated exception types in one catch block using `|` (pipe):

```java
catch (IOException | SQLException e) { }
```

Rules: (1) Exception types must be unrelated (no parent-child). (2) The variable `e` is implicitly `final`. (3) Reduces code duplication when handling is identical.

---

**Q13 🟢: What is `NullPointerException`? How to avoid it?**

**Answer**: Thrown when you call a method or access a field on a `null` reference.

Prevention techniques:
1. Null checks: `if (obj != null)`
2. `Optional<T>` (Java 8): `Optional.ofNullable(obj).orElse(default)`
3. Objects.requireNonNull(): `Objects.requireNonNull(param, "must not be null")`
4. Use `"literal".equals(variable)` instead of `variable.equals("literal")`
5. Avoid returning `null` — return empty collections or Optional
6. `@NonNull` / `@Nullable` annotations

---

**Q14 🟡: What is exception chaining? Why is it important?**

**Answer**: Wrapping a low-level exception inside a higher-level one while preserving the original as the "cause":

```java
catch (SQLException e) {
    throw new ServiceException("Failed to save patient", e);   // e is the cause
}
```

Important because: (1) The caller gets a meaningful business exception. (2) The original technical error is preserved for debugging. (3) Stack trace shows the full chain. Without chaining, the root cause is lost and production debugging becomes impossible.

---

**Q15 🟡: What is `final` vs `finally` vs `finalize()`?**

**Answer**:
| | `final` | `finally` | `finalize()` |
|---|---------|-----------|-------------|
| Type | Keyword | Block | Method |
| Purpose | Prevent change/override/extend | Ensure cleanup always runs | GC callback before destruction |
| Usage | Variables, methods, classes | After try-catch | Override in Object subclass |
| Status | ✅ Active | ✅ Active | ⚠️ **Deprecated** (Java 9) |

`final int x = 10;` — constant. `finally { conn.close(); }` — cleanup. `finalize()` — don't use, use `try-with-resources` instead.

---

### Category B: Custom Exceptions & Best Practices (8 Questions)

---

**Q16 🟡: How do you create a custom exception?**

**Answer**: Extend `Exception` (for checked) or `RuntimeException` (for unchecked). Provide constructors for message and cause:

```java
public class PatientNotFoundException extends RuntimeException {
    public PatientNotFoundException(String message) {
        super(message);
    }
    public PatientNotFoundException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

---

**Q17 🟡: When should you create a checked vs unchecked custom exception?**

**Answer**: **Checked** when the caller can meaningfully recover (retry, use default, ask user). **Unchecked** when it's a programming error or the caller can't do anything useful (invalid argument, illegal state). Modern frameworks (Spring) prefer unchecked because most checked exceptions end up being logged-and-rethrown anyway.

---

**Q18 🔴: How do you implement a global exception handler in Spring Boot?**

**Answer**: Using `@RestControllerAdvice` with `@ExceptionHandler` methods:

```java
@RestControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(PatientNotFoundException.class)
    public ResponseEntity<ErrorResponse> handle(PatientNotFoundException ex) {
        return ResponseEntity.status(NOT_FOUND)
            .body(new ErrorResponse(ex.getMessage()));
    }
    
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleAll(Exception ex) {
        return ResponseEntity.status(INTERNAL_SERVER_ERROR)
            .body(new ErrorResponse("Unexpected error"));
    }
}
```

This centralizes exception-to-HTTP-response mapping, keeping controllers clean.

---

**Q19 🟡: What happens if an exception is thrown in a `catch` block?**

**Answer**: The exception propagates normally. The `finally` block still executes before the new exception leaves the method. If there's no enclosing try-catch to handle it, it propagates up the call stack.

```java
try {
    throw new RuntimeException("first");
} catch (RuntimeException e) {
    throw new RuntimeException("second");   // New exception from catch
} finally {
    System.out.println("finally runs");     // Still executes!
}
// "finally runs" prints, then RuntimeException("second") propagates
```

---

**Q20 🟡: Can a `try` block exist without `catch`?**

**Answer**: Yes, `try` can exist with only `finally` (no `catch`):
```java
try {
    riskyOperation();
} finally {
    cleanup();    // Cleanup happens, but exception still propagates
}
```
The exception is NOT caught — it propagates to the caller. But finally ensures cleanup happens first. This is used in try-with-resources internally.

---

**Q21 🟡: What is `StackOverflowError` vs `OutOfMemoryError`?**

**Answer**:
| | StackOverflowError | OutOfMemoryError |
|---|---|---|
| Memory area | Stack (per thread) | Heap (shared) |
| Cause | Too-deep/infinite recursion | Too many objects, memory leak |
| Fix | Add base case, reduce recursion depth | Increase heap (`-Xmx`), fix leak |
| Example | `void f() { f(); }` | Creating millions of objects without GC |
| Type | Error (unchecked) | Error (unchecked) |

---

**Q22 🟡: Can we have a `return` statement in `finally`?**

**Answer**: **Yes, but NEVER do it.** A return in finally overrides the try/catch return value AND silently swallows any exception being thrown. It's a severe anti-pattern that creates silent bugs.

---

**Q23 🔴: What is the difference between `ClassNotFoundException` and `NoClassDefFoundError`?**

**Answer**:
| | ClassNotFoundException | NoClassDefFoundError |
|---|---|---|
| Type | Checked Exception | Error (unchecked) |
| When | Class not found at **runtime** via reflection | Class present at **compile time** but missing at runtime |
| Cause | `Class.forName("Missing")`, `ClassLoader.loadClass()` | Deleted jar, corrupt classpath after compilation |
| Fix | Check classpath, verify class name | Fix deployment, rebuild dependencies |

---

### Category C: Object Class (12 Questions)

---

**Q24 🟢: What is the `Object` class? Why is it important?**

**Answer**: `Object` is the root class of all Java classes. Every class implicitly extends Object. It provides 11 fundamental methods that every object inherits: `toString()`, `equals()`, `hashCode()`, `getClass()`, `clone()`, `finalize()`, `wait()` (3 overloads), `notify()`, `notifyAll()`. It establishes the common behavior contract for all Java objects.

---

**Q25 🟢: Why should you override `toString()`?**

**Answer**: Default `toString()` returns `ClassName@hexHashCode` which is meaningless. Override to provide human-readable representation for: debugging, logging, error messages, UI display. It's called automatically by `println()`, string concatenation, and loggers. In production, use Lombok's `@ToString` for auto-generation.

---

**Q26 🟢: What is the `equals()` and `hashCode()` contract?**

**Answer**: Three rules:
1. If `a.equals(b)` → `a.hashCode() == b.hashCode()` **MUST** be true
2. If `a.hashCode() != b.hashCode()` → `a.equals(b)` **MUST** be false
3. If `a.hashCode() == b.hashCode()` → `a.equals(b)` **MAY** be true or false

Breaking rule 1 causes `HashMap`/`HashSet` to malfunction — equal objects end up in different buckets and can't find each other.

---

**Q27 🟡: What happens if you override `equals()` without `hashCode()`?**

**Answer**: Hash-based collections (`HashMap`, `HashSet`) will malfunction. Two logically equal objects will have different hash codes, land in different buckets, and never be compared with `equals()`. Result: `set.contains(equalObject)` returns `false`, `map.get(equalKey)` returns `null`.

---

**Q28 🟡: What is the difference between `==` and `equals()`?**

**Answer**:
- `==`: Compares **references** (memory addresses) for objects; compares **values** for primitives
- `equals()`: Compares **content/logical equality** (if properly overridden)

Default `Object.equals()` uses `==` (reference comparison). Classes like `String`, `Integer`, `LocalDate` override it for content comparison. Your custom classes should override it if logical equality matters.

---

**Q29 🟡: How do you properly override `equals()`?**

**Answer**: 5-step recipe:
1. Check `this == obj` (same reference → true)
2. Check `obj == null` (null → false)
3. Check `getClass()` match (different class → false)
4. Cast to your type
5. Compare significant fields using `Objects.equals()` for objects, `==` for primitives

Follow contracts: reflexive, symmetric, transitive, consistent, null-returns-false.

---

**Q30 🟡: What is the difference between shallow copy and deep copy?**

**Answer**:
- **Shallow copy**: Copies field values. For references, copies the reference (not the object). Both copies share the same nested objects.
- **Deep copy**: Copies everything including nested objects. Completely independent copies.

```java
// Shallow: clone.address == original.address (same object)
// Deep: clone.address != original.address (different object, same data)
```

Use deep copy when the cloned object should be completely independent. Prefer copy constructors over `clone()`.

---

**Q31 🟡: Why is `clone()` considered broken? What to use instead?**

**Answer**: `clone()` problems:
1. Requires `Cloneable` marker interface (no method — confusing design)
2. Returns `Object` — needs casting
3. Performs shallow copy by default — must manually implement deep copy
4. Doesn't call constructors — can create objects in invalid state
5. `CloneNotSupportedException` is checked — annoying to handle

**Better alternatives**: Copy constructors, static factory methods (`Patient.copyOf(original)`), or serialization-based deep copy.

---

**Q32 🟡: What is `getClass()` and how is it different from `instanceof`?**

**Answer**:
- `getClass()`: Returns exact runtime class. `obj.getClass() == Patient.class` — only matches Patient, NOT subclasses.
- `instanceof`: Type check including subclasses. `obj instanceof Patient` — true for Patient AND all its subclasses.

Use `getClass()` in `equals()` for strict type matching. Use `instanceof` when you want to include subclass compatibility.

---

**Q33 🟡: Why is `finalize()` deprecated? What replaces it?**

**Answer**: Deprecated in Java 9 because:
1. No guarantee it will be called (GC may never run)
2. Delays garbage collection (objects must be finalized first)
3. Performance overhead
4. Can "resurrect" objects (making them reachable again) — confusing
5. Order of finalization is unpredictable

**Replacements**: `try-with-resources` for I/O resources, `Cleaner` (Java 9+) for native resources, explicit `close()` methods.

---

**Q34 🔴: What is the `wait()` and `notify()` mechanism?**

**Answer**: Methods for **inter-thread communication**. Must be called inside a `synchronized` block on the lock object.

- `wait()`: Thread releases the lock and sleeps until another thread calls `notify()`/`notifyAll()` on the same object
- `notify()`: Wakes up ONE randomly chosen waiting thread
- `notifyAll()`: Wakes up ALL waiting threads (preferred — avoids missed signals)

```java
// Producer-Consumer pattern
synchronized (buffer) {
    while (buffer.isFull()) {
        buffer.wait();              // Consumer releases lock and waits
    }
    buffer.add(item);
    buffer.notifyAll();             // Wake up consumers
}
```

Modern alternative: `java.util.concurrent` classes (`BlockingQueue`, `Condition`, `Lock`).

---

**Q35 🔴: Why must `wait()` be called in a loop, not an `if`?**

**Answer**: Because of **spurious wakeups** — a thread can wake up without being notified (JVM specification allows this). Also, between getting notified and reacquiring the lock, another thread might have changed the condition.

```java
// ❌ WRONG — if
synchronized (lock) {
    if (conditionNotMet) {
        lock.wait();         // Wakes up, but condition might still not be met!
    }
    proceed();               // May proceed with invalid state
}

// ✅ CORRECT — while loop
synchronized (lock) {
    while (conditionNotMet) {
        lock.wait();         // Re-checks condition after each wakeup
    }
    proceed();               // Guaranteed condition is met
}
```

---

### Category D: Tricky Output Questions (10 Questions)

---

**Q36 🟢: Predict the output:**
```java
try {
    System.out.println("try");
    return;
} finally {
    System.out.println("finally");
}
```

**Answer**: `try` then `finally`. The finally block executes even when try has a `return` statement.

---

**Q37 🟡: Predict the output:**
```java
public static int test() {
    int x = 10;
    try {
        return x;
    } finally {
        x = 20;
    }
}
System.out.println(test());
```

**Answer**: **`10`**. The return value (10) is saved before the finally block runs. Finally changes `x` to 20, but the already-saved return value (10) is used. Primitives are returned by value.

---

**Q38 🟡: Predict the output:**
```java
try {
    System.out.println("A");
    int x = 10 / 0;
    System.out.println("B");
} catch (ArithmeticException e) {
    System.out.println("C");
} catch (Exception e) {
    System.out.println("D");
} finally {
    System.out.println("E");
}
System.out.println("F");
```

**Answer**: `A C E F`
- "A" prints, then division by zero occurs, "B" is skipped
- ArithmeticException caught by first catch → "C"
- Finally always runs → "E"
- Execution continues normally → "F"

---

**Q39 🟡: Predict the output:**
```java
try {
    try {
        throw new ArithmeticException("inner");
    } finally {
        System.out.println("inner finally");
    }
} catch (ArithmeticException e) {
    System.out.println("caught: " + e.getMessage());
} finally {
    System.out.println("outer finally");
}
```

**Answer**:
```
inner finally
caught: inner
outer finally
```
Inner try has no catch → inner finally runs → exception propagates to outer try → caught → outer finally runs.

---

**Q40 🟡: What is printed?**
```java
System.out.println(1);
try {
    System.out.println(2);
    System.exit(0);
    System.out.println(3);
} finally {
    System.out.println(4);
}
System.out.println(5);
```

**Answer**: `1 2`. `System.exit(0)` terminates the JVM immediately. The finally block does NOT execute (one of the rare cases). Lines 3, 4, 5 never print.

---

**Q41 🟡: Predict the output:**
```java
Object o = null;
try {
    o.toString();
} catch (NullPointerException e) {
    System.out.println("NPE");
} catch (Exception e) {
    System.out.println("Exception");
} finally {
    System.out.println("Finally");
}
```

**Answer**: `NPE Finally`. `NullPointerException` is caught by the first matching catch. Finally always executes.

---

**Q42 🟡: Can you throw `null` in Java?**

**Answer**: `throw null;` compiles but throws **`NullPointerException`** at runtime (because `throw` tries to use the null reference). This is a weird edge case — never do this.

```java
try {
    throw null;
} catch (NullPointerException e) {
    System.out.println("NPE caught");   // This executes!
}
```

---

**Q43 🔴: Predict the output:**
```java
public static String test() {
    try {
        throw new RuntimeException("error");
    } catch (RuntimeException e) {
        return "catch";
    } finally {
        return "finally";
    }
}
System.out.println(test());
```

**Answer**: **`"finally"`**. The catch block sets the return to "catch", but the finally block's return overrides it to "finally". The `RuntimeException` is also silently swallowed — it will NOT propagate. This is why returning from finally is dangerous.

---

**Q44 🟡: What happens here?**
```java
try {
    int[] arr = new int[5];
    arr[10] = 50;
} catch (ArrayIndexOutOfBoundsException | ArithmeticException e) {
    System.out.println("Multi-caught: " + e.getClass().getSimpleName());
    // e = new RuntimeException("test");    ← Would this compile?
}
```

**Answer**: Prints `Multi-caught: ArrayIndexOutOfBoundsException`. The commented line would **NOT compile** because in a multi-catch, the variable `e` is **implicitly final** and cannot be reassigned.

---

**Q45 🔴: Predict the output:**
```java
public class Test {
    public static void main(String[] args) {
        try {
            method1();
        } catch (Exception e) {
            System.out.println(e.getMessage());
            System.out.println("Suppressed: " + e.getSuppressed().length);
        }
    }
    
    static void method1() throws Exception {
        try (AutoCloseable c = () -> { throw new Exception("close"); }) {
            throw new Exception("try");
        }
    }
}
```

**Answer**:
```
try
Suppressed: 1
```
The exception from try block ("try") is the primary exception. The exception from close() ("close") is suppressed and attached to the primary. `getSuppressed()` returns an array with 1 element.

---

### Category E: Scenario-Based Questions (10 Questions)

---

**Q46 🟡: In your project, how did you handle exceptions?**

**Answer**: *(Use your Project Story Bank)*

"In the Healthcare project, I implemented a 3-layer exception handling strategy:

1. **Custom exception hierarchy**: `HealthcareException` (base) → `PatientNotFoundException`, `DuplicateAdmissionException`, `InvalidAssessmentException`. All unchecked (extending `RuntimeException`), carrying error codes and timestamps.

2. **`@RestControllerAdvice`**: A global handler that mapped business exceptions to HTTP responses — `PatientNotFoundException` → 404, `DuplicateAdmissionException` → 409 (Conflict), validation errors → 400. A catch-all for unexpected exceptions returned 500.

3. **Exception chaining**: When the repository layer threw `DataAccessException`, we wrapped it in a `ServiceException` with the original cause preserved for debugging."

---

**Q47 🟡: How would you handle a checked exception that you can't recover from?**

**Answer**: Wrap it in an unchecked exception and let it propagate:

```java
try {
    Class.forName("com.driver.Missing");
} catch (ClassNotFoundException e) {
    throw new RuntimeException("Required driver not found", e);
}
```

This is what Spring does — wraps all checked exceptions (like `SQLException`) into unchecked `DataAccessException`. The caller isn't forced to handle something they can't fix.

---

**Q48 🟡: What is the difference between `throw e` and `throw new Exception(e)`?**

**Answer**:
- `throw e`: Re-throws the **original** exception with its original stack trace intact
- `throw new Exception(e)`: Creates a **new** exception wrapping the original. New stack trace starting from this point, original is the cause

```java
catch (IOException e) {
    throw e;                          // Same object, same stack trace
    throw new ServiceException(e);    // New object, original is getCause()
}
```

Use `throw e` when you just want to log and re-throw. Use wrapping when you want to translate exception types across layers.

---

**Q49 🟢: Can we throw checked exceptions from a method without declaring in throws?**

**Answer**: No. If a method throws a checked exception, it MUST declare it with `throws`. The compiler enforces this. Unchecked exceptions don't need `throws` declaration (but you can still add it for documentation).

---

**Q50 🟡: Can a child class throw a broader checked exception than the parent?**

**Answer**: **No**. When overriding a method, the child can throw:
- The **same** checked exception
- A **narrower** (subclass) checked exception
- **No** checked exception at all
- Any **unchecked** exception (regardless of parent)

But NEVER a **broader** checked exception. This is because the caller is handling based on the parent's declaration — a broader exception would slip through unhandled.

```java
class Parent {
    void read() throws FileNotFoundException { }   // Narrow
}
class Child extends Parent {
    // void read() throws IOException { }           // ❌ Broader — compile error!
    void read() throws FileNotFoundException { }    // ✅ Same — OK
    // void read() { }                              // ✅ None — OK
}
```

---

**Q51 🟡: What exception does `Integer.parseInt("abc")` throw?**

**Answer**: `NumberFormatException` — which extends `IllegalArgumentException` → `RuntimeException`. It's unchecked, so you don't need try-catch, but you should validate input before parsing in production code.

---

**Q52 🟡: How to make an object `AutoCloseable`?**

**Answer**: Implement the `AutoCloseable` interface and its single `close()` method:

```java
public class MyResource implements AutoCloseable {
    @Override
    public void close() throws Exception {
        // Release resources
    }
}

try (MyResource res = new MyResource()) {
    // Use resource
}   // close() called automatically
```

`Closeable` (extends `AutoCloseable`) is for I/O resources — its `close()` throws only `IOException` and is idempotent (safe to call multiple times).

---

**Q53 🔴: What is `ExceptionInInitializerError`? When does it occur?**

**Answer**: Thrown when a static initializer block or static variable initialization throws an exception:

```java
class Broken {
    static int x = 10 / 0;    // ArithmeticException during class loading
    // → Wrapped in ExceptionInInitializerError
}
```

It's an `Error` (not Exception) because it means the class cannot be loaded — the class is permanently unusable for the rest of the JVM's lifetime.

---

**Q54 🟡: What is a `StackTraceElement`? How to use it?**

**Answer**: Each element in a stack trace represents a single frame — a method call. You can programmatically access it:

```java
catch (Exception e) {
    StackTraceElement[] stack = e.getStackTrace();
    for (StackTraceElement elem : stack) {
        System.out.println(elem.getClassName() + "." + 
                          elem.getMethodName() + ":" + 
                          elem.getLineNumber());
    }
}
// Output: com.hospital.PatientService.save:42
//         com.hospital.PatientController.create:28
```

---

**Q55 🔴: How do custom exceptions help with microservices?**

**Answer**: In microservices, custom exceptions help standardize error responses across services:

1. Each microservice defines its own exception hierarchy
2. A `@ControllerAdvice` maps exceptions to standard error DTOs with error codes
3. When Service A calls Service B and gets an error response, Service A can create an appropriate exception from the error code
4. Error codes (like `PATIENT_NOT_FOUND`, `INVALID_ASSESSMENT`) are shared across services via a common library or documented API contract
5. This enables consistent error handling, logging, and monitoring across the entire system

---

> [!TIP]
> **Day 3 Completion Checklist** ✅
> - [ ] Can draw the Throwable hierarchy from memory
> - [ ] Know the difference between Error, checked Exception, and unchecked Exception
> - [ ] Can trace try-catch-finally execution flow in all 6 scenarios
> - [ ] Understand `throw` vs `throws` with examples
> - [ ] Can explain exception propagation up the call stack
> - [ ] Know multi-catch rules and try-with-resources with `AutoCloseable`
> - [ ] Can explain suppressed exceptions
> - [ ] Can create custom checked and unchecked exceptions with best practices
> - [ ] Know all 12 exception handling best practices
> - [ ] Can list all 11 Object class methods
> - [ ] Can override `equals()` correctly with the 5-step recipe
> - [ ] Understand the equals/hashCode contract and what breaks without it
> - [ ] Know shallow vs deep copy and why `clone()` is discouraged
> - [ ] Can explain `finalize()` deprecation and its replacement
> - [ ] Can predict output for all 10 tricky questions

---

**Tomorrow (Day 4)**: Collections Framework — Part 1 (List, Set, Map internals, HashMap deep dive — the second most asked topic after Strings) 🚀
