---
type: interview
series: Java Interview
part: 4
tags: [java, interview]
---

 # ⚠️ Java Core Interview Reference — Part 4: Exceptions & Generics

> [!info] **Part 4 of 9** — Exception Handling + Generics
> Previous: [[01 - Java/Interview/03 - Collections|Part 3 — Collections]] | Hub: [[01 - Java/Interview/00 - Overview|Interview Hub]]
> Tags: #java #interview #core-java #exceptions #generics

---

## 📑 Table of Contents

- [[#🌳 Section 1 — Exception Hierarchy (Q241–Q250)]]
- [[#🧯 Section 2 — try / catch / finally (Q251–Q264)]]
- [[#🚀 Section 3 — throw, throws & Custom Exceptions (Q265–Q276)]]
- [[#🧪 Section 4 — Best Practices & Real Traps (Q277–Q286)]]
- [[#🧬 Section 5 — Generics Basics (Q287–Q298)]]
- [[#🫥 Section 6 — Type Erasure (Q299–Q306)]]
- [[#🃏 Section 7 — Wildcards & PECS (Q307–Q316)]]
- [[#🧩 Section 8 — Quick Fire Round]]

---

# 🌳 Section 1 — Exception Hierarchy (Q241–Q250)

## ❓ Q241. Draw the exception hierarchy. ⭐⭐

```
                    Object
                       │
                  Throwable
            ┌──────────┴──────────┐
          Error                Exception
            │           ┌──────────┴───────────┐
  OutOfMemoryError   RuntimeException      IOException
  StackOverflowError      │              SQLException
  NoClassDefFoundError    │           ClassNotFoundException
                          │           FileNotFoundException
        ┌─────────────────┼──────────────────┐
NullPointerException  IllegalArgumentException  ArithmeticException
IndexOutOfBounds      IllegalStateException     ClassCastException
                      NumberFormatException     ConcurrentModificationException

  ◄── UNCHECKED ──►                    ◄──── CHECKED ────►
  (Error + RuntimeException)           (everything else under Exception)
```

---

## ❓ Q242. `Error` vs `Exception`? ⭐

| | `Error` | `Exception` |
|---|---------|-------------|
| Cause | JVM / system level | application level |
| Recoverable? | ❌ usually not | ✅ usually yes |
| Should you catch it? | ❌ no | ✅ yes |
| Examples | `OutOfMemoryError`, `StackOverflowError` | `IOException`, `NullPointerException` |

> [!tip] You **can** technically catch an `Error`, but you should not — the JVM is already in a broken state. The one legitimate case is logging before shutdown.

---

## ❓ Q243. Checked vs Unchecked exceptions? ⭐⭐⭐

| | **Checked** | **Unchecked** |
|---|-------------|---------------|
| Compiler forces handling | ✅ yes | ❌ no |
| Extends | `Exception` (not Runtime) | `RuntimeException` or `Error` |
| Meaning | expected external problem | programming bug |
| Examples | `IOException`, `SQLException` | `NPE`, `IllegalArgumentException` |
| Handle by | `try-catch` or `throws` | fix the code |

**Memory rule 🧠:** *Checked = the world can fail (file missing, network down). Unchecked = your code is wrong.*

---

## ❓ Q244. Is `ClassNotFoundException` checked or unchecked?

**Checked.** But `NoClassDefFoundError` is an **Error** — the class was present at compile time and missing at runtime. Different problems:
- `ClassNotFoundException` → you called `Class.forName("...")` and it was not found
- `NoClassDefFoundError` → the JVM tried to link a class it saw at compile time, or the class's static initializer previously failed

---

## ❓ Q245. Why do many people dislike checked exceptions?

- They force `try-catch` boilerplate everywhere
- They break lambdas and streams (you cannot throw checked exceptions from most functional interfaces)
- They leak implementation details up the call stack
- People "swallow" them with an empty catch block, which is worse than nothing

Modern frameworks (Spring, Hibernate) wrap checked exceptions into **unchecked** ones on purpose.

---

## ❓ Q246. What are the most common runtime exceptions?

| Exception | Typical cause |
|---|---|
| `NullPointerException` | calling a method on `null` |
| `ArrayIndexOutOfBoundsException` | bad array index |
| `StringIndexOutOfBoundsException` | bad `substring`/`charAt` |
| `ClassCastException` | invalid downcast |
| `NumberFormatException` | `Integer.parseInt("abc")` |
| `ArithmeticException` | integer `/ 0` |
| `IllegalArgumentException` | invalid method argument |
| `IllegalStateException` | object in the wrong state |
| `UnsupportedOperationException` | modifying an immutable collection |
| `ConcurrentModificationException` | modifying while iterating |

---

## ❓ Q247. Does `1.0 / 0` throw `ArithmeticException`?

**No!** Floating-point division by zero gives `Infinity`, `-Infinity`, or `NaN`. Only **integer** division by zero throws.

```java
System.out.println(1 / 0);      // 💥 ArithmeticException
System.out.println(1.0 / 0);    // Infinity
System.out.println(0.0 / 0);    // NaN
System.out.println(Double.NaN == Double.NaN);  // false! use Double.isNaN()
```

---

## ❓ Q248. What are Helpful NullPointerExceptions? (Java 14+)

The JVM now tells you exactly **which** part was null:
```
Cannot invoke "String.length()" because "<local1>.name" is null
```
Enabled by default since Java 15. Mention this — it shows you use modern Java. ✨

---

## ❓ Q249. What is `StackOverflowError` vs `OutOfMemoryError`?

- `StackOverflowError` → too deep recursion; the **thread stack** is exhausted
- `OutOfMemoryError: Java heap space` → the **heap** is full and GC cannot free anything
- `OutOfMemoryError: Metaspace` → too many loaded classes (classloader leak)
- `OutOfMemoryError: unable to create native thread` → OS thread limit hit

---

## ❓ Q250. What is `Throwable` and its key methods?

```java
e.getMessage();        // description
e.getCause();          // the wrapped original exception
e.getStackTrace();     // StackTraceElement[]
e.printStackTrace();   // ⚠️ avoid in production — use a logger
e.getSuppressed();     // exceptions suppressed by try-with-resources
e.addSuppressed(t);
```

---

# 🧯 Section 2 — try / catch / finally (Q251–Q264)

## ❓ Q251. What is the order of catch blocks?

**Most specific first.** Catching a parent before a child is a **compile error**.

```java
try { }
catch (FileNotFoundException e) { }   // child first ✅
catch (IOException e) { }
catch (Exception e) { }
```

---

## ❓ Q252. What is multi-catch? (Java 7)

```java
catch (IOException | SQLException e) {   // e is implicitly FINAL
    log.error("failed", e);
}
```
The types must not be in a parent-child relationship with each other.

---

## ❓ Q253. Is `finally` ALWAYS executed? ⭐⭐

**Almost always.** It runs even if `try` or `catch` returns or throws.

**It does NOT run when:**
1. `System.exit()` is called
2. The JVM crashes or is killed (`kill -9`)
3. The thread is killed / an infinite loop or deadlock in `try`
4. A power failure 🔌 (yes, interviewers accept this)

---

## ❓ Q254. What happens if both `try` and `finally` return? ⭐

**`finally` wins** — it overwrites the return value.

```java
int m() {
    try { return 1; }
    finally { return 2; }    // returns 2 😱
}
```

> [!danger] Never `return` inside `finally` — it silently swallows exceptions too. Most linters flag it as an error.

---

## ❓ Q255. The classic puzzle: does `finally` change a returned primitive?

```java
int m() {
    int x = 1;
    try { return x; }        // the VALUE 1 is copied to the return slot here
    finally { x = 2; }       // too late
}
// returns 1 ✅
```
For a **mutable object**, mutation in `finally` **is** visible, because the reference was copied, not the object.

---

## ❓ Q256. What is try-with-resources? (Java 7) ⭐⭐

Automatically calls `close()` on anything implementing `AutoCloseable`.

```java
try (BufferedReader br = new BufferedReader(new FileReader("f.txt"));
     Connection conn = getConnection()) {
    return br.readLine();
}   // closed automatically, in REVERSE order, even if an exception is thrown
```

**Java 9 improvement** — use an existing effectively-final variable:
```java
BufferedReader br = new BufferedReader(...);
try (br) { ... }
```

---

## ❓ Q257. What is a suppressed exception? ⭐

If `try` throws **and** `close()` also throws, the primary exception is kept and the close exception is attached as **suppressed** — nothing is lost.

```java
for (Throwable t : e.getSuppressed()) log.warn("suppressed", t);
```
Before try-with-resources, the `finally` exception would **replace** and hide the real one — a classic debugging nightmare. 🐞

---

## ❓ Q258. `AutoCloseable` vs `Closeable`?

- `Closeable` (Java 5, `java.io`) → `close() throws IOException`, idempotent
- `AutoCloseable` (Java 7, `java.lang`) → `close() throws Exception`, the parent interface

`Closeable extends AutoCloseable`.

---

## ❓ Q259. Can we have try without catch?

Yes:
- `try` + `finally`
- `try` with resources (no catch needed)

But `try` alone → compile error.

---

## ❓ Q260. Can we have nested try blocks?

Yes. The inner block is checked first; if it has no matching catch, the exception propagates outward.

---

## ❓ Q261. What is exception propagation?

An uncaught exception moves **up the call stack** until a matching handler is found. If none exists, the thread dies and the default handler prints the stack trace.

- **Unchecked** exceptions propagate freely
- **Checked** exceptions must be declared with `throws` at each level

---

## ❓ Q262. What happens if an exception is thrown inside `catch`?

The new exception propagates up; `finally` still runs first. The original exception is **lost** unless you chain it as a cause.

---

## ❓ Q263. What is exception chaining? ⭐

Preserving the original cause when re-throwing:

```java
try {
    lowLevel();
} catch (SQLException e) {
    throw new DataAccessException("Could not load user " + id, e);   // ⭐ pass e!
}
```

> [!danger] Losing the cause (`throw new MyException("failed")` with no `e`) destroys the stack trace and makes production bugs unfixable. This is one of the most common real code review comments.

---

## ❓ Q264. What is rethrow with more precise type analysis? (Java 7)

```java
void m() throws IOException, SQLException {   // compiler infers precise types
    try { risky(); }
    catch (Exception e) { log(e); throw e; }  // ✅ allowed since Java 7
}
```

---

# 🚀 Section 3 — throw, throws & Custom Exceptions (Q265–Q276)

## ❓ Q265. `throw` vs `throws`? ⭐

| `throw` | `throws` |
|---------|----------|
| statement inside a method | clause in the method signature |
| throws **one** object | declares **many** types |
| `throw new IOException();` | `void m() throws IOException, SQLException` |

---

## ❓ Q266. Can we throw an exception without `throws` in the signature?

Yes for **unchecked** exceptions. Checked exceptions must be caught or declared.

---

## ❓ Q267. How do you create a custom exception? ⭐

```java
public class InsufficientFundsException extends RuntimeException {
    private final BigDecimal shortfall;

    public InsufficientFundsException(String message, BigDecimal shortfall, Throwable cause) {
        super(message, cause);           // ⭐ always offer a cause constructor
        this.shortfall = shortfall;
    }
    public BigDecimal getShortfall() { return shortfall; }
}
```

**Checked or unchecked?**
- Caller can realistically recover → **checked**
- It is a bug or unrecoverable → **unchecked** (most modern code prefers this)

---

## ❓ Q268. Overriding rules for exceptions? ⭐⭐

An overriding method:
- ✅ can throw **fewer** or **narrower** checked exceptions
- ✅ can throw **any** unchecked exception
- ❌ cannot throw **broader or new** checked exceptions

```java
class P { void m() throws IOException {} }
class C extends P {
    void m() throws FileNotFoundException {}   // ✅ narrower
    // void m() throws Exception {}            // ❌ broader
}
```

---

## ❓ Q269. Can a constructor throw an exception?

Yes. The object is then **never fully created** and becomes eligible for GC. This is the standard way to enforce invariants:

```java
public Age(int value) {
    if (value < 0) throw new IllegalArgumentException("age < 0");
    this.value = value;
}
```

---

## ❓ Q270. `IllegalArgumentException` vs `IllegalStateException`?

- **IllegalArgumentException** → the *argument* is wrong (`setAge(-5)`)
- **IllegalStateException** → the *object* is in the wrong state for this call (`iterator.remove()` before `next()`)

---

## ❓ Q271. What is `Objects.requireNonNull()`?

Fail fast with a clear message, at the boundary instead of deep inside:
```java
this.name = Objects.requireNonNull(name, "name must not be null");
```

---

## ❓ Q272. What is the `finally` + `try-with-resources` execution order?

```java
try (Resource r = new Resource()) {   // 1. open
    use(r);                           // 2. body
} catch (Exception e) {               // 4. catch  (AFTER close!)
} finally {                           // 5. finally
}
// 3. close() happens BEFORE catch and finally ⭐
```

---

## ❓ Q273. How do you handle exceptions in a `Thread`?

A thread's exception does **not** propagate to the main thread.
```java
Thread.setDefaultUncaughtExceptionHandler((t, e) -> log.error("thread " + t.getName(), e));
t.setUncaughtExceptionHandler(...);
```
With `ExecutorService.submit()`, the exception is captured in the `Future` and only appears when you call `future.get()` (wrapped in `ExecutionException`). ⚠️ This is why exceptions silently disappear in thread pools.

---

## ❓ Q274. Can `main` declare `throws`?

Yes. The JVM then prints the stack trace and exits with a non-zero status.

---

## ❓ Q275. What happens to an exception thrown in a `static` block?

It is wrapped in an **`ExceptionInInitializerError`** and the class becomes permanently unusable — every later use throws `NoClassDefFoundError`.

---

## ❓ Q276. How do you throw a checked exception from a lambda?

You cannot directly — most functional interfaces do not declare `throws`. Options: wrap in an unchecked exception, write your own throwing functional interface, or handle it inside the lambda.

```java
list.forEach(f -> {
    try { process(f); }
    catch (IOException e) { throw new UncheckedIOException(e); }
});
```

---

# 🧪 Section 4 — Best Practices & Real Traps (Q277–Q286)

## ❓ Q277. What are exception handling best practices? ⭐

1. ✅ Catch **specific** exceptions, not `Exception`
2. ❌ Never swallow: `catch (Exception e) { }` is a crime 🚨
3. ✅ Always preserve the **cause** when wrapping
4. ✅ Use try-with-resources instead of manual `finally` close
5. ✅ Fail fast — validate inputs early
6. ❌ Do not use exceptions for **control flow** (they are expensive: stack trace capture)
7. ✅ Log **or** rethrow — never both (double logging noise)
8. ✅ Throw the most specific meaningful exception
9. ❌ Never `catch (Throwable)` unless you are a framework
10. ✅ Document with `@throws` in Javadoc

---

## ❓ Q278. Why are exceptions expensive?

`fillInStackTrace()` walks the entire call stack when the exception object is created. In a hot loop this dominates the runtime. If you truly need a cheap signal exception (rare), override `fillInStackTrace()` to return `this`.

---

## ❓ Q279. What is the anti-pattern of using exceptions for flow control?

```java
// ❌ BAD
try { return map.get(k).toString(); } catch (NullPointerException e) { return "none"; }
// ✅ GOOD
return map.containsKey(k) ? map.get(k).toString() : "none";
```

---

## ❓ Q280. Should you catch `NullPointerException`?

Almost never. An NPE means a bug — fix the bug, do not hide it. Use `Optional`, null checks, or `Objects.requireNonNull`.

---

## ❓ Q281. What is the difference between `printStackTrace()` and a logger?

`printStackTrace()` writes to `System.err` — unstructured, no timestamp, no log level, not captured by log aggregation. Always use `log.error("context", e)`.

---

## ❓ Q282. How do you test that a method throws an exception?

```java
assertThrows(IllegalArgumentException.class, () -> new Age(-1));   // JUnit 5
```

---

## ❓ Q283. What is a global exception handler in a web app?

Spring: `@ControllerAdvice` + `@ExceptionHandler` translate exceptions into HTTP responses centrally, so controllers stay clean.

---

## ❓ Q284. What happens when an exception is thrown inside `finally` while an exception is already propagating?

The **finally exception replaces** the original — the first one is lost forever. This is exactly the problem try-with-resources solved with suppressed exceptions.

---

## ❓ Q285. Can you catch multiple exception types and rethrow as one?

Yes — that is exception wrapping/translation. Common in layered architecture: DAO exceptions → service exceptions → API errors.

---

## ❓ Q286. What is the difference between "handle" and "declare"?

Handle = `try-catch` here. Declare = `throws`, pushing responsibility to the caller. Declare when the caller has more context to decide what to do.

---

# 🧬 Section 5 — Generics Basics (Q287–Q298)

## ❓ Q287. What are generics and why do we need them? ⭐

Type parameters that give **compile-time type safety** and remove casting.

```java
// Before generics
List list = new ArrayList();
list.add("hello");
String s = (String) list.get(0);      // manual cast, runtime risk
list.add(42);                          // 💥 discovered only at runtime

// With generics
List<String> list = new ArrayList<>();
list.add(42);                          // ❌ compile error — caught early ✅
String s = list.get(0);                // no cast
```

**Benefits:** type safety, no casts, reusable algorithms, clearer APIs.

---

## ❓ Q288. What are the naming conventions for type parameters?

| Letter | Meaning |
|---|---|
| `T` | Type |
| `E` | Element (collections) |
| `K`, `V` | Key, Value |
| `N` | Number |
| `R` | Return type |
| `S`, `U` | 2nd, 3rd types |

---

## ❓ Q289. How do you write a generic class and a generic method?

```java
// Generic class
class Box<T> {
    private T item;
    void set(T item) { this.item = item; }
    T get() { return item; }
}

// Generic method — <T> goes BEFORE the return type
public static <T> void printAll(List<T> list) { list.forEach(System.out::println); }

// Multiple parameters
public static <K, V> Map<V, K> invert(Map<K, V> map) { ... }
```

---

## ❓ Q290. What is a bounded type parameter? ⭐

```java
class NumberBox<T extends Number> {        // T must be Number or a subclass
    double doubled() { return item.doubleValue(); }   // ✅ Number methods available
}
```

**Multiple bounds** — class first, then interfaces:
```java
<T extends Number & Comparable<T> & Serializable>
```

---

## ❓ Q291. Why can't you use primitives as type arguments?

Because of **type erasure** — generics compile down to `Object`, and primitives are not objects. Use wrappers (`List<Integer>`). Project Valhalla may change this someday.

---

## ❓ Q292. What is the diamond operator?

```java
Map<String, List<Integer>> m = new HashMap<>();   // Java 7: type inferred
Runnable r = new Runnable<>() { };                // Java 9: works with anonymous classes
```

---

## ❓ Q293. What is a raw type and why avoid it?

`List` without a type parameter. It exists only for backward compatibility. It disables all generic checks and produces "unchecked" warnings.

```java
List raw = new ArrayList<String>();
raw.add(42);                     // compiles! 💥 breaks later
```

---

## ❓ Q294. Is `List<Object>` the same as `List<?>` or raw `List`?

**No, all three differ:**

| | Can add anything? | Type safe? |
|---|---|---|
| `List` (raw) | ✅ yes | ❌ no checks |
| `List<Object>` | ✅ yes | ✅ checked |
| `List<?>` | ❌ only `null` | ✅ checked |

---

## ❓ Q295. Is `List<String>` a subtype of `List<Object>`? ⭐

**No — generics are invariant.** This is intentional:

```java
List<Object> objs = new ArrayList<String>();   // ❌ compile error (good!)
// if it were allowed:
objs.add(42);                                   // would corrupt the String list
```
Arrays **are** covariant, which is why they fail at runtime with `ArrayStoreException` instead.

---

## ❓ Q296. Can a generic class extend another generic class?

```java
class MyList<T> extends ArrayList<T> { }              // pass through
class StringList extends ArrayList<String> { }        // fix the type
```

---

## ❓ Q297. Can you have static generic members?

- Static **methods** with their own type parameter → ✅
- Static **fields** of the class's type parameter → ❌ (there is only one class, but many T's)

```java
class Box<T> {
    static T item;              // ❌ compile error
    static <U> U pick(U u) { }  // ✅ its own parameter
}
```

---

## ❓ Q298. What is a recursive generic bound?

```java
public interface Comparable<T> { int compareTo(T o); }
class Enum<E extends Enum<E>> { }        // "E is comparable to itself"
```
Used for self-referential builders and enums. It looks strange but it means "the type parameter must be the same as the implementing type".

---

# 🫥 Section 6 — Type Erasure (Q299–Q306)

## ❓ Q299. What is type erasure? ⭐⭐

The compiler **removes** all generic type information after checking it. At runtime, `List<String>` and `List<Integer>` are both just `List`.

```java
List<String> a = new ArrayList<>();
List<Integer> b = new ArrayList<>();
a.getClass() == b.getClass();     // true! 😱
```

**Why?** Backward compatibility — Java 5 generics had to run on existing bytecode and existing libraries (**migration compatibility**).

**What the compiler does:**
1. Replaces `T` with `Object` (or the first bound)
2. Inserts casts where needed
3. Generates **bridge methods** to preserve polymorphism

---

## ❓ Q300. What are the consequences of erasure? ⭐

```java
// ❌ 1. No overload on generic type
void m(List<String> l) {}
void m(List<Integer> l) {}          // same erasure → compile error

// ❌ 2. No instanceof with a type argument
if (obj instanceof List<String>) {} // error; only List<?> allowed

// ❌ 3. No new T()
T item = new T();                   // error

// ❌ 4. No generic arrays
T[] arr = new T[10];                // error

// ❌ 5. No generic exceptions
class MyEx<T> extends Exception {}  // error

// ❌ 6. No static field of type T
```

---

## ❓ Q301. Why can't you create a generic array? ⭐

Arrays are **covariant and reified** (they know their type at runtime), generics are **invariant and erased**. Mixing them would break the array store check.

**The standard workaround:**
```java
@SuppressWarnings("unchecked")
T[] arr = (T[]) new Object[10];         // used inside ArrayList itself!
```
Or pass the type: `T[] arr = (T[]) Array.newInstance(clazz, size);`

---

## ❓ Q302. What is a bridge method?

A synthetic method the compiler generates so that overriding still works after erasure.

```java
class MyComparator implements Comparable<MyClass> {
    public int compareTo(MyClass o) { ... }
    // compiler adds: public int compareTo(Object o) { return compareTo((MyClass) o); }
}
```
You can see them with `javap -c`.

---

## ❓ Q303. How can you get generic type info at runtime then?

Erasure removes **type arguments of variables**, but **class and field declarations keep their signature** in the class file metadata.

```java
class StringList extends ArrayList<String> { }
Type t = StringList.class.getGenericSuperclass();
// → java.util.ArrayList<java.lang.String>  ✅ recoverable
```
This is the trick behind Jackson's `TypeReference` and Spring's `ParameterizedTypeReference` — the anonymous subclass preserves the type. 🎩

---

## ❓ Q304. What is heap pollution?

When a variable of a parameterized type refers to an object of a different type — usually via raw types or varargs. It causes a `ClassCastException` far away from the real bug.

---

## ❓ Q305. What is `@SafeVarargs`?

Generic varargs create an array of a generic type internally (`T... args` → `T[]`), which triggers an unchecked warning. `@SafeVarargs` says "I only read from it, I never store the wrong type".

```java
@SafeVarargs
static <T> List<T> listOf(T... items) { return Arrays.asList(items); }
```
Allowed only on `static`, `final`, or `private` methods.

---

## ❓ Q306. Does erasure hurt performance?

No — generics are purely a **compile-time** feature; the bytecode is the same as hand-written casts. The cost is expressiveness, not speed. (Boxing primitives **does** cost, but that is separate.)

---

# 🃏 Section 7 — Wildcards & PECS (Q307–Q316)

## ❓ Q307. What is a wildcard `?`?

An unknown type. Three forms:

| Form | Name | Meaning |
|---|---|---|
| `List<?>` | unbounded | some unknown type |
| `List<? extends Number>` | **upper** bounded | Number or a subtype |
| `List<? super Integer>` | **lower** bounded | Integer or a supertype |

---

## ❓ Q308. What is PECS? ⭐⭐⭐ (very common)

> **P**roducer **E**xtends, **C**onsumer **S**uper

- If the collection **produces** values you read → use `? extends T`
- If the collection **consumes** values you write → use `? super T`
- If you do both → use plain `T`

```java
public static <T> void copy(List<? super T> dest, List<? extends T> src) {
    //                       ↑ CONSUMER super       ↑ PRODUCER extends
    for (T item : src) dest.add(item);
}
```

---

## ❓ Q309. Why can't you add to a `List<? extends Number>`? ⭐

Because `?` could be `Integer`, `Double`, or `Float` — the compiler cannot know which, so **no add is safe**.

```java
List<? extends Number> list = new ArrayList<Integer>();
list.add(1);          // ❌ compile error
list.add(1.5);        // ❌ compile error
list.add(null);       // ✅ only null is safe
Number n = list.get(0);   // ✅ reading is safe — everything is at least a Number
```

---

## ❓ Q310. Why CAN you add to a `List<? super Integer>`?

Because whatever `?` is (`Integer`, `Number`, or `Object`), an `Integer` always fits.

```java
List<? super Integer> list = new ArrayList<Number>();
list.add(42);              // ✅
Object o = list.get(0);    // ⚠️ you can only read as Object
```

---

## ❓ Q311. `<T>` vs `<?>` — when to use which?

- Use a **type parameter `T`** when you need to **refer to the type** (as a return value, in multiple places, or to relate two arguments)
- Use a **wildcard `?`** when the type appears only once and you do not care what it is

```java
void printAll(Collection<?> c) { }        // ✅ wildcard is enough
<T> T firstOf(List<T> list) { }           // ✅ needs T for the return type
```

---

## ❓ Q312. Real JDK examples of PECS

```java
Collections.copy(List<? super T> dest, List<? extends T> src);
Collections.max(Collection<? extends T> coll);
Stream.flatMap(Function<? super T, ? extends Stream<? extends R>> mapper);
list.forEach(Consumer<? super T> action);
```

---

## ❓ Q313. What is capture conversion / the "capture of ?" error?

The compiler assigns a temporary name (`CAP#1`) to the unknown type. When you need to work with it, use a private helper method that captures it into a real type parameter:

```java
public static void swap(List<?> list, int i, int j) { swapHelper(list, i, j); }
private static <T> void swapHelper(List<T> list, int i, int j) {
    T tmp = list.get(i); list.set(i, list.get(j)); list.set(j, tmp);
}
```

---

## ❓ Q314. Can you use wildcards in a class declaration?

No — `class Box<?>` is illegal. Wildcards are only for **variable types, parameters, and return types**.

---

## ❓ Q315. What does `Class<?>` mean?

"A `Class` object of some unknown type." Using raw `Class` loses type checking, so `Class<?>` is the safe way to say "any class".

---

## ❓ Q316. How do generics interact with inheritance in method overriding?

Return types may be covariant, and generic signatures must match after erasure. Overriding `List<String> get()` with `ArrayList<String> get()` is fine; with `List<Object> get()` is not.

---

# 🧩 Section 8 — Quick Fire Round

> [!question]- Can `finally` be used without `catch`?
> Yes — `try-finally` is valid.

> [!question]- What is the parent of all exceptions?
> `java.lang.Throwable`.

> [!question]- Is `NullPointerException` checked?
> No — unchecked (`RuntimeException`).

> [!question]- Can you catch `Exception` to also catch `Error`?
> No. `Error` is a sibling of `Exception`, not a subclass. Only `catch (Throwable)` gets both.

> [!question]- What happens if a `catch` block itself throws?
> The new exception propagates; `finally` still runs; the original is lost unless chained.

> [!question]- Difference between `throw new Exception()` and `throw e`?
> Rethrowing `e` preserves the original stack trace; creating a new one starts a fresh trace at that line.

> [!question]- Can an interface method declare `throws`?
> Yes, and implementations may declare fewer/narrower checked exceptions.

> [!question]- What is `UncheckedIOException`?
> Java 8 wrapper that turns `IOException` into a runtime exception — designed for lambdas and streams.

> [!question]- What generic type does `List.of()` infer from `List.of()` with no arguments?
> `Object`, unless the target type says otherwise (`List<String> l = List.of();`).

> [!question]- What is `Collections.emptyList()` returning generically?
> A `List<T>` inferred from context — a nice example of a generic method.

> [!question]- Can you overload `void m(List<String>)` and `void m(List<Integer>)`?
> No — same erasure, compile error.

> [!question]- Which is correct: `Consumer<? super T>` or `Consumer<? extends T>`?
> `super` — a Consumer consumes (PECS).

---

## 🎓 Self-Test Checklist for Part 4

- [ ] I can draw the Throwable hierarchy and mark the checked/unchecked boundary
- [ ] I know the 4 cases where `finally` does not run
- [ ] I can explain try-with-resources + suppressed exceptions
- [ ] I always pass the cause when wrapping an exception
- [ ] I can explain type erasure and its 6 consequences
- [ ] I can state PECS and apply it to `copy(dest, src)`
- [ ] I can explain why generics are invariant but arrays are covariant
- [ ] I know why you cannot create `new T[]`

---

> [!success] ✅ Part 4 complete — Q241–Q316
> 👉 Next: [[01 - Java/Interview/05 - Concurrency|Part 5 — Concurrency]]

#java #interview #core-java #exceptions #generics #part4
