---
type: interview
series: Java Interview
part: 1
tags: [java, interview]
---

# ☕ Java Core Interview Reference — Part 1: Language Basics

> [!info] About this note
> **Part 1 of 9** — Java Basics & Language Fundamentals
> Format: Question ➜ Short answer ➜ Deep answer ➜ Code ➜ Interview trap
> Tags: #java #interview #core-java #basics

---

## 🗺️ Series Map

| Part | Topic | Status |
|------|-------|--------|
| **1** | ☕ Language Basics & Fundamentals | ✅ You are here |
| 2 | 🧬 OOP Deep Dive | ⏳ |
| 3 | 📦 Collections Framework | ⏳ |
| 4 | ⚠️ Exceptions & Generics | ⏳ |
| 5 | 🧵 Multithreading & Concurrency | ⏳ |
| 6 | 🧠 JVM Memory, GC & Class Loading | ⏳ |
| 7 | 🚀 Java 8+ (Lambda, Stream, Optional) | ⏳ |
| 8 | 💾 I/O, Serialization, Reflection, Annotations | ⏳ |
| 9 | 🎯 Design Patterns + Tricky Output Puzzles | ⏳ |

---

## 📑 Table of Contents

- [[#🏁 Section 1 — Java Platform (Q1–Q8)]]
- [[#🔢 Section 2 — Data Types & Variables (Q9–Q18)]]
- [[#➗ Section 3 — Operators & Control Flow (Q19–Q26)]]
- [[#🔤 Section 4 — Strings (Q27–Q36)]]
- [[#📦 Section 5 — Wrapper Classes & Autoboxing (Q37–Q42)]]
- [[#🔑 Section 6 — Keywords: static, final, this, super (Q43–Q52)]]
- [[#🏗️ Section 7 — Constructors & Initialization Order (Q53–Q58)]]
- [[#📚 Section 8 — Arrays & Varargs (Q59–Q65)]]
- [[#🚪 Section 9 — Packages & Access Modifiers (Q66–Q70)]]
- [[#🧩 Section 10 — Quick Fire Round]]

---

# 🏁 Section 1 — Java Platform (Q1–Q8)

## ❓ Q1. What is Java and what are its main features?

**Short answer:** Java is an object-oriented, class-based, platform-independent programming language that runs on the JVM.

**Key features:**

| Feature | Meaning |
|---------|---------|
| 🌍 Platform Independent | Write once, run anywhere (WORA) via bytecode |
| 🧬 Object Oriented | Everything lives inside classes (except primitives) |
| 🔒 Secure | No pointers, bytecode verifier, security manager |
| 💪 Robust | Strong typing, exception handling, automatic memory management |
| 🧵 Multithreaded | Threads are built into the language |
| 🗑️ Automatic GC | You never call `free()` |
| 📦 Portable | Fixed sizes for primitives on every platform |

> [!tip] Interview tip
> Do not just list words. Say **why**: "Java is portable because `int` is always 32-bit on every OS, unlike C where it changes."

---

## ❓ Q2. Difference between JDK, JRE and JVM? ⭐ (asked 90% of the time)

**Short answer:** JVM runs the code, JRE = JVM + libraries, JDK = JRE + developer tools.

```
┌──────────────────────────── JDK ────────────────────────────┐
│  javac, javadoc, jar, jdb, javap ...                         │
│  ┌───────────────────────── JRE ─────────────────────────┐   │
│  │  Core libraries (java.lang, java.util, java.io ...)   │   │
│  │  ┌──────────────────── JVM ────────────────────────┐  │   │
│  │  │  ClassLoader | Memory Areas | Execution Engine  │  │   │
│  │  └─────────────────────────────────────────────────┘  │   │
│  └───────────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────────┘
```

| | JVM | JRE | JDK |
|---|-----|-----|-----|
| Full name | Java Virtual Machine | Java Runtime Environment | Java Development Kit |
| Purpose | Executes bytecode | Runs Java apps | Develops Java apps |
| Contains compiler? | ❌ | ❌ | ✅ `javac` |
| Platform dependent? | ✅ Yes | ✅ Yes | ✅ Yes |

> [!warning] Trap
> "Java is platform independent" — but the **JVM itself is platform dependent**. You download a different JVM for Windows and Linux. That is exactly what makes your `.class` file portable.

---

## ❓ Q3. How does Java achieve platform independence?

**Answer:** Compilation happens in two steps.

```
Hello.java  --[ javac ]-->  Hello.class (bytecode)  --[ JVM ]-->  Machine code
   Source          compiler        Platform neutral      Platform specific
```

Bytecode is an intermediate language understood by every JVM. The JVM translates it to native instructions for that specific OS/CPU.

---

## ❓ Q4. What is JIT compiler?

**Short answer:** Just-In-Time compiler is part of the JVM that compiles **hot** bytecode into native machine code at runtime, so it does not need to be interpreted again and again.

**How it works:**
1. JVM starts by **interpreting** bytecode (fast startup, slow execution).
2. JVM counts how many times a method runs.
3. When a method becomes "hot" (many calls / loops), JIT compiles it to native code.
4. Next calls run at near-C speed. 🚀

> [!note] Extra point that impresses
> The JIT also does optimizations the compiler cannot: **inlining**, **dead code elimination**, **escape analysis**, **loop unrolling** — because it knows real runtime behaviour.

---

## ❓ Q5. Why is Java not a 100% object-oriented language?

**Answer:** Because of **primitive data types** (`int`, `char`, `boolean`, `double`, ...). They are not objects and do not inherit from `Object`.

Also arguable: `static` members belong to a class, not to an object.

> [!tip] Good closing line
> "Languages like Smalltalk or Ruby are 100% OO. Java kept primitives for **performance** — an `int` on the stack is much cheaper than an object on the heap."

---

## ❓ Q6. Explain the `main` method signature. ⭐

```java
public static void main(String[] args) { }
```

| Part | Why it is needed |
|------|------------------|
| `public` | JVM is outside your class, so it must be visible everywhere |
| `static` | JVM must call it **without creating an object** |
| `void` | JVM does not use any return value |
| `main` | Fixed name that JVM searches for |
| `String[] args` | Command line arguments |

**Valid variations:**
```java
public static void main(String... args)      // ✅ varargs works
static public void main(String[] args)       // ✅ order of modifiers free
public static void main(String args[])       // ✅ C-style array
public static final synchronized void main(String[] a) // ✅ still valid
```

**Invalid:**
```java
public void main(String[] args)     // ❌ not static -> NoSuchMethodError at runtime
public static int main(String[] a)  // ❌ wrong return type
public static void Main(String[] a) // ❌ Java is case sensitive
```

> [!warning] Trap question
> "Can we **overload** main?" ➜ **Yes**, compiler allows it, but JVM only calls `main(String[])`. Other versions must be called manually.

---

## ❓ Q7. Can we run a Java program without a `main` method?

**Answer:** In modern Java (7+): **No** for normal execution.

Before Java 7 you could use a `static` block to print something before JVM complained. Since Java 7 the JVM checks for `main` **first**, so you get:
```
Error: Main method not found in class X
```

> [!tip] Java 21+ update
> Java 21 introduced a preview of **unnamed classes and instance main methods** — you can write just `void main() { }`. Mentioning this shows you follow modern Java.

---

## ❓ Q8. What is bytecode? How to see it?

**Answer:** Bytecode is the platform-neutral instruction set inside `.class` files.

```bash
javac Hello.java     # produce Hello.class
javap -c Hello       # disassemble and read the bytecode
```

Sample output:
```
0: getstatic  #2   // Field java/lang/System.out
3: ldc        #3   // String Hello
5: invokevirtual #4 // Method println
8: return
```

---

# 🔢 Section 2 — Data Types & Variables (Q9–Q18)

## ❓ Q9. List all primitive data types with size and range. ⭐

| Type | Size | Default | Range | Wrapper |
|------|------|---------|-------|---------|
| `byte` | 8 bit | `0` | −128 … 127 | `Byte` |
| `short` | 16 bit | `0` | −32,768 … 32,767 | `Short` |
| `int` | 32 bit | `0` | −2³¹ … 2³¹−1 | `Integer` |
| `long` | 64 bit | `0L` | −2⁶³ … 2⁶³−1 | `Long` |
| `float` | 32 bit | `0.0f` | ~7 decimal digits | `Float` |
| `double` | 64 bit | `0.0d` | ~15 decimal digits | `Double` |
| `char` | 16 bit | `'\u0000'` | 0 … 65,535 (unsigned!) | `Character` |
| `boolean` | JVM-dependent (~1 bit logical) | `false` | true / false | `Boolean` |

> [!warning] Trap
> `char` is the **only unsigned** primitive in Java. And `boolean` size is **not defined** by the spec — do not say "1 bit" confidently, say "not precisely specified, usually 1 byte in arrays".

---

## ❓ Q10. What are default values? Do local variables get them?

**Answer:** **Instance** and **static** fields get default values. **Local variables do NOT.**

```java
class Demo {
    int x;                 // ✅ 0 automatically
    static String s;       // ✅ null automatically

    void method() {
        int y;
        System.out.println(y); // ❌ compile error: variable y might not have been initialized
    }
}
```

**Why?** Fields live on the heap and the JVM zeroes memory. Local variables live on the stack frame, which is reused — so Java forces you to assign explicitly. This is a **safety feature**.

---

## ❓ Q11. Difference between instance variable, static variable and local variable?

| | Instance | Static (class) | Local |
|---|----------|---------------|-------|
| Declared | inside class, outside method | with `static` keyword | inside method/block |
| Memory | Heap (inside object) | Method Area / Metaspace | Stack |
| Copies | one per object | **one per class** | one per method call |
| Default value | ✅ yes | ✅ yes | ❌ no |
| Lifetime | as long as object lives | as long as class is loaded | until method ends |

---

## ❓ Q12. What is type casting? Widening vs Narrowing.

**Widening (implicit / automatic)** — no data loss:
```
byte → short → int → long → float → double
        char ↗
```
```java
int i = 100;
long l = i;      // ✅ automatic
double d = l;    // ✅ automatic
```

**Narrowing (explicit)** — possible data loss:
```java
double d = 9.99;
int i = (int) d;   // 9  (fraction is truncated, NOT rounded)

int big = 300;
byte b = (byte) big;  // 44  ⚠️ overflow wrap-around
```

> [!warning] Classic trap
> ```java
> byte a = 10, b = 20;
> byte c = a + b;   // ❌ compile error!
> ```
> Because `a + b` is promoted to `int`. Fix: `byte c = (byte)(a + b);`
> But `byte c = 10 + 20;` compiles fine — compile-time constants are checked at compile time.

---

## ❓ Q13. `int` vs `Integer`?

| | `int` | `Integer` |
|---|-------|-----------|
| Type | primitive | object (wrapper) |
| Memory | stack (as local) | heap |
| Default | `0` | `null` |
| Can be null? | ❌ | ✅ |
| Usable in collections? | ❌ | ✅ `List<Integer>` |
| Size | 4 bytes | ~16 bytes header + 4 |

---

## ❓ Q14. Why does `0.1 + 0.2 != 0.3` in Java? ⭐

```java
System.out.println(0.1 + 0.2);          // 0.30000000000000004
System.out.println(0.1 + 0.2 == 0.3);   // false
```

**Reason:** `float`/`double` follow **IEEE 754** binary floating point. Numbers like 0.1 cannot be represented exactly in binary (same as 1/3 cannot be written exactly in decimal).

**Solution — use `BigDecimal` with String constructor:**
```java
BigDecimal a = new BigDecimal("0.1");
BigDecimal b = new BigDecimal("0.2");
System.out.println(a.add(b));            // 0.3 ✅
```

> [!danger] Never do this
> `new BigDecimal(0.1)` — passing a `double` copies the error into BigDecimal. Always use the **String** constructor for money. 💰

---

## ❓ Q15. `float` vs `double` — which to choose?

- `float`: 32 bit, ~7 digits precision, needs `f` suffix → `float f = 1.5f;`
- `double`: 64 bit, ~15 digits, **default** for decimal literals
- For **money** use neither → use `BigDecimal` or store cents in `long`.

```java
float f = 1.5;    // ❌ error: literal is double
float f = 1.5f;   // ✅
```

---

## ❓ Q16. What is integer overflow? Does Java throw an error?

**Answer:** No exception. It silently **wraps around**.

```java
int max = Integer.MAX_VALUE;   // 2147483647
System.out.println(max + 1);   // -2147483648  😱
```

**Safe way (Java 8+):**
```java
Math.addExact(max, 1);   // throws ArithmeticException: integer overflow ✅
```

---

## ❓ Q17. What is `var`? (Java 10)

**Answer:** Local variable type inference. The compiler figures out the type — Java stays **statically typed**, this is not JavaScript.

```java
var list = new ArrayList<String>();  // ArrayList<String>
var i = 10;                          // int
```

**Where `var` is NOT allowed:**
```java
var x;                    // ❌ no initializer
var y = null;             // ❌ cannot infer
class A { var f = 1; }    // ❌ not for fields
void m(var a) { }         // ❌ not for parameters
var[] arr = {1,2};        // ❌ not for arrays like this
```

---

## ❓ Q18. Is Java pass-by-value or pass-by-reference? ⭐⭐ (favourite trap)

**Answer:** Java is **always pass-by-value**. For objects, the **value of the reference** is copied.

```java
void change(Dog d) {
    d.setName("Rex");    // ✅ affects caller — same object
    d = new Dog("Max");  // ❌ only changes local copy of reference
}

Dog dog = new Dog("Buddy");
change(dog);
System.out.println(dog.getName());  // "Rex", NOT "Max"
```

**Mental picture:**
```
caller:  dog ──────┐
                   ▼
                 [ Dog object ]   ← both point here at first
                   ▲
method:    d ──────┘   then d is re-pointed to a new object,
                       but `dog` never moves.
```

> [!tip] One-line answer to memorize
> "Java passes **references by value**. You can change the object's state, but you cannot make the caller's variable point somewhere else."

---

# ➗ Section 3 — Operators & Control Flow (Q19–Q26)

## ❓ Q19. `i++` vs `++i`?

- `i++` (post): use the old value, then increment.
- `++i` (pre): increment, then use the new value.

```java
int i = 5;
System.out.println(i++);  // 5  (i becomes 6)
System.out.println(++i);  // 7
```

**Famous puzzle:**
```java
int i = 0;
i = i++;
System.out.println(i);   // 0  ⚠️ not 1
```
Because `i++` returns 0, then that 0 is assigned back over the incremented value.

---

## ❓ Q20. `>>` vs `>>>`?

| Operator | Name | Behaviour |
|----------|------|-----------|
| `<<` | Left shift | multiply by 2ⁿ |
| `>>` | Signed right shift | keeps sign bit (fills with sign) |
| `>>>` | Unsigned right shift | always fills with `0` |

```java
System.out.println(-8 >> 1);    // -4
System.out.println(-8 >>> 1);   // 2147483644  (huge positive)
```

> [!note] There is **no** `<<<` operator in Java.

---

## ❓ Q21. `&` vs `&&` (and `|` vs `||`)?

| | `&` / `\|` | `&&` / `\|\|` |
|---|---|---|
| Type | bitwise **or** logical | logical only |
| Short-circuit? | ❌ evaluates both sides | ✅ stops early |

```java
if (obj != null && obj.getName().equals("x"))  // ✅ safe
if (obj != null &  obj.getName().equals("x"))  // ❌ NPE risk
```

---

## ❓ Q22. `==` vs `.equals()`? ⭐

- `==` compares **references** (memory address) for objects, **values** for primitives.
- `.equals()` compares **content** — if the class overrides it.

```java
String a = new String("hi");
String b = new String("hi");
a == b;         // false
a.equals(b);    // true
```

> [!warning] `Object.equals()` default implementation is just `this == obj`. If your class does not override it, `equals` behaves like `==`.

---

## ❓ Q23. What is a `switch` statement? What types are allowed?

**Allowed:** `byte`, `short`, `char`, `int`, their wrappers, `enum`, `String` (Java 7+), and sealed types/patterns (Java 21).
**Not allowed:** `long`, `float`, `double`, `boolean`.

**Classic switch — fall-through danger:**
```java
switch (day) {
    case 1: System.out.println("Mon");   // no break → falls to next!
    case 2: System.out.println("Tue"); break;
    default: System.out.println("Other");
}
```

**Enhanced switch (Java 14+) — no fall-through:**
```java
String result = switch (day) {
    case 1, 7 -> "Weekend";
    case 2, 3, 4, 5, 6 -> "Weekday";
    default -> {
        yield "Unknown";     // yield returns a value from a block
    }
};
```

---

## ❓ Q24. `while` vs `do-while`?

- `while`: checks condition first → may run **0** times.
- `do-while`: runs body first → runs **at least 1** time.

```java
do { System.out.println("runs once"); } while (false);
```

---

## ❓ Q25. What is a labeled break/continue?

Used to exit **outer** loops directly.

```java
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (j == 2) continue outer;  // next i
        if (i == 2) break outer;     // exit both loops
    }
}
```

> [!tip] Java has **no `goto`** — `goto` is a reserved keyword but unused. Labels are the safe replacement.

---

## ❓ Q26. Ternary operator and its traps.

```java
int max = (a > b) ? a : b;
```

**Trap — auto unboxing NPE:**
```java
Integer x = null;
int y = true ? 1 : x;   // fine
int z = false ? 1 : x;  // 💥 NullPointerException (unboxing null)
```

---

# 🔤 Section 4 — Strings (Q27–Q36)

## ❓ Q27. Why is `String` immutable in Java? ⭐⭐

**Answer:** Once created, the character content of a `String` never changes.

**Reasons:**

| Reason | Explanation |
|--------|-------------|
| 🏊 String Pool | Many references share one object. If one could change it, all would break. |
| 🔒 Security | Usernames, URLs, file paths, DB connections are Strings. Immutability blocks change-after-check attacks. |
| 🧵 Thread safety | Immutable = automatically thread-safe, no synchronization needed. |
| #️⃣ HashCode caching | `String` caches its hashCode → fast `HashMap` keys. |
| 🧬 Class loading | Class names are Strings; mutability would allow loading a wrong class. |

**How is it implemented?**
- `String` class is `final` (cannot be subclassed).
- Internal `private final byte[] value` (was `char[]` before Java 9 Compact Strings).
- No method modifies the array; every "modifying" method returns a **new** String.

```java
String s = "hello";
s.toUpperCase();
System.out.println(s);   // "hello" — unchanged!
s = s.toUpperCase();
System.out.println(s);   // "HELLO" ✅
```

---

## ❓ Q28. What is the String Constant Pool (SCP)?

**Answer:** A special area in the **heap** (since Java 7; before that in PermGen) where string literals are stored and reused.

```java
String a = "java";   // goes to pool
String b = "java";   // reuses SAME object from pool
a == b;              // true ✅

String c = new String("java");  // NEW object in heap
a == c;              // false
a.equals(c);         // true
```

**Diagram:**
```
HEAP
┌──────────────────────────────────────┐
│  ┌─── String Pool ───┐               │
│  │  "java"  ◄────────┼──── a, b      │
│  └───────────────────┘               │
│                                      │
│   [ String obj "java" ] ◄──── c      │
└──────────────────────────────────────┘
```

---

## ❓ Q29. `new String("abc")` — how many objects are created? ⭐

**Answer:** **1 or 2.**
- 1 object in the **pool** (only if `"abc"` is not already there).
- 1 object in the **heap** (always, because of `new`).

If the literal already existed in the pool → only **1** new object.

---

## ❓ Q30. What does `intern()` do?

**Answer:** Puts the string into the pool (or returns the existing pooled one).

```java
String a = new String("java");
String b = a.intern();
String c = "java";
b == c;   // true ✅
a == b;   // false
```

---

## ❓ Q31. `String` vs `StringBuilder` vs `StringBuffer`? ⭐⭐

| | `String` | `StringBuilder` | `StringBuffer` |
|---|---------|-----------------|----------------|
| Mutable | ❌ | ✅ | ✅ |
| Thread safe | ✅ (immutable) | ❌ | ✅ (synchronized) |
| Speed | slow for concat | ⚡ fastest | slower (lock overhead) |
| Since | 1.0 | 1.5 | 1.0 |
| Use when | fixed text, keys | single-thread building | multi-thread building (rare) |

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World").insert(0, ">> ").reverse();
```

> [!tip] Real answer for "which one to use?"
> "`StringBuilder` in 99% of cases. `StringBuffer` is legacy — if I need thread safety I usually keep the builder local to one thread anyway, which is cheaper than locking."

---

## ❓ Q32. Why is concatenation in a loop bad?

```java
// ❌ BAD — O(n²), creates a new String each iteration
String s = "";
for (int i = 0; i < 10000; i++) s += i;

// ✅ GOOD — O(n)
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 10000; i++) sb.append(i);
String s = sb.toString();
```

> [!note] Nuance that scores points
> A **single** `"a" + b + "c"` expression is fine — the compiler converts it to `StringBuilder` (or `invokedynamic` StringConcatFactory in Java 9+). The problem is only **inside loops**, where a new builder is created every iteration.

---

## ❓ Q33. Important `String` methods to know

```java
"hello".length();               // 5
"hello".charAt(1);              // 'e'
"hello".substring(1, 3);        // "el"  (end index exclusive)
"hello".indexOf("l");           // 2
"hello".contains("ell");        // true
"  hi  ".trim();                // "hi"
"  hi  ".strip();               // "hi"  (Java 11, Unicode aware)
"a,b,c".split(",");             // ["a","b","c"]
String.join("-", "a","b");      // "a-b"
"Hi".equalsIgnoreCase("HI");    // true
"ab".repeat(3);                 // "ababab"  (Java 11)
"".isEmpty();                   // true
"  ".isBlank();                 // true   (Java 11)
"a".compareTo("b");             // -1
String.valueOf(10);             // "10"
"%s is %d".formatted("age", 5); // Java 15
```

---

## ❓ Q34. `String.equals()` vs `==` in real interview code

```java
String s1 = "java";
String s2 = "ja" + "va";              // compile-time constant → pool
String s3 = new String("java").intern();
String part = "ja";
String s4 = part + "va";              // runtime concat → NEW object

s1 == s2;   // true  ✅ (constant folding)
s1 == s3;   // true  ✅
s1 == s4;   // false ❌  ← the trap
```

> [!warning] Rule: concatenation with a **non-final variable** happens at runtime → new object, not pooled. If `part` were `final String part = "ja";` then `s1 == s4` would be **true**.

---

## ❓ Q35. What is a String's `hashCode()` formula?

```
s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]
```
**Why 31?** It is an odd prime, gives good distribution, and `31 * i` can be optimized by the JVM to `(i << 5) - i`.

---

## ❓ Q36. Text Blocks (Java 15)

```java
String json = """
    {
      "name": "Ali",
      "age": 25
    }
    """;
```
No more `\n` and `\"` everywhere. 🎉

---

# 📦 Section 5 — Wrapper Classes & Autoboxing (Q37–Q42)

## ❓ Q37. What are wrapper classes and why do we need them?

**Answer:** Object versions of primitives (`int → Integer`).

**Needed for:**
- Collections & generics: `List<Integer>` (generics do not accept primitives)
- `null` to represent "no value"
- Utility methods: `Integer.parseInt()`, `Integer.MAX_VALUE`, `Integer.toBinaryString()`
- Reflection / frameworks that work with `Object`

---

## ❓ Q38. Autoboxing and unboxing?

```java
Integer boxed = 10;        // autoboxing   → Integer.valueOf(10)
int unboxed = boxed;       // unboxing     → boxed.intValue()

List<Integer> list = new ArrayList<>();
list.add(5);               // autoboxing happens automatically
```

---

## ❓ Q39. The Integer cache trap ⭐⭐ (very common)

```java
Integer a = 127, b = 127;
System.out.println(a == b);   // true  ✅

Integer c = 128, d = 128;
System.out.println(c == d);   // false ❌  😱
```

**Why?** `Integer.valueOf()` caches objects from **−128 to 127**. Inside that range the same object is reused; outside it, a new object is created.

**Cached by default:** `Boolean`, `Byte`, `Character`(0–127), `Short`, `Integer`, `Long` (−128..127).
**Not cached:** `Float`, `Double`.

> [!tip] Lesson: **always compare wrappers with `.equals()`**, never `==`.

---

## ❓ Q40. How can unboxing cause NullPointerException?

```java
Map<String, Integer> map = new HashMap<>();
int count = map.get("missing");   // 💥 NPE — get() returns null, unboxed to int
```

**Fix:**
```java
int count = map.getOrDefault("missing", 0);   // ✅
```

---

## ❓ Q41. `parseInt()` vs `valueOf()`?

```java
int i    = Integer.parseInt("10");   // returns primitive int
Integer o = Integer.valueOf("10");   // returns Integer object (uses cache)
```
Both throw `NumberFormatException` for bad input.

---

## ❓ Q42. Are wrapper classes immutable?

**Yes** — all wrapper classes are `final` and immutable. That is why they are safe as `HashMap` keys.

---

# 🔑 Section 6 — Keywords: static, final, this, super (Q43–Q52)

## ❓ Q43. Explain the `static` keyword completely. ⭐⭐

`static` = belongs to the **class**, not the object.

**1️⃣ Static variable** — one copy shared by all objects
```java
class Counter {
    static int count = 0;     // shared
    Counter() { count++; }
}
```

**2️⃣ Static method** — called without an object
```java
Math.max(1, 2);
```

**3️⃣ Static block** — runs once when the class is loaded
```java
static { System.out.println("class loaded"); }
```

**4️⃣ Static nested class** — does not need an outer instance
```java
class Outer { static class Inner { } }
new Outer.Inner();
```

---

## ❓ Q44. Why can't a static method access instance variables?

Because static methods run **without any object**, so there is no `this` to read the instance data from.

```java
class A {
    int x = 5;
    static void m() {
        System.out.println(x);   // ❌ compile error
    }
}
```

---

## ❓ Q45. Can we override a static method?

**No.** Static methods are **hidden**, not overridden. Binding happens at compile time based on the **reference type**, not the object type.

```java
class Parent { static void show() { System.out.println("Parent"); } }
class Child extends Parent { static void show() { System.out.println("Child"); } }

Parent p = new Child();
p.show();   // "Parent"  ← method hiding, not overriding
```

> [!warning] This is a favourite trap. Say the words: **"method hiding"**.

---

## ❓ Q46. Explain `final` in all its usages.

| Applied to | Meaning |
|-----------|---------|
| **variable** | value cannot be reassigned (constant) |
| **method** | cannot be overridden |
| **class** | cannot be extended (e.g. `String`, `Integer`) |
| **parameter** | cannot be reassigned inside the method |

> [!warning] Huge trap
> `final` on an object reference means the **reference** cannot change, **not** the object's content.
> ```java
> final List<String> list = new ArrayList<>();
> list.add("ok");                 // ✅ allowed
> list = new ArrayList<>();       // ❌ compile error
> ```

---

## ❓ Q47. `final` vs `finally` vs `finalize()`? ⭐

| | `final` | `finally` | `finalize()` |
|---|--------|-----------|--------------|
| Type | keyword | block | method of `Object` |
| Purpose | restrict change/inherit/override | always execute cleanup code | called by GC before object destroy |
| Status | ✅ used | ✅ used | ⚠️ **deprecated since Java 9**, removed in Java 18+ |

Use **try-with-resources** instead of `finalize()`.

---

## ❓ Q48. What is a blank final variable?

A `final` field with no initial value — it **must** be assigned in the constructor (or instance block).

```java
class A {
    final int id;
    A(int id) { this.id = id; }   // ✅ valid
}
```

---

## ❓ Q49. What does `this` do?

- refers to the current object
- `this.field = field;` resolves name shadowing
- `this(...)` calls another constructor of the **same class** (must be the first statement)
- can be passed as an argument or returned (used for method chaining)

---

## ❓ Q50. What does `super` do?

- `super.field` / `super.method()` accesses the parent version
- `super(...)` calls a parent constructor (must be the first statement)

```java
class Child extends Parent {
    Child() {
        super(10);           // must be first
        System.out.println("child");
    }
}
```

---

## ❓ Q51. Can a class be both `abstract` and `final`?

**No.** `abstract` means "must be extended", `final` means "cannot be extended". They contradict. ⛔

Similarly invalid: `abstract static`, `abstract final` methods, `abstract private` methods.

---

## ❓ Q52. What is the `transient` and `volatile` keyword? (preview)

- `transient`: field is **skipped** during serialization. → detail in Part 8
- `volatile`: value is always read from main memory, not the CPU cache → detail in Part 5

---

# 🏗️ Section 7 — Constructors & Initialization Order (Q53–Q58)

## ❓ Q53. What is a constructor? Rules?

**Rules:**
- Same name as the class
- No return type (not even `void`)
- Called automatically on `new`
- Can be overloaded
- Cannot be `final`, `static`, `abstract`, or `synchronized`
- **Can** be `private` (Singleton pattern!)

---

## ❓ Q54. Default constructor vs no-arg constructor?

- **Default constructor**: created by the **compiler** when you write **no** constructor at all.
- **No-arg constructor**: written by **you** with empty parameters.

> [!warning] If you write **any** constructor, the compiler stops adding the default one. So this breaks:
> ```java
> class A { A(int x) {} }
> new A();   // ❌ compile error
> ```

---

## ❓ Q55. What is constructor chaining?

```java
class Person {
    String name; int age;
    Person() { this("Unknown", 0); }              // → calls below
    Person(String name) { this(name, 0); }
    Person(String name, int age) { this.name = name; this.age = age; }
}
```

`this()` and `super()` **cannot both** appear in the same constructor, and each must be the **first** statement.

---

## ❓ Q56. What is the exact initialization order? ⭐⭐ (killer question)

**When the class is first loaded (once):**
1. Static variables & static blocks — **in the order they appear in the code**

**Every time you create an object:**
2. Parent's instance blocks → parent constructor body
3. Instance variables & instance initializer blocks (in code order)
4. Constructor body

```java
class Parent {
    static { System.out.println("1 parent static"); }
    { System.out.println("3 parent instance"); }
    Parent() { System.out.println("4 parent ctor"); }
}
class Child extends Parent {
    static { System.out.println("2 child static"); }
    { System.out.println("5 child instance"); }
    Child() { System.out.println("6 child ctor"); }
}
// new Child()  →  1, 2, 3, 4, 5, 6
```

> [!tip] Memory hook: **statics first (parent → child), then for the object: parent all the way, then child.**

---

## ❓ Q57. Can a constructor call a `static` method? Can a static method create an object?

Both **yes**. Statics do not need an object, and constructors can use anything visible.

---

## ❓ Q58. Can a constructor be `private`? Why would we do that?

**Yes.** Used for:
- 🔒 Singleton pattern
- 🏭 Static factory methods (`Integer.valueOf()`, `List.of()`)
- 🛠️ Utility classes (`Math`, `Collections`) to prevent instantiation
- 🧱 Builder pattern

```java
final class Singleton {
    private static final Singleton INSTANCE = new Singleton();
    private Singleton() { }
    public static Singleton getInstance() { return INSTANCE; }
}
```

---

# 📚 Section 8 — Arrays & Varargs (Q59–Q65)

## ❓ Q59. How do you declare and initialize arrays?

```java
int[] a = new int[5];              // all zeros
int[] b = {1, 2, 3};               // literal
int[] c = new int[]{1, 2, 3};      // needed when passing inline
int[][] grid = new int[3][4];      // 2D
int[][] jagged = new int[3][];     // rows with different lengths
jagged[0] = new int[2];
```

---

## ❓ Q60. Is array size fixed? What is `length` vs `length()` vs `size()`?

- Array size is **fixed** at creation.
- `array.length` → **field**, no parentheses
- `string.length()` → **method**
- `collection.size()` → **method**

---

## ❓ Q61. Array vs ArrayList? ⭐

| | Array | ArrayList |
|---|-------|-----------|
| Size | fixed | dynamic (grows ~1.5×) |
| Types | primitives + objects | objects only |
| Performance | faster, less memory | small overhead |
| Type safety | runtime (`ArrayStoreException`) | compile-time via generics |
| Methods | almost none | add, remove, contains, ... |
| Length | `.length` | `.size()` |

---

## ❓ Q62. What is array covariance and why is it dangerous?

```java
Object[] objs = new String[2];   // ✅ allowed — arrays are covariant
objs[0] = 42;                    // 💥 ArrayStoreException at RUNTIME
```
Generics are **invariant** to prevent exactly this: `List<Object> l = new ArrayList<String>();` does not compile. ✅

---

## ❓ Q63. Useful array utilities

```java
Arrays.toString(arr);            // "[1, 2, 3]"
Arrays.deepToString(grid);       // for 2D
Arrays.sort(arr);
Arrays.binarySearch(arr, 5);     // array must be sorted first!
Arrays.fill(arr, 0);
Arrays.copyOf(arr, 10);
Arrays.copyOfRange(arr, 1, 3);
Arrays.equals(a, b);             // element by element
System.arraycopy(src, 0, dst, 0, len);
```

> [!warning] `arr1 == arr2` and `arr1.equals(arr2)` both compare **references** for arrays. Use `Arrays.equals()`.

---

## ❓ Q64. What are varargs?

```java
int sum(int... numbers) {          // numbers is really an int[]
    int total = 0;
    for (int n : numbers) total += n;
    return total;
}
sum();            // ✅ 0 args allowed
sum(1, 2, 3);
sum(new int[]{1, 2});
```

**Rules:** only **one** varargs parameter, and it must be the **last** one.

---

## ❓ Q65. Shallow copy vs deep copy of an array?

```java
int[] a = {1,2,3};
int[] b = a;                     // ❌ same array, not a copy
int[] c = a.clone();             // ✅ copy (fine for primitives)

Person[] p2 = p1.clone();        // ⚠️ SHALLOW: elements still point to same objects
```

---

# 🚪 Section 9 — Packages & Access Modifiers (Q66–Q70)

## ❓ Q66. Explain all access modifiers. ⭐

| Modifier | Same class | Same package | Subclass (other pkg) | Everywhere |
|----------|:---------:|:------------:|:-------------------:|:----------:|
| `private` | ✅ | ❌ | ❌ | ❌ |
| *default* (no keyword) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

> [!note] A **top-level class** can only be `public` or default — never `private` or `protected`.

---

## ❓ Q67. Can a Java file have multiple classes?

**Yes**, but only **one** can be `public`, and the file name must match that public class.

---

## ❓ Q68. What is a package? Why use it?

Namespace for grouping related classes. Benefits: avoid name conflicts, control access (default/protected), better organization.

```java
package com.company.service;
import java.util.List;
import java.util.*;              // wildcard, does NOT import subpackages
import static java.lang.Math.PI; // static import
```

`java.lang` is imported automatically. ✨

---

## ❓ Q69. Does `import` make the program slower or bigger?

**No.** `import` is only a **compile-time** convenience so you can write short names. It does not load or copy anything at runtime.

---

## ❓ Q70. What is `java.lang` and what is inside it?

Auto-imported core package: `Object`, `String`, `StringBuilder`, wrappers, `Math`, `System`, `Thread`, `Runnable`, `Exception`, `Throwable`, `Enum`, `Class`.

---

# 🧩 Section 10 — Quick Fire Round

> [!question]- Is Java 100% platform independent?
> No. Bytecode is portable, but the **JVM is platform specific**.

> [!question]- What is the difference between `path` and `classpath`?
> `PATH` = where the OS finds executables (`java`, `javac`). `CLASSPATH` = where the JVM finds `.class` files and JARs.

> [!question]- Why is `String[] args` and not `String args`?
> Because a program can receive **many** command-line arguments.

> [!question]- What happens if `main` throws an exception?
> The JVM prints the stack trace and terminates that thread with a non-zero exit code.

> [!question]- Can we have an empty `.java` file?
> Yes, it compiles fine and produces no `.class` file.

> [!question]- Is `null` a keyword?
> No — `null` is a **literal** (like `true`/`false`). `goto` and `const` are reserved but unused keywords.

> [!question]- What is the output of `System.out.println('a' + 1);`
> `98` — `char` is promoted to `int`. To print `"a1"` write `"" + 'a' + 1`.

> [!question]- What is the output of `System.out.println(1 + 2 + "3" + 4 + 5);`
> `3345` — left to right: `1+2=3`, then everything becomes concatenation.

> [!question]- Can we declare a class inside a method?
> Yes — a **local class** (or anonymous class, or lambda).

> [!question]- Difference between `System.out`, `System.err`, `System.in`?
> `out` = standard output stream, `err` = error stream (unbuffered, usually red), `in` = standard input.

> [!question]- What is `Integer.MIN_VALUE` absolute value trap?
> `Math.abs(Integer.MIN_VALUE)` returns a **negative** number, because `+2147483648` does not fit in an `int`.

> [!question]- What does `n & 1` tell you?
> `0` = even, `1` = odd. Faster than `%` and works on negatives too.

---

## 🎓 Self-Test Checklist for Part 1

- [ ] I can explain JDK/JRE/JVM in 30 seconds with the diagram
- [ ] I can explain why Java is pass-by-value with the Dog example
- [ ] I can explain String immutability with 4 reasons
- [ ] I know the Integer cache −128..127 trap
- [ ] I can write the initialization order 1→6 from memory
- [ ] I know why `byte c = a + b;` fails to compile
- [ ] I can explain method hiding vs overriding
- [ ] I know the access modifier table by heart

---

> [!success] ✅ Part 1 complete — 70 questions
> **Next up ➜ Part 2: 🧬 OOP Deep Dive** — inheritance, polymorphism, abstraction, encapsulation, interface vs abstract class, `equals`/`hashCode` contract, `Object` class methods, inner classes, `Comparable` vs `Comparator`, immutable class design, cloning, records, sealed classes.
>
> 👉 Type: **"give me part 2"**

#java #interview #core-java #part1
